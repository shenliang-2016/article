#### `Path`类

Java SE 7发行版中引入的`Path`类是`java.nio.file`包的主要入口点之一。如果您的应用程序使用文件 I/O，您将需要了解此类的强大功能。

----

**版本提醒：** 如果您的JDK7之前的代码使用的是`java.io.File`，则仍可以使用`File.toPath`方法来利用`Path`类功能。有关更多信息，请参阅 [遗留 文件 I/O 代码](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html) 。

----

顾名思义，`Path`类是文件系统中路径的编程表示。`Path`对象包含用于构造路径的文件名和目录列表，用于检查，定位和操作文件。

`Path`实例反映了底层平台。在Solaris OS中，`Path`使用Solaris语法（`/home/joe/foo`），在Microsoft Windows中，`Path`使用Windows语法（`C:\home\joe\foo`）。路径不是系统无关的。您无法比较Solaris文件系统中的路径并期望它与Windows文件系统中的路径匹配，即使目录结构相同且两个实例都找到相同的相对文件路径。

与`Path`对应的文件或目录可能不存在。您可以创建一个`Path`实例并以各种方式对其进行操作：您可以将内容附加到它，提取它的部分内容，将它与另一个路径进行比较。在适当的时候，您可以使用 [`Files`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html) 类中的方法来检查`Path`对应的文件是否存在，创建文件，打开文件，删除文件，更改权限等等。

下一节详细介绍了`Path`类。

##### `Path`操作

`Path`类包括各种方法，可用于获取有关路径，访问路径元素，将路径转换为其他表单或提取路径部分的信息。还存在用于匹配路径字符串的方法和用于去除路径中的冗余的方法。本课程介绍了这些`Path`方法，有时称为语法操作，因为它们在路径本身上运行而不访问文件系统。

本小节涵盖以下内容：

- [创建 `Path`](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#create)
- [获取`Path`相关信息](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#info)
- [删除`Path`中的冗余内容](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#normal)
- [转化`Path`](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#convert)
- [合并两个`Path`](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#resolve)
- [在两个`Path`中间创建`Path`](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#relativize)
- [比较两个`Path`](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#compare)

**创建`Path`**

`Path`实例包含用于指定文件或目录位置的信息。在定义时，`Path`提供一个或多个名称。可能包含根元素或文件名，但两者都不是必需的。路径可能只包含一个目录或文件名。

您可以使用`Paths`（注意复数）帮助器类中的以下`get`方法之一轻松创建`Path`对象：

```java
Path p1 = Paths.get("/tmp/foo");
Path p2 = Paths.get(args[0]);
Path p3 = Paths.get(URI.create("file:///Users/joe/FileTest.java"));
```

`Paths.get`方法是以下代码的简写：

```java
Path p4 = FileSystems.getDefault().getPath("/users/sally");
```

The following example creates `/u/joe/logs/foo.log` assuming your home directory is `/u/joe`, or `C:\joe\logs\foo.log` if you are on Windows.

以下示例创建`/u/joe/logs/foo.log`，假设您的主目录是`/u/joe`，或者如果您在Windows上，则创建`C:\joe\logs\foo.log`。

```java
Path p5 = Paths.get(System.getProperty("user.home"),"logs", "foo.log");
```

**获取`Path`相关信息**

您可以将`Path`视为将这些名称元素存储为序列。目录结构中的最高元素位于索引`0`。目录结构中的最低元素位于索引`[n-1]`，其中`n`是`Path`中名称元素的数量。方法可用于使用这些索引检索单个元素或`Path`的子序列。

本课中的示例使用以下目录结构。

![Sample directory structure](https://docs.oracle.com/javase/tutorial/figures/essential/io-dirStructure.gif)

示例目录结构。

以下代码片段定义了`Path`实例，然后调用了几个方法来获取有关路径的信息：

```java
// None of these methods requires that the file corresponding
// to the Path exists.
// Microsoft Windows syntax
Path path = Paths.get("C:\\home\\joe\\foo");

// Solaris syntax
Path path = Paths.get("/home/joe/foo");

System.out.format("toString: %s%n", path.toString());
System.out.format("getFileName: %s%n", path.getFileName());
System.out.format("getName(0): %s%n", path.getName(0));
System.out.format("getNameCount: %d%n", path.getNameCount());
System.out.format("subpath(0,2): %s%n", path.subpath(0,2));
System.out.format("getParent: %s%n", path.getParent());
System.out.format("getRoot: %s%n", path.getRoot());
```

以下是Windows和Solaris OS的输出：

| Returns in the Solaris OS | Method Invoked | Returns in Microsoft Windows | Comment                                  |
| ------------------------- | -------------- | ---------------------------- | ---------------------------------------- |
| `/home/joe/foo`           | `toString`     | `C:\home\joe\foo`            | 返回`Path`的字符串表示形式。如果路径是使用`Filesystems.getDefault().getPath(String)`或`Paths.get`（后者是`getPath`的便捷方法）创建的，则该方法执行次要的语法清理。例如，在UNIX操作系统中，它会将输入字符串`//home/joe/foo`更正为`/home/joe/foo`。 |
| `foo`                     | `getFileName`  | `foo`                        | 返回文件名或名称元素序列的最后一个元素。                     |
| `home`                    | `getName(0)`   | `home`                       | 返回与指定索引对应的路径元素。第`0`个元素是最靠近根的路径元素。        |
| `3`                       | `getNameCount` | `3`                          | 返回路径中元素的个数。                              |
| `home/joe`                | `subpath(0,2)` | `home\joe`                   | 返回由开始和结束索引指定的`Path`（不包括根元素）的子序列。         |
| `/home/joe`               | `getParent`    | `\home\joe`                  | 返回上级文件夹路径。                               |
| `/`                       | `getRoot`      | `C:\`                        | 返回路径的根目录。                                |

前面的示例显示了绝对路径的输出。在以下示例中，指定了相对路径：

```
// Solaris syntax
Path path = Paths.get("sally/bar");
or
// Microsoft Windows syntax
Path path = Paths.get("sally\\bar");
```

以下是Windows和Solaris OS的输出：

| Method Invoked | Returns in the Solaris OS | Returns in Microsoft Windows |
| -------------- | ------------------------- | ---------------------------- |
| `toString`     | `sally/bar`               | `sally\bar`                  |
| `getFileName`  | `bar`                     | `bar`                        |
| `getName(0)`   | `sally`                   | `sally`                      |
| `getNameCount` | `2`                       | `2`                          |
| `subpath(0,1)` | `sally`                   | `sally`                      |
| `getParent`    | `sally`                   | `sally`                      |
| `getRoot`      | `null`                    | `null`                       |