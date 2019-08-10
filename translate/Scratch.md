#### 处理复数

如果复数和单数形式都可能，则消息中的单词可能会有所不同。使用`ChoiceFormat`类，您可以将数目映射到单词或短语，从而允许您构造语法正确的消息。

在英语中，单词的复数和单数形式通常是不同的。当您构建包含数量的消息时，这可能会出现问题。例如，如果您的消息报告磁盘上的文件数，则可能存在以下变化：

```
There are no files on XDisk.
There is one file on XDisk.
There are 2 files on XDisk.
```

解决此问题的最快方式就是创建如下的`MessageFormat`模式：

```
There are {0,number} file(s) on {1}.
```

很不幸，上面的模式产生的语法不正确：

```
There are 1 file(s) on XDisk.
```

你可以做的更好，你可以使用 [`ChoiceFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/ChoiceFormat.html) 类。在本节中你将看到如何处理消息中的复数。通过一个简单的例子[`ChoiceFormatDemo`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/ChoiceFormatDemo.java) 逐步展示。该程序也使用了`MessageFormat`类，该类在上一节中讨论。

**1. 定义消息模式**

首先，标示消息中的变量：

![Three lines of text, with the variables in each line highlighted.](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-3.gif)

接下来，用参数替换消息中的变量，创建一个能够应用于`MessageFormat`对象的模式：

```
There {0} on {1}.
```

磁盘名称的参数，由`{1}`表示，很容易处理。你只需像处理`MessageFormat`模式中的其它`String`变量一样处理它们。此参数匹配参数值数组中下标为 1 的元素。

处理参数`{0}`更加复杂一些，因为两个原因：

* 参数替换过程会随着文件数量而有所不同。为了在运行时构建该阶段，你需要将文件数量映射到一个特定的`String`。比如，数量 1 映射到包含`is one file`短语的`String`。`ChoiceFormat`类允许你执行必要的映射。
* 如果磁盘包含多个文件，该短语包含一个整数。`MessageFormat`类允许你在短语中插入一个整数。

**2. 创建一个 ResourceBundle**

因为消息文本必须被翻译，将它隔离到一个`ResourceBundle`中：

```java
ResourceBundle bundle = ResourceBundle.getBundle(
    "ChoiceBundle", currentLocale);
```

例子程序使用属性文件支持`ResourceBundle`。[`ChoiceBundle_en_US.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/ChoiceBundle_en_US.properties) 包含以下内容：

```
pattern = There {0} on {1}.
noFiles = are no files
oneFile = is one file
multipleFiles = are {2} files
```

此属性文件的内容展示了消息将如何被构建和格式化。第一行包含`MessageFormat`模式。其它的行包含替换模式中的参数`{0}`的短语。对应于`multipleFiles`键的短语包含参数`{2}`，将被一个数字替换。

这里是属性文件的法语版本， [`ChoiceBundle_fr_FR.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/ChoiceBundle_fr_FR.properties) ：

```
pattern = Il {0} sur {1}.
noFiles = n'y a pas de fichiers
oneFile = y a un fichier
multipleFiles = y a {2} fichiers
```

**3. 创建一个消息格式化器**

这一步实例化`MessageFormat`并设置它的`Locale`：

```java
MessageFormat messageForm = new MessageFormat("");
messageForm.setLocale(currentLocale);
```

**4. 创建 Choice Formatter**

`ChoiceFormat`对象允许你选择，基于一个`double`数字，一个特定的`String`。该`double`数字的范围，以及它所映射到的`String`对象，在数组中指定：

```java
double[] fileLimits = {0,1,2};
String [] fileStrings = {
    bundle.getString("noFiles"),
    bundle.getString("oneFile"),
    bundle.getString("multipleFiles")
};
```

`ChoiceFormat`将`double`数组中的每个元素映射到具有相同索引的`String`数组中的元素。在示例代码中，0 映射到通过调用`bundle.getString(“noFiles”)`返回的`String`。巧合的是，索引与`fileLimits`数组中的值相同。如果代码将`fileLimits[0]`设置为 7，那么`ChoiceFormat`会将数字 7 映射到`fileStrings[0]`。

在实例化`ChoiceFormat`时指定`double`和`String`数组：

```java
ChoiceFormat choiceForm = new ChoiceFormat(fileLimits, fileStrings);
```

**5. 应用该模式**

还记得你在第一步中创建的模式吗？是时候从`ResourceBundle`中获取它并将它应用于`MessageFormat`对象：

```java
String pattern = bundle.getString("pattern");
messageForm.applyPattern(pattern);
```

**6. 分配该格式**

这一步中你将第四步中创建的`ChoiceFormat`对象分配给`MessageFormat`对象：

```java
Format[] formats = {choiceForm, null, NumberFormat.getInstance()};
messageForm.setFormats(formats);
```

`setFormats`方法将`Format`对象分配给消息模式中的参数。在调用`setFormats`方法之前，必须调用`applyPattern`方法。下表显示了`Format`数组的元素如何对应于消息模式中的参数：

 `ChoiceFormatDemo` 程序的`Format` 数组

| Array Element                | Pattern Argument |
| ---------------------------- | ---------------- |
| `choiceForm`                 | `{0}`            |
| `null`                       | `{1}`            |
| `NumberFormat.getInstance()` | `{2}`            |

**7. 设置消息的参数和格式**

在运行时，程序将变量分配给它传递给`MessageFormat`对象的参数数组。数组中的元素对应于模式中的参数。例如，`messageArgument[1]`映射到模式参数`{1}`，它是一个包含磁盘名称的`String`。在上一步中，程序将`ChoiceFormat`对象分配给模式的参数`{0}`。因此，分配给`messageArgument[0]`的数字决定了`ChoiceFormat`对象选择哪个`String`。如果`messageArgument[0]`大于或等于2，则包含短语`is {2} files`的`String`将替换模式中的参数`{0}`。分配给`messageArgument[2]`的数字将代替模式参数`{2}`。这是尝试这个过程的代码：

```java
Object[] messageArguments = {null, "XDisk", null};

for (int numFiles = 0; numFiles < 4; numFiles++) {
    messageArguments[0] = new Integer(numFiles);
    messageArguments[2] = new Integer(numFiles);
    String result = messageForm.format(messageArguments);
    System.out.println(result);
}
```

**8. 运行示例程序**

将程序显示的消息与步骤2的`ResourceBundle`中的短语进行比较。请注意，`ChoiceFormat`对象选择正确的短语，`MessageFormat`对象用于构造正确的消息。 `ChoiceFormatDemo`程序的输出如下：

```
currentLocale = en_US
There are no files on XDisk.
There is one file on XDisk.
There are 2 files on XDisk.
There are 3 files on XDisk.

currentLocale = fr_FR
Il n'y a pas des fichiers sur XDisk.
Il y a un fichier sur XDisk.
Il y a 2 fichiers sur XDisk.
Il y a 3 fichiers sur XDisk.
```