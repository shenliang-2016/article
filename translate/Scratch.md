#### 遍历文件树

您是否需要创建一个递归访问文件树中所有文件的应用程序？ 也许您需要删除树中的每个`.class`文件，或查找去年未访问过的每个文件。您可以使用`FileVisitor`接口执行此操作。

本章节涵盖以下内容：

- [`FileVisitor` 接口](https://docs.oracle.com/javase/tutorial/essential/io/walk.html#filevisitor)
- [启动流程](https://docs.oracle.com/javase/tutorial/essential/io/walk.html#invoke)
- [考虑何时创建 `FileVisitor`](https://docs.oracle.com/javase/tutorial/essential/io/walk.html#order)
- [流程控制](https://docs.oracle.com/javase/tutorial/essential/io/walk.html#return)
- [实例](https://docs.oracle.com/javase/tutorial/essential/io/walk.html#ex)

**`FileVisitor` 接口**

要遍历文件树，首先需要实现`FileVisitor`。`FileVisitor`指定遍历过程中关键点所需的行为：访问文件时，访问目录之前，访问目录之后，或发生故障时。该接口有四种方法对应于这些情况：

- [`preVisitDirectory`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileVisitor.html#preVisitDirectory-T-java.nio.file.attribute.BasicFileAttributes-) – 目录实体被访问之前被调用。
- [`postVisitDirectory`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileVisitor.html#postVisitDirectory-T-java.io.IOException-) – 目录下所有实体都被访问之后被调用。如果发生异常，特定异常会被传递给此方法。
- [`visitFile`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileVisitor.html#visitFile-T-java.nio.file.attribute.BasicFileAttributes-) – 当文件被访问时被调用。文件的 `BasicFileAttributes` 属性被传递给此方法，或者你可以使用 [file attributes](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) 包读取特定属性集合。比如，你可以选择读取文件的 `DosFileAttributeView` 属性来确定该文件是否设置了“隐藏”位。
- [`visitFileFailed`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileVisitor.html#visitFileFailedy-T-java.io.IOException-) – 无法访问文件时调用。特定异常传递给该方法。您可以选择是抛出异常，将其打印到控制台还是日志文件，等等。

如果您不需要实现所有四个`FileVisitor`方法，而不是实现`FileVisitor`接口，则可以扩展`SimpleFileVisitor`类。此类实现`FileVisitor`接口，访问树中的所有文件，并在遇到错误时抛出`IOError`。您可以扩展此类并仅覆盖所需的方法。

下面是一个扩展`SimpleFileVisitor`以打印文件树中所有条目的示例。它打印条目是条目是常规文件，符号链接，目录或者其他“未指定”类型的文件。它还会打印每个文件的大小（以字节为单位）。遇到的任何异常都会打印到控制台。

`FileVisitor` 方法以粗体字表示：

```java
import static java.nio.file.FileVisitResult.*;

public static class PrintFiles
    extends SimpleFileVisitor<Path> {

    // Print information about
    // each type of file.
    @Override
    public FileVisitResult visitFile(Path file,
                                   BasicFileAttributes attr) {
        if (attr.isSymbolicLink()) {
            System.out.format("Symbolic link: %s ", file);
        } else if (attr.isRegularFile()) {
            System.out.format("Regular file: %s ", file);
        } else {
            System.out.format("Other: %s ", file);
        }
        System.out.println("(" + attr.size() + "bytes)");
        return CONTINUE;
    }

    // Print each directory visited.
    @Override
    public FileVisitResult postVisitDirectory(Path dir,
                                          IOException exc) {
        System.out.format("Directory: %s%n", dir);
        return CONTINUE;
    }

    // If there is some error accessing
    // the file, let the user know.
    // If you don't override this method
    // and an error occurs, an IOException 
    // is thrown.
    @Override
    public FileVisitResult visitFileFailed(Path file,
                                       IOException exc) {
        System.err.println(exc);
        return CONTINUE;
    }
}
```

**启动流程**

一旦实现了`FileVisitor`，如何启动文件遍历？`Files`类中有两个`walkFileTree`方法。

- [`walkFileTree(Path, FileVisitor)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#walkFileTree-java.nio.file.Path-java.nio.file.FileVisitor-)
- [`walkFileTree(Path, Set, int, FileVisitor)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#walkFileTree-java.nio.file.Path-java.util.Set-int-java.nio.file.FileVisitor-)

第一种方法只需要指定遍历的起点和`FileVisitor`实例。您可以按如下方式调用`PrintFiles`文件访问者：

```java
Path startingDir = ...;
PrintFiles pf = new PrintFiles();
Files.walkFileTree(startingDir, pf);
```

第二个`walkFileTree`方法使您可以另外指定访问目录层级数和一组`FileVisitOption`枚举的限制。如果要确保此方法遍历整个文件树，可以为最大深度参数指定`Integer.MAX_VALUE`。

您可以指定`FileVisitOption`枚举，`FOLLOW_LINKS`，表示应遵循符号链接。

此代码段显示了如何调用四参数方法：

```java
import static java.nio.file.FileVisitResult.*;

Path startingDir = ...;

EnumSet<FileVisitOption> opts = EnumSet.of(FOLLOW_LINKS);

Finder finder = new Finder(pattern);
Files.walkFileTree(startingDir, opts, Integer.MAX_VALUE, finder);
```

**考虑何时创建文件访问器**

首先深度遍历文件树，但是您不能对访问子目录的迭代顺序做出任何假设。

如果您的程序将更改文件系统，则需要仔细考虑如何实现`FileVisitor`。

例如，如果您正在编写递归删除，则首先删除目录中的文件，然后再删除目录本身。在这种情况下，您需要在`postVisitDirectory`中删除目录。

如果您正在编写递归拷贝，则需要在尝试将文件复制到`preVisitDirectory`之前（在`visitFiles`中）创建新目录。如果要保留源目录的属性（类似于UNIX `cp -p`命令），则需要在`postVisitDirectory`中复制文件后执行此操作。复制示例展示了如何执行此操作。

如果您正在编写文件搜索，则在`visitFile`方法中执行比较。此方法查找符合条件的所有文件，但不查找目录。如果要查找文件和目录，还必须在`preVisitDirectory`或`postVisitDirectory`方法中执行比较。`Find`示例展示了如何执行此操作。

您需要决定是否要遵循符号链接。例如，如果要删除文件，则可能不建议使用符号链接。如果要复制文件树，则可能需要允许它。默认情况下，`walkFileTree`不遵循符号链接。

为文件调用`visitFile`方法。如果已指定`FOLLOW_LINKS`选项，并且文件树具有指向父目录的循环链接，则使用`FileSystemLoopException`在`visitFileFailed`方法中报告循环目录。以下来自 [`Copy`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Copy.java) 的代码段展示了如何捕获循环链接：

```java
@Override
public FileVisitResult
    visitFileFailed(Path file,
        IOException exc) {
    if (exc instanceof FileSystemLoopException) {
        System.err.println("cycle detected: " + file);
    } else {
        System.err.format("Unable to copy:" + " %s: %s%n", file, exc);
    }
    return CONTINUE;
}
```

这种情况只会发生在程序遵循符号链接时。

**流程控制**

也许您想要遍历文件树以查找特定目录，并且在找到时，您希望该进程终止。也许你想跳过特定的目录。

`FileVisitor`方法返回 [`FileVisitResult`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileVisitResult.html) 值。您可以使用在`FileVisitor`方法中返回的值中止文件遍历过程或控制是否访问目录：

- `CONTINUE` – 表示文件遍历应继续。如果`preVisitDirectory`方法返回`CONTINUE`，则访问该目录。
- `TERMINATE` – 立即终止文件遍历。此值返回之后不会再有文件遍历方法被调用。
- `SKIP_SUBTREE` – 当 `preVisitDirectory` 返回此值，特定目录及其子目录被跳过。该分支被从目录树上修剪出去。
- `SKIP_SIBLINGS` – 当 `preVisitDirectory` 返回此值时，不访问特定目录，`postVisitDirectory` 不会被调用，未被访问的兄弟都不再会被访问。如果改值由 `postVisitDirectory` 方法返回，兄弟目录或文件就不再会被访问。基本上，特定目录中不会有后续访问发生。

下面的代码片段中，名为 `SCCS` 的目录被跳过：

```java
import static java.nio.file.FileVisitResult.*;

public FileVisitResult
     preVisitDirectory(Path dir,
         BasicFileAttributes attrs) {
    (if (dir.getFileName().toString().equals("SCCS")) {
         return SKIP_SUBTREE;
    }
    return CONTINUE;
}
```

下面的代码片段中，一旦特定文件被找到，文件名就会被打印输出到标准输出，同时文件遍历过程结束。

```java
import static java.nio.file.FileVisitResult.*;

// The file we are looking for.
Path lookingFor = ...;

public FileVisitResult
    visitFile(Path file,
        BasicFileAttributes attr) {
    if (file.getFileName().equals(lookingFor)) {
        System.out.println("Located file: " + file);
        return TERMINATE;
    }
    return CONTINUE;
}
```

**实例**

下面的例子展示了文件遍历机制：

- [`Find`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Find.java) – 递归遍历文件树寻找符合符合特定通配符模式的文件或者目录。该实例在 [查找文件](https://docs.oracle.com/javase/tutorial/essential/io/find.html) 章节中介绍。
- [`Chmod`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Chmod.java) – 递归修改文件树的权限（仅适用于 POSIX 系统）。
- [`Copy`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Copy.java) – 递归拷贝文件树。
- [`WatchDir`](https://docs.oracle.com/javase/tutorial/essential/io/examples/WatchDir.java) – 演示监视目录以查找已创建，删除或修改的文件的机制。使用`-r`选项调用此程序会监视整个树以进行更改。有关文件通知服务的详细信息，请参阅 [查看目录以进行更改](https://docs.oracle.com/javase/tutorial/essential/io/notification.html) 。