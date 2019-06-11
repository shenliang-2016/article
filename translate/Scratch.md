### 文件 I/O

----

**注意：**  本教程介绍的文件 I/O 机制包含在 JDK 7 发布版本中。Java SE 6 版本中的文件 I/O 教程非常简短，不过你仍然可以下载 [Java SE Tutorial 2008-03-14](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-tutorials-419421.html#tutorial-2008_03_14-oth-JPR) 版本的教程，其中包含早期版本的文件 I/O 内容。

----

`java.nio.file` 包以及它的相关包，`java.nio.file.attribute`，提供对文件 I/O 的完善支持，用来访问默认文件系统。尽管该 API 包含许多类，你只需要关注少量几个入口点。你将发现这些 API 非常直观而且容易使用。

本教程以一个问题 [path 是什么?](https://docs.oracle.com/javase/tutorial/essential/io/path.html) 开始，然后，介绍 [Path 类](https://docs.oracle.com/javase/tutorial/essential/io/pathClass.html) ，包的主要入口点。接下来解释了`Path` 类中的方法相关的 [语法操作](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html) 。本教程随后转向包中的其他主要的类，`Files` 类，其中包含文件操作方法。首先介绍许多 [文件操作](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html) 通用的概念。然后介绍用于文件 [检查](https://docs.oracle.com/javase/tutorial/essential/io/check.html), [删除](https://docs.oracle.com/javase/tutorial/essential/io/delete.html), [拷贝](https://docs.oracle.com/javase/tutorial/essential/io/copy.html), 以及 [移动](https://docs.oracle.com/javase/tutorial/essential/io/move.html) 的方法。

本教程介绍了如何管理 [元数据](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) ，在继续介绍 [文件I/O](https://docs.oracle.com/javase/tutorial/essential/io/file.html) 和 [目录I/O](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html) 之前。[随机访问文件](https://docs.oracle.com/javase/tutorial/essential/io/rafs.html) 解释了 [符号和硬链接](https://docs.oracle.com/javase/tutorial/essential/io/links.html) 特定的问题。 

接下来，介绍一些非常强大但更高级的主题。首先，演示了 [递归遍历文件树](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) ，然后是有关如何 [使用通配符搜索文件的信息](https://docs.oracle.com/javase/tutorial/essential/io/find.html) 。接下来，将解释和演示如何 [查看更改目录](https://docs.oracle.com/javase/tutorial/essential/io/notification.html) 。然后，对 [不适合其他地方的方法](https://docs.oracle.com/javase/tutorial/essential/io/misc.html) 进行了一些介绍。

最后，如果您在 Java SE 7 发行版之前编写了文件 I/O代码，则会有[从旧API到新API的映射](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html#mapping) ，以及关于`File.toPath`方法的重要信息，供希望 [利用新API而不重写现有代码](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html#interop) 的开发人员使用。

#### 什么是 Path?（其他文件系统事实）

文件系统以某种形式存储和组织某些形式的媒体上的文件，通常是一个或多个硬盘驱动器，以便可以容易地检索它们。目前使用的大多数文件系统都以树（或*hierarchical*）结构存储文件。在树的顶部是一个（或多个）根节点。在根节点下，有文件和目录（Microsoft Windows中的*文件夹*）。每个目录都可以包含文件和子目录，而这些文件和子目录又可以包含文件和子目录，等等，可能达到几乎无限的深度。

本章节涵盖以下内容：

- [什么是 Path?](https://docs.oracle.com/javase/tutorial/essential/io/path.html#path)
- [相对还是绝对?](https://docs.oracle.com/javase/tutorial/essential/io/path.html#relative)
- [符号链接](https://docs.oracle.com/javase/tutorial/essential/io/path.html#symlink)

**什么是 Path?**

下图显示了包含单个根节点的示例目录树。Microsoft Windows支持多个根节点。每个根节点都映射到一个卷，例如`C:\`或`D:\`。Solaris OS支持单个根节点，用斜杠字符`/`表示。

![Sample directory structure](https://docs.oracle.com/javase/tutorial/figures/essential/io-dirStructure.gif)

目录结构示例

从根节点开始，文件通过文件系统的路径标识。例如，上图中的`statusReport`文件在Solaris OS中由以下表示法描述：

```
/home/sally/statusReport
```

在Microsoft Windows中，`statusReport`由以下表示法描述：

```
C:\home\sally\statusReport
```

用于分隔目录名称的字符（也称为*分隔符*）特定于文件系统：Solaris OS使用正斜杠（`/`），Microsoft Windows使用反斜杠斜杠（`\`）。

**相对还是绝对？**

路径是 *relative* 或 *absolute* 的。绝对路径始终包含查找文件所需的根元素和完整目录列表。例如，`/home/sally/statusReport`是绝对路径。查找文件所需的所有信息都包含在路径字符串中。

相对路径需要与另一个路径组合才能访问文件。例如，`joe/foo`是一个相对路径。没有更多信息，程序无法可靠地找到文件系统中的`joe/foo`目录。

**符号链接**

文件系统对象通常是目录或文件。每个人都熟悉这些对象。但是一些文件系统也支持符号链接的概念。符号链接也称为*符号链接*或*软链接*。

*符号链接*是一个特殊文件，用作对另一个文件的引用。在大多数情况下，符号链接对应用程序是透明的，符号链接上的操作会自动重定向到链接的目标。（指向的文件或目录称为链接的*target*。）例外情况是删除或重命名符号链接，在这种情况下链接本身被删除或重命名，而不是链接的目标。

在下图中，`logFile`似乎是用户的常规文件，但它实际上是指向`dir/logs/HomeLogFile`的符号链接。`HomeLogFile`是链接的目标。

![Sample symbolic link](https://docs.oracle.com/javase/tutorial/figures/essential/io-symlink.gif)

符号链接示例。

符号链接通常对用户是透明的。读取或写入符号链接与读取或写入任何其他文件或目录相同。

短语*解析链接*意味着用文件系统中的实际位置替换符号链接。在示例中，解析`logFile`会产生`dir/logs/HomeLogFile`。

在实际场景中，大多数文件系统都可以自由使用符号链接。偶尔，粗心创建的符号链接可能会导致循环引用。当链接的目标指向原始链接时，会发生循环引用。循环引用可能是间接引用：目录`a`指向目录`b`，而目录`b`指向目录`c`，目录`c`中包含一个指向目录`a`的子目录。当程序递归地遍历目录结构时，循环引用可能会导致严重破坏。但是，此问题已被考虑到，并且不会导致程序无限循环。

下一章节将讨论Java编程语言中文件 I/O 支持的核心，即`Path`类。

