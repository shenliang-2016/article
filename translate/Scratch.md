**连接两个路径**

您可以使用`resolve`方法组合路径。传入*部分路径*，这是一个不包含根元素的路径，则该部分路径将附加到原始路径之后。

例如，请考虑以下代码段：

```java
// Solaris
Path p1 = Paths.get("/home/joe/foo");
// Result is /home/joe/foo/bar
System.out.format("%s%n", p1.resolve("bar"));

or

// Microsoft Windows
Path p1 = Paths.get("C:\\home\\joe\\foo");
// Result is C:\home\joe\foo\bar
System.out.format("%s%n", p1.resolve("bar"));
```

将绝对路径传递给`resolve`方法会返回传入的路径：

```java
// Result is /home/joe
Paths.get("foo").resolve("/home/joe");
```

**在两个路径中间创建路径**

编写文件 I/O 代码时的一个常见需求是能够构建从文件系统中的一个位置到另一个位置的路径。你可以使用`relativize`方法来满足这个要求。此方法构造一个源自原始路径并在传入路径指定的位置结束的路径。新路径*相对与*原始路径。

例如，考虑定义为`joe`和`sally`的两个相对路径：

```java
Path p1 = Paths.get("joe");
Path p2 = Paths.get("sally");
```

在没有任何其他信息的情况下，假设`joe`和`sally`是兄弟目录，意味着节点位于目录树结构中的同一级别。要从`joe`导航到`sally`，你可能会先向上导航到共同的父节点，然后再导航到`sally`：

```java
// Result is ../sally
Path p1_to_p2 = p1.relativize(p2);
// Result is ../joe
Path p2_to_p1 = p2.relativize(p1);
```

考虑下面的稍微复杂一些的例子：

```java
Path p1 = Paths.get("home");
Path p3 = Paths.get("home/sally/bar");
// Result is sally/bar
Path p1_to_p3 = p1.relativize(p3);
// Result is ../..
Path p3_to_p1 = p3.relativize(p1);
```

在这个例子中，两个路径共享同一个节点`home`。要从`home`导航到`bar`，首先要向上导航到`sally`，然后再向下导航到`bar`。从`bar`到`home`的导航需要向上移动两个级别。

如果只有一个路径包含根元素，则不能构造相对路径。如果两个路径都包含根元素，则是否能够构造相对路径取决于系统。

递归[`Copy`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Copy.java)示例使用`relativize`和`resolve`方法。

**比较两个路径**

`Path`类支持[`equals`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#equals-java.lang.Object-)， 使您能够测试两条路径是否相等。[`startsWith`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#startsWith-java.nio.file.Path-)和[`endsWith `](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#endsWith-java.nio.file.Path-)方法使您可以测试路径是否以特定字符串开头或结尾。这些方法易于使用。 例如：

```java
Path path = ...;
Path otherPath = ...;
Path beginning = Paths.get("/home");
Path ending = Paths.get("foo");

if (path.equals(otherPath)) {
    // equality logic here
} else if (path.startsWith(beginning)) {
    // path begins with "/home"
} else if (path.endsWith(ending)) {
    // path ends with "foo"
}
```

`Path`类实现[`Iterable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html)接口。[`iterator`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#iterator--)方法返回一个对象，使您可以迭代路径中的名称元素。返回的第一个元素是最接近目录树中的根的元素。以下代码片段遍历路径，打印每个名称元素：

```java
Path path = ...;
for (Path name: path) {
    System.out.println(name);
}
```

`Path`类还实现了[`Comparable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html)接口。您可以使用`compareTo`来比较`Path`对象，这对于排序很有用。

您还可以将`Path`对象放入`Collection`中。有关此强大功能的详细信息，请参阅 [Collections](https://docs.oracle.com/javase/tutorial/collections/index.html) 。

如果要验证两个`Path`对象是否表示同一个文件，可以使用`isSameFile`方法，如 [检查两个路径是否定位到相同文件](https://docs.oracle.com/javase/tutorial/essential/io/check.html#same) 中所述。

#### 文件操作

[`Files`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html)类是`java.nio.file`包的另一个主要入口点。该类提供了一组丰富的静态方法，用于读取，写入和操作文件和目录。`Files`方法适用于`Path`对象的实例。在继续讨论其余部分之前，您应该熟悉以下常见概念：

- [释放系统资源](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#resources)
- [捕获异常](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#exception)
- [可变参数](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#varargs)
- [原子操作](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#atomic)
- [方法链](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#chaining)
- [什么*是* Glob?](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#glob)
- [连接敏感](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#linkaware)

**释放系统资源**

此API中使用的许多资源（如流或通道）实现或扩展[`java.io.Closeable`](https://docs.oracle.com/javase/8/docs/api/java /io/Closeable.html)接口。`Closeable`资源意味着是必须调用`close`方法以在不再需要时释放资源。忽略关闭资源可能会对应用程序的性能产生负面影响。下一节中描述的`try-with-resources`语句为您处理此步骤。

**捕获异常**

对于文件 I/O，意外情况是客观事实：预期中的文件存在（或不存在），程序无法访问文件系统，默认文件系统实现不支持特定功能 ， 等等。可能遇到许多错误。

访问文件系统的所有方法都可以抛出`IOException`。最佳实践是通过将这些方法嵌入Java SE 7发行版中引入的`try-with-resources`语句来捕获这些异常。`try-with-resources`语句的优点是编译器在不再需要时自动生成代码以关闭资源。以下代码显示了它的样子：

```java
Charset charset = Charset.forName("US-ASCII");
String s = ...;
try (BufferedWriter writer = Files.newBufferedWriter(file, charset)) {
    writer.write(s, 0, s.length());
} catch (IOException x) {
    System.err.format("IOException: %s%n", x);
}
```

更多信息，请参阅 [try-with-resources语句](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html) 。

或者，您可以将文件 I/O方法嵌入到`try`块中，然后在`catch`块中捕获所有异常。如果你的代码打开了任何流或通道，你应该在`finally`块中关闭它们。前面的示例使用`try-catch-finally`方法看起来如下所示：

```java
Charset charset = Charset.forName("US-ASCII");
String s = ...;
BufferedWriter writer = null;
try {
    writer = Files.newBufferedWriter(file, charset);
    writer.write(s, 0, s.length());
} catch (IOException x) {
    System.err.format("IOException: %s%n", x);
} finally {
    if (writer != null) writer.close();
}
```

更多信息，请参阅 [捕获和处理异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/handling.html) 。

除了`IOException`之外，许多特定的异常扩展了[`FileSystemException`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystemException.html)。这个类有一些有用的方法可以返回涉及的文件[`getFile`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystemException.html#getFile-- )，详细的消息字符串[`getMessage`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystemException.html#getMessage--)，文件系统操作失败的原因[`getReason`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystemException.html#getReason--)和涉及的其他文件，如果有的话[`getOtherFile`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystemException.html#getOtherFile--)。

以下代码段显示了如何使用`getFile`方法：

```java
try (...) {
    ...    
} catch (NoSuchFileException x) {
    System.err.format("%s does not exist\n", x.getFile());
}
```

为清楚起见，本课程中的文件 I/O 示例可能不会包含异常处理，但您的代码应始终包含它。

**可变参数**

当指定标志时，几个`Files`方法接受任意数量的参数。例如，在以下方法签名中，`CopyOption`参数后面的省略号表示该方法接受可变数量的参数，或*varargs*，因为它们通常的调用方法为：

```java
Path Files.move(Path, Path, CopyOption...)
```

当方法接受可变参数时，您可以传递一个以逗号分隔的值列表或值的数组（`CopyOption []`）。

在`move`示例中，可以按如下方式调用该方法：

```java
import static java.nio.file.StandardCopyOption.*;

Path source = ...;
Path target = ...;
Files.move(source,
           target,
           REPLACE_EXISTING,
           ATOMIC_MOVE);
```

有关可变参数语法的更多信息，请参阅 [任意数量的参数](https://docs.oracle.com/javase/tutorial/java/javaOO/arguments.html#varargs) 。

**原子操作**

一些`Files`方法，例如`move`，可以在某些文件系统中以原子方式执行某些操作。

*原子文件操作*是不能被中断或“部分”执行的操作。执行整个操作或操作失败。当您在文件系统的同一区域上运行多个进程时，这很重要，并且您需要保证每个进程都访问一个完整的文件。

**方法链**

许多文件 I/O 方法都支持*方法链*的概念。

您首先调用返回对象的方法。然后，您立即在*该*对象上调用一个方法，该对象返回另一个对象，依此类推。许多 I/O 示例使用以下技术：

```java
String value = Charset.defaultCharset().decode(buf).toString();
UserPrincipal group =
    file.getFileSystem().getUserPrincipalLookupService().
         lookupPrincipalByName("me");
```

此技术生成紧凑的代码，使您可以避免声明不需要的临时变量。

**什么是 Glob?**

`Files`类中的两个方法接受一个glob参数，但什么是*glob*？

您可以使用glob语法指定模式匹配行为。

glob模式被指定为字符串，并与其他字符串匹配，例如目录或文件名。Glob语法遵循几个简单的规则：

 - 星号，`*`匹配任意数量的字符（包括无）。

 - 两个星号，`**`，就像`*`一样，但是跨越目录边界。此语法通常用于匹配完整路径。

 - 问号`?`与一个字符精确匹配。

 - 大括号指定子模式的集合。例如：

   - `{sun，moon，stars}`匹配"sun"，“moon”或“stars”。
   - `{temp *，tmp *}`匹配以“temp”或“tmp”开头的所有字符串。

 - 方括号表示一组单个字符，或者，当使用连字符（`-`）时，表示一系列字符。例如：

   - `[aeiou]`匹配任何小写元音。
   - `[0-9]`匹配任何数字。
   - `[A-Z]`匹配任何大写字母。
   - `[a-z，A-Z]`匹配任何大写或小写字母。

  在方括号内，`*`，`？`和`\`匹配自己。

 - 所有其他字符匹配自己。

 - 要匹配`*`，`?`或其他特殊字符，可以使用反斜杠字符`\`来转义它们。例如：`\\`匹配单个反斜杠，`\?`匹配问号。

以下是glob语法的一些示例：

 - `* .html`  - 匹配以*.html*结尾的所有字符串
 - `???` - 匹配所有字符串，正好是三个字母或数字
 - `* [0-9] *` - 匹配包含数值的所有字符串
 - `*。{htm，html，pdf}` - 匹配任何以*.htm* *，* *.html* *或* *.pdf*结尾的字符串
 - `a?*。java`  - 匹配以`a`开头的任何字符串，后跟至少一个字母或数字，以*.java*结尾
 - `{foo *，* [0-9] *}` - 匹配以*foo*开头的任何字符串或包含数字值的任何字符串

----

**注意：** 如果您在键盘上键入glob模式并且它包含一个特殊字符，则必须将模式放在引号（`“*”`）中，使用反斜杠（`\ *`）或使用命令行支持任何转义机制。

----

glob语法功能强大且易于使用。但是，如果它不足以满足您的需求，您还可以使用正则表达式。有关详细信息，请参阅 [正则表达式](https://docs.oracle.com/javase/tutorial/essential/regex/index.html) 课程。

有关glob语法的更多信息，请参阅`FileSystem`类中的方法 [`getPathMatcher`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#getPathMatcher-java.lang.String-) 的API规范。

**链接敏感**

`Files`类是“链接感知”的。 每个`Files`方法都会检测遇到符号链接时要执行的操作，或者它提供了一个选项，使您可以配置在遇到符号链接时的行为。

