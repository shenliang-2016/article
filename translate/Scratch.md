### Unicode

*Unicode*是一种计算行业标准，旨在对全世界书面语言中使用的字符进行一致且唯一的编码。Unicode标准使用十六进制表示字符。例如，值 0x0041 表示拉丁字符 A。Unicode标准最初使用16位来设计字符，因为当时主要计算机是16位PC。

创建Java语言规范时，接受Unicode标准，并将`char`原语定义为16位数据类型，十六进制范围内的字符从 0x0000 到 0xFFFF。

由于16位编码支持2<sup>16</sup>（65,536）个字符，这不足以定义全世界使用的所有字符，因此Unicode标准扩展为 0x10FFFF，支持超过一百万个字符。Java编程语言中字符的定义无法从16位更改为32位，而不会导致数百万Java应用程序无法正常运行。为了纠正定义，开发了一种方案来处理无法以16位编码的字符。

值超出16位范围且在 0x10000 到 0x10FFFF 范围内的字符称为*补充字符*，并定义为一对`char`值。

本课程包含以下章节：

- [术语](https://docs.oracle.com/javase/tutorial/i18n/text/terminology.html) - 解释代码点和其他术语。
- [补充字符作为代理](https://docs.oracle.com/javase/tutorial/i18n/text/supplementaryChars.html) - 16位代理用于实现补充字符，这些补充字符不能作为单个原始`char`数据类型实现。
- [字符和字符串API](https://docs.oracle.com/javase/tutorial/i18n/text/characterClass.html) -`Character`，`String`相关的 API 以及相关的类的列表。
- [示例用法](https://docs.oracle.com/javase/tutorial/i18n/text/usage.html) - 提供了几个有用的代码片段。
- [设计注意事项](https://docs.oracle.com/javase/tutorial/i18n/text/design.html) - 要记住[设计注意事项](https://docs.oracle.com/javase/tutorial/i18n/text/design.html)，以确保您的应用程序可以使用任何语言脚本。
- [更多信息](https://docs.oracle.com/javase/tutorial/i18n/text/info.html) - 提供了更多资源的列表。

#### 术语

*字符*是具有语义值的最小文本单元。

*字符集*是可能由多种语言使用的字符集合。例如，拉丁字符集由英语和大多数欧洲语言使用，尽管希腊语字符集仅由希腊语使用。

*编码字符集*是一个字符集，其中每个字符被分配一个唯一的编号。

*代码点*是可以在编码字符集中使用的值。代码点是32位`int`数据类型，其中低21位表示有效代码点值，高11位表示0。

Unicode *代码单元*是一个16位的`char`值。例如，假设一个`String`包含字母“abc”，后跟 Deseret LONG I，用两个`char`值表示。该字符串包含四个字符，四个代码点，但包含五个代码单元。

要以Unicode表示字符，十六进制值以字符串 U+ 为前缀。Unicode标准的有效代码点范围是 U+0000 到 U+10FFFF，包括端点。拉丁字符A的代码点值是 U+0041。代表欧元货币的字符 € 具有代码点值 U+20AC。 Deseret 字母表中的第一个字母 LONG I 的代码点值为 U+10400。

下表显示了几个字符的代码点值：

| Character       | Unicode Code Point | Glyph                                                        |
| --------------- | ------------------ | ------------------------------------------------------------ |
| Latin A         | U+0041             | ![The Latin character A](https://docs.oracle.com/javase/tutorial/figures/i18n/000041.gif) |
| Latin sharp S   | U+00DF             | ![The Latin small letter sharp S](https://docs.oracle.com/javase/tutorial/figures/i18n/0000df.gif) |
| Han for East    | U+6771             | ![The Han character for east, eastern or eastward](https://docs.oracle.com/javase/tutorial/figures/i18n/006771.gif) |
| Deseret, LONG I | U+10400            | ![The Deseret capital letter long I](https://docs.oracle.com/javase/tutorial/figures/i18n/010400.gif) |

如前所述，在 U+10000 到 U+10FFFF 范围内的字符被称为补充字符。从 U+0000 到 U+FFFF 的字符集有时被称为*基本多语言平面（BMP）*。

更多术语可以在 [更多信息](https://docs.oracle.com/javase/tutorial/i18n/text/info.html) 页面上列出的*Unicode术语表*中找到。

