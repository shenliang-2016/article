### 规范化文本

*规范化*是一个过程，通过它您可以执行某些文本转换，使其可以以前所未有的方式进行协调。假设您想要搜索或排序文本，在这种情况下，您需要将该文本规范化以考虑应该表示为相同文本的代码点。

什么可以规范化？当您需要转换使用变音符号的字符，更改所有字母大小写，分解连字或将半角片假名字符转换为全角字符等时，可以应用规范化。

根据 [Unicode Standard Annex #15](http://www.unicode.org/reports/tr15/) ，Normalizer的API支持以下四种在 [`java.text.Normalizer.Form`](https://docs.oracle.com/javase/8/docs/api/java/text/Normalizer.Form.html) 中定义的Unicode文本规范化形式：

 - 规范化形式D（NFD）：规范分解
 - 规范化形式C（NFC）：规范分解，然后是规范组合
 - 规范化形式KD（NFKD）：兼容性分解
 - 规范化形式KC（NFKC）：兼容性分解，然后是规范组合

让我们来看看如何通过使用这些规范化形式来规范化带有分音符的拉丁文小写字母“o”：

| Original word | NFC     | NFD           | NFKC    | NFKD          |
| ------------- | ------- | ------------- | ------- | ------------- |
| "schön"       | "schön" | "scho\u0308n" | "schön" | "scho\u0308n" |

您可以注意到原始单词在 NFC 和 NFKC 中保持不变。这是因为使用 NFD 和 NFKD，复合字符被映射到它们的规范分解。但是对于 NFC 和 NFKC，如果可能的话，将组合字符序列映射到组合。由于没有用于分解的组合，因此它在 NFC 和 NFKC 中被分解。

在下面的代码示例  [`NormSample.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/NormSample.java) 中，您还可以注意到另一个规范化功能。半宽和全宽片假名字符将具有相同的兼容性分解，因此是兼容性等价物。但是，它们不是规范的等价物。

为了确保您确实需要对文本进行规范化，可以使用`isNormalized`方法来确定给定的`char`值序列是否已规范化。如果此方法返回`false`，则表示您必须规范化此序列，并且应使用`normalize`方法，该方法根据指定的规范化形式规范化`char`值。例如，要将文本转换为规范的分解形式，您必须使用以下`normalize`方法：

```java
normalized_string = Normalizer.normalize(target_chars, Normalizer.Form.NFD);
```

此外，`normalize`方法会将重音重新排列为正确的规范顺序，因此您无需担心自己的重音重排。

以下示例表示一个应用程序，使您可以选择规范化形式和要规范化的模板：

------

**注意:**  如果您没有看到 applet 正在运行，则需要至少安装 [Java SE Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 版本。

------

此 applet 的完整代码在 [`NormSample.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/NormSample.java) 中。

### 使用JTextComponent类的双向文本

本节讨论如何使用 [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 类处理双向文本。双向文本是包含从左到右和从右到左两个方向运行的文本的文本。双向文本的示例是包含数字（从左到右运行）的阿拉伯文本（从右向左运行）。显示和管理双向文本更加困难。但是 [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 会为您处理这些问题。

本节涵盖以下主题：

- [确定双向文本的方向](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#directionality)
- [显示和移动插入光标](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#displaying-and-moving-carets)
- [命中测试](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#hit-testing)
- [高亮选择](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#highlighting-selections)
- [设置组件方向](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#setting-component-orientation)

有关这些问题的更多信息，或者如果您希望在处理这些问题时有更多控制权，请参阅在 [2D Graphics](https://docs.oracle.com/javase/tutorial/2d/index.html) 中的 [Working with Bidirectional Text](https://docs.oracle.com/javase/tutorial/2d/text/textlayoutbidirectionaltext.html) 。

**[确定双向文本方向]()**

例子 [`BidiTextComponentDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BidiTextComponentDemo.java) ，基于 [`TextComponentDemo.java`](https://docs.oracle.com/javase/tutorial/uiswing/examples/components/index.html#TextComponentDemo) ，在 [`JTextPane`](https://docs.oracle.com/javase/8/docs/api/javax/swing/JTextPane.html) 对象中显示双向文本。大多数情况下，Java 平台能够确定双向 Unicode 文本的方向：

![BidiTextComponentDemo.java](https://docs.oracle.com/javase/tutorial/figures/i18n/text/biditextcomponentdemo.jpg)

**在JTextComponent对象中显式指定文本方向**

你可以指定 [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 对象的 [`Document`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/Document.html) 对象的方向。比如，下面的语句指定 [`JTextPane`](https://docs.oracle.com/javase/8/docs/api/javax/swing/JTextPane.html) 对象`textPane`中的文本方向为从右到左：

```java
textPane.getDocument().putProperty(
    TextAttribute.RUN_DIRECTION,
    TextAttribute.RUN_DIRECTION_RTL);
```

另外，你可以基于区域设置特定 Swing 组件的方向。比如，下面的语句基于区域`ar-SA`设定`textPane`对象的方向：

```java
Locale arabicSaudiArabia = 
    new Locale.Builder().setLanguage("ar").setRegion("SA").build();

textPane.setComponentOrientation(
    ComponentOrientation.getOrientation(arabicSaudiArabia));
```

由于阿拉伯语的运行方向是从右到左，因此`textPane`对象中包含的文本的方向也是从右到左。

有关更多信息，请参阅 [Setting Component Orientation](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#setting-component-orientation) 一节。

**[显示和移动插入光标]()**

在可编辑文本中，插入符号用于以图形方式表示当前插入点，即文本中将插入新字符的位置。在 [`BidiTextComponentDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BidiTextComponentDemo.java) 示例中，插入符号包含一个小三角形，指向插入字符的显示方向。

默认情况下， [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 对象创建一个键映射（类型为 [`Keymap`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/Keymap.html)），该键映射由所有[`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 实例共享为默认键映射。键映射允许应用程序将键击绑定到操作。默认键映射（对于支持插入符移动的[`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 对象）包括使用左右箭头键向前和向后移动插入符号之间的绑定，以支持在双向文本中移动插入符号。

**[命中测试]()**

通常，设备空间中的位置必须转换为文本偏移量。例如，当用户在可选文本上单击鼠标时，鼠标的位置将转换为文本偏移并用作选择范围的一端。从逻辑上讲，这与定位插入符相反。

您可以将插入符侦听器附加到 [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 的实例。插入符号侦听器使您能够处理插入符号事件，这些事件在插入符号移动或文本组件中的选择发生更改时发生。使用 [`addCaretListener`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html#addCaretListener-javax.swing.event.CaretListener-) 方法附加插入符侦听器。有关更多信息，请参见 [How to Write a Caret Listener](https://docs.oracle.com/javase/tutorial/uiswing/events/caretlistener.html) 。

**[高亮选择]()**

所选字符范围由高亮区域以图形方式表示，高亮区域是以逆视频或不同背景颜色显示字形的区域。

[`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 对象实现逻辑高亮显示。这意味着所选字符在文本模型中始终是连续的，并且允许突出显示区域不连续。以下是逻辑高亮的示例：

![BidiTextComponentDemo: logical highlighting](https://docs.oracle.com/javase/tutorial/figures/i18n/text/biditextcomponentdemo-selected.jpg)

**[设置组件方向]()**

Swing 的布局管理器了解区域设置如何影响UI，没有必要为每个区域设置创建新布局。例如，在文本从右向左流动的区域设置中，布局管理器将以相同的方向排列组件。

示例 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 已本地化为 English, United States; English, United Kingdom; French, France; French, Canada; and Arabic, Saudi Arabia。

以下使用 en-US 语言环境：

![Mortgage Calculator, en-US locale](https://docs.oracle.com/javase/tutorial/figures/i18n/format/mortgage-calculator-en-us.jpg)

以下使用 ar-SA 语言环境：

![Mortgage Calculator, ar-SA locale](https://docs.oracle.com/javase/tutorial/figures/i18n/format/mortgage-calculator-ar-sa.jpg)

请注意，组件的布局方向与相应的区域设置相同：en-US从左到右，ar-SA从右到左。 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 示例调用方法 [`applyComponentOrientation`](https://docs.oracle.com/javase/8/docs/api/java/awt/Component.html#applyComponentOrientation-java.awt.ComponentOrientation-) 和 [`getOrientation`](https://docs.oracle.com/javase/8/docs/api/java/awt/ComponentOrientation.html#getOrientation-java.util.Locale-) 以按区域设置指定其组件的方向：

```java
private static JFrame frame;

// ...

private static void createAndShowGUI(Locale currentLocale) {

    // Create and set up the window.
    // ...
    // Add contents to the window.
    // ...
    frame.applyComponentOrientation(
        ComponentOrientation.getOrientation(currentLocale));
    // ...
  }
```

例子 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 需要以下资源文件：

- [`resources/Resources.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources.properties)
- [`resources/Resources_ar.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources_ar.properties)
- [`resources/Resources_fr.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources_fr.properties)

