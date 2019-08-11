#### 补充字符作为代理

为了支持补充字符而不更改`char`原始数据类型并导致与以前的Java程序不兼容，补充字符由一对称为代理项的代码点值定义。第一个代码点是从 U+D800 到 U+DBFF 的高代理范围，第二个代码点是从 U+DC00 到 U+DFFF 的低代理范围。例如，Deseret 字符 LONG I，U+10400，用这对代理值定义：U+D801和 U+DC00。

#### 字符和字符串 API

`Character`类封装了`char`数据类型。对于J2SE第5版，在`Character`类中添加了许多方法来支持补充字符。这些API分为两类：在`char`和代码点值之间转换的方法以及验证或映射代码点的有效性的方法。

本节描述了`Character`类中可用方法的子集。 有关可用API的完整列表，请参阅 [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 类规范。

**转换方法和 Character 类**

下表包含`Character`类中最有用的转换方法或便于转换的方法。 `codePointAt`和`codePointBefore`方法包含在此列表中，因为文本通常在字符序列中找到，例如`String`，并且这些方法可用于提取所需的子字符串。

| Method(s)                                                    | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`toChars(int codePoint, char[] dst, int dstIndex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toChars-int-char:A-int-)<br />[`toChars(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toChars-int-) | 将指定的Unicode代码点转换为其UTF-16表示形式，并将其放在`char`数组中。示例用法：`Character.toChars(0x10400)` 。 |
| [`toCodePoint(char high, char low)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toCodePoint-char-char-) [`toCodePoint(CharSequence, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toCodePoint-java.lang.CharSequence-int-)<br />[`toCodePoint(char[], int, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toCodePoint-char:A-int-int-) | 将指定的参数转换为其补充代码点值。不同的方法接受不同的输入格式。 |
| [`codePointAt(char[] a, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointAt-char:A-int-)<br />[`codePointAt(char[] a, int index, int limit)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointAt-char:A-int-int-)<br />[`codePointAt(CharSequence seq, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointAt-java.lang.CharSequence-int-) | 返回指定索引处的Unicode代码点。第三种方法采用`CharSequence`，第二种方法需要索引的上限。 |
| [`codePointBefore(char[] a, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointBefore-char:A-int-)<br />[`codePointBefore(char[] a, int index, int start)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointBefore-char:A-int-int-)<br />[`codePointBefore(CharSequence seq, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointBefore-java.lang.CharSequence-int-)<br />[`codePointBefore(char[], int, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointBefore-char:A-int-int-) | 返回指定索引之前的Unicode代码点。第三种方法接受`CharSequence`，其他方法接受`char`数组。第二种方法需要索引下限。 |
| [`charCount(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#charCount-int-) | 为可由单个`char`表示的字符返回值1。为需要两个`char`s的补充字符返回值2。 |

**Character 类中的验证和映射方法**

前面使用`char`基本数据类型的一些方法，例如`isLowerCase(char)`和`isDigit(char)`，被支持补充字符的方法所取代，例如`isLowerCase(int)`和`isDigit(int)`。前面的方法仍然支持，但不能使用补充字符。要创建全局应用程序并确保代码与任何语言无缝协作，建议您使用这些方法的较新形式。

请注意，出于性能原因，大多数接受代码点的方法都不会验证代码点参数的有效性。您可以使用`isValidCodePoint`方法实现此目的。

下表列出了`Character`类中的一些验证和映射方法。

| Method(s)                                                    | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`isValidCodePoint(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isValidCodePoint-int-) | 如果代码点属于 0x0000 到 0x10FFFF 闭区间范围则返回`true`。   |
| [`isSupplementaryCodePoint(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isSupplementaryCodePoint-int-) | 如果代码点属于 0x10000 到 0x10FFFF 闭区间范围则返回`true`。  |
| [`isHighSurrogate(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isHighSurrogate-char-) | 如果指定`char`处于高代理范围 \uD800 到 \uDBFF 闭区间内时返回`true`。 |
| [`isLowSurrogate(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLowSurrogate-char-) | 如果指定`char`处于低代理范围 \uDC00 到 \uDFFF 闭区间内时返回`true`。 |
| [`isSurrogatePair(char high, char low)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isSurrogatePair-char-char-) | 如果指定的高和低代理代码值表示有效的代理项对，则返回`true`。 |
| [`codePointCount(CharSequence, int, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointCount-java.lang.CharSequence-int-int-)<br />[`codePointCount(char[], int, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointCount-char:A-int-int-) | 返回`CharSequence`或`char`数组中的Unicode代码点数。          |
| [`isLowerCase(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLowerCase-int-) [`isUpperCase(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isUpperCase-int-) | 如果指定的Unicode代码点是小写或大写字符，则返回`true`。      |
| [`isDefined(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isDefined-int-) | 如果在Unicode标准中定义了指定的Unicode代码点，则返回`true`。 |
| [`isJavaIdentifierStart(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isJavaIdentifierStart-char-) [`isJavaIdentifierStart(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isJavaIdentifierStart-int-) | 如果允许指定的字符或Unicode代码点作为Java标识符中的第一个字符，则返回`true`。 |
| [`isLetter(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLetter-int-) [`isDigit(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isDigit-int-) [`isLetterOrDigit(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLetterOrDigit-int-) | 如果指定的Unicode代码点是字母，数字或字母或数字，则返回`true`。 |
| [`getDirectionality(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#getDirectionality-int-) | 返回给定Unicode代码点的Unicode方向性属性。                   |
| [`Character.UnicodeBlock.of(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html#of-int-) | 返回表示包含给定Unicode代码点的Unicode块的对象，如果代码点不是已定义块的成员，则返回`null`。 |

**String 类中的方法**

`String`，`StringBuffer`和`StringBuilder`类也有使用补充字符的构造函数和方法。下表列出了一些常用方法。 有关可用API的完整列表，请参阅[`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)，[`StringBuffer` ](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html)和[`StringBuilder`](https://docs.oracle.com/javase/8/docs/api /java/lang/StringBuilder.html)类的 javadoc。

| Constructor or Methods                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`String(int[] codePoints, int offset, int count)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#String-int:A-int-int-) | 分配一个新的`String`实例，该实例包含Unicode代码点数组的子数组中的字符。 |
| [`String.codePointAt(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#codePointAt-int-)<br />[`StringBuffer.codePointAt(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#codePointAt-int-)<br />[`StringBuilder.codePointAt(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#codePointAt-int-) | 返回指定索引处的Unicode代码点。                              |
| [`String.codePointBefore(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#codePointBefore-int-)<br />[`StringBuffer.codePointBefore(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#codePointBefore-int-)<br />[`StringBuilder.codePointBefore(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#codePointBefore-int-) | 返回指定索引之前的Unicode代码点。                            |
| [`String.codePointCount(int beginIndex, int endIndex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#codePointCount-int-int-) [`StringBuffer.codePointCount(int beginIndex, int endIndex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#codePointCount-int-int-) [`StringBuilder.codePointCount(int beginIndex, int endIndex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#codePointCount-int-int-) | 返回指定范围内的Unicode代码点数。                            |
| [`StringBuffer.appendCodePoint(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#appendCodePoint-int-) [`StringBuilder.appendCodePoint(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#appendCodePoint-int-) | 将指定代码点的字符串表示形式追加到序列中。                   |
| [`String.offsetByCodePoints(int index, int codePointOffset)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#offsetByCodePoints-int-int-) [`StringBuffer.offsetByCodePoints(int index, int codePointOffset)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#offsetByCodePoints-int-int-) [`StringBuilder.offsetByCodePoints(int index, int codePointOffset)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#offsetByCodePoints-int-int-) | 返回给定索引偏移给定数量的代码点的索引。                     |

#### 例子

此页面包含一些代码片段，向您展示几个常见方案。

**从代码点创建 `String`**

```java
String newString(int codePoint) {
    return new String(Character.toChars(codePoint));
}
```

**从代码点创建`String`  - 针对BMP字符进行优化**

`Character.toChars`方法创建一个临时数组，该数组使用一次然后丢弃。如果这会对性能产生负面影响，则可以使用以下方法对BMP字符进行优化（由单个`char`值表示的字符）。在这种方法中，只为补充字符调用`toChars`。

```java
String newString(int codePoint) {
    if (Character.charCount(codePoint) == 1) {
        return String.valueOf(codePoint);
    } else {
        return new String(Character.toChars(codePoint));
    }
}
```

**批量创建 `String` 对象**

要创建大量字符串，前一个代码段的批量版本会重用`toChars`方法使用的数组。此方法为每个代码点创建一个单独的`String`实例，并针对BMP字符进行了优化。

```java
String[] newStrings(int[] codePoints) {
    String[] result = new String[codePoints.length];
    char[] codeUnits = new char[2];
    for (int i = 0; i < codePoints.length; i++) {
        int count = Character.toChars(codePoints[i], codeUnits, 0);
        result[i] = new String(codeUnits, 0, count);
    }
    return result;
}
```

**生成消息**

格式化API支持补充字符。以下示例是生成消息的简单方法。

```java
// recommended
System.out.printf("Character %c is invalid.%n", codePoint);
```

以下方法很简单并且避免了连接，这使得文本更难以本地化，因为并非所有语言都以与英语相同的顺序将数值插入到字符串中。

```java
// not recommended
System.out.println("Character " + String.valueOf(char) + " is invalid.");
```

#### 设计考量

要编写使用任何脚本无缝地为任何语言工作的代码，需要记住一些事项。

| Consideration                                                | Reason                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 避免使用那些使用`char`数据类型的方法。                       | 避免使用`char`基本数据类型或使用`char`数据类型的方法，因为使用该数据类型的代码不适用于补充字符。对于采用`char`类型参数的方法，请使用相应的`int`方法（如果可用）。例如，使用`Character.isDigit(int)`方法而不是`Character.isDigit(char)`方法。 |
| 使用 `isValidCodePoint` 方法验证代码点值。                   | 代码点被定义为`int`数据类型，它允许超出代码点值有效范围的值从 0x0000 到 0x10FFFF。出于性能原因，将代码点值作为参数的方法不会检查参数的有效性，但您可以使用`isValidCodePoint`方法来检查其值。 |
| 使用 `codePointCount` 方法来对字符计数。                     | `String.length()`方法返回字符串中的代码单元数或16位`char`值。如果字符串包含增补字符，则计数可能会产生错误，因为它不会反映代码点的真实数量。要准确计算字符数（包括增补字符），请使用`codePointCount`方法。 |
| 使用 `String.toUpperCase(int codePoint)` 和 `String.toLowerCase(int codePoint)` 方法，而不是 `Character.toUpperCase(int codePoint)` 或者 `Character.toLowerCase(int codePoint)` 方法。 | 虽然`Character.toUpperCase(int)`和`Character.toLowerCase(int)`方法可以处理代码点值，但有些字符无法一对一转换。例如，小写的德语字符 ß 在转换为大写时变为两个字符 SS。同样，小希腊西格玛字符根据字符串中的位置而不同。`Character.toUpperCase(int)`和`Character.toLowerCase(int)`方法无法处理这些类型的情况; 但是，`String.toUpperCase`和`String.toLowerCase`方法正确处理这些情况。 |
| 请谨慎删除字符。                                             | 当调用索引指向补充字符的`StringBuilder.deleteCharAt(int index)`或`StringBuffer.deleteCharAt(int index)`方法时，只删除该字符的前半部分（第一个`char`值）。首先，在字符上调用`Character.charCount`方法，以确定是否必须删除一个或两个`char`值。 |
| 请谨慎逆序一个序列中的字符。                                 | 当在包含增补字符的文本上调用`StringBuffer.reverse()`或`StringBuilder.reverse()`方法时，高和低代理对被反转，这导致不正确且可能无效的代理对。 |

#### 其它资源

For more information about supplementary characters, see the following resources.

- [Java 平台中的增补字符](http://www.oracle.com/technetwork/articles/javase/supplementary-142654.html)
- [Unicode联盟](http://unicode.org/)
- [Unicode术语表](http://unicode.org/glossary/)

s