#### 查找文件

如果您曾经使用过shell脚本，则很可能使用模式匹配来查找文件。事实上，你可能已经广泛使用它了。如果您还没有使用它，模式匹配使用特殊字符来创建模式，然后可以将文件名与该模式进行比较。例如，在大多数shell脚本中，星号`*`匹配任意数量的字符。例如，以下命令列出当前目录中以`.html`结尾的所有文件：

```
% ls *.html
```

`java.nio.file`包为此有用功能提供了编程支持。每个文件系统实现都提供 [`PathMatcher`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/PathMatcher.html)。您可以使用`FileSystem`类中的 [`getPathMatcher(String)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#getPathMatcher-java.lang.String-) 方法检索文件系统的`PathMatcher`。以下代码段获取默认文件系统的路径匹配器：

```java
String pattern = ...;
PathMatcher matcher =
    FileSystems.getDefault().getPathMatcher("glob:" + pattern);
```

传递给`getPathMatcher`的字符串参数指定语法风格和要匹配的模式。此示例指定通配符语法。如果您不熟悉通配符语法，请参阅 [什么是通配符](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#glob) 。

通配符语法易于使用且灵活，但如果您愿意，还可以使用正则表达式或*正则*语法。有关正则表达式的更多信息，请参阅 [正则表达式](https://docs.oracle.com/javase/tutorial/essential/regex/index.html) 。某些文件系统实现可能支持其他语法。

如果要使用其他形式的基于字符串的模式匹配，可以创建自己的`PathMatcher`类。此页面中的示例使用通配符语法。

一旦创建了`PathMatcher`实例，就可以将文件与文件进行匹配。`PathMatcher`接口有一个方法 [`matches`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/PathMatcher.html#matches-java.nio.file.Path-) ，它接受一个`Path` 参数并返回一个布尔值：它匹配模式，或者不匹配。以下代码段查找以`.java`或`.class`结尾的文件，并将这些文件打印到标准输出：

```java
PathMatcher matcher =
    FileSystems.getDefault().getPathMatcher("glob:*.{java,class}");

Path filename = ...;
if (matcher.matches(filename)) {
    System.out.println(filename);
}
```

**递归模式匹配**

搜索与特定模式匹配的文件与遍历文件树同时进行。有多少次你知道文件在文件系统的某个地方，但具体在哪里？ 或者您可能需要在文件树中找到具有特定文件扩展名的所有文件。

`Find`示例就是这样做的。`Find`类似于UNIX的`find`实用程序，但在功能上已经减少了。您可以扩展此示例以包含其他功能。例如，`find`实用程序支持`-prune`标志以从搜索中排除整个子树。您可以通过在`preVisitDirectory`方法中返回`SKIP_SUBTREE`来实现该功能。要实现符号链接后面的`-L`选项，可以使用四参数`walkFileTree`方法并传入`FOLLOW_LINKS`枚举（但请确保在`visitFile`方法中测试循环链接）。

要运行`Find`应用程序，请使用以下格式：

```
% java Find <path> -name "<glob_pattern>"
```

模式放在引号内，因此shell不会解释任何通配符。 例如：

```
% java Find . -name "*.html"
```

以下是`Find`示例的源代码：

```java
/**
 * Sample code that finds files that match the specified glob pattern.
 * For more information on what constitutes a glob pattern, see
 * https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#glob
 *
 * The file or directories that match the pattern are printed to
 * standard out.  The number of matches is also printed.
 *
 * When executing this application, you must put the glob pattern
 * in quotes, so the shell will not expand any wild cards:
 *              java Find . -name "*.java"
 */

import java.io.*;
import java.nio.file.*;
import java.nio.file.attribute.*;
import static java.nio.file.FileVisitResult.*;
import static java.nio.file.FileVisitOption.*;
import java.util.*;


public class Find {

    public static class Finder
        extends SimpleFileVisitor<Path> {

        private final PathMatcher matcher;
        private int numMatches = 0;

        Finder(String pattern) {
            matcher = FileSystems.getDefault()
                    .getPathMatcher("glob:" + pattern);
        }

        // Compares the glob pattern against
        // the file or directory name.
        void find(Path file) {
            Path name = file.getFileName();
            if (name != null && matcher.matches(name)) {
                numMatches++;
                System.out.println(file);
            }
        }

        // Prints the total number of
        // matches to standard out.
        void done() {
            System.out.println("Matched: "
                + numMatches);
        }

        // Invoke the pattern matching
        // method on each file.
        @Override
        public FileVisitResult visitFile(Path file,
                BasicFileAttributes attrs) {
            find(file);
            return CONTINUE;
        }

        // Invoke the pattern matching
        // method on each directory.
        @Override
        public FileVisitResult preVisitDirectory(Path dir,
                BasicFileAttributes attrs) {
            find(dir);
            return CONTINUE;
        }

        @Override
        public FileVisitResult visitFileFailed(Path file,
                IOException exc) {
            System.err.println(exc);
            return CONTINUE;
        }
    }

    static void usage() {
        System.err.println("java Find <path>" +
            " -name \"<glob_pattern>\"");
        System.exit(-1);
    }

    public static void main(String[] args)
        throws IOException {

        if (args.length < 3 || !args[1].equals("-name"))
            usage();

        Path startingDir = Paths.get(args[0]);
        String pattern = args[2];

        Finder finder = new Finder(pattern);
        Files.walkFileTree(startingDir, finder);
        finder.done();
    }
}
```

递归遍历文件树内容在 [遍历文件树](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) 中介绍。

