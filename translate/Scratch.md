#### 检查文件或者目录

你有一个表示文件或目录的`Path`实例，但该文件是否存在于文件系统中？它可读吗？可写？可执行？

**校验文件或者目录的存在性**

`Path`类中的方法是语法意义上的，这意味着它们在`Path`实例上运行。但最终您必须访问文件系统以验证特定的`Path`是否存在。您可以使用[`exists(Path，LinkOption ...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#exists-java.nio.file.Path-java.nio.file.LinkOption ...-) 和 [`notExists(Path，LinkOption ...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html＃notExists-java.nio.file.Path-java.nio.file.LinkOption ...-) 方法。注意`!Files.exists(path)`不等同于`Files.notExists(path)`。当您测试文件存在时，可能会有三个结果：

 - 验证文件存在。
 - 验证文件不存在。
 - 文件的状态未知。当程序无权访问该文件时，可能会发生此结果。

如果`exists`和`notExists`都返回`false`，则无法验证文件是否存在。

**检查文件的可访问性**

To verify that the program can access a file as needed, you can use the [`isReadable(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isReadable-java.nio.file.Path-), [`isWritable(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isWritable-java.nio.file.Path-), and [`isExecutable(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isExecutable-java.nio.file.Path-) methods.

The following code snippet verifies that a particular file exists and that the program has the ability to execute the file.

```java
Path file = ...;
boolean isRegularExecutableFile = Files.isRegularFile(file) &
         Files.isReadable(file) & Files.isExecutable(file);
```

------

**注意：** 一旦这些方法中的任何一个完成，就无法保证可以访问该文件。许多应用程序中的常见安全漏洞是执行检查然后访问该文件。有关更多信息，请使用您最喜欢的搜索引擎查找`TOCTTOU`（发音为*TOCK-too*）。

----

**检查两个路径是否定位同一个文件**

当您有一个使用符号链接的文件系统时，可能有两个不同的路径来定位同一个文件。[`isSameFile(Path，Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isSameFile-java.nio.file.Path- java.nio.file.Path-) 方法比较两个路径以确定它们是否在文件系统上找到相同的文件。例如：

```java
Path p1 = ...;
Path p2 = ...;

if (Files.isSameFile(p1, p2)) {
    // Logic when the paths locate the same file
}
```