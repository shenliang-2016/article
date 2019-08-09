#### 自定义格式

你可以使用`DecimalFormat`类来格式化十进制数字为特定于语言区域的字符串。这个类允许你控制前导和尾随的`0`，前缀和后缀，组（千）分隔符，以及小数点的显示。如果你希望改变格式化符号，比如小数点，你可以结合使用`DecimalFormatSymbols`和`DecimalFormat`类。这些类提供了数字格式化的极大弹性，不过它们也会使你的代码变得复杂。

下面将举例说明上述两个类的使用，下面的代码示例来自 [`DecimalFormatDemo`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/DecimalFormatDemo.java) 。

**构建模式**

你使用一个模式`String`来指定`DecimalFormat`的格式化属性。该模式决定了格式化之后的数字的样子。有关模式语法的完整描述，参考 [Number Format Pattern Syntax](https://docs.oracle.com/javase/tutorial/i18n/format/decimalFormat.html#numberpattern) 。

下面的例子创建一个格式化器，通过传递一个模式`String`给一个`DecimalFormat`构造器。`format`方法接受一个`double`值作为参数并返回`String`形式的格式化数字：

```java
DecimalFormat myFormatter = new DecimalFormat(pattern);
String output = myFormatter.format(value);
System.out.println(value + " " + pattern + " " + output);
```

上面代码的输出在下面表中列出。`value`是一个数字，一个`double`，将要被格式化。`pattern`是一个`String`，指定格式化属性。`output`是一个`String`，表示格式化的数字。

`DecimalFormatDemo` 程序的输出：

| `value`    | `pattern`         | `output`    | 解释                                       |
| ---------- | ----------------- | ----------- | ---------------------------------------- |
| 123456.789 | ###,###.###       | 123,456.789 | 井号 (#) 代表一个数字，逗号是千分位分隔符的占位符，点号是小数点占位符。   |
| 123456.789 | ###.##            | 123456.79   | `value` 小数点右边有3位数字，但是 `pattern` 只有两个。 `format` 方法通过舍入处理这种情况。 |
| 123.78     | 000000.000        | 000123.780  | `pattern` 指定前导和尾随`0`，因为`0`替代了模式中的井号 (#)。 |
| 12345.67   | $###,###.###      | $12,345.67  | `pattern` 中第一个字符是美元符号 ($)，注意它会直接出现在格式化 `output` 的最左边数字前面。 |
| 12345.67   | \u00A5###,###.### | ¥12,345.67  | `pattern` 使用 Unicode 编码 00A5 指定货币符号为日元 (J¥)。 |

**区域敏感的格式**

上面的例子为默认`Locale`创建一个`DecimalFormat`对象。如果你需要一个非默认`Locale`的`DecimalFormat`对象，你实例化一个`NumberFormat`然后将其转化为`DecimalFormat`。例子如下：

```java
NumberFormat nf = NumberFormat.getNumberInstance(loc);
DecimalFormat df = (DecimalFormat)nf;
df.applyPattern(pattern);
String output = df.format(value);
System.out.println(pattern + " " + output + " " + loc.toString());
```

运行前面的例子将产生下面的输出。格式化数字，下面结果中的第二列，随着`Locale`变化：

```
###,###.###      123,456.789     en_US
###,###.###      123.456,789     de_DE
###,###.###      123 456,789     fr_FR
```

到目前为止，这里讨论的格式模式遵循美国英语的惯例。例如，在模式`###,###.##`中，逗号是千位分隔符，句点表示小数点。如果最终用户没有接触到它，那么这个约定很好。但是，某些应用程序（如电子表格和报表生成器）允许最终用户定义自己的格式设置模式。对于这些应用程序，最终用户指定的格式模式应使用本地化表示法。在这些情况下，您需要在`DecimalFormat`对象上调用`applyLocalizedPattern`方法。

**修改格式化符号**

你可以使用 [DecimalFormatSymbols](https://docs.oracle.com/javase/8/docs/api/java/text/DecimalFormatSymbols.html) 类来改变由`format`方法产生而出现的格式化数字中的符号。这些符号包含小数点、千分位分隔符、负号、以及百分号等等。

下面的例子展示了`DecimalFormatSymbols`类的使用，它将一个奇怪的格式应用于数字。不常见的格式是调用`setDecimalSeparator`、`setGroupingSeparator`以及`setGroupingSize`方法的结果。

```java
DecimalFormatSymbols unusualSymbols = new DecimalFormatSymbols(currentLocale);
unusualSymbols.setDecimalSeparator('|');
unusualSymbols.setGroupingSeparator('^');

String strange = "#,##0.###";
DecimalFormat weirdFormatter = new DecimalFormat(strange, unusualSymbols);
weirdFormatter.setGroupingSize(4);

String bizarre = weirdFormatter.format(12345.678);
System.out.println(bizarre);

```

运行之后，输出下面这种包含栅栏的格式：

```
1^2345|678
```

**数字格式化模式语法**

你可以设计自己的数字格式化模式，这些模式需要遵循下面的 BNF 图定义的规则：

```
pattern    := subpattern{;subpattern}
subpattern := {prefix}integer{.fraction}{suffix}
prefix     := '\\u0000'..'\\uFFFD' - specialCharacters
suffix     := '\\u0000'..'\\uFFFD' - specialCharacters
integer    := '#'* '0'* '0'
fraction   := '0'* '#'*
```

其中使用的记号解释如下：

| Notation  | Description        |
| --------- | ------------------ |
| `X*`      | 0 个或者多个 X          |
| `(X | Y)` | X 或者 Y             |
| `X..Y`    | 从 X 到 Y 的闭区间中的任意字符 |
| `S - T`   | 存在于 S 而不存在于 T 中的字符 |
| `{X}`     | X 是可选的             |

在前面的 BNF 图中，第一个子模式指定了正数的格式。第二个子模式是可选的，指定负数的格式。

虽然未在 BNF 图中注明，但逗号可能出现在整数部分内。

在子模式中，您可以使用特殊符号指定格式。这些符号如下表所述：

| Symbol | Description                              |
| ------ | ---------------------------------------- |
| 0      | 一个数字                                     |
| #      | 一个数字，0 表示不存在                             |
| .      | 小数点占位符                                   |
| ,      | 千分位占位符                                   |
| E      | 为指数格式分隔尾数和指数                             |
| ;      | 分隔格式                                     |
| -      | 默认符号前缀                                   |
| %      | 乘以 100 并展示为百分数                           |
| ?      | 乘以 1000 并展示位千分数                          |
| ¤      | 货币符号，被货币记号替换。如果双重使用，则会被国际货币记号替换。如果在模式中使用，使用货币小数分隔符代替小数分隔符。 |
| X      | 任何其他字符都可以在前缀或后缀中使用                       |
| '      | 用来以单引号包括前缀或者后缀中的特殊字符                     |

