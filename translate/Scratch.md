**删除`Path`中的冗余**

许多文件系统使用“.” 符号表示当前目录，“..”表示父目录。您可能遇到路径包含冗余目录信息的情况。也许服务器配置为将其日志文件保存在“/dir/logs/.”目录，并且您要删除路径末尾的“/.” 符号。

下面的例子都包含冗余信息：

```
/home/./joe/foo
/home/sally/../joe/foo
```

`normalize`方法删除任何冗余元素，包括出现的任何“.” 或“*directory*/..”。前面的两个示例都规范化为`/home/joe/foo`。

值得注意的是，`normalize`在清理路径时不会检查文件系统。这是一种纯粹的语法操作。在第二个示例中，如果`sally`是符号链接，则删除`sally/..`可能会导致`Path`不再定位目标文件。

要在确保结果找到正确文件的同时清理路径，可以使用`toRealPath`方法。此方法将在下一节 [转换路径](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#convert) 中介绍。

**转换路径**

您可以使用三种方法转换`Path`。如果需要将路径转换为可以从浏览器打开的字符串，则可以使用 [`toUri`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#toUri--)。 例如：

```java
Path p1 = Paths.get("/home/logfile");
// Result is file:///home/logfile
System.out.format("%s%n", p1.toUri());
```

[`toAbsolutePath`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#toAbsolutePath--)方法将路径转换为绝对路径。如果传入的路径已经是绝对路径，则返回相同的`Path`对象。处理用户输入的文件名时，`toAbsolutePath`方法非常有用。例如：

```java
public class FileTest {
    public static void main(String[] args) {

        if (args.length < 1) {
            System.out.println("usage: FileTest file");
            System.exit(-1);
        }

        // Converts the input string to a Path object.
        Path inputPath = Paths.get(args[0]);

        // Converts the input Path
        // to an absolute path.
        // Generally, this means prepending
        // the current working
        // directory.  If this example
        // were called like this:
        //     java FileTest foo
        // the getRoot and getParent methods
        // would return null
        // on the original "inputPath"
        // instance.  Invoking getRoot and
        // getParent on the "fullPath"
        // instance returns expected values.
        Path fullPath = inputPath.toAbsolutePath();
    }
}
```

`toAbsolutePath`方法转换用户输入并返回在查询时返回有用值的`Path`。此方法无需该文件存在。

[`toRealPath`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#toRealPath-java.nio.file.LinkOption...-)方法返回现有文件的实际路径。此方法执行多个操作：

 - 如果将`true`传递给此方法并且文件系统支持符号链接，则此方法将解析路径中的所有符号链接。
 - 如果`Path`是相对的，则返回绝对路径。
 - 如果`Path`包含任何冗余元素，则返回删除了这些元素的路径。

如果文件不存在或无法访问，则此方法将引发异常。当您想要处理任何这些情况时，您可以捕获异常。例如：

```java
try {
    Path fp = path.toRealPath();
} catch (NoSuchFileException x) {
    System.err.format("%s: no such" + " file or directory%n", path);
    // Logic for case when file doesn't exist.
} catch (IOException x) {
    System.err.format("%s%n", x);
    // Logic for other sort of file error.
}
```