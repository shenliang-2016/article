## 格式化

本课程介绍如何格式化数字、日期、时间和文本消息。因为终端用户能够看到这些数据元素，它们的格式必须符合各种自然传统。跟随下面的例子你将学会如何做到：

- 以语言敏感的方式格式化数据元素
- 保持代码的语言无关性
- 避免为特殊的语言编写格式化程序

**[数字和货币](https://docs.oracle.com/javase/tutorial/i18n/format/numberintro.html)**

本涨价解释了如何使用 `NumberFormat`, `DecimalFormat`, 和 `DecimalFormatSymbols` 类。

**[日期和时间](https://docs.oracle.com/javase/tutorial/i18n/format/dateintro.html)**

------

**版本提示：** 本章节使用了`java.util`包中的日期和时间 APIs 。而`java.time` APIs 在 JDK 8 中可用，提供了全面的日期和时间模型，是对`java.util`包中相关类的重大改进。`java.time` APIs 描述参见 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 章节。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面可能会有特殊意义。

------

本章节聚焦在 `DateFormat`, `SimpleDateFormat`, 和 `DateFormatSymbols` 类。

**[消息](https://docs.oracle.com/javase/tutorial/i18n/format/messageintro.html)**

本节介绍`MessageFormat`和`ChoiceFormat`类如何帮助您解决格式化文本消息时可能遇到的一些问题。

### 数字和货币

程序以与语言环境无关的方式存储和操作数字。在显示或打印数字之前，程序必须将其转换为区域设置敏感格式的字符串。例如，在法国，数字123456.78的格式应为123 456,78，在德国则应为123.456,78。在本节中，您将学习如何使程序独立于小数点，千位分隔符和其他格式设置属性的语言环境约定。

**[使用预定义格式](https://docs.oracle.com/javase/tutorial/i18n/format/numberFormat.html)**

使用`NumberFormat`类提供的工厂方法，您可以获取数字，货币和百分比的特定于语言环境的格式。

**[使用模式格式化](https://docs.oracle.com/javase/tutorial/i18n/format/decimalFormat.html)**

使用`DecimalFormat`类，您可以使用`String`模式指定数字的格式。`DecimalFormatSymbols`类允许您修改格式符号，如小数分隔符和减号。

#### 使用预定义格式

通过调用由 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 类提供的方法，你可以根据 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 格式化数字、货币和百分比。接下来举例说明格式化技术的程序名为 [`NumberFormatDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/NumberFormatDemo.java) 。

**数字**

你可以使用 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 方法来格式化基本类型的数字，比如`double`，以及它们对应的包装对象，比如 [`Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) 。

下面的例子代码根据 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 格式化 [`Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) ，调用 [`getNumberInstance`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#getNumberInstance-java.util.Locale-) 方法返回一个特定于语言的 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 实例。其中的 [`format`](https://docs.oracle.com/javase/8/docs/api/java/text/Format.html#format-java.lang.Object-) 方法接受 [`Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) 作为参数并返回 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 形式的格式化数字。

```java
static public void displayNumber(Locale currentLocale) {

    Integer quantity = new Integer(123456);
    Double amount = new Double(345987.246);
    NumberFormat numberFormatter;
    String quantityOut;
    String amountOut;

    numberFormatter = NumberFormat.getNumberInstance(currentLocale);
    quantityOut = numberFormatter.format(quantity);
    amountOut = numberFormatter.format(amount);
    System.out.println(quantityOut + "   " + currentLocale.toString());
    System.out.println(amountOut + "   " + currentLocale.toString());
}
```

此示例打印以下内容，它显示了相同数字的格式如何随`Locale`而变化：

```
123 456   fr_FR
345 987,246   fr_FR
123.456   de_DE
345.987,246   de_DE
123,456   en_US
345,987.246   en_US
```

**使用阿拉伯数字以外的数字形状**

默认情况下，当文本包含数字值时，将使用阿拉伯数字显示这些值。如果首选其他`Unicode`数字形状，请使用 [`java.awt.font.NumericShaper`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html) 类。`NumericShaper` API使您可以在任何`Unicode`数字形状中显示内部表示为ASCII值的数值。 有关详细信息，请参阅 [将拉丁数字转换为其他Unicode数字](https://docs.oracle.com/javase/tutorial/i18n/text/shapedDigits.html) 。

此外，某些区域设置具有变体代码，这些代码指定使用Unicode数字形状代替阿拉伯数字，例如泰语的区域设置。有关更多信息，请参阅 [创建区域设置](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html) 中的 [变体代码](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html#variant-code) 部分。

**货币**

如果您正在编写业务应用程序，则可能需要格式化和显示货币。您可以使用与数字相同的方式格式化货币，但调用 [`getCurrencyInstance`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#getCurrencyInstance-java.util.Locale-) 以创建格式化器除外。当您调用 [`format`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#format-double-) 方法时，它返回一个 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) ，其中包含格式化的数字和相应的货币符号。

下面的例子代码展示了如何以特定于语言的方式格式化货币：

```java
static public void displayCurrency( Locale currentLocale) {

    Double currencyAmount = new Double(9876543.21);
    Currency currentCurrency = Currency.getInstance(currentLocale);
    NumberFormat currencyFormatter = 
        NumberFormat.getCurrencyInstance(currentLocale);

    System.out.println(
        currentLocale.getDisplayName() + ", " +
        currentCurrency.getDisplayName() + ": " +
        currencyFormatter.format(currencyAmount));
}
```

上面程序输出：

```
French (France), Euro: 9 876 543,21 €
German (Germany), Euro: 9.876.543,21 €
English (United States), US Dollar: $9,876,543.21
```

乍一看，这个输出可能看起来不对，因为数值都是一样的。当然，9 876 543,21€ 不等于 $9,876,543.21。但是，请记住， [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 类不知道汇率。属于 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 类的方法格式化货币但不转换它们。

请注意， [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 类的设计使得任何给定货币永远不会有多个 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例。因此，没有公共构造函数。如前面的代码示例所示，您使用 [`getInstance`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getInstance-java.util.Locale-) 方法获取 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例。

例子 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 同样举例说明了如何使用 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 类。（注意这个示例代码不会转化货币值。）下面使用 en-US 语言设置：

![Mortgage Calculator, en-US locale](https://docs.oracle.com/javase/tutorial/figures/i18n/format/mortgage-calculator-en-us.jpg)

下面使用了 en-UK 语言设置：

![Mortgage Calculator, en-UK locale](https://docs.oracle.com/javase/tutorial/figures/i18n/format/mortgage-calculator-en-uk.jpg)

例子 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 需要以下资源文件：

- [`resources/Resources.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources.properties)
- [`resources/Resources_ar.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources_ar.properties)
- [`resources/Resources_fr.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources_fr.properties)

[`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 类包含其它方法可以检索其它货币相关信息：

- [`getAvailableCurrencies`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getAvailableCurrencies--) : 返回 JDK 中所有可用的货币

- [`getCurrencyCode`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getCurrencyCode--) : 返回 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例的 ISO 4217 数字代码

- [`getSymbol`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getSymbol--) : 返回 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例的符号。您可以选择将 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 对象指定为参数。请考虑以下摘录：

  ```java
  Locale enGBLocale = 
      new Locale.Builder().setLanguage("en").setRegion("GB").build();

  Locale enUSLocale =
      new Locale.Builder().setLanguage("en").setRegion("US").build();

  Currency currencyInstance = Currency.getInstance(enUSLocale);

  System.out.println(
      "Symbol for US Dollar, en-US locale: " +
      currencyInstance.getSymbol(enUSLocale));

  System.out.println(
      "Symbol for US Dollar, en-UK locale: " +
      currencyInstance.getSymbol(enGBLocale));
  ```

  输出如下：

  ```
  Symbol for US Dollar, en-US locale: $
  Symbol for US Dollar, en-UK locale: USD
  ```

  这个例子展示了货币符号会随着语言设置而变化。

- [`getDisplayName`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getDisplayName--) : 返回 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例的显示名称。与 [`getSymbol`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getSymbol--) 方法一样，您可以选择指定 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 对象。

**对ISO 4217货币代码的可扩展支持**

[ISO 4217](http://www.iso.org/iso/support/faqs/faqs_widely_used_standards/widely_used_standards_other/currency_codes.htm) 是国际标准组织发布的标准。它指定三个字母的代码（和等效的三位数字代码）来表示货币和资金。该标准由外部机构维护，独立于Java SE平台发布。

假设一个国家换用不同的货币，ISO 4217维护机构就会发布货币更新。要实现此更新，从而在运行时取代默认货币，请创建名为`*<JAVA_HOME>*/lib/currency.properties`的属性文件。此文件包含ISO 3166国家/地区代码的键/值对以及ISO 4217货币数据。值部分由三个以逗号分隔的ISO 4217货币值组成：字母代码，数字代码和次要单元。 以散列字符（＃）开头的任何行都被视为注释行。 例如：

```
# Sample currency property for Canada
CA=CAD,124,2
```

`CAD`代表加元，`124`是加元的数字代码，`2`是次要单位，是货币表示小数货币所需的小数位数。例如，以下属性文件将默认加拿大货币取代为没有任何小于一美元的单位的加元：

```
CA=CAD,124,0
```

**百分比**

您还可以使用 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 类的方法来设置百分比的格式。要获取特定于语言环境的格式化程序，请调用 [`getPercentInstance`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#getPercentInstance-java.util.Locale-) 方法。使用此格式化程序，小数部分（例如0.75）显示为75％。

以下代码示例显示如何格式化百分比。

```java
static public void displayPercent(Locale currentLocale) {

    Double percent = new Double(0.75);
    NumberFormat percentFormatter;
    String percentOut;

    percentFormatter = NumberFormat.getPercentInstance(currentLocale);
    percentOut = percentFormatter.format(percent);
    System.out.println(percentOut + "   " + currentLocale.toString());
}
```

这个例子输出：

```
75 %   fr_FR
75%   de_DE
75%   en_US
```

