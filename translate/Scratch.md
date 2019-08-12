#### 字符边界

如果你的应用允许终端用户高亮当个字符或者在文本中每次移动一个字符，就需要定位字符边界。为了创建一个`BreakIterator`实例来定位字符边界，调用`getCharacterInstance`方法，如下：

```java
BreakIterator characterIterator =
    BreakIterator.getCharacterInstance(currentLocale);
```

此类型的`BreakIterator`实例探测用户字符之间的边界，而不仅仅是 Unicode 字符。

一个用户字符可能由一个或者多个 Unicode 字符组成。比如，用户字符 ü 能够由结合 Unicode 字符 \u0075 (u) 和 \u00a8 (¨) 来构成。这不是最好的例子，因为用户字符 ü 还可以由单个的 Unicode 字符 \u00fc 表示。我们接下来使用阿拉伯语来举例。

阿拉伯语中的单词"房屋"是：

![The Arabic pictograph for House](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-5.gif)

这个单词包含三个用户字符，但是它是由下面六个 Unicode 字符组成：

```java
String house = "\u0628" + "\u064e" + "\u064a" + "\u0652" + "\u067a" + "\u064f";
```

`house`字符串中在位置1、3和5上的 Unicode 字符是变音符号。阿拉伯语中使用变音符号改变单词的含义。例子中的变音符号是非空格字符，因为它们出现在基本字符之上。在阿拉伯语的字处理软件中，你不能在屏幕上为每个字符串中的 Unicdoe 字符移动光标。相反，你必须为每个用户字符移动光标，而每个用户字符可能由多个 Unicode 字符组成。因此，你必须使用`BreakInterator`来扫描字符串中的用户字符。

例子程序 [`BreakIteratorDemo`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BreakIteratorDemo.java) ，创建一个`BreakIterator`来扫描阿拉伯字符。改程序传递`BreakIterator`，以及之前创建的`String`对象，给名为`listPositions`的方法：

```java
BreakIterator arCharIterator = BreakIterator.getCharacterInstance(
                                   new Locale ("ar","SA"));
listPositions (house, arCharIterator);
```

`listPositions`方法使用一个`BreakIterator`来定位字符串中的字符边界。注意，`BreakIteratorDemo`使用`setText`方法将特定字符串分配给`BreakIterator`。改程序使用`first`方法来检索首个字符边界，然后调用`next`方法直到返回`BreakIterator.DONE`被返回。代码如下：

```java
static void listPositions(String target, BreakIterator iterator) {
                
    iterator.setText(target);
    int boundary = iterator.first();

    while (boundary != BreakIterator.DONE) {
        System.out.println (boundary);
        boundary = iterator.next();
    }
}
```

`listPositions`方法打印下面的字符串`house`中用户字符的字符边界位置。注意，其中的变音字符的位置没有列出：

```
0
2
4
6
```

#### 单词边界

通过调用`getWordIterator`方法来实例化`BreakIterator`以探测单词边界：

```java
BreakIterator wordIterator =
    BreakIterator.getWordInstance(currentLocale);
```

你将会希望创建这样一个`BreakIterator`，当你的应用程序需要操作单个词汇时。这些操作通常是常见的字处理功能，比如选择、剪切、粘贴以及拷贝等等。或者，你的应用程序可能需要搜索单词，同时它必须能够区别整个单词域简单的字符串。

当`BreakIterator`分析单词边界时，它区分单词和不属于单词一部分的字符。这些包含空格、制表符、标点符号以及大部分的符号等，两侧都是单词边界。

后面的示例（来自程序  [`BreakIteratorDemo`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BreakIteratorDemo.java) ）标记了文本中的单词边界。该程序创建`BreakIterator`，然后调用`markBoundaries`方法：

```java
Locale currentLocale = new Locale ("en","US");

BreakIterator wordIterator =
    BreakIterator.getWordInstance(currentLocale);

String someText = "She stopped. " +
    "She said, \"Hello there,\" and then went " +
    "on.";

markBoundaries(someText, wordIterator);
```

`markBoundaries`方法在`BreakIteratorDemo.java`中定义。此方法通过在目标字符串下打印插入符号（^）来标记边界。在下面的代码中，注意`while`循环，其中`markBoundaries`通过调用`next`方法来扫描字符串：

```java
static void markBoundaries(String target, BreakIterator iterator) {

    StringBuffer markers = new StringBuffer();
    markers.setLength(target.length() + 1);
    for (int k = 0; k < markers.length(); k++) {
        markers.setCharAt(k,' ');
    }

    iterator.setText(target);
    int boundary = iterator.first();

    while (boundary != BreakIterator.DONE) {
        markers.setCharAt(boundary,'^');
        boundary = iterator.next();
    }

    System.out.println(target);
    System.out.println(markers);
}
```

`markBoundaries`方法的输出如下。注意插入符号（^）与标点符号和空格相关的位置：

```
She stopped.  She said, "Hello there," and then
^  ^^      ^^ ^  ^^   ^^^^    ^^    ^^^^  ^^   ^

went on.
^   ^^ ^^
```

`BreakIterator`类可以轻松地从文本中选择单词。您不必编写自己的例程来处理各种语言的标点符号规则， `BreakIterator`类为您完成此操作。

以下示例中的`extractWords`方法提取并打印给定字符串的单词。请注意，此方法使用`Character.isLetterOrDigit`来避免打印包含空格字符的“单词”。

```java
static void extractWords(String target, BreakIterator wordIterator) {

    wordIterator.setText(target);
    int start = wordIterator.first();
    int end = wordIterator.next();

    while (end != BreakIterator.DONE) {
        String word = target.substring(start,end);
        if (Character.isLetterOrDigit(word.charAt(0))) {
            System.out.println(word);
        }
        start = end;
        end = wordIterator.next();
    }
}
```

`BreakIteratorDemo`程序调用`extractWords`，并将其传递给前一个示例中使用的相同目标字符串。 `extractWords`方法打印出以下单词列表：

```
She
stopped
She
said
Hello
there
and
then
went
on
```

#### 语句边界

您可以使用`BreakIterator`来确定句子边界。首先使用`getSentenceInstance`方法创建`BreakIterator`：

```java
BreakIterator sentenceIterator =
    BreakIterator.getSentenceInstance(currentLocale);
```

为了显示句子边界，程序使用`markBoundaries`方法，该方法在  [Word Boundaries](https://docs.oracle.com/javase/tutorial/i18n/text/word.html) 一节中讨论。`markBoundaries`方法在字符串下面打印插入符号（^）以指示边界位置。这里有些例子：

```
She stopped.  She said, "Hello there," and then went on.
^             ^                                         ^

He's vanished!  What will we do?  It's up to us.
^               ^                 ^             ^

Please add 1.5 liters to the tank.
^                                 ^
```

#### 行边界

格式化文本或执行换行的应用程序必须找到潜在的换行符。您可以使用使用`getLineInstance`方法创建的`BreakIterator`找到这些换行符或边界：

```java
BreakIterator lineIterator =
    BreakIterator.getLineInstance(currentLocale);
```

此`BreakIterator`确定可以在下一行中断开以继续的文本在字符串中的位置。`BreakIterator`检测到的位置是潜在的换行符。屏幕上显示的实际换行符可能不一样。

下面的两个示例使用`BreakIteratorDemo.java`的`markBoundaries`方法来显示`BreakIterator`检测到的行边界。`markBoundaries`方法通过在目标字符串下面打印插入符号（^）来指示行边界。

根据`BreakIterator`，在一系列空白字符（空格，制表符，换行符）终止后会出现行边界。在以下示例中，请注意您可以在检测到的任何边界处断开行：

```
She stopped.  She said, "Hello there," and then went on.
^   ^         ^   ^     ^      ^     ^ ^   ^    ^    ^  ^
```

在连字符后立即发生潜在的换行：

```
There are twenty-four hours in a day.
^     ^   ^      ^    ^     ^  ^ ^   ^
```

下一个示例使用名为`formatLines`的方法将一长串文本分成固定长度的行。此方法使用`BreakIterator`来定位潜在的换行符。`formatLines`方法简短，而且由于`BreakIterator`，它与`locale`无关。下面是源代码：

```java
static void formatLines(
    String target, int maxLength,
    Locale currentLocale) {

    BreakIterator boundary = BreakIterator.
        getLineInstance(currentLocale);
    boundary.setText(target);
    int start = boundary.first();
    int end = boundary.next();
    int lineLength = 0;

    while (end != BreakIterator.DONE) {
        String word = target.substring(start,end);
        lineLength = lineLength + word.length();
        if (lineLength >= maxLength) {
            System.out.println();
            lineLength = word.length();
        }
        System.out.print(word);
        start = end;
        end = boundary.next();
    }
}
```

`BreakIteratorDemo`程序调用`formatLines`方法，如下所示：

```
String moreText =
    "She said, \"Hello there,\" and then " +
    "went on down the street. When she stopped " +
    "to look at the fur coats in a shop + "
    "window, her dog growled. \"Sorry Jake,\" " +
    "she said. \"I didn't know you would take " +
    "it personally.\"";

formatLines(moreText, 30, currentLocale);
```

 `formatLines` 的调用输出：

```
She said, "Hello there," and
then went on down the
street. When she stopped to
look at the fur coats in a
shop window, her dog
growled. "Sorry Jake," she
said. "I didn't know you
would take it personally."
```

