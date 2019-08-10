## 使用文本

几乎所有具有用户界面的程序都操纵文本。在国际市场上，您的程序显示的文本必须符合来自世界各地的语言规则。Java编程语言提供了许多类，可帮助您以与语言环境无关的方式处理文本。

[检查字符属性](https://docs.oracle.com/javase/tutorial/i18n/text/charintro.html)

本章节解释如何使用`Character`比较方法来检测所有主要语言的字符属性。

[比较字符串](https://docs.oracle.com/javase/tutorial/i18n/text/collationintro.html)

本章节中你将学到如何使用`Collator`类执行区域无关的字符串比较。

[探测文本边界](https://docs.oracle.com/javase/tutorial/i18n/text/boundaryintro.html)

本章节展示`BreakIterator`类如何探测字符、词语、语句以及行边界。

[转化非Unicode文本](https://docs.oracle.com/javase/tutorial/i18n/text/convertintro.html)

世界各地的不同计算机系统以各种编码方案存储文本。本节介绍可帮助您在Unicode和其他编码之间转换文本的类。

[正则化 API](https://docs.oracle.com/javase/tutorial/i18n/text/normalizerapi.html)

本节解释如何使用正则化 API 来转化不同正则化形式的文本。

[通过 JTextComponent 类使用双向文本](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html)

本节讨论如何使用双向文本，该文本包含从左到右和从右到左两个方向运行的文本。

### 检查字符属性

您可以根据字符的属性对字符进行分类。例如，X 是大写字母，4 是十进制数字。检查字符属性是验证最终用户输入的数据的常用方法。例如，如果您在线销售图书，您的订单输入屏幕应验证数量字段中的字符是否都是数字。

不习惯编写全球化软件的开发人员可以通过将字符与字符常量进行比较来确定字符的属性。例如，他们可能会编写如下代码：

```java
char ch;
//...

// This code is WRONG!

// check if ch is a letter
if ((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z'))
    // ...

// check if ch is a digit
if (ch >= '0' && ch <= '9')
    // ...

// check if ch is a whitespace
if ((ch == ' ') || (ch =='\n') || (ch == '\t'))
    // ...
```

上面的代码时错误的，因为它只能用于英语和很少几种其它语言。为了国际化该程序，改成如下形式：

```java
char ch;
// ...

// This code is OK!

if (Character.isLetter(ch))
    // ...

if (Character.isDigit(ch))
    // ...

if (Character.isSpaceChar(ch))
    // ...
```

[`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 方法依赖 Unicode 标准来确定字符的属性。Unicode 是一种支持世界主要语言的16位字符编码。在Java编程语言中，`char`值表示 Unicode 字符。如果使用适当的`Character`方法检查`char`的属性，则代码将适用于所有主要语言。例如，如果字符是中文，德语，阿拉伯语或其他语言的字母，则`Character.isLetter`方法返回`true`。

以下列表给出了一些最有用的`Character`比较方法。 `Character` API文档完全指定了方法。

- `isDigit`
- `isLetter`
- `isLetterOrDigit`
- `isLowerCase`
- `isUpperCase`
- `isSpaceChar`
- `isDefined`

`Character.getType`方法返回字符的 Unicode 类别。每个类别对应于`Character`类中定义的常量。例如，`getType`返回字符 A 的`Character.UPPERCASE_LETTER`常量。有关`getType`返回的类别常量的完整列表，请参阅[`Character`](https://docs.oracle.com /javase/8/docs/api/java/lang/Character.html) API文档。以下示例显示如何使用`getType`和`Character`类别常量。这些`if`语句中的所有表达式都是`true`：

```java
if (Character.getType('a') == Character.LOWERCASE_LETTER)
    // ...

if (Character.getType('R') == Character.UPPERCASE_LETTER)
    // ...

if (Character.getType('>') == Character.MATH_SYMBOL)
    // ...

if (Character.getType('_') == Character.CONNECTOR_PUNCTUATION)
    // ...
```