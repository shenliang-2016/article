### 将拉丁数字转化为其它 Unicode 数字

默认地，当文本包含数值时，那些数值使用拉丁数字显示。当需要使用其它 Unicode 数字字形时，使用 [`java.awt.font.NumericShaper`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html) 类。`NumericShaper` API 使得你可以以任何 Unicode 数字字形显示内部由 ASCII 编码表示的数值。

下面的代码片段，来自 [`ArabicDigits`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ArabicDigits.java) 示例，显示了如何使用`NumericShaper`实例来转化拉丁数字为阿拉伯数字。确定字形的一行代码显示为粗体。

```java
ArabicDigitsPanel(String fontname) {
    HashMap map = new HashMap();
    Font font = new Font(fontname, Font.PLAIN, 60);
    map.put(TextAttribute.FONT, font);
    map.put(TextAttribute.NUMERIC_SHAPING,
        NumericShaper.getShaper(NumericShaper.ARABIC));

    FontRenderContext frc = new FontRenderContext(null, false, false);
    layout = new TextLayout(text, map, frc);
}

// ...

public void paint(Graphics g) {
    Graphics2D g2d = (Graphics2D)g;
    layout.draw(g2d, 10, 50);
}
```

用于阿拉伯数字的`NumericShaper`实例被获取并放入一个用于 [`TextLayout.NUMERIC_SHAPING`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/TextAttribute.html#NUMERIC_SHAPING) 属性键的`HashMap`。改散列映射被传入`TextLayout`接口。`paint`方法渲染文本之后，数字被期望中的脚本显示。这个例子中，拉丁数字0到9，显示为阿拉伯数字。

![ArabicDigits example output showing Arabic digits from 0 through 9](https://docs.oracle.com/javase/tutorial/figures/i18n/ArabicDigits.png)

前面的示例使用`NumericShaper.ARABIC`常量来检索所需的整形器，但`NumericShaper`类为许多语言提供常量。这些常量被定义为位掩码，并被称为`NumericShaper`的基于位掩码的常量。

**基于枚举的范围常量**

指定特定数字集的另一种方法是使用 [`NumericShaper.Range`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.Range.html) 枚举类型（枚举）。这个在Java SE 7发行版中引入的枚举也提供了一组常量。虽然这些常量是使用不同的机制定义的，但`NumericShaper.ARABIC`位掩码在功能上等同于`NumericShaper.Range.ARABIC`枚举，并且每个常量类型都有一个相应的`getShaper`方法：

- [`getShaper(int singleRange)`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getShaper-int-)
- [`getShaper(NumericShaper.Range singleRange)`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getShaper-java.awt.font.NumericShaper.Range-)

 [`ArabicDigitsEnum`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ArabicDigitsEnum.java) 例子等同于上面的阿拉伯数字的例子，除了它使用了`NumericShaper.Range`枚举来指定语言脚本：

```java
ArabicDigitsEnumPanel(String fontname) {
    HashMap map = new HashMap();
    Font font = new Font(fontname, Font.PLAIN, 60);
    map.put(TextAttribute.FONT, font);
    map.put(TextAttribute.NUMERIC_SHAPING,
        NumericShaper.getShaper(NumericShaper.Range.ARABIC));
    FontRenderContext frc = new FontRenderContext(null, false, false);
    layout = new TextLayout(text, map, frc);
}
```

两种`getShaper` 方法都接受`singleRange`参数。使用其它常量类型，你可以指定一个特定脚本的数字范围。基于位掩码的常量能够通过`OR`组合使用，或者你可以创建一个`NumericShaper.Range`枚举集合。下面展示了如何使用每种常量类型定义范围：

```java
NumericShaper.MONGOLIAN | NumericShaper.THAI |
NumericShaper.TIBETAN
EnumSet.of(
    NumericShaper.Range.MONGOLIAN,
    NumericShaper.Range.THAI,
    NumericShaper.Range.TIBETAN)
```

你可以查询`NumericShaper`对象来确定它支持的范围，通过使用用于基于位掩码的造型器的 [`getRanges`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getRanges--) 方法，或者使用用于基于枚举的造型器的 [`getRangeSet`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getRangeSet--) 方法。

------

注意：

您可以使用传统的基于位掩码的常量或基于`Range`枚举的常量。在决定使用哪个时，请考虑以下几点：

 -  `Range` API需要JDK 7或更高版本。
 -  `Range` API涵盖了比位掩码API更多的Unicode范围。
 -  位掩码API比`Range` API快一点。

------

**根据语言上下文渲染数字**

 [`ArabicDigits`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ArabicDigits.java) 示例旨在将造型器用于特定语言，但有时必须根据语言上下文呈现数字。例如，如果数字前面的文本使用泰语脚本，则首选泰语数字。如果文本以藏文显示，则首选藏文数字。

您可以使用`getContextualShaper`方法之一完成此操作：

- [getContextualShaper(int ranges)](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getContextualShaper-int-)
- [getContextualShaper(int ranges, int defaultContext)](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getContextualShaper-int-int-)
- [getContextualShaper(Set ranges)](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getContextualShaper-java.util.Set-)
- [getContextualShaper(Set ranges, NumericShaper.Range defaultContext)](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getContextualShaper-java.util.Set-java.awt.font.NumericShaper.Range-)

前两个方法使用位掩码常量，后两个使用枚举常量。接受`defaultContext`参数的方法使您可以指定在文本之前显示数值时使用的初始整形器。如果未定义默认上下文，则使用拉丁形状显示任何前导数字。

 [`ShapedDigits`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ShapedDigits.java) 示例显示了整形器的工作方式。显示五个文本布局：

1. 第一种布局不使用整形器，所有数字均显示为拉丁文。
2. 无论语言上下文如何，第二种布局都将所有数字整形为阿拉伯数字。
3. 第三种布局采用了使用阿拉伯数字的上下文整形器。默认上下文定义为阿拉伯语。
4. 第四种布局采用使用阿拉伯数字的上下文整形器，但整形器不指定默认上下文。
5. 第五种布局采用了使用`ALL_RANGES`位掩码的上下文整形器，但整形器未指定默认上下文。

![ShapedDigits example output illustrating how contextual shapers work](https://docs.oracle.com/javase/tutorial/figures/i18n/ShapedDigits.png)

以下代码行显示了如何定义整形器，如果被使用了：

1. 没有使用整形器；
2. `NumericShaper arabic = NumericShaper.getShaper(NumericShaper.ARABIC);`
3. `NumericShaper contextualArabic = NumericShaper.getContextualShaper(NumericShaper.ARABIC, NumericShaper.ARABIC);`
4. `NumericShaper contextualArabicASCII = NumericShaper.getContextualShaper(NumericShaper.ARABIC);`
5. `NumericShaper contextualAll = NumericShaper.getContextualShaper(NumericShaper.ALL_RANGES);`

参考 [`ShapedDigits.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ShapedDigits.java) 示例获取更多实现细节。

