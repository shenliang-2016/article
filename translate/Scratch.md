### 探测文本边界

操作文本的应用程序需要定位文本中的边界。比如，考虑常见的文字处理软件功能：高亮一个字符、切分一个单词、移动光标到下一个语句，以及行尾单词的折行。为了执行这些功能，文字处理器必须能够探测文本中的逻辑边界。幸运的是，你不需要自己编写这种边界分析程序。你可以直接使用 [`BreakIterator`](https://docs.oracle.com/javase/8/docs/api/java/text/BreakIterator.html)  类提供的方法。

**[关于 BreakIterator 类](https://docs.oracle.com/javase/tutorial/i18n/text/about.html)**

本节讨论 `BreakIterator` 类的实例方法和虚拟光标。

**[字符边界](https://docs.oracle.com/javase/tutorial/i18n/text/char.html)**

本节中，你将学到用户字符和 Unicode 字符之间的差异，以及如何使用 `BreakIterator` 定位用户字符。

**[词汇边界](https://docs.oracle.com/javase/tutorial/i18n/text/word.html)**

如果你的应用程序需要选择或者定位文本中的单词，你将发现 `BreakIterator` 非常有用。

**[语句边界](https://docs.oracle.com/javase/tutorial/i18n/text/sentence.html)**

确定语句的边界可能是有问题的，因为语句这个术语在许多书面语言中含义并不明确。本节介绍几种你可能遇到的问题，以及 `BreakIterator` 类处理它们的方法。

**[行边界](https://docs.oracle.com/javase/tutorial/i18n/text/line.html)**

本节介绍如何使用 `BreakIterator` 类定义文本字符串中潜在的行。

#### 关于 BreakIterator 类

`BreakIterator` 类是区域敏感的，因为文本边界会因语言而不同。比如，不同的语言的断行语法规则是不同的。为了确定 `BreakIterator` 支持的区域，调用 `getAvailableLocales` 方法，如下：

```java
Locale[] locales = BreakIterator.getAvailableLocales();
```

你可以使用 `BreakIterator` 类分析四种边界：字符、单词、语句以及潜在断行。当实例化一个 `BreakIterator` 时，你调用合适的工厂方法：

* `getCharacterInstance`
* `getWordInstance`
* `getSentenceInstance`
* `getLineInstance`

每个 `BreakInterator` 实例只能够探测一种边界类型。如果你希望同时定位字符边界和单词边界，你需要创建两个单独的实例。

`BreakIterator` 拥有一个虚拟光标指向文本字符串中的当前边界。你可以在文本中使用`previous`和`next` 方法来移动该光标。比如，如果你已经使用`getWordInstance`创建了`BreakIterator`，每次你调用`next` 方法，该光标将移动到文本中的下一个单词边界。光标移动方法返回一个整数，表示边界的位置。此位置是文本字符串中将跟随边界的字符的索引。与字符串索引一样，边界从零开始。第一个边界处于位置0，最后一个边界是字符串的长度。下图显示了一行文本中`previous`和`next`方法检测到的单词边界：

[![The text 'Hope is the thing with feathers', with the boundaries indicated.](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-4.gif)](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-4.gif)
*此图片已缩小到适合页面。单击图像以其自然大小查看它。*

您应该仅将`BreakIterator`类与自然语言文本一起使用。要标记编程语言，请使用`StreamTokenizer`类。

以下部分给出了每种边界分析的示例。编码示例来自名为 [`BreakIteratorDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BreakIteratorDemo.java) 的源代码文件。

