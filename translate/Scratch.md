#### 读、写以及创建文件

This page discusses the details of reading, writing, creating, and opening files. There are a wide array of file I/O methods to choose from. To help make sense of the API, the following diagram arranges the file I/O methods by complexity.

本页讨论了读取，写入，创建和打开文件的细节。有多种文件I/O方法可供选择。为了帮助理解API，下图按复杂性排列文件I/O方法。

![Line drawing with file I/O methods arranged from least complex (on the left) to most complex (on the right).](https://docs.oracle.com/javase/tutorial/figures/essential/io-fileiomethods.gif)

文件 I/O 方法从简单到复杂排列

图的最左边是实用方法`readAllBytes`，`readAllLines`和`write`方法，专为简单的常见情况而设计。在这些方法的右边是用于迭代一行或多行文本的方法，例如`newBufferedReader`，`newBufferedWriter`，然后是`newInputStream`和`newOutputStream`。这些方法可与`java.io`包互操作。这些方法的右边是处理`ByteChannels`，`SeekableByteChannels`和`ByteBuffers`的方法，例如`newByteChannel`方法。最后，最右边的是使用`FileChannel`的方法，用于需要文件锁定或内存映射I/O的高级应用程序。

----

**注意：** 创建新文件的方法使您可以为文件指定一组可选的初始属性。例如，在支持POSIX标准集（例如UNIX）的文件系统上，您可以在创建文件时指定文件所有者，组所有者或文件权限。 [管理元数据](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) 页面介绍了文件属性以及如何访问和设置它们。

----

本章节包括以下几个主题：

- [ `OpenOptions` 参数](https://docs.oracle.com/javase/tutorial/essential/io/file.html#openOptions)
- [为小文件提供的通用方法](https://docs.oracle.com/javase/tutorial/essential/io/file.html#common)
- [文本文件使用的带缓冲的I/O方法](https://docs.oracle.com/javase/tutorial/essential/io/file.html#textfiles)
- [无缓冲的流使用的方法及可以与 `java.io` APIs 互操作的方法](https://docs.oracle.com/javase/tutorial/essential/io/file.html#streams)
- [Channels 和 `ByteBuffers` 使用的方法](https://docs.oracle.com/javase/tutorial/essential/io/file.html#channels)
- [创建常规文件和临时文件的方法](https://docs.oracle.com/javase/tutorial/essential/io/file.html#creating)

**`OpenOptions` 参数**

本节中的几个方法采用可选的`OpenOptions`参数。此参数是可选的，API会告诉您在未指定时该方法的默认行为。

支持以下`StandardOpenOptions`枚举：

- `WRITE` – 打开文件用于写入。
- `APPEND` – 添加新数据到文件末尾。该选项与`WRITE`或者`CREATE`选项配合使用。
- `TRUNCATE_EXISTING` – 将文件截断为 0 字节。该选项与`WRITE`选项配合使用。
- `CREATE_NEW` – 创建一个新文件，如果文件已经存在，则抛出异常。
- `CREATE` – 如果文件存在则打开，否者创建一个新文件。
- `DELETE_ON_CLOSE` – 当流被关闭时删除文件。此选项对临时文件很有用。
- `SPARSE` – 提示新创建的文件将是稀疏的。此高级选项在某些文件系统（例如NTFS）上使用，其中具有数据“间隙”的大文件可以以更有效的方式存储，其中这些空间隙不占用磁盘空间。
- `SYNC` – 保持文件（内容和元数据）与底层存储设备同步。
- `DSYNC` – 保持文件内容与底层存储设备同步。

**为小文件提供的通用方法**

读取文件中所有字节或所有行

如果你有一个小文件并且想要一次读取它的全部内容，你可以使用 [`readAllBytes(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#readAllBytes-java.nio.file.Path-) 或 [`readAllLines(Path, Charset)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#readAllLines-java.nio.file.Path-java.nio.charset.Charset-) 方法。这些方法可以为您完成大部分工作，例如打开和关闭流，但不适用于处理大型文件。以下代码显示了如何使用`readAllBytes`方法：

```java
Path file = ...;
byte[] fileArray;
fileArray = Files.readAllBytes(file);
```

将所有字节或所有行写入文件

你可以使用一个写入方法将字节或者行写入文件。

- [`write(Path, byte[], OpenOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#write-java.nio.file.Path-byte:A-java.nio.file.OpenOption...-)
- [`write(Path, Iterable< extends CharSequence>, Charset, OpenOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#write-java.nio.file.Path-java.lang.Iterable-java.nio.charset.Charset-java.nio.file.OpenOption...-)

下面的代码片段展示了如何使用 `write` 方法。

```java
Path file = ...;
byte[] buf = ...;
Files.write(file, buf);
```