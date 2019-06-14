#### 删除文件或者目录

您可以删除文件，目录或链接。使用符号链接时，链接将被删除，而不是链接的目标。对于目录，目录必须为空，否则删除失败。

`Files`类提供了两种删除方法。

[`delete(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#delete-java.nio.file.Path-)方法 如果删除失败，则删除文件或抛出异常。例如，如果文件不存在，则抛出`NoSuchFileException`。您可以捕获异常以确定删除失败的原因，如下所示：

```java
try {
    Files.delete(path);
} catch (NoSuchFileException x) {
    System.err.format("%s: no such" + " file or directory%n", path);
} catch (DirectoryNotEmptyException x) {
    System.err.format("%s not empty%n", path);
} catch (IOException x) {
    // File permission problems are caught here.
    System.err.println(x);
}
```

[`deleteIfExists(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#deleteIfExists-java.nio.file.Path-) 方法 还会删除该文件，但如果该文件不存在，则不会抛出异常。如果有多个线程删除文件并且您不想仅因为一个线程首先执行此操作而抛出异常，则静默失败非常有用。

#### 复制文件或者目录

您可以使用[`copy(Path, Path, CopyOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#copy-java.nio.file.Path-java.nio.file.Path-java.nio.file.CopyOption...-) 方法复制文件或目录。如果目标文件存在，则复制失败，除非指定了`REPLACE_EXISTING`选项。

目录可以复制。但是，目录中的文件不会被复制，因此即使原始目录包含文件，新目录也是空的。

复制符号链接时，将复制链接的目标。如果要复制链接本身而不是链接的内容，请指定`NOFOLLOW_LINKS`或`REPLACE_EXISTING`选项。

此方法采用`varargs`参数。支持以下`StandardCopyOption`和`LinkOption`枚举：

 - `REPLACE_EXISTING`  - 即使目标文件已存在，也执行复制。如果目标是符号链接，则复制链接本身（而不是链接的目标）。如果目标是非空目录，则复制将失败，并抛出`FileAlreadyExistsException`异常。
 - `COPY_ATTRIBUTES`  - 将与文件关联的文件属性复制到目标文件。支持的确切文件属性是文件系统和平台相关的，但跨平台支持`last-modified-time`并复制到目标文件。
 - `NOFOLLOW_LINKS`  - 表示不应遵循符号链接。如果要复制的文件是符号链接，则复制链接（而不是链接的目标）。

如果你不熟悉 `enums`，参考 [Enum Types](https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html) 。

下面的例子展示了如何使用 `copy` 方法：

```java
import static java.nio.file.StandardCopyOption.*;
...
Files.copy(source, target, REPLACE_EXISTING);
```

除了文件复制，`Files`类还定义了可以用来在文件和流之间复制的方法。[`copy(InputStream, Path, CopyOptions...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#copy-java.io.InputStream-java.nio.file.Path-java.nio.file.CopyOption...-) 方法可以被用来从输入流复制所有字节到文件。[`copy(Path, OutputStream)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#copy-java.nio.file.Path-java.io.OutputStream-) 方法可以被用于将文件中的所有字节拷贝到输出流中。

[`Copy`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Copy.java) 例子使用 `copy` 和 `Files.walkFileTree` 方法来支持递归复制。参考 [Walking the File Tree](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) 获取跟多信息。

#### 移动文件或者目录

您可以使用[`move(Path, Path, CopyOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#move-java.nio.file.Path-java.nio.file.Path-java.nio.file.CopyOption ...-) 方法移动文件或目录。如果目标文件存在，则移动失败，除非指定了`REPLACE_EXISTING`选项。

可以移动空目录。如果目录不为空，则在不移动该目录内容的情况下移动目录时允许移动。在UNIX系统上，移动同一分区中的目录通常包括重命名目录。在这种情况下，即使目录包含文件，此方法也可以工作。

此方法采用`varargs`参数 - 支持以下`StandardCopyOption`枚举：

 - `REPLACE_EXISTING`  - 即使目标文件已存在，也执行移动。如果目标是符号链接，则替换符号链接，但它指向的内容不受影响。
 - `ATOMIC_MOVE`  - 将移动作为原子文件操作执行。如果文件系统不支持原子移动，则抛出异常。使用`ATOMIC_MOVE`，您可以将文件移动到目录中，并保证观察目录的任何进程都可以访问完整的文件。

以下显示了如何使用`move`方法：

```java
import static java.nio.file.StandardCopyOption.*;
...
Files.move(source, target, REPLACE_EXISTING);
```

虽然您可以在单个目录上实现`move`方法，但该方法通常与文件树递归机制一起使用。更多信息，请参阅 [遍历文件树](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) 。

