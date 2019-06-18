#### 创建和读取目录

前面讨论过的一些方法，如`delete`，可以处理文件，链接和目录。但是如何列出文件系统的所有顶层目录？如何列出目录的内容或创建目录？

本节介绍以下特定于目录的功能：

- [列出文件系统根目录](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#listall)
- [创建目录](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#create)
- [创建临时目录](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#createTemp)
- [列出目录内容](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#listdir)
- [使用通配符过滤目录列表](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#glob)
- [编写你自己的目录过滤器](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#filter)

**列出文件系统根目录**

您可以使用 [`FileSystem.getRootDirectories`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#getRootDirectories--) 方法列出文件系统的所有根目录。 此方法返回 `Iterable`，这使您可以使用 [增强的for语句](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/for.html)  迭代所有根目录。

以下代码段打印默认文件系统的根目录：

```java
Iterable<Path> dirs = FileSystems.getDefault().getRootDirectories();
for (Path name: dirs) {
    System.err.println(name);
}
```

**创建目录**

您可以使用 [`createDirectory(Path, FileAttribute)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createDirectory-java.nio.file.Path-java.nio.file.attribute.FileAttribute...-) 方法创建新目录。如果未指定任何`FileAttributes`，则新目录将具有默认属性。例如：

```java
Path dir = ...;
Files.createDirectory(path);
```

以下代码段在具有特定权限的POSIX文件系统上创建新目录：

```java
Set<PosixFilePermission> perms =
    PosixFilePermissions.fromString("rwxr-x---");
FileAttribute<Set<PosixFilePermission>> attr =
    PosixFilePermissions.asFileAttribute(perms);
Files.createDirectory(file, attr);
```

要在一个或多个父目录可能尚不存在时创建多个级别的目录，可以使用简便方法 [`createDirectories(Path, FileAttribute)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createDirectories-java.nio.file.Path-java.nio.file.attribute.FileAttribute...-) 。与 `createDirectory(Path, FileAttribute<?>)` 方法一样，您可以指定一组可选的初始文件属性。以下代码段使用默认属性：

```java
Files.createDirectories(Paths.get("foo/bar/test"));
```

根据需要，从上到下创建目录。在 `foo/bar/test` 示例中，如果`foo`目录不存在，则创建它。接下来，如果需要，将创建`bar`目录，最后创建`test`目录。

创建一些（但不是全部）父目录后，此方法可能会失败。

**创建临时目录**

你可以使用下面的 `createTempDirectory` 方法之一创建临时目录：

- [`createTempDirectory(Path, String, FileAttribute...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createTempDirectory-java.nio.file.Path-java.lang.String-java.nio.file.attribute.FileAttribute...-)
- [`createTempDirectory(String, FileAttribute...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createTempDirectory-java.lang.String-java.nio.file.attribute.FileAttribute...-)

第一种方法允许代码指定临时目录的位置，第二种方法在默认的temporary-fle目录中创建新目录。

**列出目录内容**

您可以使用 [`newDirectoryStream(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newDirectoryStream-java.nio.file.Path-) 方法列出目录的所有内容。此方法返回实现 [`DirectoryStream`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/DirectoryStream.html) 接口的对象。实现 [`DirectoryStream`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/DirectoryStream.html) 接口的类也实现了 `Iterable`，因此您可以遍历目录流，读取所有对象。这种方法适用于非常大的目录。

----

**请记住：** 返回的`DirectoryStream` 是一个流。如果您没有使用`try-with-resources`语句，请不要忘记在`finally`块中关闭流。`try-with-resources`语句会为您解决此问题。

----

以下代码段显示了如何打印目录的内容：

```java
Path dir = ...;
try (DirectoryStream<Path> stream = Files.newDirectoryStream(dir)) {
    for (Path file: stream) {
        System.out.println(file.getFileName());
    }
} catch (IOException | DirectoryIteratorException x) {
    // IOException can never be thrown by the iteration.
    // In this snippet, it can only be thrown by newDirectoryStream.
    System.err.println(x);
}
```

迭代器返回的`Path`对象是针对目录解析的条目的名称。因此，如果要列出`/tmp`目录的内容，则返回的条目格式为 `/tmp/a`，`/tmp/b`，依此类推。

此方法返回目录的全部内容：文件，链接，子目录和隐藏文件。如果您希望对检索的内容更具选择性，可以使用其他 `newDirectoryStream` 方法之一，如本页后面所述。

请注意，如果在目录迭代期间发生异常，则抛出 `DirectoryIteratorException` ，并以`IOException`作为原因。迭代器方法不能抛出异常。

**使用通配符过滤目录列表**

如果只想获取每个名称与特定模式匹配的文件和子目录，可以使用 [`newDirectoryStream(Path, String)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newDirectoryStream-java.nio.file.Path-java.lang.String-) 方法，该方法提供内置的全局过滤器。如果您不熟悉通配符语法，请参阅 [什么是通配符](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#glob) 。

例如，以下代码段列出了与Java相关的文件：`.class`，`.java`和`.jar`文件：

```java
Path dir = ...;
try (DirectoryStream<Path> stream =
     Files.newDirectoryStream(dir, "*.{java,class,jar}")) {
    for (Path entry: stream) {
        System.out.println(entry.getFileName());
    }
} catch (IOException x) {
    // IOException can never be thrown by the iteration.
    // In this snippet, it can // only be thrown by newDirectoryStream.
    System.err.println(x);
}
```

**编写你自己的目录过滤器**

您可能希望根据模式匹配以外的某些条件过滤目录的内容。您可以通过实现 [`DirectoryStream.Filter`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/DirectoryStream.Filter.html) 接口来创建自己的过滤器。此接口由一个方法`accept`组成，该方法确定文件是否满足搜索要求。

例如，以下代码段实现了仅检索目录的过滤器：

```java
DirectoryStream.Filter<Path> filter =
    newDirectoryStream.Filter<Path>() {
    public boolean accept(Path file) throws IOException {
        try {
            return (Files.isDirectory(path));
        } catch (IOException x) {
            // Failed to determine if it's a directory.
            System.err.println(x);
            return false;
        }
    }
};
```

创建过滤器后，可以使用 [`newDirectoryStream(Path, DirectoryStream.Filter)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newDirectoryStream-java.nio.file.Path-java.nio.file.DirectoryStream.Filter-) 方法调用它。以下代码段使用`isDirectory`过滤器仅将目录的子目录打印到标准输出：

```java
Path dir = ...;
try (DirectoryStream<Path>
                       stream = Files.newDirectoryStream(dir, filter)) {
    for (Path entry: stream) {
        System.out.println(entry.getFileName());
    }
} catch (IOException x) {
    System.err.println(x);
}
```

此方法仅用于过滤单个目录。但是，如果要查找文件树中的所有子目录，可以使用 [遍历文件树](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) 机制。

