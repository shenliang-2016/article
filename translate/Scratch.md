#### Character Streams

Java平台使用Unicode编码存储字符值。字符流I/O自动将此内部格式转换为本地字符集。在西文语言环境中，本地字符集通常是ASCII码的8位超集。

对于大多数应用程序，使用字符流的I/O并不比使用字节流的I/O复杂。使用流类完成的输入和输出会自动转换为本地字符集和从本地字符集转换。使用字符流代替字节流的程序会自动适应本地字符集，并且可以进行国际化 - 所有这些都不需要程序员的额外工作。

如果国际化不是优先考虑事项，您可以简单地使用字符流类而不必过多关注字符集问题。之后，如果国际化成为优先事项，您的程序可以进行调整而无需进行大量重新编码。更多信息，请参阅 [国际化](https://docs.oracle.com/javase/tutorial/i18n/index.html) 。

**使用 Character Streams**

所有字符流类都来自 [`Reader`](https://docs.oracle.com/javase/8/docs/api/java/io/Reader.html) 和 [`Writer`](https://docs.oracle.com/javase/8/docs/api/java/io/Writer.html) 。 与字节流一样，还有专门用于文件I/O的字符流类： [`FileReader`](https://docs.oracle.com/javase/8/docs/api/java/io/FileReader.html) 和 [`FileWriter`](https://docs.oracle.com/javase/8/docs/api/java/io/FileWriter.html) 。  [`CopyCharacters`](https://docs.oracle.com/javase/tutorial/essential/io/examples/CopyCharacters.java) 示例说明了这些类。

```java
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class CopyCharacters {
    public static void main(String[] args) throws IOException {

        FileReader inputStream = null;
        FileWriter outputStream = null;

        try {
            inputStream = new FileReader("xanadu.txt");
            outputStream = new FileWriter("characteroutput.txt");

            int c;
            while ((c = inputStream.read()) != -1) {
                outputStream.write(c);
            }
        } finally {
            if (inputStream != null) {
                inputStream.close();
            }
            if (outputStream != null) {
                outputStream.close();
            }
        }
    }
}
```

`CopyCharacters`与`CopyBytes`非常相似。最重要的区别是`CopyCharacters`使用`FileReader`和`FileWriter`来代替`FileInputStream`和`FileOutputStream`进行输入和输出。请注意，`CopyBytes`和`CopyCharacters`都使用`int`变量来读取和写入。但是，在`CopyCharacters`中，`int`变量在其最后16位中保存一个字符值；在`CopyBytes`中，`int`变量在其最后8位中保存一个字节值。

**使用字节流的字符流**

字符流通常是字节流的“包装器”。字符流使用字节流来执行物理I/O，而字符流处理字符和字节之间的转换。例如，`FileReader`使用`FileInputStream`，而`FileWriter`使用`FileOutputStream`。

有两个通用的字节到字符“桥接”流：[`InputStreamReader`](https://docs.oracle.com/javase/8/docs/api/java/io/InputStreamReader.html) 和 [`OutputStreamWriter`](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStreamWriter.html)。当没有符合您需求的预打包字符流类时，使用它们来创建字符流。 [网络课程](https://docs.oracle.com/javase/tutorial/networking/index.html) 中的 [sockets](https://docs.oracle.com/javase/tutorial/networking/sockets/readingWriting.html) 显示了如何从套接字类提供的字节流创建字符流。

**面向行的 I/O **

字符I/O通常以比单个字符更大的单位出现。 一个常见的单位是行：一串字符，末尾有一个行终止符。行终止符可以是回车/换行序列（`\r\n`），单个回车符（`\r`）或单个换行符（`\n`）。支持所有可能的行终止符允许程序读取在任何广泛使用的操作系统上创建的文本文件。

让我们修改`CopyCharacters`示例以使用面向行的I/O。为此，我们必须使用两个我们以前从未见过的类， [`BufferedReader`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html) 和 [`PrintWriter`](https://docs.oracle.com/javase/8/docs/api/java/io/PrintWriter.html)。我们将在 [Buffered I/O](https://docs.oracle.com/javase/tutorial/essential/io/buffers.html) 和 [Formatting](https://docs.oracle.com/javase/tutorial/essential/io/formatting.html) 中更深入地探索这些类。现在，我们只对他们对面向行的I/O的支持感兴趣。

`CopyLines`示例调用`BufferedReader.readLine`和`PrintWriter.println`来一次输入和输出一行。

```java
import java.io.FileReader;
import java.io.FileWriter;
import java.io.BufferedReader;
import java.io.PrintWriter;
import java.io.IOException;

public class CopyLines {
    public static void main(String[] args) throws IOException {

        BufferedReader inputStream = null;
        PrintWriter outputStream = null;

        try {
            inputStream = new BufferedReader(new FileReader("xanadu.txt"));
            outputStream = new PrintWriter(new FileWriter("characteroutput.txt"));

            String l;
            while ((l = inputStream.readLine()) != null) {
                outputStream.println(l);
            }
        } finally {
            if (inputStream != null) {
                inputStream.close();
            }
            if (outputStream != null) {
                outputStream.close();
            }
        }
    }
}
```

调用`readLine`会返回一行文本。`CopyLines`使用`println`输出每一行，`println`附加当前操作系统的行终止符。这可能与输入文件中使用的行终止符不同。

构造文本输入和输出的方法有很多种，不仅限于字符和行。有关更多信息，请参阅 [扫描和格式化](https://docs.oracle.com/javase/tutorial/essential/io/scanfor.html) 。

#### Buffered Streams

到目前为止，我们看到的大多数示例都使用无缓冲的I/O，这意味着每个读取或写入请求都由底层操作系统直接处理。这可以使程序效率低得多，因为每个这样的请求经常触发磁盘访问，网络活动或一些相对昂贵的其他操作。

为了减少这种开销，Java平台实现了带缓冲的I/O流。缓冲输入流从称为缓冲区的存储区读取数据；仅当缓冲区为空时才调用本机输入API。类似地，缓冲输出流将数据写入缓冲区，并且仅在缓冲区已满时才调用本机输出API。

程序可以使用我们现在多次使用的包装习惯用法将无缓冲的流转换为缓冲流，其中无缓冲的流对象被传递给缓冲流类的构造函数。 以下是如何修改`CopyCharacters`示例中的构造函数调用以使用缓冲I/O：

```java
inputStream = new BufferedReader(new FileReader("xanadu.txt"));
outputStream = new BufferedWriter(new FileWriter("characteroutput.txt"));
```

有四个用于包装无缓冲流的缓冲流类： [`BufferedInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedInputStream.html) 和 [`BufferedOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedOutputStream.html) 创建缓冲字节流，[`BufferedReader`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html) 和 [`BufferedWriter`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedWriter.html) 创建缓冲字符流。

**刷新 Buffered Streams**

在关键时刻从缓冲区提取数据通常是有意义的，而无需等待它填充满。这称为刷新缓冲区。

一些缓冲的输出类支持`autoflush`，由可选的构造函数参数指定。启用`autoflush`时，某些关键事件会导致刷新缓冲区。例如，自动刷新的`PrintWriter`对象在每次调用`println`或`format`时刷新缓冲区。有关这些方法的更多信息，请参阅 [Formatting](https://docs.oracle.com/javase/tutorial/essential/io/formatting.html) 。

要手动刷新流，请调用其`flush`方法。`flush`方法在任何输出流上都有效，但除非缓冲流，否则无效。

#### 扫描和格式化

程序I/O通常涉及到人们喜欢使用的整齐格式化数据的转换。为了帮助您完成这些杂务，Java平台提供了两个API。 [scanner](https://docs.oracle.com/javase/tutorial/essential/io/scanning.html) API将输入分解为与数据位相关联的各个符号。 [formatting](https://docs.oracle.com/javase/tutorial/essential/io/formatting.html) API将数据组装成格式良好，人类可读的形式。

##### 扫描

[`Scanner`](https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html) 类型的对象非常有用，它可以将格式化的输入拆分为单个符号并按照符号各自的数据类型转换它们。

**将输入拆分为符号**

默认情况下，扫描程序使用空格分隔符号。（空格字符包括空格，制表符和行终止符。其完整列表，请参阅文档 [`Character.isWhitespace`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isWhitespace-char-) ）要查看扫描的工作原理，让我们看看 [`ScanXan`](https://docs.oracle.com/javase/tutorial/essential/io/examples/ScanXan.java) ，这是一个读取`xanadu.txt`中单个单词的程序。将它们打印出来，每行一个。

```java
import java.io.*;
import java.util.Scanner;

public class ScanXan {
    public static void main(String[] args) throws IOException {

        Scanner s = null;

        try {
            s = new Scanner(new BufferedReader(new FileReader("xanadu.txt")));

            while (s.hasNext()) {
                System.out.println(s.next());
            }
        } finally {
            if (s != null) {
                s.close();
            }
        }
    }
}
```

请注意，`ScanXan`在使用`Scanner`对象完成后会调用`Scanner`的`close`方法。即使`Scanner`不是流，您也需要将其关闭以指示您已完成对其基础流的处理。

`ScanXan`的输出如下所示：

```
In
Xanadu
did
Kubla
Khan
A
stately
pleasure-dome
...
```

要使用不同的符号分隔符，请调用`useDelimiter()`，指定正则表达式。例如，假设您希望符号分隔符为逗号，可选地后跟空格。你可以调用：

```java
s.useDelimiter(",\\s*");
```

**转换单个符号**

`ScanXan`示例将所有输入符号视为简单的`String`值。`Scanner`还支持所有Java语言的原始类型（`char`除外）的符号，以及`BigInteger`和`BigDecimal`。此外，数值可以使用千位分隔符。因此，在美国语言环境中，`Scanner`正确读取字符串`32,767`表示整数值。

我们必须提到语言环境，因为千位分隔符和小数符号是特定于语言环境的。因此，如果我们未指定`Scanner`应使用美国语言环境，则以下示例将无法在所有语言环境中正常运行。这通常不必担心，因为您的输入数据通常来自使用相同语言环境的源。但是这个例子是Java Tutorial的一部分，并且分发到世界各地。

`ScanSum`示例读取双精度值列表并将其相加。代码如下：

```java
import java.io.FileReader;
import java.io.BufferedReader;
import java.io.IOException;
import java.util.Scanner;
import java.util.Locale;

public class ScanSum {
    public static void main(String[] args) throws IOException {

        Scanner s = null;
        double sum = 0;

        try {
            s = new Scanner(new BufferedReader(new FileReader("usnumbers.txt")));
            s.useLocale(Locale.US);

            while (s.hasNext()) {
                if (s.hasNextDouble()) {
                    sum += s.nextDouble();
                } else {
                    s.next();
                }   
            }
        } finally {
            s.close();
        }

        System.out.println(sum);
    }
}
```

下面是样本输入文件 [`usnumbers.txt`](https://docs.oracle.com/javase/tutorial/essential/io/examples/usnumbers.txt) ：

```
8.5
32,767
3.14159
1,000,000.1
```

输出字符串是`1032778.74159`。在某些语言环境中，句点将是不同的字符，因为`System.out`是`PrintStream`对象，并且该类不提供覆盖默认语言环境的方法。我们可以覆盖整个程序的语言环境 - 或者我们可以只使用格式化，如下一个主题 [Formatting](https://docs.oracle.com/javase/tutorial/essential/io/formatting.html) 中所述。