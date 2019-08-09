### 消息

我们都喜欢使用那些可以让我们知道什么东西正在运行的程序。程序通常通过显示状态和错误消息来及时通知我们。当然，这些消息需要被转化以便于全世界的终端用户理解。 [Isolating Locale-Specific Data](https://docs.oracle.com/javase/tutorial/i18n/resbundle/index.html) 章节讨论转化文本消息。通常，将一个消息`String`放到`ResourceBundle`中之后你的任务就完成了。不过，如果你的消息中携带了变量数据，你就必须执行某些额外步骤来准备转化。

*复合*消息包含变量数据。在下面的复合消息中，变量数据由下划线标出：

```html
The disk named MyDisk contains 300 files.
The current balance of account #34-09-222 is $2,745.72.
405,390 people have visited your website since January 1, 2009.
Delete all files older than 120 days.
```

您可能想通过连接短语和变量来构造前面列表中的最后一条消息，如下所示：

```java
double numDays;
ResourceBundle msgBundle;
// ...
String message = msgBundle.getString(
                     "deleteolder" +
                     numDays.toString() +
                     msgBundle.getString("days"));
```

此方法在英语环境下工作良好，但是在那些动词放在句子末尾的语言环境中不行。因为消息中的词语的顺序是硬编码的，你的本地化器将无法为所有语言创建语法正确的翻译。

当你需要使用复合消息时你应该如何编写你的本地化器？你可以使用`MessageFormat`类，就是本章节的主题。

------

**警告：**复合消息很难翻译，因为消息文本是分成若干片段的。如果你使用复合消息，本地化过程将更加耗时和消耗资源。因而你应该只在必要时才使用复合消息。

------

**[处理复合消息](https://docs.oracle.com/javase/tutorial/i18n/format/messageFormat.html)**

一条复合消息可能包含若干种变量：日期、时间、字符串、数字、货币、以及百分数。为了以区域无关的形式格式化复合消息，你可以构建一个可应用于`MessageFormat`对象的模式。

**[处理复数](https://docs.oracle.com/javase/tutorial/i18n/format/choiceFormat.html)**

如果复数和单数单词形式都可能，则消息中的单词通常会有所不同。使用`ChoiceFormat`类，您可以将数字映射到单词或短语，从而允许您构造语法正确的消息。

#### 处理复合消息

一条复合消息可能包含若干种变量：日期、时间、字符串、数字、货币、以及百分数。为了以区域无关的形式格式化复合消息，你可以构建一个可应用于`MessageFormat`对象的模式，并将该模式存储到一个`ResourceBundle`种。

接下来逐步分析例子程序，本节举例说明如何国际化一个复合消息。例子程序使用 [`MessageFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/MessageFormat.html) 类。例子程序的完整源码在文件 [`MessageFormatDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/MessageFormatDemo.java) 中。德国区域的属性放在 [`MessageBundle_de_DE.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/MessageBundle_de_DE.properties) 文件中。

**1. 标示消息中的变量**

假定你想要国际化下面的消息：

![The following line of text: At 1:15 on April 13, 1998, we detected 7 spaceships on the planet Mars.  The variable data (1:15, April 13,1998, 7, and Mars) have been underlined.](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-2.gif)

注意，我们已经用下划线标出变量数据并且标示出将使用何种对象类型来表示该数据。

**2. 将消息模式隔离到一个 ResourceBundle 中**

将消息保存到名为`MessageBundle`的`ResouceBundle`中。如下所示：

```java
ResourceBundle messages =
   ResourceBundle.getBundle("MessageBundle", currentLocale);
```

该`ResouceBundle`由对应各种`Locale`的属性文件支持。因为该`ResourceBundle`名为`MessageBundle`，则用于 U.S.English 的属性文件名为`MessageBundle_en_US.properties`。该文件的内容如下：

```
template = At {2,time,short} on {2,date,long}, \
    we detected {1,number,integer} spaceships on \
    the planet {0}.
planet = Mars
```

属性文件的第一行包含了消息模式。如果你比较该模式与第一步中展示的消息文本，你将会发现消息文本中的每个变量都被大括号包围的参数替换了。每个参数都以称为参数号的数字开头，该数值对应于持有参数值的`Object`数组中元素的下标。注意，模式中的参数号并没有一定顺序。你可以讲参数放在模式中任何位置。唯一的要求就是参数号在参数值数组中有对应的元素。

下一步讨论该参数值数组，但是首先让我们看看模式中每个参数。下表提供了有关参数的一些细节：

| Argument             | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| `{2,time,short}`     | `Date`对象的时间部分，`short`风格指定`DateFormat.SHORT`格式化风格。 |
| `{2,date,long}`      | `Date`对象的日期部分，同一个`Date`对象被用于时间和日期变量。在`Object`参数数组中持有该`Date`对象的元素的下标是 2。 |
| `{1,number,integer}` | 一个`Number`对象，进一步使用`integer`数字样式限定。          |
| `{0}`                | `ResourceBundle`中对应于`planet`键的`String`。               |

有关参数语法的完整描述，参考 [`MessageFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/MessageFormat.html) 类的文档。

**3. 设置消息参数**

以下代码行为模式中的每个参数赋值。 `messageArguments`数组中元素的索引与模式中的参数号匹配。例如，索引1处的`Integer`元素对应于模式中的`{1,number,integer}`参数。因为它必须被翻译，元素0处的`String`对象将使用`getString`方法从`ResourceBundle`获取。以下是定义消息参数数组的代码：

```java
Object[] messageArguments = {
    messages.getString("planet"),
    new Integer(7),
    new Date()
};
```

**4. 创建格式化器**

接下来，创建一个`MessageFormat`对象。你设定`Locale`因为消息包含`Date`和`Number`对象，应该给以区域敏感的方式格式化。

```java
MessageFormat formatter = new MessageFormat("");
formatter.setLocale(currentLocale);
```

**5. 使用模式和参数格式化消息**

此步骤显示模式，消息参数和格式化程序如何一起工作。首先，使用`getString`方法从`ResourceBundle`获取模式`String`。模式的关键是“模板”。使用`applyPattern`方法将模式`String`传递给格式化器。然后通过调用`format`方法使用消息参数数组格式化消息。 `format`方法返回的`String`已准备好显示。所有这一切都只需两行代码即可完成：

```java
formatter.applyPattern(messages.getString("template"));
String output = formatter.format(messageArguments);
```

**6. 运行例子程序**

演示程序打印英语和德语语言环境的翻译消息，并正确格式化日期和时间变量。请注意，英语和德语动词（“detected”和“entdeckt”）位于相对于变量的不同位置：

```
currentLocale = en_US
At 10:16 AM on July 31, 2009, we detected 7
spaceships on the planet Mars.
currentLocale = de_DE
Um 10:16 am 31. Juli 2009 haben wir 7 Raumschiffe
auf dem Planeten Mars entdeckt.
```