# Java™教程

[主页](https://docs.oracle.com/javase/tutorial/index.html)

## Java教程学习路径

> Java教程是为JDK 8编写的。本页描述的示例和实践没有利用后续版本中引入的改进。

## 入门

- [入门](https://docs.oracle.com/javase/tutorial/getStarted/index.html) - 介绍Java技术和安装Java开发软件并使用它来创建简单程序的课程。
- [学习Java语言](https://docs.oracle.com/javase/tutorial/java/index.html) - 描述基本概念（如类，对象，继承，数据类型，泛型和包）的课程。
- [基本Java类](https://docs.oracle.com/javase/tutorial/essential/index.html) - 有关异常，基本输入/输出，并发，正则表达式和平台环境的课程。

## 基础

- [集合](https://docs.oracle.com/javase/tutorial/collections/index.html) - 使用和扩展Java集合框架的经验教训。
- [Lambda表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)：了解如何以及为何在应用程序中使用Lambda表达式。
- [聚合操作](https://docs.oracle.com/javase/tutorial/collections/streams/index.html)：探索聚合操作，流和Lambda表达式如何协同工作以提供强大的过滤功能。
- [JAR文件中的打包程序](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html) - 有关创建和签署JAR文件的课程。
- [国际化](https://docs.oracle.com/javase/tutorial/i18n/index.html) - 设计软件的介绍，以便可以轻松地适应（本地化）各种语言和区域。
- [反射](https://docs.oracle.com/javase/tutorial/reflect/index.html) - 表示（“反映”）当前Java虚拟机中的类，接口和对象的API。
- [安全性](https://docs.oracle.com/javase/tutorial/security/index.html) - Java平台功能，有助于保护应用程序免受恶意软
- [JavaBeans](https://docs.oracle.com/javase/tutorial/javabeans/index.html) - Java平台的组件技术。
- [扩展机制](https://docs.oracle.com/javase/tutorial/ext/index.html) - 如何使Java平台上运行的所有应用程序都可以使用自定义API。
- [泛型](https://docs.oracle.com/javase/tutorial/extra/generics/index.html) - 对类型系统的增强，支持对各种类型的对象的操作，同时提供编译时类型安全性。

## 客户端开发

- [JavaFX入门](http://www.oracle.com/pls/topic/lookup?ctx=javase80&id=JFXST804) - 一组示例应用程序，旨在帮助您开始使用常见的JavaFX任务
- [Scene Builder入门](http://www.oracle.com/pls/topic/lookup?ctx=javase80&id=JSBGS101) - 逐步向您展示如何使用JavaFX Scene Builder工具创建简单的问题跟踪应用程序。
- [使用Swing创建GUI](https://docs.oracle.com/javase/tutorial/uiswing/index.html) - 全面介绍Java平台上的GUI创建。
- [部署](https://docs.oracle.com/javase/tutorial/deployment/index.html) - 如何使用JAR文件打包应用程序和applet，并使用Java Web Start和Java Plug-in进行部署。
- [2D图形](https://docs.oracle.com/javase/tutorial/2d/index.html) - 如何在应用程序中显示和打印2D图形。
- [全屏独占模式API](https://docs.oracle.com/javase/tutorial/extra/fullscreen/index.html) - 如何编写更充分利用用户图形硬件的应用程序。

## 服务端开发

- [JDBC数据库访问](https://docs.oracle.com/javase/tutorial/jdbc/index.html) - 介绍用于Java应用程序与各种数据库和数据源之间的连接的API。
- [JMX](https://docs.oracle.com/javase/tutorial/jmx/index.html) - Java Management Extensions提供了一种管理应用程序，设备和服务等资源的标准方法。
- [JNDI](https://docs.oracle.com/javase/tutorial/jndi/index.html) - Java命名和目录接口支持访问DNS和LDAP等命名和目录服务。
- [JAXP](https://docs.oracle.com/javase/tutorial/jaxp/index.html) - 介绍用于XML处理的Java API（JAXP）1.4技术。
- [RMI](https://docs.oracle.com/javase/tutorial/rmi/index.html) - 远程方法调用API允许对象调用在另一个Java虚拟机上运行的对象的方法。
- [并发](https://docs.oracle.com/javase/tutorial/essential/concurrency/index.html) - Java平台具有API，可帮助您开发多线程程序。

# 必要的类

本章节讨论了Java平台中对大多数程序员来说必不可少的类。

[![Trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**异常**](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html) 解释了异常机制以及它如何用于处理错误和其他异常情况。本课程描述了异常是什么，如何抛出和捕获异常，一旦捕获异常后如何处理异常，以及如何使用异常类层次结构。

[![Trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**基本 I/O**](https://docs.oracle.com/javase/tutorial/essential/io/index.html) 涵盖用于基本输入和输出的Java平台类。它主要关注I / O流，这是一个强大的概念，可以大大简化I / O操作。本课程还介绍了序列化，它允许程序将整个对象写入流并再次读回。然后，本课程将介绍一些文件系统操作，包括随机访问文件。最后，它简要介绍了新I / O API的高级功能。

[![Trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**并发**](https://docs.oracle.com/javase/tutorial/essential/concurrency/index.html) 解释了如何编写同时执行多个任务的应用程序。Java平台的设计初衷是为了支持并发编程，在Java编程语言和Java类库中提供基本的并发支持。从5.0版开始，Java平台还包含高级并发API。本课程介绍了平台的基本并发支持，并总结了`java.util.concurrent`包中的一些高级API。

[![Trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**平台环境**](https://docs.oracle.com/javase/tutorial/essential/environment/index.html) 由启动应用程序时提供的底层操作系统，Java虚拟机，类库和各种配置数据定义。本课程描述了应用程序用于检查和配置其平台环境的一些API。

[![Trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**正则表达式**](https://docs.oracle.com/javase/tutorial/essential/regex/index.html) 是一种基于集合中每个字符串共享的共同特征来描述一组字符串的方法。它们可用于搜索，编辑或操作文本和数据。正则表达式的复杂程度各不相同，但是一旦理解了它们的构造基础，您就能够解密（或创建）任何正则表达式。本课程讲授`java.util.regex` API支持的正则表达式语法，并提供了几个示例来说明各种对象如何交互。

## 异常

Java 编程语言使用*exceptions*处理错误和其他意外事件。本章节描述何时及如何使用异常。

[什么是异常？](https://docs.oracle.com/javase/tutorial/essential/exceptions/definition.html)

异常是程序运行过程中发生的某种事件，该事件会干扰指令的正常执行流程。

[捕获或指定强制要求](https://docs.oracle.com/javase/tutorial/essential/exceptions/catchOrDeclare.html)

本章节涵盖如何捕获及处理异常。这种套路包含 `try`, `catch`, 和 `finally` 块，以及链式异常和日志记录。

[如何抛出异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/throwing.html)

本章节涵盖 `throw` 语句和 `Throwable` 类以及它的子类。

[`try-with-resources` 语句](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html)

本节描述了`try-with-resources`语句，它是一个声明一个或多个资源的`try`语句。资源是一个对象，必须在程序完成后关闭它。`try-with-resources`语句确保在语句结束时关闭每个资源。

[未检查异常 - 争议](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html)

本章节解释由`RuntimeException`子类表示的未检查异常的正确和错误应用。

[异常的优势](https://docs.oracle.com/javase/tutorial/essential/exceptions/advantages.html)

使用异常来管理错误相对于传统的错误管理技术具有一些优势。本章节中将介绍它们。

[小结](https://docs.oracle.com/javase/tutorial/essential/exceptions/summary.html)

### 什么是异常

术语*异常*是异常事件的简称。

------

**定义：** 异常是一个事件，在程序执行过程中产生，打乱程序指令的正常执行流程。

------

当方法中发生错误时，该方法会创建一个对象并将其交给运行时系统。该对象称为异常对象，包含有关错误的信息，包括错误发生时的类型和程序状态。创建异常对象并将其交给运行时系统称为抛出异常。

在方法抛出异常后，运行时系统会尝试查找要处理它的内容。处理异常的可能“某事”的集合是已被调用以获取发生错误的方法的有序方法列表。该方法列表称为调用堆栈（请参见下图）。

![The call stack showing three method calls, where the first method called has the exception handler.](https://docs.oracle.com/javase/tutorial/figures/essential/exceptions-callstack.gif)

运行时系统在调用堆栈中搜索包含可以处理异常的代码块的方法。这段代码称为异常处理程序。搜索从发生错误的方法开始，并按照调用方法的相反顺序通过调用堆栈。找到适当的处理程序后，运行时系统会将异常传递给处理程序。如果抛出的异常对象的类型与处理程序可以处理的类型匹配，则认为异常处理程序是合适的。

选择的异常处理程序被称为可以捕获异常。如果运行时系统穷举搜索调用堆栈上的所有方法而没有找到适当的异常处理程序，如下图所示，则运行时系统（以及程序）终止。

![The call stack showing three method calls, where the first method called has the exception handler.](https://docs.oracle.com/javase/tutorial/figures/essential/exceptions-errorOccurs.gif)

使用异常管理错误相对于传统错误管理更有优势，这些优势在 [异常的的优势](https://docs.oracle.com/javase/tutorial/essential/exceptions/advantages.html) 章节中介绍。

### 捕获或指定强制要求

有效的Java编程语言代码必须遵守*捕获或指定强制要求*。这意味着可能抛出某些异常的代码必须包含以下任一项：

- 捕获异常的`try`语句。`try`必须为异常提供处理程序，如 [捕获和处理异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/handling.html) 中所述。
- 一个方法，指定它可以抛出异常。该方法必须提供一个`throws`子句，列出异常，如 [指定方法引发的异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/declaring.html) 中所述。

不符合捕获或指定强制要求的代码将无法编译。

并非所有例外都受捕获或指定强制要求的约束。为了理解原因，我们需要查看三个基本类别的异常，其中只有一个受要求限制。

**三种异常**

第一种异常是*受检查的异常*。这些是编写良好的应用程序应该能够预期和从中恢复的特殊异常条件。例如，假设应用程序提示用户输入文件名，然后通过将名称传递给`java.io.FileReader`的构造函数来打开该文件。通常，用户提供现有可读文件的名称，因此`FileReader`对象构造成功，并且应用程序的执行正常进行。但有时用户提供不存在的文件的名称，构造函数抛出`java.io.FileNotFoundException`。一个编写良好的程序将捕获此异常并通知用户该错误，可能提示需要正确的文件名。

受检查的异常受捕获或者指定强制要求的约束。除`Error`，`RuntimeException`及其子类指示的异常外，所有异常都是受检查的异常。

第二种异常是*错误*。这些是应用程序外部的特殊异常条件，应用程序通常无法预测或从中恢复。例如，假设应用程序成功打开文件以进行输入，但由于硬件或系统故障而无法读取文件。不成功的读取将抛出`java.io.IOError`。应用程序可能会选择捕获此异常，以便通知用户该问题 - 但它也可能有助于程序打印堆栈跟踪并退出。

错误不受捕获或者指定强制要求的约束。错误是`Error`及其子类指示的异常。

第三种异常是*运行时异常*。这些是应用程序内部的异常条件，应用程序通常无法预测或从中恢复。这些通常表示编程错误，例如逻辑错误或 API 的不当使用。例如，考虑前面描述的应用程序将文件名传递给`FileReader`的构造函数。如果逻辑错误导致将`null`传递给构造函数，则构造函数将抛出`NullPointerException`。应用程序可以捕获此异常，但消除导致异常发生的错误可能更有意义。

运行时异常不受捕获或者指定强制要求的约束。运行时异常是`RuntimeException`及其子类指示的异常。

错误和运行时异常统称为不受检查的异常。

**绕过捕获或者指定强制要求**

一些程序员认为捕获或者指定强制要求是异常机制中的一个严重缺陷，并通过使用未经检查的异常代替已检查的异常来绕过它。通常，不建议这样做。[未经检查的异常 - 争议](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html) 部分讨论何时适合使用未经检查的异常。

### 捕获并处理异常

本节描述如何使用三个异常处理程序组件`try`，`catch`和`finally`块 - 来编写异常处理程序。然后，解释了Java SE 7中引入的`try-with-resources`语句。`try-with-resources`语句特别适合使用`Closeable`资源的情况，例如流。

本节的最后一部分将介绍一个示例，并分析各种场景中发生的情况。

以下示例定义并实现名为`ListOfNumbers`的类。构造时，`ListOfNumbers`创建一个`ArrayList`，其中包含10个整数元素，顺序值为 0 到 9 。`ListOfNumbers`类还定义了一个名为`writeList`的方法，该方法将数字列表写入一个名为`OutFile.txt` 的文本文件。此示例使用`java.io`中定义的输出类，这些类在 [基本 I / O](https://docs.oracle.com/javase/tutorial/essential/io/index.html) 中介绍。

```java
// Note: This class will not compile yet.
import java.io.*;
import java.util.List;
import java.util.ArrayList;

public class ListOfNumbers {

    private List<Integer> list;
    private static final int SIZE = 10;

    public ListOfNumbers () {
        list = new ArrayList<Integer>(SIZE);
        for (int i = 0; i < SIZE; i++) {
            list.add(new Integer(i));
        }
    }

    public void writeList() {
	// The FileWriter constructor throws IOException, which must be caught.
        PrintWriter out = new PrintWriter(new FileWriter("OutFile.txt"));

        for (int i = 0; i < SIZE; i++) {
            // The get(int) method throws IndexOutOfBoundsException, which must be caught.
            out.println("Value at: " + i + " = " + list.get(i));
        }
        out.close();
    }
}
```

粗体的第一行是对构造函数的调用。构造函数初始化文件上的输出流。如果无法打开文件，构造函数将抛出`IOException`。第二个粗体行是对`ArrayList`类的`get`方法的调用，如果其参数的值太小（小于0）或太大（大于`ArrayList`当前包含的元素的数量），则抛出`IndexOutOfBoundsException`。

如果您尝试编译[`ListOfNumbers`](https://docs.oracle.com/javase/tutorial/essential/exceptions/examples/ListOfNumbers.java)类，编译器将打印一条错误消息，关于由`FileWriter`构造函数抛出的异常。但是，它不会显示有关`get`抛出的异常的错误消息。原因是构造函数抛出的异常`IOException`是一个受检查的异常，而`get`方法抛出的异常是一个不受检查的异常。

现在您已经熟悉了`ListOfNumbers`类以及可以在其中抛出异常的位置，您已准备好编写异常处理程序来捕获和处理这些异常。

#### `try`语句块

构造异常处理器的第一步是把可能抛出异常的代码放进`try`语句块中。通常，一个`try`语句块如下：

```
try {
    code
}
catch and finally blocks . . .
```

示例中标记为*code*的段包含一个或多个可能引发异常的合法代码行。 （`catch`和`finally`块将在接下来的两个小节中解释。）

要从`ListOfNumbers`类构造`writeList`方法的异常处理程序，请将`tryList`方法的异常抛出语句包含在`tryblock`中。有不止一种方法可以做到这一点。您可以将可能引发异常的每行代码放在其单独的`try`块中，并为每个代码提供单独的异常处理程序。或者，您可以将所有`writeList`代码放在一个`try`块中，并将多个处理程序与它相关联。以下列表对整个方法使用一个`try`块，因为所讨论的代码非常短。

```java
private List<Integer> list;
private static final int SIZE = 10;

public void writeList() {
    PrintWriter out = null;
    try {
        System.out.println("Entered try statement");
        out = new PrintWriter(new FileWriter("OutFile.txt"));
        for (int i = 0; i < SIZE; i++) {
            out.println("Value at: " + i + " = " + list.get(i));
        }
    }
    catch and finally blocks  . . .
}
```

如果`try`块中的代码发生异常，则该异常就会被与之相关联的异常处理器处理。为了将异常处理器关联到`try`块，你必须将一个`catch`块放在其后。下一节 [`catch` 块](https://docs.oracle.com/javase/tutorial/essential/exceptions/catch.html) 中详细介绍。

#### `catch`语句块

通过在`try`块之后直接提供一个或多个`catch`块，可以将异常处理程序与`try`块关联。`try`块的末尾和第一个`catch`块的开头之间没有代码。

```java
try {

} catch (ExceptionType name) {

} catch (ExceptionType name) {

}
```

每个`catch`块都是一个异常处理程序，它处理由其参数指示的异常类型。参数类型*ExceptionType*声明了处理程序可以处理的异常类型，并且必须是从`Throwable`类继承的类的名称。处理程序可以使用*name*引用异常。

`catch`块包含在调用异常处理程序时执行的代码。当处理程序是调用堆栈中的第一个处理程序时，运行时系统调用异常处理程序，其中*ExceptionType*与抛出的异常的类型匹配。如果抛出的对象可以合法地分配给异常处理程序的参数，则系统认为它是匹配的。

以下是`writeList`方法的两个异常处理程序：

```java
try {

} catch (IndexOutOfBoundsException e) {
    System.err.println("IndexOutOfBoundsException: " + e.getMessage());
} catch (IOException e) {
    System.err.println("Caught IOException: " + e.getMessage());
}
```

异常处理程序不仅可以打印错误消息或停止程序，它们还可以执行错误恢复，提示用户做出决定，或使用链式异常将错误传播到更高级别的处理程序，如 [链式异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/chained.html) 部分所述。

**一个异常处理器捕获多个类型的异常**

在Java SE 7及更高版本中，单个`catch`块可以处理多种类型的异常。此功能可以减少代码重复并减少捕获过于宽泛的异常的诱惑。

在`catch`子句中，指定块可以处理的异常类型，并使用竖线`|`分隔每个异常类型：

```java
catch (IOException|SQLException ex) {
    logger.log(ex);
    throw ex;
}
```

**注意：**如果`catch`块处理多个异常类型，则`catch`参数隐式为`final`的。在此示例中，`catch`参数`ex`是`final`的，因此您无法在`catch`块中为其分配任何值。

#### `final` 语句块

当`try`块退出时，`finally`块总是执行。这确保即使发生意外异常也会执行`finally`块。但最终不仅仅是异常处理有用 - 它允许程序员避免因返回，继续或中断而意外绕过清理代码。将清理代码放在`finally`块中始终是一种很好的做法，即使没有预期的例外情况也是如此。

------

**注意：**如果在执行`try`或`catch`代码时 JVM 退出，则`finally`块可能无法执行。同样，如果执行`try`或`catch`代码的线程被中断或终止，则即使应用程序作为一个整体继续，`finally`块也可能不会执行。

------

您在此处使用的`writeList`方法的`try`块打开了`PrintWriter`。程序应该在退出`writeList`方法之前关闭该流。这带来了一个有点复杂的问题，因为`writeList`的`try`块可以以三种方式之一退出。

1. `new FileWriter`语句失败并抛出`IOException`。
2. `list.get(i)`语句失败并抛出`IndexOutOfBoundsException`。
3. 一切都成功，`try`块正常退出。

无论`try`块中发生了什么，运行时系统总是执行`finally`块中的语句。所以这是进行清理的最佳位置。

下面的`writeList`方法的`finally`块清理然后关闭`PrintWriter`。

```java
finally {
    if (out != null) { 
        System.out.println("Closing PrintWriter");
        out.close(); 
    } else { 
        System.out.println("PrintWriter not open");
    } 
}
```

------

**重要提示：**`finally`块是防止资源泄漏的关键工具。关闭文件或以其他方式恢复资源时，将代码放在`finally`块中以确保始终恢复资源。

请考虑在这些情况下使用`try-with-resources`语句，这会在不再需要时自动释放系统资源。[try-with-resources](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html) 语句部分提供了更多信息。

------

#### `try-with-resources` 语句

`try-with-resources`语句是一个声明一个或多个资源的`try`语句。*资源*是一个在程序完成后必须关闭的对象。`try-with-resources`语句确保在语句结束时关闭每个资源。任何实现`java.lang.AutoCloseable`的对象（包括实现`java.io.Closeable`的所有对象）都可以用作资源。

以下示例从文件中读取第一行。它使用`BufferedReader`实例从文件中读取数据。`BufferedReader`是一个在程序完成后必须关闭的资源：

```java
static String readFirstLineFromFile(String path) throws IOException {
    try (BufferedReader br =
                   new BufferedReader(new FileReader(path))) {
        return br.readLine();
    }
}
```

在此示例中，在`try-with-resources`语句中声明的资源是`BufferedReader`。声明语句出现在`try`关键字后面的括号内。Java SE 7及更高版本中的类`BufferedReader`实现了接口`java.lang.AutoCloseable`。因为`BufferedReader`实例是在`try-with-resource`语句中声明的，所以无论`try`语句是正常还是意外结束（由于方法`BufferedReader.readLine`抛出一个异常`IOException`），它都会被关闭。

在Java SE 7之前，您可以使用`finally`块来确保资源被关闭，无论`try` 语句是正常还是意外结束。以下示例使用`finally`块而不是`try-with-resources`语句：

```java
static String readFirstLineFromFileWithFinallyBlock(String path)
                                                     throws IOException {
    BufferedReader br = new BufferedReader(new FileReader(path));
    try {
        return br.readLine();
    } finally {
        if (br != null) br.close();
    }
}
```

但是，在这个例子中，如果方法`readLine`和`close`都抛出异常，那么方法`readFirstLineFromFileWithFinallyBlock`会抛出`finally`块抛出的异常；而从`try`块抛出的异常被抑制。相反，在示例`readFirstLineFromFile`中，如果从`try`块和`try-with-resources`语句抛出异常，则方法`readFirstLineFromFile`抛出从`try`块抛出的异常；而从`try-with-resources`块抛出的异常被抑制。在Java SE 7及更高版本中，您可以检索已抑制的异常。有关详细信息，请参阅 [Suppressed Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html#suppressed-exceptions) 部分。

您可以在`try-with-resources`语句中声明一个或多个资源。以下示例检索`zip`文件`zipFileName`中打包的文件的名称，并创建包含这些文件名称的文本文件：

```java
public static void writeToFileZipFileContents(String zipFileName,
                                           String outputFileName)
                                           throws java.io.IOException {

    java.nio.charset.Charset charset =
         java.nio.charset.StandardCharsets.US_ASCII;
    java.nio.file.Path outputFilePath =
         java.nio.file.Paths.get(outputFileName);

    // Open zip file and create output file with 
    // try-with-resources statement

    try (
        java.util.zip.ZipFile zf =
             new java.util.zip.ZipFile(zipFileName);
        java.io.BufferedWriter writer = 
            java.nio.file.Files.newBufferedWriter(outputFilePath, charset)
    ) {
        // Enumerate each entry
        for (java.util.Enumeration entries =
                                zf.entries(); entries.hasMoreElements();) {
            // Get the entry name and write it to the output file
            String newLine = System.getProperty("line.separator");
            String zipEntryName =
                 ((java.util.zip.ZipEntry)entries.nextElement()).getName() +
                 newLine;
            writer.write(zipEntryName, 0, zipEntryName.length());
        }
    }
}
```

在这个例子中，`try-with-resources`语句包含两个由分号分隔的声明：`ZipFile`和`BufferedWriter`。当直接跟随它的代码块正常或由于异常而终止时，`BufferedWriter`和`ZipFile`对象的`close`方法将按此顺序自动调用。请注意，资源的“close”方法是在它们创建的*相反*顺序中调用的。

以下示例使用`try-with-resources`语句自动关闭`java.sql.Statement`对象：

```java
public static void viewTable(Connection con) throws SQLException {

    String query = "select COF_NAME, SUP_ID, PRICE, SALES, TOTAL from COFFEES";

    try (Statement stmt = con.createStatement()) {
        ResultSet rs = stmt.executeQuery(query);

        while (rs.next()) {
            String coffeeName = rs.getString("COF_NAME");
            int supplierID = rs.getInt("SUP_ID");
            float price = rs.getFloat("PRICE");
            int sales = rs.getInt("SALES");
            int total = rs.getInt("TOTAL");

            System.out.println(coffeeName + ", " + supplierID + ", " + 
                               price + ", " + sales + ", " + total);
        }
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    }
}
```

此示例中使用的资源`java.sql.Statement`是 JDBC 4.1 及更高版本 API 的一部分。

**注意：** `try-with-resources`语句可以像普通的`try`语句一样使用`catch`和`finally`块。在`try-with-resources`语句中，任何`catch`或`finally`块在声明的资源关闭后运行。

**被抑制的异常**

可以从与`try-with-resources`语句关联的代码块中抛出异常。在示例`writeToFileZipFileContents`中，可以从`try`块抛出异常，当`try-with-resources`语句尝试关闭`ZipFile`和`BufferedWriter`时，最多可以抛出两个异常对象。 如果从`try`块抛出异常并且从`try-with-resources`语句抛出一个或多个异常，那么从`try-with-resources`语句抛出的那些异常将被抑制，并抛由`writeToFileZipFileContents`方法中的异常代码块抛出的异常。您可以通过从`try`块抛出的异常中调用`Throwable.getSuppressed`方法来检索这些被抑制的异常。

**实现`AutoCloseable`或`Closeable`接口的类**

请参阅[`AutoCloseable`](https://docs.oracle.com/javase/8/docs/api/java/lang/AutoCloseable.html) 和 [`Closeable`](https:// docs.oracle.com/javase/8/docs/api/java/io/Closeable.html) 接口的Javadoc，其中包含实现这些接口之一的类列表。`Closeable`接口扩展了`AutoCloseable`接口。 `Closeable` 接口的`close`方法抛出类型为`IOException`的异常，而`AutoCloseable`接口的`close`方法抛出类型为`Exception`的异常。因此，`AutoCloseable`接口的子类可以覆盖`close`方法的这种行为，以抛出专门的异常，例如`IOException`，或者根本没有异常。

#### 把它们放在一起

前面的章节描述了如何为`ListOfNumbers`类中的`writeList`方法构造`try`，`catch`和`finally`代码块。现在，让我们来看看代码并研究会发生什么。

当所有组件放在一起时，`writeList`方法如下所示。

```java
public void writeList() {
    PrintWriter out = null;

    try {
        System.out.println("Entering" + " try statement");

        out = new PrintWriter(new FileWriter("OutFile.txt"));
        for (int i = 0; i < SIZE; i++) {
            out.println("Value at: " + i + " = " + list.get(i));
        }
    } catch (IndexOutOfBoundsException e) {
        System.err.println("Caught IndexOutOfBoundsException: "
                           +  e.getMessage());
                                 
    } catch (IOException e) {
        System.err.println("Caught IOException: " +  e.getMessage());
                                 
    } finally {
        if (out != null) {
            System.out.println("Closing PrintWriter");
            out.close();
        } 
        else {
            System.out.println("PrintWriter not open");
        }
    }
}
```

如前所述，这个方法的`try`块有三种不同的退出可能性，下面是其中两个：

1. `try`语句中的代码失败并抛出异常。这可能是由`new FileWriter`语句引起的`IOException`或由`for`循环中的错误索引值引起的`IndexOutOfBoundsException`。
2. 一切都成功，`try`语句正常退出。

让我们看一下在这两种退出可能性期间`writeList`方法会发生什么。

**场景1: 发生异常**

创建`FileWriter`的语句可能由于多种原因而失败。例如，如果程序无法创建或写入指定的文件，则`FileWriter`的构造函数将抛出`IOException`。

当`FileWriter`抛出`IOException`时，运行时系统立即停止执行`try`块；正在执行的方法调用未完成。然后，运行时系统开始在方法调用堆栈的顶部搜索适当的异常处理程序。在这个例子中，当发生`IOException`时，`FileWriter`构造函数位于调用堆栈的顶部。但是，`FileWriter`构造函数没有适当的异常处理程序，因此运行时系统在方法调用堆栈中检查下一个方法 - `writeList`方法。 `writeList`方法有两个异常处理程序：一个用于`IOException`，另一个用于`IndexOutOfBoundsException`。

运行时系统按照`try`语句之后出现的顺序检查`writeList`的处理程序。第一个异常处理程序的参数是`IndexOutOfBoundsException`。这与抛出的异常类型不匹配，因此运行时系统会检查下一个异常处理程序 - `IOException`。这与抛出的异常类型相匹配，因此运行时系统结束搜索适当的异常处理程序。既然运行时已经找到了一个合适的处理程序，那么执行`catch`块中的代码。

异常处理程序执行后，运行时系统将控制权传递给`finally`块。无论上面捕获的异常如何，`finally`块中的代码都会执行。在这种情况下，`FileWriter`从未打开过，不需要关闭。在`finally`块完成执行后，程序继续执行`finally`块之后的第一个语句。

这是`ListOfNumbers`程序的完整输出，当抛出`IOException`时出现。

```
Entering try statement
Caught IOException: OutFile.txt
PrintWriter not open 
```

以下清单中的粗体代码显示了在此场景中执行的语句：

```java
public void writeList() {
   PrintWriter out = null;

    try {
        System.out.println("Entering try statement");
        out = new PrintWriter(new FileWriter("OutFile.txt"));
        for (int i = 0; i < SIZE; i++)
            out.println("Value at: " + i + " = " + list.get(i));
                               
    } catch (IndexOutOfBoundsException e) {
        System.err.println("Caught IndexOutOfBoundsException: "
                           + e.getMessage());
                                 
    } catch (IOException e) {
        System.err.println("Caught IOException: " + e.getMessage());
    } finally {
        if (out != null) {
            System.out.println("Closing PrintWriter");
            out.close();
        } 
        else {
            System.out.println("PrintWriter not open");
        }
    }
}
```

**场景2: `try`语句块正常退出**

在这种情况下，`try`块范围内的所有语句都成功执行，并且不会抛出异常。执行从`try`块的末尾开始，运行时系统将控制传递给`finally`块。 因为一切都很成功，所以当控件到达`finally`块时，`PrintWriter`就是打开状态的，此时就会关闭`PrintWriter`。 同样，在`finally`块完成执行后，程序继续执行`finally`块之后的第一个语句。

当没有抛出异常时，这是`ListOfNumbers`程序的输出。

```
Entering try statement
Closing PrintWriter
```

以下示例中的粗体代码显示了在此场景中执行的语句。

```java
public void writeList() {
    PrintWriter out = null;
    try {
        System.out.println("Entering try statement");
        out = new PrintWriter(new FileWriter("OutFile.txt"));
        for (int i = 0; i < SIZE; i++)
            out.println("Value at: " + i + " = " + list.get(i));
                  
    } catch (IndexOutOfBoundsException e) {
        System.err.println("Caught IndexOutOfBoundsException: "
                           + e.getMessage());

    } catch (IOException e) {
        System.err.println("Caught IOException: " + e.getMessage());
                                 
    } finally {
        if (out != null) {
            System.out.println("Closing PrintWriter");
            out.close();
        } 
        else {
            System.out.println("PrintWriter not open");
        }
    }
}
```

### 指定方法产生的异常

上一节展示了如何在`ListOfNumbers`类中为`writeList`方法编写异常处理程序。有时，代码可以捕获可能在其中发生的异常。但是，在其他情况下，最好让调用堆栈中的方法进一步处理异常。例如，如果您将`ListOfNumbers`类作为类包的一部分提供，则可能无法预测包的所有用户的需求。在这种情况下，最好不要捕获异常而使允许进一步调用堆栈的方法来处理它。

如果`writeList`方法没有捕获可能在其中发生的受检查异常，则`writeList`方法必须指定它可以抛出这些异常。让我们修改原始的`writeList`方法来指定它可以抛出的异常。提醒您，这是不能编译的`writeList`方法的原始版本。

```java
public void writeList() {
    PrintWriter out = new PrintWriter(new FileWriter("OutFile.txt"));
    for (int i = 0; i < SIZE; i++) {
        out.println("Value at: " + i + " = " + list.get(i));
    }
    out.close();
}
```

要指定`writeList`可以抛出两个异常，请将`throws`子句添加到`writeList`方法的方法声明中。 `throws`子句包含`throws`关键字，后跟逗号分隔的该方法抛出的所有异常列表。该子句在方法名称和参数列表之后以及定义方法主体的大括号之前。下面是一个例子。

```java
public void writeList() throws IOException, IndexOutOfBoundsException {
```

请记住，`IndexOutOfBoundsException`是一个不受检查的异常；在`throws`子句中包含它不是强制性的。你可以写下面的内容。

```java
public void writeList() throws IOException {
```

### 如何抛出异常

在捕获异常之前，某些代码必须抛出一个异常。任何代码都可以抛出异常：您的代码，来自其他人编写的包中的代码，例如Java平台附带的包或Java运行时环境。无论什么抛出异常，它总是通过`throw`语句抛出。

您可能已经注意到，Java平台提供了许多异常类。所有类都是[`Throwable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Throwable.html) 类的后代，所有类都允许程序区分各种类在程序执行期间可能发生的异常类型。

您还可以创建自己的异常类来表示您编写的类中可能出现的问题。实际上，如果您是程序包开发人员，则可能必须创建自己的一组异常类，以允许用户将程序包中可能发生的错误与Java平台或其他程序包中发生的错误区分开来。

您还可以创建*链式*异常。有关更多信息，请参阅 [链式异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/chained.html) 部分。

**`throw` 语句**

所有方法都使用`throw`语句来抛出异常。 `throw`语句需要一个参数：一个throwable对象。 Throwable对象是`Throwable`类的任何子类的实例。 这是一个`throw`语句的例子：

```java
throw someThrowableObject;
```

让我们看一下上下文中的`throw`语句。以下`pop`方法取自实现公共堆栈对象的类。该方法从堆栈中删除顶部元素并返回该对象。

```java
public Object pop() {
    Object obj;

    if (size == 0) {
        throw new EmptyStackException();
    }

    obj = objectAt(size - 1);
    setObjectAt(size - 1, null);
    size--;
    return obj;
}
```

`pop`方法检查堆栈中是否有任何元素。如果堆栈为空（其大小等于`0`），则`pop`实例化一个新的`EmptyStackException`对象（`java.util`的成员）并抛出它。本章中的 [创建异常类](https://docs.oracle.com/javase/tutorial/essential/exceptions/creating.html) 部分介绍了如何创建自己的异常类。现在，您需要记住的是，您只能抛出从`java.lang.Throwable`类继承的对象。

请注意，`pop`方法的声明不包含`throws`子句。 `EmptyStackException`不是一个受检查的异常，因此不需要`pop`来声明它可能发生。

**可抛出的类及其子类**

从`Throwable`类继承的对象包括直接后代（直接从`Throwable`类继承的对象）和间接后代（从`Throwable`类的子孙继承的对象）。下图说明了`Throwable`类的类层次结构及其最重要的子类。正如你所看到的，`Throwable`有两个直接的后代：[`Error`](https://docs.oracle.com/javase/8/docs/api/java/lang/Error.html) 和 [`Exception`](https://docs.oracle.com/javase/8/docs/api/java/lang/Exception.html) 

![The Throwable class and its most significant subclasses.](https://docs.oracle.com/javase/tutorial/figures/essential/exceptions-throwable.gif)

可抛出类

**`Error` 类**

当发生 Java 虚拟机的动态链接故障或其他硬故障时，虚拟机会抛出 `Error` 。 简单的程序通常会*不*捕获或抛出`Error` 。

**`Exception` 类**

大多数程序抛出并捕获派生自`Exception`类的对象。`Exception` 表示发生了问题，但这不是一个严重的系统问题。你编写的大多数程序都会抛出并捕获`Exception` 而不是`Error` 。

Java平台定义了`Exception`类的许多后代。这些后代表示可能发生的各种类型的异常。例如，`IllegalAccessException`表示无法找到特定方法，而`NegativeArraySizeException`表示程序试图创建一个负大小的数组。

一个`Exception`子类，`RuntimeException`，保留用于指示错误使用API的异常。运行时异常的一个示例是`NullPointerException` ，当方法尝试通过`null`引用访问对象的成员时发生。 [不受检查的异常－争议](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html) 部分讨论了为什么大多数应用程序不应抛出运行时异常或子类`RuntimeException`。

#### 链式异常

应用程序通常会通过抛出另一个异常来响应异常。实际上，第一个异常*导致*第二个异常。知道一个异常何时导致另一个异常非常有用。*链接异常*帮助程序员执行此操作。

以下是`Throwable`中支持链式异常的方法和构造函数。

```java
Throwable getCause()
Throwable initCause(Throwable)
Throwable(String, Throwable)
Throwable(Throwable)
```

`initCause`和`Throwable`构造函数的`Throwable`参数是导致当前异常的异常。 `getCause`返回导致当前异常的异常，`initCause`设置当前异常的原因。

以下示例显示如何使用链式异常。

```java
try {

} catch (IOException e) {
    throw new SampleException("Other IOException", e);
}
```

在此示例中，当捕获`IOException`时，将创建一个新的`SampleException`异常，并附加原始原因，并将异常链抛出到下一个更高级别的异常处理程序。

**访问堆栈轨迹信息**

现在让我们假设更高级别的异常处理程序想要以自己的格式转储堆栈跟踪信息。

------

**定义：** 堆栈跟踪提供有关当前线程的执行历史记录的信息，并列出在发生异常时调用的类和方法的名称。堆栈跟踪是一种有用的调试工具，通常在抛出异常时可以利用它。

------

以下代码显示如何在异常对象上调用`getStackTrace`方法。

```java
catch (Exception cause) {
    StackTraceElement elements[] = cause.getStackTrace();
    for (int i = 0, n = elements.length; i < n; i++) {       
        System.err.println(elements[i].getFileName()
            + ":" + elements[i].getLineNumber() 
            + ">> "
            + elements[i].getMethodName() + "()");
    }
}
```

**日志 API**

下一个代码片段记录了`catch`块中发生异常的位置。但是，它不是手动解析堆栈跟踪并将输出发送到`System.err()`，而是使用[`java.util.logging`](https：// docs .oracle.com / javase / 8 / docs / api / java / util / logging / package-summary.html) 包中的日志工具将输出发送到文件。

```java
try {
    Handler handler = new FileHandler("OutFile.log");
    Logger.getLogger("").addHandler(handler);
    
} catch (IOException e) {
    Logger logger = Logger.getLogger("package.name"); 
    StackTraceElement elements[] = e.getStackTrace();
    for (int i = 0, n = elements.length; i < n; i++) {
        logger.log(Level.WARNING, elements[i].getMethodName());
    }
}
```

#### 创建异常类

当面对选择要抛出的异常类型时，您可以使用其他人编写的异常 -  Java平台提供了许多可以使用的异常类 - 或者您可以编写自己的异常类。如果您对以下任何问题的回答是肯定的，您应该编写自己的异常类；否则，你可能会使用别人的。

- 您是否需要Java平台中未提供的异常类型？
- 它是否可以帮助用户将他们的异常与其他供应商编写的类别所引发的异常区分开来？
- 您的代码是否会抛出多个相关异常？
- 如果您使用其他人的异常，用户是否可以访问这些异常？ 一个类似的问题是，你的包是否是独立且自包含的？

**例子**

假设您正在编写链表类。该类支持以下方法，其中包括：

- **objectAt (int n)**  - 返回列表中第n个位置的对象。如果参数小于0或大于列表中当前对象的数量，则引发异常。
- **firstObject ()**  - 返回列表中的第一个对象。如果列表不包含任何对象，则抛出异常。
- **indexOf (Object o)**  - 在列表中搜索指定的`Object`并返回其在列表中的位置。如果传递给方法的对象不在列表中，则抛出异常。

链表类可以抛出多个异常，并且能够通过一个异常处理程序捕获链表所引发的所有异常是很方便的。此外，如果您计划在包中分发链接列表，则应将所有相关代码打包在一起。因此，链表应该提供自己的一组异常类。

下图说明了链接列表抛出的异常的一个可能的类层次结构。

![A possible class hierarchy for the exceptions thrown by a linked list.](https://docs.oracle.com/javase/tutorial/figures/essential/exceptions-hierarchy.gif)

**选择一个超类**

任何`Exception`子类都可以用作`LinkedListException`的父类。但是，快速浏览这些子类表明它们不合适，因为它们太专用或者与`LinkedListException`完全无关。因此，`LinkedListException`的父类应该是`Exception`。

您编写的大多数`applet`和应用程序都会抛出`Exception`的对象。`Error`通常用于系统中严重的硬错误，例如阻止JVM运行的错误。

------

**注意：** 对于可读代码，最好将字符串`Exception`附加到从`Exception`类继承（直接或间接）的所有类的名称中。

------

### 不受检查异常－争议

由于Java编程语言的方法不需要捕获或指定不受检查的异常（`RuntimeException`，`Error`及其子类），因此程序员可能会编写仅抛出不受检查的异常或使其所有异常子类继承自`RuntimeException`的代码。这两个便捷的方式都允许程序员编写代码而不必担心编译器错误，也不必费心去指定或捕获任何异常。虽然这对程序员来说似乎很方便，但它会回避`catch`的意图或`specify`强制需求的初衷，并且可能会导致其他人使用您的类时出现问题。

为什么设计者决定强制一个方法来指定可以在其范围内抛出的所有未捕获的受检查异常？方法抛出的任何异常都是方法的公共编程接口的一部分。那些调用方法的人必须知道方法可能抛出的异常，以便他们可以决定如何处理它们。这些异常与该方法的编程接口一样，也是其参数和返回值的一部分。

下一个问题可能是：“如果记录方法的API非常好，包括它可以抛出的异常，为什么不指定运行时异常呢？”运行时异常表示编程问题导致的问题，因此，无法合理地期望API客户端代码从它们恢复或以任何方式处理它们。这些问题包括算术异常，例如除以零；指针异常，例如尝试通过空引用访问对象；和索引异常，例如尝试通过太大或太小的索引来访问数组元素。

运行时异常可以在程序中的任何地方发生，而在典型的程序中，它们可以非常多。必须在每个方法声明中添加运行时异常会降低程序的清晰度。因此，编译器不要求您捕获或指定运行时异常（尽管您可以）。

抛出`RuntimeException`的常见做法之一是用户错误地调用方法。例如，方法可以检查其中一个参数是否错误地为`null`。如果参数为`null`，则该方法可能会抛出`NullPointerException`，这是一个不受检查的异常。

一般来说，不要抛出`RuntimeException`或创建`RuntimeException`的子类，如果您不希望因为指定方法可以抛出的异常而烦恼。

这是底线指南：如果可以合理地期望客户端从异常中恢复，则将其作为受检查的异常。如果客户端无法执行任何操作以从异常中恢复，请将其设置为不受检查的异常。

### 异常的优势

现在您已经知道了什么是异常以及如何使用它们，现在是时候了解在程序中使用异常的优势了。

**优点1：将错误处理代码与“常规”代码分开**

异常提供了一种方法，可以在程序的主要逻辑中分离出异常情况时要执行的操作的详细信息。在传统的编程中，错误检测，报告和处理通常会导致混乱的意大利面条式的代码。例如，考虑这里的伪代码方法将整个文件读入内存。

```
readFile {
    open the file;
    determine its size;
    allocate that much memory;
    read the file into memory;
    close the file;
}
```

乍一看，这个功能似乎很简单，但它忽略了以下所有潜在的错误。

- 如果无法打开文件会怎么样？
- 如果无法确定文件的长度会发生什么？
- 如果无法分配足够的内存会怎样？
- 如果读取失败会发生什么？
- 如果文件无法关闭会怎样？

要处理这种情况，`readFile`函数必须有更多的代码来进行错误检测，报告和处理。以下是函数的外观示例。

```java
errorCodeType readFile {
    initialize errorCode = 0;
    
    open the file;
    if (theFileIsOpen) {
        determine the length of the file;
        if (gotTheFileLength) {
            allocate that much memory;
            if (gotEnoughMemory) {
                read the file into memory;
                if (readFailed) {
                    errorCode = -1;
                }
            } else {
                errorCode = -2;
            }
        } else {
            errorCode = -3;
        }
        close the file;
        if (theFileDidntClose && errorCode == 0) {
            errorCode = -4;
        } else {
            errorCode = errorCode and -4;
        }
    } else {
        errorCode = -5;
    }
    return errorCode;
}
```

这里有很多错误检测，报告和返回，原始的七行代码在杂乱中丢失了。更糟糕的是，代码的逻辑流程也已丢失，因此很难判断代码是否正在做正确的事情：如果函数无法分配足够的内存，文件是否真的被关闭了？ 在编写方法三个月后修改方法时，确保代码继续做正确的事情变得更加困难。许多程序员通过忽略它来解决这个问题 - 当程序崩溃时会报告错误。

异常使您可以编写代码的主要流程并在其他地方处理异常情况。如果`readFile`函数使用异常而不是传统的错误管理技术，它看起来更像是下面的样子：

```java
readFile {
    try {
        open the file;
        determine its size;
        allocate that much memory;
        read the file into memory;
        close the file;
    } catch (fileOpenFailed) {
       doSomething;
    } catch (sizeDeterminationFailed) {
        doSomething;
    } catch (memoryAllocationFailed) {
        doSomething;
    } catch (readFailed) {
        doSomething;
    } catch (fileCloseFailed) {
        doSomething;
    }
}
```

请注意，异常不会使您无需执行检测，报告和处理错误的工作，但它们确实可以帮助您更有效地组织工作。

**优势2：在调用堆栈中传播错误**

异常的第二个优点是能够在方法的调用堆栈中传播错误报告。假设`readFile`方法是主程序进行的一系列嵌套方法调用中的第四种方法：`method1`调用`method2`，它调用`method3`，最后调用`readFile`。

```java
method1 {
    call method2;
}

method2 {
    call method3;
}

method3 {
    call readFile;
}
```

假设`method1`是唯一对`readFile`中可能出现的错误感兴趣的方法。传统的错误通知技术强制`method2`和`method3`将`readFile`返回的错误代码传播到调用堆栈，直到错误代码最终到达`method1`-唯一对它们感兴趣的方法。

```java
method1 {
    errorCodeType error;
    error = call method2;
    if (error)
        doErrorProcessing;
    else
        proceed;
}

errorCodeType method2 {
    errorCodeType error;
    error = call method3;
    if (error)
        return error;
    else
        proceed;
}

errorCodeType method3 {
    errorCodeType error;
    error = call readFile;
    if (error)
        return error;
    else
        proceed;
}
```

回想一下，Java运行时环境在调用堆栈中向后搜索，以查找对处理特定异常感兴趣的任何方法。一个方法可以躲避抛出到其中的任何异常，从而允许一个调用栈中更远的方法来捕获它。因此，只有关心错误的方法才需要注意检测错误。

```java
method1 {
    try {
        call method2;
    } catch (exception e) {
        doErrorProcessing;
    }
}

method2 throws exception {
    call method3;
}

method3 throws exception {
    call readFile;
}
```

但是，正如伪代码所示，躲避异常需要中间人方法的一些努力。必须在其`throws`子句中指定可以在方法中抛出的任何受检查异常。

**优势3：分组和区分错误类型**

因为在程序中抛出的所有异常都是对象，所以异常的分组或分类是类层次结构的自然结果。Java平台中的一组相关异常类的示例是在`java.io`-`IOException`及其后代中定义的那些。`IOException`是最常用的，表示执行I / O时可能发生的任何类型的错误。它的后代表示更具体的错误。例如，`FileNotFoundException`表示文件无法在磁盘上定位。

方法可以编写可以处理非常特定异常的特定处理程序。 `FileNotFoundException`类没有后代，因此以下处理程序只能处理一种类型的异常。

```java
catch (FileNotFoundException e) {
    ...
}
```

方法可以通过在`catch`语句中指定任何异常的超类来基于其组或常规类型捕获异常。例如，要捕获所有I / O异常，不管它们的具体类型如何，异常处理程序指定一个`IOException`参数就可以了。

```java
catch (IOException e) {
    ...
}
```

这个处理程序将能够捕获所有I / O异常，包括`FileNotFoundException`，`EOFException`等。您可以通过查询传递给异常处理程序的参数来查找有关所发生情况的详细信息。例如，使用以下命令打印堆栈跟踪：

```java
catch (IOException e) {
    // Output goes to System.err.
    e.printStackTrace();
    // Send trace to stdout.
    e.printStackTrace(System.out);
}
```

您甚至可以设置一个异常处理程序来处理任何`Exception`：

```java
// A (too) general exception handler
catch (Exception e) {
    ...
}
```

`Exception`类接近`Throwable`类层次结构的顶部。因此，除了处理程序要捕获的那些异常之外，此处理程序还将捕获许多其他异常。如果您希望程序执行所有操作，您可能希望以这种方式处理异常，例如，为用户打印出错误消息然后退出。

但是，在大多数情况下，您希望异常处理程序尽可能具体。原因是处理程序必须做的第一件事是确定在确定最佳恢复策略之前发生了什么类型的异常。实际上，通过不捕获特定错误，处理程序必须适应任何可能性。过于笼统的异常处理程序可能会因为捕获和处理程序员未预料到并且程序意图之外的异常而导致代码更容易出错。

如上所述，您可以创建异常组并以一般方式处理异常，或者您可以使用特定的异常类型来区分异常并以精确的方式处理异常。

### 小结

程序可以使用异常来指示发生了错误。要抛出异常，请使用`throw`语句并为其提供一个异常对象 -  `Throwable`的后代 - 以提供有关发生的特定错误的信息。抛出未捕获的受检查异常的方法必须在其声明中包含`throws`子句。

程序可以通过结合使用`try`，`catch`和`finally`块来捕获异常。

- `try`块标识可能发生异常的代码块。
- `catch`块标识一个代码块，称为异常处理程序，可以处理特定类型的异常。
- `finally`块标识了一个保证执行的代码块，并且是在`try`块中包含的代码之后关闭文件，恢复资源和清理的正确位置。

`try`语句应包含至少一个`catch`块或`finally`块，并且可能有多个`catch`块。

异常对象的类指示抛出的异常类型。异常对象可以包含有关错误的更多信息，包括错误消息。使用异常链时，异常可以指向导致异常的异常，异常又可以指向导致它的异常，依此类推。

## 基本I/O

本课程介绍用于基本I/O的Java平台类。它首先关注*I/O Streams*，这是一个强大的概念，可以大大简化I/O操作。本课程还介绍了序列化，它允许程序将整个对象写入流并再次读取它们。然后，本课将介绍文件I/O和文件系统操作，包括随机访问文件。

`I/O Streams`部分中涵盖的大多数类都在`java.io`包中。`File I/O`部分中涵盖的大多数类都在`java.nio.file`包中。

**[I/O Streams](https://docs.oracle.com/javase/tutorial/essential/io/streams.html)**

- [Byte Streams](https://docs.oracle.com/javase/tutorial/essential/io/bytestreams.html) 处理原始二进制数据的 I/O。
- [Character Streams](https://docs.oracle.com/javase/tutorial/essential/io/charstreams.html) 处理字符数据的I/O，自动处理与本地字符集的转换。
- [Buffered Streams](https://docs.oracle.com/javase/tutorial/essential/io/buffers.html) 通过减少对本机API的调用次数来优化输入和输出。
- [Scanning and Formatting](https://docs.oracle.com/javase/tutorial/essential/io/scanfor.html) 允许程序读取和写入格式化文本。
- [I/O from the Command Line](https://docs.oracle.com/javase/tutorial/essential/io/cl.html) 描述标准流和控制台对象。
- [Data Streams](https://docs.oracle.com/javase/tutorial/essential/io/datastreams.html) 处理原始数据类型的二进制I/O和`String`值。
- [Object Streams](https://docs.oracle.com/javase/tutorial/essential/io/objectstreams.html) 处理对象的二进制I/O。

**[File I/O (Featuring NIO.2)](https://docs.oracle.com/javase/tutorial/essential/io/fileio.html)**

- [What is a Path?](https://docs.oracle.com/javase/tutorial/essential/io/path.html) 检查文件系统中的文件路径的概念。
- [The Path Class](https://docs.oracle.com/javase/tutorial/essential/io/pathClass.html) 介绍了`java.nio.file`包的基石类。
- [Path Operations](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html) 查看`Path`类中处理语法操作的方法。
- [File Operations](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html) 介绍了许多文件I/O方法的共同概念。
- [Checking a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/check.html) 演示了如何检查文件的存在及其可访问性级别。
- [Deleting a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/delete.html).
- [Copying a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/copy.html).
- [Moving a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/move.html).
- [Managing Metadata](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) 解释如何读取和设置文件属性。
- [Reading, Writing and Creating Files](https://docs.oracle.com/javase/tutorial/essential/io/file.html) 显示用于读取和写入文件的流和通道方法。
- [Random Access Files](https://docs.oracle.com/javase/tutorial/essential/io/rafs.html) 演示了如何以非顺序方式读取或写入文件。
- [Creating and Reading Directories](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html) 涵盖了特定于目录的API，例如如何列出目录的内容。
- [Links, Symbolic or Otherwise](https://docs.oracle.com/javase/tutorial/essential/io/links.html) 涵盖了特定于符号和硬链接的问题。
- [Walking the File Tree](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) 演示了如何递归访问文件树中的每个文件和目录。
- [Finding Files](https://docs.oracle.com/javase/tutorial/essential/io/find.html) 显示如何使用模式匹配搜索文件。
- [Watching a Directory for Changes](https://docs.oracle.com/javase/tutorial/essential/io/notification.html) 显示如何使用监视服务来检测在一个或多个目录中添加，删除或更新的文件。
- [Other Useful Methods](https://docs.oracle.com/javase/tutorial/essential/io/misc.html) 涵盖了本课程其他部分不适用的重要API。
- [Legacy File I/O Code](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html) 展示了如果使用`java.io.File`类的旧代码，如何利用`Path`功能。提供了将`java.io.File` API映射到`java.nio.file` API的表。

**I/O 类实战**

 [自定义网络](https://docs.oracle.com/javase/tutorial/networking/index.html) 中的许多示例使用本课程中描述的I/O流来通过网络连接读取和写入数据。

------

**安全考虑：** 某些I/O操作需要得到当前安全经理的批准。 这些课程中包含的示例程序是独立应用程序，默认情况下没有安全管理器。要在`applet`中工作，大多数这些示例都必须进行修改。有关安装在`applet`上的安全限制的信息，请参阅 [哪些Applet可以执行](https://docs.oracle.com/javase/tutorial/deployment/applet/security.html) 。

------

### I/O Streams

*I/O流*表示输入源或输出目的地。流可以表示许多不同类型的源和目标，包括磁盘文件，设备，其他程序和内存数组。

流支持许多不同类型的数据，包括简单字节，原始数据类型，本地化字符和对象。有些流只是简单地传递数据，其他流则以有用的方式操纵和转换数据。

无论它们在内部如何工作，所有流都为使用它们的程序提供相同的简单模型：流是一系列数据。程序使用*输入流*从源读取数据，一次读取一个元素：

![Reading information into a program.](https://docs.oracle.com/javase/tutorial/figures/essential/io-ins.gif)

读取信息到程序中。

程序使用*输出流*将数据写入目标，一次一个元素：

![Writing information from a program.](https://docs.oracle.com/javase/tutorial/figures/essential/io-outs.gif)

从程序写出信息。

在本节中，我们将看到可以处理各种数据的流，从原始值到高级对象。

上图所示的数据源和数据目的地可以是保存，生成或使用数据的任何东西。显然这包括磁盘文件，但源或目标也可以是另一个程序，外围设备，网络套接字或数组对象。

在下一节中，我们将使用最基本的流类型字节流来演示流I/O的常见操作。对于示例输入，我们将使用示例文件 [`xanadu.txt`](https://docs.oracle.com/javase/tutorial/essential/io/examples/xanadu.txt) ，其中包含以下内容：

```
In Xanadu did Kubla Khan
A stately pleasure-dome decree:
Where Alph, the sacred river, ran
Through caverns measureless to man
Down to a sunless sea.
```

#### Byte Streams

程序使用*字节流*来执行8位字节的输入和输出。所有字节流类都来自[`InputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html) 和 [`OutputStream`](https：//docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html) 。

有许多字节流类。为了演示字节流的工作原理，我们将重点关注文件I/O字节流，[`FileInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html) 和 [`FileOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html) 。其他种类的字节流的使用方式大致相同；它们的不同之处主要在于它们的构造方式。

**使用 Byte Streams**

我们将通过检查一个名为[`CopyBytes`](https://docs.oracle.com/javase/tutorial/essential/io/examples/CopyBytes.java) 的示例程序来探索`FileInputStream`和`FileOutputStream`。字节流复制`xanadu.txt`，一次一个字节。

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class CopyBytes {
    public static void main(String[] args) throws IOException {

        FileInputStream in = null;
        FileOutputStream out = null;

        try {
            in = new FileInputStream("xanadu.txt");
            out = new FileOutputStream("outagain.txt");
            int c;

            while ((c = in.read()) != -1) {
                out.write(c);
            }
        } finally {
            if (in != null) {
                in.close();
            }
            if (out != null) {
                out.close();
            }
        }
    }
}
```

`CopyBytes`大部分时间都消耗在一个简单的循环中，它读取输入流并一次写入一个字节的输出流，如下图所示。

![Simple byte stream input and output.](https://docs.oracle.com/javase/tutorial/figures/essential/byteStream.gif)

简单字节流输入输出。

**永远记住要关闭流**

在不再需要流时关闭流非常重要 - 同样重要的是`CopyBytes`使用`finally`块来保证即使发生错误也会关闭两个流。这种做法有助于避免严重的资源泄漏。

一个可能的错误是`CopyBytes`无法打开一个或两个文件。当发生这种情况时，对应于该文件的流变量永远不会从其初始的`null`值改变。这就是为什么`CopyBytes`在调用`close`之前需要确保每个流变量都包含一个对象引用。

**何时不使用字节流**

`CopyBytes`看起来像一个普通的程序，但它实际上代表了一种你应该避免的低级I/O. 由于`xanadu.txt`包含字符数据，最好的方法是使用[字符流](https://docs.oracle.com/javase/tutorial/essential/io/charstreams.html) ，如下一节所述。还有用于更复杂数据类型的流。字节流应仅用于最原始的I/O。

那么为什么要谈论字节流呢？因为所有其他流类型都是基于字节流构建的。

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

##### 格式化

实现格式化的流对象是 [`PrintWriter`](https://docs.oracle.com/javase/8/docs/api/java/io/PrintWriter.html)（字符流类）或 [`PrintStream`](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html)（字节流类）的实例。

------

**注意：** 您可能需要的唯一`PrintStream`对象是 [`System.out`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#out) 和 [`System.err`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#err)。（有关这些对象的更多信息，请参阅 [命令行中的 I/O](https://docs.oracle.com/javase/tutorial/essential/io/cl.html) ）当您需要创建格式化的输出流时，请实例化`PrintWriter`，而不是`PrintStream`。

------

与所有字节流和字符流对象一样，`PrintStream`和`PrintWriter`的实例实现了一组标准的写入方法，用于简单的字节和字符输出。此外，`PrintStream`和`PrintWriter`都实现了将内部数据转换为格式化输出的同一组方法。提供两个级别的格式：

- 以标准方式`print`和`println`格式化各个值。
- `format`基于格式字符串格式化几乎任意数量的值，具有许多用于精确格式化的选项。

**`print` 和 `println` 方法**

在使用适当的`toString`方法转换值后，调用`print`或`println`输出单个值。我们可以在 [`Root`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Root.java) 示例中看到这一点：

```java
public class Root {
    public static void main(String[] args) {
        int i = 2;
        double r = Math.sqrt(i);
        
        System.out.print("The square root of ");
        System.out.print(i);
        System.out.print(" is ");
        System.out.print(r);
        System.out.println(".");

        i = 5;
        r = Math.sqrt(i);
        System.out.println("The square root of " + i + " is " + r + ".");
    }
}
```

`Root` 的输出：

```
The square root of 2 is 1.4142135623730951.
The square root of 5 is 2.23606797749979.
```

`i`和`r`变量被格式化两次：第一次在`print`的重载中使用代码，第二次由Java编译器自动生成的转换代码，也使用`toString`。您可以通过这种方式格式化任何值，但是您无法控制结果。

**`format` 方法**

`format`方法根据*格式字符串*格式化多个参数。格式字符串由嵌入*格式说明符*的静态文本组成；除格式说明符外，格式字符串输出不变。

格式字符串支持许多功能。在本教程中，我们将介绍一些基础知识。完整说明，请参阅API规范中的[`格式化字符串语法`](https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html#syntax) 。

`Root2`示例使用单个`format`调用格式化两个值：

```java
public class Root2 {
    public static void main(String[] args) {
        int i = 2;
        double r = Math.sqrt(i);
        
        System.out.format("The square root of %d is %f.%n", i, r);
    }
}
```

输出：

```
The square root of 2 is 1.414214.
```

与本示例中使用的三个一样，所有格式说明符都以`％`开头，并以1或2个字符的*转换*结尾，指定生成的格式化输出的类型。这里使用的三个转换是：

- `d`将整数值格式化为十进制值。
- `f`将浮点值格式化为十进制值。
- `n`输出特定于平台的行终结符。

以下是其他一些转换：

- `x`将整数格式化为十六进制值。
- `s`将任何值格式化为字符串。
- `tB`将整数格式化为特定于语言环境的月份名称。

还有很多其他转换。

------

**注意：** 

除`%%`和`％n`外，所有格式说明符必须与参数匹配。如果不这样做，则会抛出异常。

在Java编程语言中，`\n`转义符始终生成换行符（`\u000A`）。除非您特别需要换行符，否则请勿使用`\n`。要获取本地平台的换行符，请使用`％n`。

------

除了转换之外，格式说明符还可以包含几个其他元素，以进一步自定义格式化输出。这是一个使用每种可能元素的示例 [`Format`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Format.java)。

```java
public class Format {
    public static void main(String[] args) {
        System.out.format("%f, %1$+020.10f %n", Math.PI);
    }
}
```

输出：

```
3.141593, +00000003.1415926536
```

附加元素都是可选的。下图显示了较长的格式说明符如何分解为单个元素。

![Elements of a format specifier](https://docs.oracle.com/javase/tutorial/figures/essential/io-spec.gif)

格式说明符的元素。

元素必须按所示顺序出现。从右侧开始，可选元素是：

- **精度** - 对于浮点值，这是格式化值的数学精度。对于s和其他常规转换，这是格式化值的最大宽度;如有必要，该值将被截断。
- **宽度** - 格式化值的最小宽度；必要时填充该值。默认情况下，该值使用空白填充。
- **标志** - 指定其他格式选项。在`Format`示例中，`+`标志指定应始终将数值格式化为带符号数字，`0`标志指定`0`是填充字符。其他标志包括`-`（右侧的填充）和`,`（具有特定于语言环境的千位分隔符的格式号）。请注意，某些标志不能与某些其他标志一起使用或与某些转换一起使用。
- **参数索引** - 允许您显式匹配指定的参数。您还可以指定`<`以匹配与前一个说明符相同的参数。因此该示例可以说写成：`System.out.format()"％f，％<+ 020.10f％n"，Math.PI)` 。

#### 命令行中的 I/O

程序经常从命令行运行，并在命令行环境中与用户交互。Java平台以两种方式支持这种交互：通过标准流和通过控制台。

**标准流**

标准流是许多操作系统的一个特性。默认情况下，他们从键盘读取输入并将输出写入显示器。它们还支持文件和程序之间的I/O，但该功能由命令行解释器控制，而不是程序。

Java平台支持三种标准流：*标准输入*，通过`System.in`访问；*标准输出*，通过`System.out`访问；和*标准错误*，通过`System.err`访问。这些对象是自动定义的，不需要打开。标准输出和标准错误均用于输出；单独的错误输出能力允许用户将常规输出转移到文件并在随后仍然能够读取错误消息。有关更多信息，请参阅命令行解释程序的文档。

您可能希望标准流是字符流，但由于历史原因，它们是字节流。`System.out`和`System.err`定义为`PrintStreamobjects`。虽然从技术上讲它是字节流，但`PrintStream`利用内部字符流对象来模拟字符流的许多功能。

相比之下，`System.in`是一个没有字符流功能的字节流。要将标准输入用作字符流，请在`InputStreamReader`中包装`System.in`。

```java
InputStreamReader cin = new InputStreamReader(System.in);
```

**控制台**

控制台是标准流的更高级替代方案。这是一个类型为`Console`的预定义对象，它具有标准流提供的大部分功能，以及其他功能。控制台对于安全密码输入特别有用。`Console`对象还通过其`reader`和`writer`方法提供作为真实字符流的输入和输出流。

在程序可以使用控制台之前，它必须通过调用`System.console()`来尝试检索`Console`对象。如果`Console`对象可用，则此方法返回该对象。如果`System.console`返回`NULL`，则不允许`Console`操作，因为操作系统不支持它们，或者因为程序是在非交互式环境中启动的。

`Console`对象通过其`readPassword`方法支持安全密码输入。此方法有助于以两种方式保护密码输入。首先，它抑制回显，因此密码在用户屏幕上不可见。其次，`readPassword`返回一个字符数组，而不是`String`，因此密码可以被覆盖，一旦不再需要就将其从内存中删除。

 [`Password`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Password.java) 示例是用于更改用户密码的原型程序。它演示了几种`Console`方法。

```java
import java.io.Console;
import java.util.Arrays;
import java.io.IOException;

public class Password {
    
    public static void main (String args[]) throws IOException {

        Console c = System.console();
        if (c == null) {
            System.err.println("No console.");
            System.exit(1);
        }

        String login = c.readLine("Enter your login: ");
        char [] oldPassword = c.readPassword("Enter your old password: ");

        if (verify(login, oldPassword)) {
            boolean noMatch;
            do {
                char [] newPassword1 = c.readPassword("Enter your new password: ");
                char [] newPassword2 = c.readPassword("Enter new password again: ");
                noMatch = ! Arrays.equals(newPassword1, newPassword2);
                if (noMatch) {
                    c.format("Passwords don't match. Try again.%n");
                } else {
                    change(login, newPassword1);
                    c.format("Password for %s changed.%n", login);
                }
                Arrays.fill(newPassword1, ' ');
                Arrays.fill(newPassword2, ' ');
            } while (noMatch);
        }

        Arrays.fill(oldPassword, ' ');
    }
    
    // Dummy change method.
    static boolean verify(String login, char[] password) {
        // This method always returns
        // true in this example.
        // Modify this method to verify
        // password according to your rules.
        return true;
    }

    // Dummy change method.
    static void change(String login, char[] password) {
        // Modify this method to change
        // password according to your rules.
    }
}
```

`Password`类遵循以下步骤：

1. 尝试检索`Console`对象。如果对象不可用，则中止。

2. 调用`Console.readLine`以提示并读取用户的登录名。

3. 调用`Console.readPassword`以提示并读取用户的现有密码。

4. 调用`verify`以确认用户有权更改密码。（在此示例中，`verify`是一个始终返回`true`的虚方法。）

5. 重复以下步骤，直到用户输入两次相同的密码：

     1. 两次调用`Console.readPassword`以提示并读取新密码。

        2. 如果用户同时输入相同的密码，请调用`change`以进行更改。（同样，`change`是一种虚拟方法。）

        3. 用空格覆盖两个密码。

6. 用空格覆盖旧密码。


#### 数据流

数据流支持原始数据类型值（`boolean`，`char`，`byte`，`short`，`int`，`long`，`float`和`double`）以及`String`值的二进制 I/O 。所有数据流都实现`DataInput`接口或`DataOutput`接口。本节重点介绍这些接口最广泛使用的实现 [`DataInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/DataInputStream.html) 和 [`DataOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html) 。

 [`DataStreams`](https://docs.oracle.com/javase/tutorial/essential/io/examples/DataStreams.java) 示例通过写出一组数据记录然后再次读取它们来演示数据流。每条记录包含三个与发票上的项目相关的值，如下表所示：

| Order in record | Data type | Data description | Output Method                  | Input Method                 | Sample Value     |
| --------------- | --------- | ---------------- | ------------------------------ | ---------------------------- | ---------------- |
| 1               | `double`  | Item price       | `DataOutputStream.writeDouble` | `DataInputStream.readDouble` | `19.99`          |
| 2               | `int`     | Unit count       | `DataOutputStream.writeInt`    | `DataInputStream.readInt`    | `12`             |
| 3               | `String`  | Item description | `DataOutputStream.writeUTF`    | `DataInputStream.readUTF`    | `"Java T-Shirt"` |

我们来看看`DataStreams`中的关键代码。首先，程序定义了一些常量，包含数据文件的名称和将写入的数据：

```java
static final String dataFile = "invoicedata";

static final double[] prices = { 19.99, 9.99, 15.99, 3.99, 4.99 };
static final int[] units = { 12, 8, 13, 29, 50 };
static final String[] descs = {
    "Java T-shirt",
    "Java Mug",
    "Duke Juggling Dolls",
    "Java Pin",
    "Java Key Chain"
};
```

然后`DataStreams`打开输出流。由于`DataOutputStream`只能作为现有字节流对象的包装器创建，因此`DataStreams`提供带缓冲的文件输出字节流。

```java
out = new DataOutputStream(new BufferedOutputStream(
              new FileOutputStream(dataFile)));
```

`DataStreams`写出记录并关闭输出流。

```java
for (int i = 0; i < prices.length; i ++) {
    out.writeDouble(prices[i]);
    out.writeInt(units[i]);
    out.writeUTF(descs[i]);
}
```

`writeUTF`方法以`UTF-8`的改进形式写出`String`值。这是一个可变宽度的字符编码，只需要一个字节表示常见的西方字符。

现在，`DataStreams`再次读回数据。首先，它必须提供输入流和变量来保存输入数据。与`DataOutputStream`一样，`DataInputStream`必须构造为字节流的包装器。

```java
in = new DataInputStream(new
            BufferedInputStream(new FileInputStream(dataFile)));

double price;
int unit;
String desc;
double total = 0.0;
```

现在，`DataStreams`可以读取流中的每条记录，报告它遇到的数据。

```java
try {
    while (true) {
        price = in.readDouble();
        unit = in.readInt();
        desc = in.readUTF();
        System.out.format("You ordered %d" + " units of %s at $%.2f%n",
            unit, desc, price);
        total += unit * price;
    }
} catch (EOFException e) {
}
```

请注意，`DataStreams`通过捕获 [`EOFException`](https://docs.oracle.com/javase/8/docs/api/java/io/EOFException.html)来检测文件结束条件，而不是测试无效的返回值。`DataInput`方法的所有实现都使用`EOFException`而不是返回值。

另请注意，`DataStream`中的每个特定`write`都与相应的特定`read`完全匹配。程序员需要确保输出类型和输入类型以这种方式匹配：输入流由简单的二进制数据组成，没有任何内容可以指示单个值的类型，或者它们在流中开始的位置。

`DataStreams`使用一种非常糟糕的编程技术：它使用浮点数来表示货币值。通常，浮点对于精确值是不利的。对于小数分数尤其不好，因为常见的数值（例如`0.1`）没有二进制表示。

表示货币值的正确类型是`java.math.BigDecimal`。不幸的是，`BigDecimal`是一种对象类型，因此它不适用于数据流。但是，`BigDecimal`将使用对象流，这将在下一节中介绍。

#### 对象流

正如数据流支持原始数据类型的 I/O 一样，对象流也支持对象的 I/O 。大多数（但不是全部）标准类支持其对象的序列化。因为它们确实实现了标记接口[`Serializable`](https://docs.oracle.com/javase/8/docs/api/java/io/Serializable.html) 。

对象流类是[`ObjectInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectInputStream.html)和[`ObjectOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectOutputStream.html) 。这些类实现[`ObjectInput`](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectInput.html) 和 [`ObjectOutput`](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectOutput.html) ，它们是`DataInput`和`DataOutput`的子接口。这意味着 [数据流](https://docs.oracle.com/javase/tutorial/essential/io/datastreams.html) 中涵盖的所有原始数据 I/O 方法也在对象流中实现。因此，对象流可以包含原始值和对象值的混合。 [`ObjectStreams`](https://docs.oracle.com/javase/tutorial/essential/io/examples/ObjectStreams.java) 示例说明了这一点。 `ObjectStreams`创建了与`DataStreams`相同的应用程序，并进行了一些更改。首先，价格现在是[`BigDecimal`](https://docs.oracle.com/javase/8/docs/api/java/math/BigDecimal.html)对象，以更好地表示小数值。其次，将[`Calendar`](https://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html)对象写入数据文件，表示发票日期。

如果`readObject()`没有返回预期的对象类型，试图将它强制转换为正确的类型可能抛出 [`ClassNotFoundException`](https://docs.oracle.com/javase/8/docs/api/java/lang/ClassNotFoundException.html) 。在这个简单的例子中，这不可能发生，因此我们不会尝试捕获异常。相反，我们通过在`main`方法的`throws`子句中添加`ClassNotFoundException`来通知编译器我们已经意识到了这个问题。

**复杂对象的输入输出**

`writeObject`和`readObject`方法使用起来很简单，但它们包含一些非常复杂的对象管理逻辑。这对像`Calendar`这样的类来说并不重要，它只封装了原始数据类型值。但是许多对象包含对其他对象的引用。如果`readObject`是从流中重构一个对象，它必须能够重建原始对象所引用的所有对象。这些附加对象可能有自己的引用，依此类推。在这种情况下，`writeObject`遍历整个对象引用网络，并将该网络中的所有对象写入流。因此，单次调用`writeObject`会导致大量对象被写入流。

下图中进行了演示，其中调用`writeObject`来写名为**a**的单个对象。该对象包含对象**b**和**c**的引用，而**b**包含对**d**和**e**的引用。调用`writeobject(a)`不仅会写**a **，而且还会写重建**a**所需的所有对象，因此此类依赖网络中的其他四个对象也会被写入。当**a**被`readObject`读回时，其他四个对象也被回读，并保留所有原始对象引用。

![I/O of multiple referred-to objects](https://docs.oracle.com/javase/tutorial/figures/essential/io-trav.gif)

多个引用对象的 I/O 。

您可能想知道如果同一个流上的两个对象都包含对某个对象的引用会发生什么。当他们回读时，他们都会引用一个对象吗？ 答案是肯定的。 流只能包含一个对象的副本，尽管它可以包含任意数量的对象。因此，如果您明确地将对象写入流两次，那么您实际上只写入了两次引用。例如，如果以下代码将对象`ob`两次写入流：

```java
Object ob = new Object();
out.writeObject(ob);
out.writeObject(ob);
```

每个`writeObject`必须与`readObject`匹配，因此读回流的代码将如下所示：

```java
Object ob1 = in.readObject();
Object ob2 = in.readObject();
```

这产生两个变量，`ob1`和`ob2`，它们是对同一个对象的引用。

但是，如果将单个对象写入两个不同的流，则它实际上是被复制的 - 读取两个流的单个程序将看到两个不同的对象。

### 文件 I/O

------

**注意：**  本教程介绍的文件 I/O 机制包含在 JDK 7 发布版本中。Java SE 6 版本中的文件 I/O 教程非常简短，不过你仍然可以下载 [Java SE Tutorial 2008-03-14](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-tutorials-419421.html#tutorial-2008_03_14-oth-JPR) 版本的教程，其中包含早期版本的文件 I/O 内容。

------

`java.nio.file` 包以及它的相关包，`java.nio.file.attribute`，提供对文件 I/O 的完善支持，用来访问默认文件系统。尽管该 API 包含许多类，你只需要关注少量几个入口点。你将发现这些 API 非常直观而且容易使用。

本教程以一个问题 [path 是什么?](https://docs.oracle.com/javase/tutorial/essential/io/path.html) 开始，然后，介绍 [Path 类](https://docs.oracle.com/javase/tutorial/essential/io/pathClass.html) ，包的主要入口点。接下来解释了`Path` 类中的方法相关的 [语法操作](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html) 。本教程随后转向包中的其他主要的类，`Files` 类，其中包含文件操作方法。首先介绍许多 [文件操作](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html) 通用的概念。然后介绍用于文件 [检查](https://docs.oracle.com/javase/tutorial/essential/io/check.html), [删除](https://docs.oracle.com/javase/tutorial/essential/io/delete.html), [拷贝](https://docs.oracle.com/javase/tutorial/essential/io/copy.html), 以及 [移动](https://docs.oracle.com/javase/tutorial/essential/io/move.html) 的方法。

本教程介绍了如何管理 [元数据](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) ，在继续介绍 [文件I/O](https://docs.oracle.com/javase/tutorial/essential/io/file.html) 和 [目录I/O](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html) 之前。[随机访问文件](https://docs.oracle.com/javase/tutorial/essential/io/rafs.html) 解释了 [符号和硬链接](https://docs.oracle.com/javase/tutorial/essential/io/links.html) 特定的问题。 

接下来，介绍一些非常强大但更高级的主题。首先，演示了 [递归遍历文件树](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) ，然后是有关如何 [使用通配符搜索文件的信息](https://docs.oracle.com/javase/tutorial/essential/io/find.html) 。接下来，将解释和演示如何 [查看更改目录](https://docs.oracle.com/javase/tutorial/essential/io/notification.html) 。然后，对 [不适合其他地方的方法](https://docs.oracle.com/javase/tutorial/essential/io/misc.html) 进行了一些介绍。

最后，如果您在 Java SE 7 发行版之前编写了文件 I/O代码，则会有[从旧API到新API的映射](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html#mapping) ，以及关于`File.toPath`方法的重要信息，供希望 [利用新API而不重写现有代码](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html#interop) 的开发人员使用。

#### 什么是 Path?（其他文件系统事实）

文件系统以某种形式存储和组织某些形式的媒体上的文件，通常是一个或多个硬盘驱动器，以便可以容易地检索它们。目前使用的大多数文件系统都以树（或*hierarchical*）结构存储文件。在树的顶部是一个（或多个）根节点。在根节点下，有文件和目录（Microsoft Windows中的*文件夹*）。每个目录都可以包含文件和子目录，而这些文件和子目录又可以包含文件和子目录，等等，可能达到几乎无限的深度。

本章节涵盖以下内容：

- [什么是 Path?](https://docs.oracle.com/javase/tutorial/essential/io/path.html#path)
- [相对还是绝对?](https://docs.oracle.com/javase/tutorial/essential/io/path.html#relative)
- [符号链接](https://docs.oracle.com/javase/tutorial/essential/io/path.html#symlink)

**什么是 Path?**

下图显示了包含单个根节点的示例目录树。Microsoft Windows支持多个根节点。每个根节点都映射到一个卷，例如`C:\`或`D:\`。Solaris OS支持单个根节点，用斜杠字符`/`表示。

![Sample directory structure](https://docs.oracle.com/javase/tutorial/figures/essential/io-dirStructure.gif)

目录结构示例

从根节点开始，文件通过文件系统的路径标识。例如，上图中的`statusReport`文件在Solaris OS中由以下表示法描述：

```
/home/sally/statusReport
```

在Microsoft Windows中，`statusReport`由以下表示法描述：

```
C:\home\sally\statusReport
```

用于分隔目录名称的字符（也称为*分隔符*）特定于文件系统：Solaris OS使用正斜杠（`/`），Microsoft Windows使用反斜杠斜杠（`\`）。

**相对还是绝对？**

路径是 *relative* 或 *absolute* 的。绝对路径始终包含查找文件所需的根元素和完整目录列表。例如，`/home/sally/statusReport`是绝对路径。查找文件所需的所有信息都包含在路径字符串中。

相对路径需要与另一个路径组合才能访问文件。例如，`joe/foo`是一个相对路径。没有更多信息，程序无法可靠地找到文件系统中的`joe/foo`目录。

**符号链接**

文件系统对象通常是目录或文件。每个人都熟悉这些对象。但是一些文件系统也支持符号链接的概念。符号链接也称为*符号链接*或*软链接*。

*符号链接*是一个特殊文件，用作对另一个文件的引用。在大多数情况下，符号链接对应用程序是透明的，符号链接上的操作会自动重定向到链接的目标。（指向的文件或目录称为链接的*target*。）例外情况是删除或重命名符号链接，在这种情况下链接本身被删除或重命名，而不是链接的目标。

在下图中，`logFile`似乎是用户的常规文件，但它实际上是指向`dir/logs/HomeLogFile`的符号链接。`HomeLogFile`是链接的目标。

![Sample symbolic link](https://docs.oracle.com/javase/tutorial/figures/essential/io-symlink.gif)

符号链接示例。

符号链接通常对用户是透明的。读取或写入符号链接与读取或写入任何其他文件或目录相同。

短语*解析链接*意味着用文件系统中的实际位置替换符号链接。在示例中，解析`logFile`会产生`dir/logs/HomeLogFile`。

在实际场景中，大多数文件系统都可以自由使用符号链接。偶尔，粗心创建的符号链接可能会导致循环引用。当链接的目标指向原始链接时，会发生循环引用。循环引用可能是间接引用：目录`a`指向目录`b`，而目录`b`指向目录`c`，目录`c`中包含一个指向目录`a`的子目录。当程序递归地遍历目录结构时，循环引用可能会导致严重破坏。但是，此问题已被考虑到，并且不会导致程序无限循环。

下一章节将讨论Java编程语言中文件 I/O 支持的核心，即`Path`类。

#### `Path`类

Java SE 7发行版中引入的`Path`类是`java.nio.file`包的主要入口点之一。如果您的应用程序使用文件 I/O，您将需要了解此类的强大功能。

------

**版本提醒：** 如果您的JDK7之前的代码使用的是`java.io.File`，则仍可以使用`File.toPath`方法来利用`Path`类功能。有关更多信息，请参阅 [遗留 文件 I/O 代码](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html) 。

------

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

此API中使用的许多资源（如流或通道）实现或扩展 [`java.io.Closeable`](https://docs.oracle.com/javase/8/docs/api/java/io/Closeable.html) 接口。`Closeable`资源意味着是必须调用`close`方法以在不再需要时释放资源。忽略关闭资源可能会对应用程序的性能产生负面影响。下一节中描述的`try-with-resources`语句为您处理此步骤。

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

------

**注意：** 如果您在键盘上键入glob模式并且它包含一个特殊字符，则必须将模式放在引号（`“*”`）中，使用反斜杠（`\ *`）或使用命令行支持任何转义机制。

------

glob语法功能强大且易于使用。但是，如果它不足以满足您的需求，您还可以使用正则表达式。有关详细信息，请参阅 [正则表达式](https://docs.oracle.com/javase/tutorial/essential/regex/index.html) 课程。

有关glob语法的更多信息，请参阅`FileSystem`类中的方法 [`getPathMatcher`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#getPathMatcher-java.lang.String-) 的API规范。

**链接敏感**

`Files`类是“链接感知”的。 每个`Files`方法都会检测遇到符号链接时要执行的操作，或者它提供了一个选项，使您可以配置在遇到符号链接时的行为。

#### 检查文件或者目录

你有一个表示文件或目录的`Path`实例，但该文件是否存在于文件系统中？它可读吗？可写？可执行？

**校验文件或者目录的存在性**

`Path`类中的方法是语法意义上的，这意味着它们在`Path`实例上运行。但最终您必须访问文件系统以验证特定的`Path`是否存在。您可以使用 [`exists(Path, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#exists-java.nio.file.Path-java.nio.file.LinkOption...-) 和 [`notExists(Path, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#notExists-java.nio.file.Path-java.nio.file.LinkOption...-) 方法。注意`!Files.exists(path)`不等同于`Files.notExists(path)`。当您测试文件存在时，可能会有三个结果：

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

------

**检查两个路径是否定位同一个文件**

当您有一个使用符号链接的文件系统时，可能有两个不同的路径来定位同一个文件。 [`isSameFile(Path, Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isSameFile-java.nio.file.Path-java.nio.file.Path-) 方法比较两个路径以确定它们是否在文件系统上找到相同的文件。例如：

```java
Path p1 = ...;
Path p2 = ...;

if (Files.isSameFile(p1, p2)) {
    // Logic when the paths locate the same file
}
```

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

您可以使用 [`move(Path, Path, CopyOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#move-java.nio.file.Path-java.nio.file.Path-java.nio.file.CopyOption...-) 方法移动文件或目录。如果目标文件存在，则移动失败，除非指定了`REPLACE_EXISTING`选项。

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

#### 管理元数据（文件和文件存储属性）

*元数据*的定义是“关于其他数据的数据”。使用文件系统，数据包含在其文件和目录中，元数据跟踪有关每个文件和目录对象的信息：它是常规文件，目录还是链接？ 它的大小，创建日期，上次修改日期，文件所有者，组所有者和访问权限是什么？

文件系统的元数据通常称为其*文件属性*。`Files`类包括可用于获取文件的单个属性或设置属性的方法。

| 方法                                       | 说明                                   |
| ---------------------------------------- | ------------------------------------ |
| [`size(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#size-java.nio.file.Path-) | 返回给定文件的字节尺寸。                         |
| [`isDirectory(Path, LinkOption)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isDirectory-java.nio.file.Path-java.nio.file.LinkOption...-) | 如果给定的`Path`定位到一个目录时返回`true`。         |
| [`isRegularFile(Path, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isRegularFile-java.nio.file.Path-java.nio.file.LinkOption...-) | 如果给定的`Path`定位到一个常规文件时返回`true`。       |
| [`isSymbolicLink(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isSymbolicLink-java.nio.file.Path-) | 如果给定的`Path`定位到一个符号链接时返回`true`。       |
| [`isHidden(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isHidden-java.nio.file.Path-) | 如果给定的`Path`定位到一个文件系统中的隐藏文件时返回`true`。 |
| [`getLastModifiedTime(Path, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#getLastModifiedTime-java.nio.file.Path-java.nio.file.LinkOption...-) [`setLastModifiedTime(Path, FileTime)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#setLastModifiedTime-java.nio.file.Path-java.nio.file.attribute.FileTime-) | 返回或者设置给定文件的最后修改时间。                   |
| [`getOwner(Path, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#getOwner-java.nio.file.Path-java.nio.file.LinkOption...-) [`setOwner(Path, UserPrincipal)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#setOwner-java.nio.file.Path-java.nio.file.attribute.UserPrincipal-) | 返回或者设置文件所有者。                         |
| [`getPosixFilePermissions(Path, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#getPosixFilePermissions-java.nio.file.Path-java.nio.file.LinkOption...-) [`setPosixFilePermissions(Path, Set)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#setPosixFilePermissions-java.nio.file.Path-java.util.Set-) | 返回或者设置文件的 POSIX 文件权限。                |
| [`getAttribute(Path, String, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#getAttribute-java.nio.file.Path-java.lang.String-java.nio.file.LinkOption...-) [`setAttribute(Path, String, Object, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#setAttribute-java.nio.file.Path-java.lang.String-java.lang.Object-java.nio.file.LinkOption...-) | 返回或者设置一个文件属性的值。                      |

如果程序在同一时间需要多个文件属性，则使用检索单个属性的方法可能效率低下。重复访问文件系统以检索单个属性可能会对性能产生负面影响。因此，`Files`类提供了两个`readAttributes`方法，用于在一次批量操作中获取文件的属性。

| 方法                                       | 说明                                       |
| ---------------------------------------- | ---------------------------------------- |
| [`readAttributes(Path, String, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#readAttributes-java.nio.file.Path-java.lang.String-java.nio.file.LinkOption...-) | 批量读取文件属性，其中的`String`参数指定需要读取的属性。         |
| [`readAttributes(Path, Class, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#readAttributes-java.nio.file.Path-java.lang.Class-java.nio.file.LinkOption...-) | 批量读取文件属性。 `Class <A>`参数是请求的属性类型，该方法返回该类的对象。 |

在展示`readAttributes`方法的示例之前，应该指出不同的文件系统对于应该跟踪哪些属性有不同的概念。因此，相关文件属性被组合在一起成为视图。*视图*映射到特定的文件系统实现，例如 POSIX 或 DOS，或者映射到常用功能，例如文件所有权。

支持的视图如下：

- [`BasicFileAttributeView`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/BasicFileAttributeView.html) - 提供所有文件系统实现都需要支持的基本属性的视图。
- [`DosFileAttributeView`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/DosFileAttributeView.html）) - 以标准的4位支持扩展基本属性视图支持DOS属性的文件系统。
- [`PosixFileAttributeView`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/PosixFileAttributeView.html)  - 使用文件系统支持的属性扩展基本属性视图支持POSIX标准系列，例如UNIX。这些属性包括文件所有者，组所有者和九个相关的访问权限。
- [`FileOwnerAttributeView`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/FileOwnerAttributeView.html) - 被支持文件所有者概念的任何文件系统实现支持。
- [`AclFileAttributeView`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/AclFileAttributeView.html) - 支持读取或更新文件的访问控制列表（ACL） 。支持NFSv4 ACL模型。也可以支持任何ACL模型，例如Windows ACL模型，它具有到NFSv4模型的定义良好的映射。
- [`UserDefinedFileAttributeView`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/UserDefinedFileAttributeView.html) - 支持用户定义的元数据。此视图可以映射到系统支持的任何扩展机制。例如，在Solaris OS中，您可以使用此视图来存储文件的MIME类型。

特定文件系统实现可能仅支持基本文件属性视图，或者它可能支持其中几个文件属性视图。文件系统实现可能支持此API中未包含的其他属性视图。

在大多数情况下，您不必直接处理任何`FileAttributeView`接口。（如果你确实需要直接使用`FileAttributeView`，你可以通过 [`getFileAttributeView(Path, Class, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#getFileAttributeView-java.nio.file.Path-java.lang.Class-java.nio.file.LinkOption...-) 方法来访问它。）

`readAttributes`方法使用泛型，可用于读取任何文件属性视图的属性。本节其余部分的示例使用`readAttributes`方法。

本节的其余部分包括以下主题：

- [基本文件属性](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#basic)
- [设定时间戳](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#time)
- [DOS 文件属性](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#dos)
- [POSIX 文件权限](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#posix)
- [设定文件或者组所有者](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#lookup)
- [用户自定义文件属性](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#user)
- [文件存储属性](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#store)

**基本文件属性**

如前所述，要读取文件的基本属性，可以使用`Files.readAttributes`方法之一，该方法批量读取所有基本属性。这比单独访问文件系统以读取每个单独的属性要有效得多。可变参数目前支持[`LinkOption`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/LinkOption.html) 枚举，`NOFOLLOW_LINKS`。如果不希望遵循符号链接，请使用此选项。

------

**关于时间戳的一个词：** 基本属性集包括三个时间戳：`creationTime`，`lastModifiedTime`和`lastAccessTime`。在特定实现中可能不支持任何这些时间戳，在这种情况下，相应的访问器方法返回特定于实现的值。当特定实现支持时，时间戳将作为 [`FileTime`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/FileTime.html) 对象返回。

------

以下代码片段读取并打印给定文件的基本文件属性，并使用 [`BasicFileAttributes`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/BasicFileAttributes.html) 类中的方法。

```java
Path file = ...;
BasicFileAttributes attr = Files.readAttributes(file, BasicFileAttributes.class);

System.out.println("creationTime: " + attr.creationTime());
System.out.println("lastAccessTime: " + attr.lastAccessTime());
System.out.println("lastModifiedTime: " + attr.lastModifiedTime());

System.out.println("isDirectory: " + attr.isDirectory());
System.out.println("isOther: " + attr.isOther());
System.out.println("isRegularFile: " + attr.isRegularFile());
System.out.println("isSymbolicLink: " + attr.isSymbolicLink());
System.out.println("size: " + attr.size());
```

除了本例中显示的访问器方法之外，还有一个`fileKey`方法，它返回唯一标识文件的对象，如果没有可用的文件密钥，则返回“null”。

**设定时间戳**

下面的代码片段蛇形文件的最后修改时间毫秒值。

```java
Path file = ...;
BasicFileAttributes attr =
    Files.readAttributes(file, BasicFileAttributes.class);
long currentTime = System.currentTimeMillis();
FileTime ft = FileTime.fromMillis(currentTime);
Files.setLastModifiedTime(file, ft);
}
```

**DOS 文件属性**

除DOS之外的文件系统也支持DOS文件属性，例如 Samba。以下代码段使用 [`DosFileAttributes`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/DosFileAttributes.html) 类的方法。

```java
Path file = ...;
try {
    DosFileAttributes attr =
        Files.readAttributes(file, DosFileAttributes.class);
    System.out.println("isReadOnly is " + attr.isReadOnly());
    System.out.println("isHidden is " + attr.isHidden());
    System.out.println("isArchive is " + attr.isArchive());
    System.out.println("isSystem is " + attr.isSystem());
} catch (UnsupportedOperationException x) {
    System.err.println("DOS file" +
        " attributes not supported:" + x);
}
```

不过，你可以设定一个 DOS 属性，使用 [`setAttribute(Path, String, Object, LinkOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#setAttribute-java.nio.file.Path-java.lang.String-java.lang.Object-java.nio.file.LinkOption...-) 方法，如下：

```java
Path file = ...;
Files.setAttribute(file, "dos:hidden", true);
```

**POSIX 文件权限**

*POSIX*是用于UNIX的可移植操作系统接口的首字母缩写，是一组 IEEE 和 ISO 标准，旨在确保不同版本的 UNIX 之间的互操作性。如果程序符合这些 POSIX 标准，则应该可以轻松移植到其他符合 POSIX 标准的操作系统。

除文件所有者和组所有者外，POSIX还支持九种文件权限：文件所有者、同一组成员以及“其他所有人“的读，写，执行权限。

以下代码段读取给定文件的 POSIX 文件属性并将其打印到标准输出。该代码使用 [`PosixFileAttributes`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/PosixFileAttributes.html) 类中的方法。

```java
Path file = ...;
PosixFileAttributes attr =
    Files.readAttributes(file, PosixFileAttributes.class);
System.out.format("%s %s %s%n",
    attr.owner().getName(),
    attr.group().getName(),
    PosixFilePermissions.toString(attr.permissions()));
```

[`PosixFilePermissions`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/PosixFilePermissions.html) 帮助类提供了几种有用的方法，如下所示：

- 在前面的代码片段中使用的`toString`方法将文件权限转换为字符串（例如，`rw-r--r-- `）。
- `fromString`方法接受表示文件权限的字符串，并构造文件权限的集合`Set`。
- `asFileAttribute`方法接受文件权限的集合`Set`并构造一个可以传递给`Path.createFile`或`Path.createDirectory`方法的文件属性。

以下代码段从一个文件中读取属性并创建一个新文件，将原始文件中的属性分配给新文件：

```java
Path sourceFile = ...;
Path newFile = ...;
PosixFileAttributes attrs =
    Files.readAttributes(sourceFile, PosixFileAttributes.class);
FileAttribute<Set<PosixFilePermission>> attr =
    PosixFilePermissions.asFileAttribute(attrs.permissions());
Files.createFile(file, attr);
```

`asFileAttribute`方法将权限包装为`FileAttribute`。然后，代码尝试使用这些权限创建新文件。请注意，`umask`也适用，因此新文件可能比请求的权限更安全。

要将文件的权限设置为表示为硬编码字符串的值，可以使用以下代码：

```java
Path file = ...;
Set<PosixFilePermission> perms =
    PosixFilePermissions.fromString("rw-------");
FileAttribute<Set<PosixFilePermission>> attr =
    PosixFilePermissions.asFileAttribute(perms);
Files.setPosixFilePermissions(file, perms);
```

 [`Chmod`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Chmod.java) 例子递归修改文件权限，类似于 `chmod` 工具指令。

**设定文件或者组所有者**

要将名称转换为可以存储为文件所有者或组所有者的对象，可以使用 [`UserPrincipalLookupService`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/UserPrincipalLookupService.html) 服务。此服务将查找名称或组名称字符串，并返回表示该字符串的`UserPrincipal`对象。您可以使用 [`FileSystem.getUserPrincipalLookupService`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#getUserPrincipalLookupService--) 方法获取默认文件系统的用户主体查找服务。

以下代码段显示了如何使用`setOwner`方法设置文件所有者：

```java
Path file = ...;
UserPrincipal owner = file.GetFileSystem().getUserPrincipalLookupService()
        .lookupPrincipalByName("sally");
Files.setOwner(file, owner);
```

`Files`类中没有用于设置组所有者的特殊方法。但是，直接执行此操作的安全方法是通过POSIX文件属性视图，如下所示：

```java
Path file = ...;
GroupPrincipal group =
    file.getFileSystem().getUserPrincipalLookupService()
        .lookupPrincipalByGroupName("green");
Files.getFileAttributeView(file, PosixFileAttributeView.class)
     .setGroup(group);
```

**用户自定义文件属性**

如果文件系统实现支持的文件属性不足以满足您的需要，您可以使用`UserDefinedAttributeView`来创建和跟踪您自己的文件属性。

一些实现将此概念映射到NTFS备用数据流等功能以及文件系统（如ext3和ZFS）上的扩展属性。大多数实现都对值的大小施加了限制，例如，ext3将大小限制为4千字节。

通过使用以下代码片段，可以将文件的MIME类型存储为用户定义的属性：

```java
Path file = ...;
UserDefinedFileAttributeView view = Files
    .getFileAttributeView(file, UserDefinedFileAttributeView.class);
view.write("user.mimetype",
           Charset.defaultCharset().encode("text/html");
```

要读取MIME类型属性，您可以使用以下代码段：

```java
Path file = ...;
UserDefinedFileAttributeView view = Files
.getFileAttributeView(file,UserDefinedFileAttributeView.class);
String name = "user.mimetype";
ByteBuffer buf = ByteBuffer.allocate(view.size(name));
view.read(name, buf);
buf.flip();
String value = Charset.defaultCharset().decode(buf).toString();
```

 [`Xdd`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Xdd.java) 示例显示了如何获取，设置和删除用户定义的属性。

------

**注意：** 在Linux中，您可能必须启用扩展属性才能使用户定义的属性起作用。如果在尝试访问用户定义的属性视图时收到`UnsupportedOperationException`，则需要重新挂载文件系统。以下命令使用ext3文件系统的扩展属性重新挂载根分区。如果此命令不适合您的Linux风格，请参阅文档。

```shell
$ sudo mount -o remount,user_xattr /
```

如果要使更改成为永久更改，请添加条目到 `/etc/fstab`。

------

**文件存储属性**

您可以使用 [`FileStore`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileStore.html) 类来了解有关文件存储的信息，例如有多少可用空间。 [`getFileStore(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#getFileStore-java.nio.file.Path-) 方法 获取指定文件的文件存储。

以下代码段打印特定文件所在的文件存储的空间使用情况：

```java
Path file = ...;
FileStore store = Files.getFileStore(file);

long total = store.getTotalSpace() / 1024;
long used = (store.getTotalSpace() -
             store.getUnallocatedSpace()) / 1024;
long avail = store.getUsableSpace() / 1024;
```

 [`DiskUsage`](https://docs.oracle.com/javase/tutorial/essential/io/examples/DiskUsage.java) 示例使用此API打印默认文件系统中所有存储的磁盘空间信息。此示例使用`FileSystem`类中的 [`getFileStores`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#getFileStores--) 方法 获取文件系统的所有文件存储。

#### 读、写以及创建文件

This page discusses the details of reading, writing, creating, and opening files. There are a wide array of file I/O methods to choose from. To help make sense of the API, the following diagram arranges the file I/O methods by complexity.

本页讨论了读取，写入，创建和打开文件的细节。有多种文件I/O方法可供选择。为了帮助理解API，下图按复杂性排列文件I/O方法。

![Line drawing with file I/O methods arranged from least complex (on the left) to most complex (on the right).](https://docs.oracle.com/javase/tutorial/figures/essential/io-fileiomethods.gif)

文件 I/O 方法从简单到复杂排列

图的最左边是实用方法`readAllBytes`，`readAllLines`和`write`方法，专为简单的常见情况而设计。在这些方法的右边是用于迭代一行或多行文本的方法，例如`newBufferedReader`，`newBufferedWriter`，然后是`newInputStream`和`newOutputStream`。这些方法可与`java.io`包互操作。这些方法的右边是处理`ByteChannels`，`SeekableByteChannels`和`ByteBuffers`的方法，例如`newByteChannel`方法。最后，最右边的是使用`FileChannel`的方法，用于需要文件锁定或内存映射I/O的高级应用程序。

------

**注意：** 创建新文件的方法使您可以为文件指定一组可选的初始属性。例如，在支持POSIX标准集（例如UNIX）的文件系统上，您可以在创建文件时指定文件所有者，组所有者或文件权限。 [管理元数据](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) 页面介绍了文件属性以及如何访问和设置它们。

------

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
**文本文件使用的带缓冲的I/O方法**

`java.nio.file`包支持通道 I/O，它在缓冲区中移动数据，绕过一些可能阻塞流 I/O 的层。

使用带缓冲的流 I/O 读取文件

 [`newBufferedReader(Path, Charset)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newBufferedReader-java.nio.file.Path-java.nio.charset.Charset-) 方法打开一个文件进行读取，返回一个`BufferedReader`，可用于以高效的方式从文件中读取文本。

以下代码段显示了如何使用`newBufferedReader`方法从文件中读取。该文件以“US-ASCII”编码。

```java
Charset charset = Charset.forName("US-ASCII");
try (BufferedReader reader = Files.newBufferedReader(file, charset)) {
    String line = null;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException x) {
    System.err.format("IOException: %s%n", x);
}
```

使用带缓冲的流 I/O 写入文件

您可以使用 [`newBufferedWriter(Path, Charset, OpenOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newBufferedWriter-java.nio.file.Path-java.nio.charset.Charset-java.nio.file.OpenOption...-) 方法使用`BufferedWriter`写入文件。

以下代码段显示了如何使用此方法创建以“US-ASCII”编码的文件：

```java
Charset charset = Charset.forName("US-ASCII");
String s = ...;
try (BufferedWriter writer = Files.newBufferedWriter(file, charset)) {
    writer.write(s, 0, s.length());
} catch (IOException x) {
    System.err.format("IOException: %s%n", x);
}
```

**无缓冲流的方法和可与java.io API互操作的方法**

使用流 I/O 读取文件

要打开文件进行读取，可以使用 [`newInputStream(Path, OpenOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newInputStream-java.nio.file.Path-java.nio.file.OpenOption...-) 方法。此方法返回一个无缓冲的输入流，用于从文件中读取字节。

```java
Path file = ...;
try (InputStream in = Files.newInputStream(file);
    BufferedReader reader =
      new BufferedReader(new InputStreamReader(in))) {
    String line = null;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException x) {
    System.err.println(x);
}
```

使用流 I/O 创建并写入文件

您可以使用 [`newOutputStream(Path, OpenOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newOutputStream-java.nio.file.Path-java.nio.file.OpenOption...-) 方法创建文件，附加到文件或写入文件。此方法打开或创建用于写入字节的文件，并返回无缓冲的输出流。

该方法采用可选的`OpenOption`参数。如果未指定打开选项，并且该文件不存在，则会创建一个新文件。如果文件存在，则会被截断。此选项等效于使用`CREATE和TRUNCATE_EXISTING`选项调用该方法。

以下示例打开一个日志文件。如果该文件不存在，则创建该文件。如果该文件存在，则打开该文件以进行追加。

```java
import static java.nio.file.StandardOpenOption.*;
import java.nio.file.*;
import java.io.*;

public class LogFileTest {

  public static void main(String[] args) {

    // Convert the string to a
    // byte array.
    String s = "Hello World! ";
    byte data[] = s.getBytes();
    Path p = Paths.get("./logfile.txt");

    try (OutputStream out = new BufferedOutputStream(
      Files.newOutputStream(p, CREATE, APPEND))) {
      out.write(data, 0, data.length);
    } catch (IOException x) {
      System.err.println(x);
    }
  }
}
```

**Channels和ByteBuffers的方法**

使用通道I / O读取和写入文件

当流 I/O 一次读取一个字符时，通道 I/O 一次读取一个缓冲区。 [`ByteChannel`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/ByteChannel.html) 接口提供基本的读写功能。  [`SeekableByteChannel`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html) 是一个`ByteChannel`，它能够维持通道中的位置并改变该位置。`SeekableByteChannel`还支持截断与通道关联的文件并查询文件的大小。

移动到文件中的不同点然后从该位置读取或写入的能力使得可以随机访问文件。有关更多信息，请参阅 [Random Access Files](https://docs.oracle.com/javase/tutorial/essential/io/rafs.html) 。

下面是两个读写通道 I/O 的方法：

- [`newByteChannel(Path, OpenOption...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newByteChannel-java.nio.file.Path-java.nio.file.OpenOption...-)
- [`newByteChannel(Path, Set, FileAttribute...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#newByteChannel-java.nio.file.Path-java.util.Set-java.nio.file.attribute.FileAttribute...-)

------

**注意：** `newByteChannel`方法返回`SeekableByteChannel`的实例。使用默认文件系统，您可以将此可搜索字节通道转换为 [`FileChannel`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/FileChannel.html) ，从而提供对更高级功能的访问，例如将文件区域直接映射到内存中以便更快地访问，锁定文件的某个区域以便其他进程无法访问它，或者从绝对位置读取和写入字节而不影响通道的当前位置。

------

两种`newByteChannel`方法都允许您指定`OpenOption`选项列表。 除了支持`newOutputStream`方法使用的相同 [open options](https://docs.oracle.com/javase/tutorial/essential/io/file.html#openOptions) ，还有一个选项：需要`READ`，因为`SeekableByteChannel`支持读取和写入。

指定`READ`将打开要读取的通道。指定`WRITE`或`APPEND`会打开要写入的通道。如果未指定这些选项，则打开通道进行读取。

以下代码段读取文件并将其打印到标准输出：

```java
// Defaults to READ
try (SeekableByteChannel sbc = Files.newByteChannel(file)) {
    ByteBuffer buf = ByteBuffer.allocate(10);

    // Read the bytes with the proper encoding for this platform.  If
    // you skip this step, you might see something that looks like
    // Chinese characters when you expect Latin-style characters.
    String encoding = System.getProperty("file.encoding");
    while (sbc.read(buf) > 0) {
        buf.rewind();
        System.out.print(Charset.forName(encoding).decode(buf));
        buf.flip();
    }
} catch (IOException x) {
    System.out.println("caught exception: " + x);
}
```

以下示例是为 UNIX 和其他 POSIX 文件系统编写的，它创建了一个具有一组特定文件权限的日志文件。此代码创建日志文件或附加到日志文件（如果已存在）。创建日志文件时，所有者具有读/写权限，组具有只读权限。

```java
import static java.nio.file.StandardOpenOption.*;
import java.nio.*;
import java.nio.channels.*;
import java.nio.file.*;
import java.nio.file.attribute.*;
import java.io.*;
import java.util.*;

public class LogFilePermissionsTest {

  public static void main(String[] args) {
  
    // Create the set of options for appending to the file.
    Set<OpenOption> options = new HashSet<OpenOption>();
    options.add(APPEND);
    options.add(CREATE);

    // Create the custom permissions attribute.
    Set<PosixFilePermission> perms =
      PosixFilePermissions.fromString("rw-r-----");
    FileAttribute<Set<PosixFilePermission>> attr =
      PosixFilePermissions.asFileAttribute(perms);

    // Convert the string to a ByteBuffer.
    String s = "Hello World! ";
    byte data[] = s.getBytes();
    ByteBuffer bb = ByteBuffer.wrap(data);
    
    Path file = Paths.get("./permissions.log");

    try (SeekableByteChannel sbc =
      Files.newByteChannel(file, options, attr)) {
      sbc.write(bb);
    } catch (IOException x) {
      System.out.println("Exception thrown: " + x);
    }
  }
}
```

**创建常规文件和临时文件的方法**

创建文件

您可以使用 [`createFile(Path, FileAttribute)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createFile-java.nio.file.Path-java.nio.file.attribute.FileAttribute...-) 方法创建具有初始属性集的空文件。例如，如果在创建时希望文件具有特定的文件权限集，请使用`createFile`方法执行此操作。如果未指定任何属性，则使用默认属性创建文件。如果该文件已存在，则`createFile`将抛出异常。

在单个原子操作中，`createFile`方法检查文件是否存在，并使用指定的属性创建该文件，这使得该过程对恶意代码更安全。

以下代码段创建一个具有默认属性的文件：

```java
Path file = ...;
try {
    // Create the empty file with default permissions, etc.
    Files.createFile(file);
} catch (FileAlreadyExistsException x) {
    System.err.format("file named %s" +
        " already exists%n", file);
} catch (IOException x) {
    // Some other sort of failure, such as permissions.
    System.err.format("createFile error: %s%n", x);
}
```

[POSIX文件权限](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#posix) 有一个示例，它使用 `createFile(Path, FileAttribute<?>)` 来创建具有预设权限的文件。

您还可以使用`newOutputStream`方法创建新文件，如 [使用流 I/O 创建和写入文件](https://docs.oracle.com/javase/tutorial/essential/io/file.html#createStream) 中所述。如果打开新输出流并立即关闭它，则会创建一个空文件。

创建临时文件

您可以使用以下`createTempFile`方法之一创建临时文件：

- [`createTempFile(Path, String, String, FileAttribute)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createTempFile-java.nio.file.Path-java.lang.String-java.lang.String-java.nio.file.attribute.FileAttribute...-)
- [`createTempFile(String, String, FileAttribute)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createTempFile-java.lang.String-java.lang.String-java.nio.file.attribute.FileAttribute...-)

第一种方法允许代码指定临时文件的目录，第二种方法在默认临时文件目录中创建新文件。这两种方法都允许您为文件名指定后缀，第一种方法允许您指定前缀。以下代码段给出了第二种方法的示例：

```java
try {
    Path tempFile = Files.createTempFile(null, ".myapp");
    System.out.format("The temporary file" +
        " has been created: %s%n", tempFile)
;
} catch (IOException x) {
    System.err.format("IOException: %s%n", x);
}
```

运行此文件的结果如下所示：

```
The temporary file has been created: /tmp/509668702974537184.myapp
```

临时文件名的特定格式是特定于平台的。

#### 随机存取文件

*随机访问文件*允许对文件内容进行非顺序或随机访问。要随机访问文件，请打开文件，查找特定位置，然后读取或写入该文件。

使用 [`SeekableByteChannel`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html) 接口可以实现此功能。 `SeekableByteChannel`接口使用当前位置的概念扩展通道 I/O. 使用方法可以设置或查询位置，然后可以从该位置读取数据或将数据写入该位置。API由一些易于使用的方法组成：

- [`position`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#position--) – 返回通道的当前位置
- [`position(long)`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#position-long-) – 设定通道的当前位置
- [`read(ByteBuffer)`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#read-java.nio.ByteBuffer-) – 从通道读取字节进入缓冲区
- [`write(ByteBuffer)`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#write-java.nio.ByteBuffer-) – 将缓冲区中的字节写入通道
- [`truncate(long)`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#truncate-long-) – 切断文件（或者其它实体）与通道的联系

[使用通道 I/O 读取和写入文件](https://docs.oracle.com/javase/tutorial/essential/io/file.html#channelio)  展示了`Path.newByteChannel`方法返回`SeekableByteChannel`的实例。在默认文件系统上，您可以按原样使用该通道，也可以将其强制转换为 [`FileChannel`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/FileChannel.html) ，以便访问更高级的功能，例如将文件区域直接映射到内存中以便更快地访问，锁定文件区域，或从绝对位置读取和写入字节而不影响通道的当前位置。

以下代码段使用`newByteChannel`方法之一打开用于读取和写入的文件。返回的`SeekableByteChannel`将强制转换为`FileChannel`。然后，从文件的开头读取12个字节，字符串 "I was here!" 是在那个地方写的。文件中的当前位置移动到末尾，并附加从开头的12个字节。最后，字符串， "I was here!" 附加，并关闭文件上的通道。

```java
String s = "I was here!\n";
byte data[] = s.getBytes();
ByteBuffer out = ByteBuffer.wrap(data);

ByteBuffer copy = ByteBuffer.allocate(12);

try (FileChannel fc = (FileChannel.open(file, READ, WRITE))) {
    // Read the first 12
    // bytes of the file.
    int nread;
    do {
        nread = fc.read(copy);
    } while (nread != -1 && copy.hasRemaining());

    // Write "I was here!" at the beginning of the file.
    fc.position(0);
    while (out.hasRemaining())
        fc.write(out);
    out.rewind();

    // Move to the end of the file.  Copy the first 12 bytes to
    // the end of the file.  Then write "I was here!" again.
    long length = fc.size();
    fc.position(length-1);
    copy.flip();
    while (copy.hasRemaining())
        fc.write(copy);
    while (out.hasRemaining())
        fc.write(out);
} catch (IOException x) {
    System.out.println("I/O Exception: " + x);
}
```

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

------

**请记住：** 返回的`DirectoryStream` 是一个流。如果您没有使用`try-with-resources`语句，请不要忘记在`finally`块中关闭流。`try-with-resources`语句会为您解决此问题。

------

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

#### 符号链接或其它链接

如前所述，`java.nio.file`包，特别是`Path`类，是“链接感知”的。每个`Path`方法都会检测遇到符号链接时要执行的操作，或者它提供了一个选项，使您可以在遇到符号链接时配置行为。

到目前为止的讨论是关于 [符号或软链接](https://docs.oracle.com/javase/tutorial/essential/io/path.html#symlink) ，但一些文件系统也支持硬链接。*硬链接*比符号链接更具限制性，如下所示：

- 链接的目标必须存在。
- 目录上通常不允许使用硬链接。
- 不允许硬链接跨越分区或卷。因此，它们不能跨文件系统存在。
- 硬链接的样子和行为像普通文件一样，因此很难分辨它们。
- 对于所有意图和目的，硬链接是与原始文件相同的实体。它们具有相同的文件权限，时间戳等。所有属性都相同。

由于这些限制，硬链接不像符号链接那样频繁使用，但`Path`方法与硬链接无缝协作。

有几种方法专门处理链接，并在以下部分中介绍：

- [创建符号链接](https://docs.oracle.com/javase/tutorial/essential/io/links.html#symLink)
- [创建硬链接](https://docs.oracle.com/javase/tutorial/essential/io/links.html#hardLink)
- [删除符号链接](https://docs.oracle.com/javase/tutorial/essential/io/links.html#detect)
- [寻找链接的目标](https://docs.oracle.com/javase/tutorial/essential/io/links.html#read)

**创建符号链接**

如果文件系统支持，则可以使用 [`createSymbolicLink(Path, Path, FileAttribute)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createSymbolicLink-java.nio.file.Path-java.nio.file.Path-java.nio.file.attribute.FileAttribute...-) 方法创建符号链接。第二个`Path`参数表示目标文件或目录，可能存在也可能不存在。以下代码段创建了具有默认权限的符号链接：

```java
Path newLink = ...;
Path target = ...;
try {
    Files.createSymbolicLink(newLink, target);
} catch (IOException x) {
    System.err.println(x);
} catch (UnsupportedOperationException x) {
    // Some file systems do not support symbolic links.
    System.err.println(x);
}
```

`FileAttributes` 可变参数使您可以指定在创建链接时以原子方式设置的初始文件属性。但是，此参数仅供将来使用，目前尚未实现。

**创建硬链接**

您可以使用 [`createLink(Path, Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#createLink-java.nio.file.Path-java.nio.file.Path-) 方法创建指向现有文件的硬（或常规）链接。第二个`Path`参数定位现有文件，它必须存在或抛出`NoSuchFileException`。以下代码段显示了如何创建链接：

```java
Path newLink = ...;
Path existingFile = ...;
try {
    Files.createLink(newLink, existingFile);
} catch (IOException x) {
    System.err.println(x);
} catch (UnsupportedOperationException x) {
    // Some file systems do not
    // support adding an existing
    // file to a directory.
    System.err.println(x);
}
```

**删除符号链接**

要确定`Path`实例是否为符号链接，可以使用 [`isSymbolicLink(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#isSymbolicLink-java.nio.file.Path-) 方法。以下代码段显示了如何使用：

```java
Path file = ...;
boolean isSymbolicLink =
    Files.isSymbolicLink(file);
```

更多信息，参考 [管理元数据](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html).

**寻找链接的目标**

您可以使用 [`readSymbolicLink(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#readSymbolicLink-java.nio.file.Path-) 方法获取符号链接的目标，如下所示：

```java
Path link = ...;
try {
    System.out.format("Target of link" +
        " '%s' is '%s'%n", link,
        Files.readSymbolicLink(link));
} catch (IOException x) {
    System.err.println(x);
}
```

如果`Path`不是符号链接，则此方法将抛出`NotLinkException`。

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

#### 监控目录和文件变化

您是否曾经发现自己使用IDE或其他编辑器编辑文件，并出现一个对话框，通知您文件系统中的某个打开文件已更改并需要重新加载？ 或者，与NetBeans IDE一样，应用程序只是在不通知您的情况下安静地更新文件。以下示例对话框显示了此通知在免费编辑器 [jEdit](http://sourceforge.net/projects/jedit/) 中的显示方式：

![Sample jEdit Dialog stating: The following files were changed on disk by another program.](https://docs.oracle.com/javase/tutorial/figures/essential/io-jEditDialog.png)

`jEdit`对话框显示检测到修改过的文件

要实现此功能（称为文件更改通知），程序必须能够检测文件系统上相关目录的内容。一种方法是轮询文件系统以查找更改，但这种方法效率低下。它不能扩展到具有数百个要监视的打开文件或目录的应用程序。

`java.nio.file`包提供了一个名为`Watch Service API`的文件更改通知API。此API使您可以使用监视服务注册目录（或多个目录）。注册时，您告诉服务您感兴趣的事件类型：文件创建，文件删除或文件修改。当服务检测到感兴趣的事件时，它将被转发到注册的进程。已注册的进程有一个线程（或一个线程池），专门用于监视它已注册的任何事件。当一个事件进入时，它会根据需要进行处理。

本章节涵盖以下内容：

- [监控服务概览](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#overview)
- [试一试](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#try)
- [创建监控服务并注册事件](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#register)
- [事件处理](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#process)
- [获取文件名](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#name)
- [此 API 的使用时机](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#concerns)

**监控服务概览**

`WatchService` API相当底层，允许自定义。您可以按原样使用它，也可以选择在此机制之上创建高级API，以便它适合您的特定需求。

以下是实现监视服务所需的基本步骤：

- 为文件系统创建`WatchService` “观察者”。
- 对于要监视的每个目录，请将其注册到观察程序。注册目录时，您可以指定要通知的事件类型。您为每个注册的目录收到一个`WatchKey`实例。
- 实现无限循环以等待传入事件。当事件发生时，`WatchKey`将发出信号并放入观察者的队列中。
- 从观察者的队列中检索`WatchKey`。您可以从`WatchKey`中获取文件名。
- 检索`WatchKey`的每个待处理事件（可能有多个事件）并根据需要进行处理。
- 重置`WatchKey`，然后继续等待事件。
- 关闭服务：当线程退出或关闭时（通过调用其`closed`方法），监视服务退出。

`WatchKeys`是线程安全的，可以与`java.nio.concurrent`包一起使用。您可以将 [线程池](https://docs.oracle.com/javase/tutorial/essential/concurrency/pools.html) 专用于此工作。

**试一试**

因为此API更高级，所以在继续之前尝试一下。将 [`WatchDir`](https://docs.oracle.com/javase/tutorial/essential/io/examples/WatchDir.java) 示例保存到您的计算机，然后进行编译。创建将传递给示例的`test`目录。`WatchDir`使用单个线程来处理所有事件，因此它在等待事件时阻止键盘输入。在单独的窗口中或在后台运行程序，如下所示：

```
java WatchDir test &
```

在`test`目录中创建，删除和编辑文件。发生任何这些事件时，会向控制台输出一条消息。完成后，删除`test`目录并退出`WatchDir`。或者，如果您愿意，可以手动终止该过程。

您还可以通过指定`-r`选项来查看整个文件树。指定`-r`时，`WatchDir`遍历文件树，使用监视服务注册每个目录。

**创建监控服务并注册事件**

第一步是使用`FileSystem`类中的 [`newWatchService`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#newWatchService--) 方法创建一个新的 [`WatchService`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html) ，如下所示：

```java
WatchService watcher = FileSystems.getDefault().newWatchService();
```

接下来，使用监视服务注册一个或多个对象。可以注册实现 [`Watchable`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Watchable.html) 接口的任何对象。`Path`类实现`Watchable`接口，因此每个要监视的目录都注册为`Path`对象。

与任何`Watchable`一样，`Path类`实现两个 `register` 方法。此页面使用双参数版本， [`register(WatchService, WatchEvent.Kind...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#register-java.nio.file.WatchService-java.nio.file.WatchEvent.Kind...-) 。（三参数版本采用`WatchEvent.Modifier`，目前尚未实现。）

使用监视服务注册对象时，可以指定要监视的事件类型。支持的 [`StandardWatchEventKinds`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/StandardWatchEventKinds.html) 事件类型如下：

- `ENTRY_CREATE` – 目录实体被创建
- `ENTRY_DELETE` – 目录实体被删除
- `ENTRY_MODIFY` – 目录实体被修改
- `OVERFLOW` – 表示事件可能已丢失或丢弃。您无需注册`OVERFLOW`事件即可接收它。

以下代码段显示了如何为所有三种事件类型注册`Path`实例：

```java
import static java.nio.file.StandardWatchEventKinds.*;

Path dir = ...;
try {
    WatchKey key = dir.register(watcher,
                           ENTRY_CREATE,
                           ENTRY_DELETE,
                           ENTRY_MODIFY);
} catch (IOException x) {
    System.err.println(x);
}
```

**事件处理**

事件处理循环中事件的顺序如下：

1. 获取一个`WatchKey`。提供了3个方法：
   - [`poll`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html#poll--) – 返回排队的键（如果可用）。如果不可用，则立即返回`null`值。
   - [`poll(long, TimeUnit)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html#poll-long-java.util.concurrent.TimeUnit-) – 返回排队的键（如果有）。如果排队的键不能立即可用，程序将等待指定的时间。`TimeUnit`参数确定指定的时间是纳秒，毫秒还是某个其他时间单位。
   - [`take`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html#take--) – 返回排队的键。如果没有可用的排队键，则此方法将等待。
2. 处理`WatchKey`对应的等待事件。您从 [`pollEvents`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchKey.html#pollEvents--) 方法获取 [`WatchEvents`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchEvent.html) 的 `List` 。
3. 使用 [`kind`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchEvent.html#kind--) 方法检索事件类型。无论`WatchKey`注册的是什么事件，都可以收到`OVERFLOW`事件。您可以选择处理它或忽略它，但您应该测试这种情况。
4. 检索与事件关联的文件名。文件名存储为事件的上下文，因此 [`context`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchEvent.html#context--) 方法用于检索它。
5. 处理完`WatchKey`事件后，需要通过调用 [`reset`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchEvent.html#reset--) 将`WatchKey`恢复到 `ready` 状态。如果此方法返回`false`，则该`WatchKey`不再有效，并且循环可以退出。这一步非常重要。如果您未能调用`reset`，则此`WatchKey`不会再接收任何事件。

`WatchKey`是有状态的，在任何给定时刻，它的状态可能是下面中的一个：

- `Ready` 表示`WatchKey`已准备好接受事件。首次创建时，`WatchKey`处于就绪状态。
- `Signaled` 表示一个或多个事件已排队。一旦发出`WatchKey`信号，它就不再处于就绪状态，直到调用 [`reset`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchKey.html#reset--) 方法。
- `Invalid` 表示`WatchKey`不再有效。发生以下事件之一时会进入此状态：
  - 该过程使用 [`cancel`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchKey.html#cancel--) 方法明确取消`WatchKey`。
  - 目录变为不可访问。
  - 监控服务被 [关闭](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html#close--) 。

以下是事件处理循环的示例。它取自 [`Email`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Email.java) 示例，该示例监视目录，等待新文件出现。当新文件可用时，将使用 [`probeContentType(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#probeContentType-java.nio.file.Path-) 方法检查它是否为`text/plain`文件。目的是将`text/plain`文件通过电子邮件发送到一个地址别名，但该实现细节留给读者。

监控服务API特有的方法以粗体显示：

```java
for (;;) {

    // wait for key to be signaled
    WatchKey key;
    try {
        key = watcher.take();
    } catch (InterruptedException x) {
        return;
    }

    for (WatchEvent<?> event: key.pollEvents()) {
        WatchEvent.Kind<?> kind = event.kind();

        // This key is registered only
        // for ENTRY_CREATE events,
        // but an OVERFLOW event can
        // occur regardless if events
        // are lost or discarded.
        if (kind == OVERFLOW) {
            continue;
        }

        // The filename is the
        // context of the event.
        WatchEvent<Path> ev = (WatchEvent<Path>)event;
        Path filename = ev.context();

        // Verify that the new
        //  file is a text file.
        try {
            // Resolve the filename against the directory.
            // If the filename is "test" and the directory is "foo",
            // the resolved name is "test/foo".
            Path child = dir.resolve(filename);
            if (!Files.probeContentType(child).equals("text/plain")) {
                System.err.format("New file '%s'" +
                    " is not a plain text file.%n", filename);
                continue;
            }
        } catch (IOException x) {
            System.err.println(x);
            continue;
        }

        // Email the file to the
        //  specified email alias.
        System.out.format("Emailing file %s%n", filename);
        //Details left to reader....
    }

    // Reset the key -- this step is critical if you want to
    // receive further watch events.  If the key is no longer valid,
    // the directory is inaccessible so exit the loop.
    boolean valid = key.reset();
    if (!valid) {
        break;
    }
}
```

**获取文件名**

从事件上下文中检索文件名。[`Email`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Email.java) 示例使用以下代码检索文件名：

```java
WatchEvent<Path> ev = (WatchEvent<Path>)event;
Path filename = ev.context();
```

编译 `Email` 示例时，它会生成以下错误：

```
Note: Email.java uses unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
```

此错误是将`WatchEvent<T>`强制转换为 `WatchEvent<Path>`的代码行的结果。[`WatchDir`](https://docs.oracle.com/javase/tutorial/essential/io/examples/WatchDir.java) 示例通过创建一个抑制未经检查的警告的实用程序强制转换方法来避免此错误，如下所示：

```java
@SuppressWarnings("unchecked")
static <T> WatchEvent<T> cast(WatchEvent<?> event) {
    return (WatchEvent<Path>)event;
}
```

如果不熟悉 `@SuppressWarnings` 语法，参考 [注解](https://docs.oracle.com/javase/tutorial/java/annotations/index.html) 。

**使用时机**

Watch Service API专为需要通知文件更改事件的应用程序而设计。它非常适合任何应用程序，如编辑器或IDE，可能有许多打开的文件，需要确保文件与文件系统同步。它也非常适合于监视目录的应用程序服务器，可能等待`.jsp`或`.jar`文件变化，以便随时部署它们。

此API不适用于索引硬盘驱动器。大多数文件系统实现都具有文件更改通知的本机支持。Watch Service API在可用的情况下利用此支持。但是，当文件系统不支持此机制时，Watch Service将轮询文件系统，等待事件。

#### 其它有用的方法

一些有用的方法不适用于本课程的其他地方，在此处介绍。本节包括以下内容：

- [确定`MIME`类型](https://docs.oracle.com/javase/tutorial/essential/io/misc.html#mime)
- [默认文件系统](https://docs.oracle.com/javase/tutorial/essential/io/misc.html#default)
- [路径分隔符](https://docs.oracle.com/javase/tutorial/essential/io/misc.html#separator)
- [文件系统文件存储](https://docs.oracle.com/javase/tutorial/essential/io/misc.html#stores)

**确定`MIME`类型**

要确定文件的MIME类型，您可能会发现 [`probeContentType(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#probeContentType-java.nio.file.Path-) 方法很有用。 例如：T

```java
try {
    String type = Files.probeContentType(filename);
    if (type == null) {
        System.err.format("'%s' has an" + " unknown filetype.%n", filename);
    } else if (!type.equals("text/plain") {
        System.err.format("'%s' is not" + " a plain text file.%n", filename);
        continue;
    }
} catch (IOException x) {
    System.err.println(x);
}
```

请注意，如果无法确定内容类型，则 `probeContentType` 将返回`null`。

此方法的实现具有高度平台相关性，并非绝对可靠。内容类型由平台的默认文件类型检测器确定。例如，如果检测器根据`.class`扩展名将文件的内容类型确定为`application/x-java`，则可能会被欺骗。

如果默认值不足以满足您的需要，您可以提供自定义 [`FileTypeDetector`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/spi/FileTypeDetector.html) 。

 [`Email`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Email.java) 示例使用 `probeContentType`方法。

**默认文件系统**

要检索默认文件系统，请使用 [`getDefault`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystems.html#getDefault--) 方法。通常，这个 `FileSystems` 方法（注意复数）被链接到 `FileSystem` 方法之一（注意单数），如下所示：

```java
PathMatcher matcher =
    FileSystems.getDefault().getPathMatcher("glob:*.*");
```

**路径分隔符**

POSIX文件系统的路径分隔符是正斜杠，`/`，对于Microsoft Windows，是反斜杠`\`。其他文件系统可能使用其他分隔符。要检索默认文件系统的路径分隔符，可以使用以下方法之一：

```java
String separator = File.separator;
String separator = FileSystems.getDefault().getSeparator();
```

 [`getSeparator`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#getSeparator--) 方法还用于检索任何可用文件系统的路径分隔符。

**文件系统的文件存储**

文件系统具有一个或多个文件存储来保存其文件和目录。文件存储表示底层存储设备。在UNIX操作系统中，每个安装的文件系统都由文件存储表示。在Microsoft Windows中，每个卷都由文件存储表示：`C:`，`D:`，依此类推。

要检索文件系统的所有文件存储列表，可以使用 [`getFileStores`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#getFileStores--) 方法。此方法返回一个`Iterable`，它允许您使用增强的for语句迭代所有根目录。

```java
for (FileStore store: FileSystems.getDefault().getFileStores()) {
   ...
}
```

如果要检索特定文件所在的文件存储，请使用`Files`类中的 [`getFileStore`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#getFileStore-java.nio.file.Path-) 方法，如下所示：

```java
Path file = ...;
FileStore store= Files.getFileStore(file);
```

 [`DiskUsage`](https://docs.oracle.com/javase/tutorial/essential/io/examples/DiskUsage.java) 示例使用 `getFileStores` 方法。

#### 遗留文件 I/O 代码

**与遗留代码互操作**

在Java SE 7发布之前，`java.io.File`类是用于文件I/O的机制，但它有几个缺点。

- 许多方法在失败时都没有抛出异常，因此无法获得有用的错误消息。例如，如果文件删除失败，程序将收到“删除失败”，但不知道是否因为该文件不存在，用户没有权限，或者还有其他问题。
- 重命名方法不能跨平台一致地工作。
- 对符号链接没有真正的支持。
- 需要更多对元数据的支持，例如文件权限，文件所有者和其他安全属性。
- 访问文件元数据效率低下。
- 许多`File`方法都没有扩展。通过服务器请求大型目录列表可能会导致挂起。大目录也可能导致内存资源问题，导致拒绝服务。
- 如果存在循环符号链接，则无法编写可递归遍历文件树的可靠代码并进行适当响应。

也许你有遗留代码使用`java.io.File`并希望利用`java.nio.file.Path`功能，而对代码的影响最小。

`java.io.File`类提供了`toPath`方法，该方法将旧样式`File`实例转换为`java.nio.file.Path`实例，如下所示：

```java
Path input = file.toPath();
```

然后，您可以利用`Path`类可用的丰富功能集。

例如，假设您有一些删除文件的代码：

```java
file.delete();
```

您可以修改此代码以使用`Files.delete`方法，如下所示：

```java
Path fp = file.toPath();
Files.delete(fp);
```

相反，`Path.toFile`方法为`Path`对象构造`java.io.File`对象。

**`java.io.File`功能映射到`java.nio.file`**

由于文件I/O的Java实现已在Java SE 7发行版中完全重新构建，因此您无法将一种方法替换为另一种方法。如果要使用`java.nio.file`包提供的丰富功能，最简单的解决方案是使用上一节中建议的`File.toPath`方法。但是，如果您不想使用该方法或者它不足以满足您的需求，则必须重写文件I/O代码。

这两个API之间没有一对一的对应关系，但是下表让您全面了解`java.io.File` API中的哪些功能在`java.nio.file` API中映射到哪里，并告诉您哪里可以获取更多信息。

| java.io.File Functionality               | java.nio.file Functionality              | Tutorial Coverage                        |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| `java.io.File`                           | `java.nio.file.Path`                     | [The Path Class](https://docs.oracle.com/javase/tutorial/essential/io/pathClass.html) |
| `java.io.RandomAccessFile`               | The `SeekableByteChannel` functionality. | [Random Access Files](https://docs.oracle.com/javase/tutorial/essential/io/rafs.html) |
| `File.canRead`, `canWrite`, `canExecute` | `Files.isReadable`, `Files.isWritable`, and `Files.isExecutable`.On UNIX file systems, the [Managing Metadata (File and File Store Attributes)](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) package is used to check the nine file permissions. | [Checking a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/check.html)[Managing Metadata](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) |
| `File.isDirectory()`, `File.isFile()`, and `File.length()` | `Files.isDirectory(Path, LinkOption...)`, `Files.isRegularFile(Path, LinkOption...)`, and `Files.size(Path)` | [Managing Metadata](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) |
| `File.lastModified()` and `File.setLastModified(long)` | `Files.getLastModifiedTime(Path, LinkOption...)` and `Files.setLastMOdifiedTime(Path, FileTime)` | [Managing Metadata](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) |
| The `File` methods that set various attributes: `setExecutable`, `setReadable`, `setReadOnly`, `setWritable` | These methods are replaced by the `Files` method `setAttribute(Path, String, Object, LinkOption...)`. | [Managing Metadata](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) |
| `new File(parent, "newfile")`            | `parent.resolve("newfile")`              | [Path Operations](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html) |
| `File.renameTo`                          | `Files.move`                             | [Moving a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/move.html) |
| `File.delete`                            | `Files.delete`                           | [Deleting a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/delete.html) |
| `File.createNewFile`                     | `Files.createFile`                       | [Creating Files](https://docs.oracle.com/javase/tutorial/essential/io/file.html#createFile) |
| `File.deleteOnExit`                      | Replaced by the `DELETE_ON_CLOSE` option specified in the `createFile` method. | [Creating Files](https://docs.oracle.com/javase/tutorial/essential/io/file.html#createFile) |
| `File.createTempFile`                    | `Files.createTempFile(Path, String, FileAttributes<?>)`, `Files.createTempFile(Path, String, String, FileAttributes<?>)` | [Creating Files](https://docs.oracle.com/javase/tutorial/essential/io/file.html#createFile)[Creating and Writing a File by Using Stream I/O](https://docs.oracle.com/javase/tutorial/essential/io/file.html#createStream)[Reading and Writing Files by Using Channel I/O](https://docs.oracle.com/javase/tutorial/essential/io/file.html#channelio) |
| `File.exists`                            | `Files.exists` and `Files.notExists`     | [Verifying the Existence of a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/check.html) |
| `File.compareTo` and `equals`            | `Path.compareTo` and `equals`            | [Comparing Two Paths](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#compare) |
| `File.getAbsolutePath` and `getAbsoluteFile` | `Path.toAbsolutePath`                    | [Converting a Path](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#convert) |
| `File.getCanonicalPath` and `getCanonicalFile` | `Path.toRealPath` or `normalize`         | [Converting a Path (`toRealPath`)](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#convert)[Removing Redundancies From a Path (`normalize`)](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#normal) |
| `File.toURI`                             | `Path.toURI`                             | [Converting a Path](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#convert) |
| `File.isHidden`                          | `Files.isHidden`                         | [Retrieving Information About the Path](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html#info) |
| `File.list` and `listFiles`              | `Path.newDirectoryStream`                | [Listing a Directory's Contents](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#listdir) |
| `File.mkdir` and `mkdirs`                | `Path.createDirectory`                   | [Creating a Directory](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#create) |
| `File.listRoots`                         | `FileSystem.getRootDirectories`          | [Listing a File System's Root Directories](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html#listall) |
| `File.getTotalSpace`, `File.getFreeSpace`, `File.getUsableSpace` | `FileStore.getTotalSpace`, `FileStore.getUnallocatedSpace`, `FileStore.getUsableSpace`, `FileStore.getTotalSpace` | [File Store Attributes](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html#store) |

### 小结

`java.io`包中包含许多程序可用于读写数据的类。大多数类实现顺序访问流。顺序访问流可以分为两类：读取和写入字节的以及读取和写入Unicode字符的。每个顺序访问流都具有特殊性，例如读取或写入文件，过滤数据作为其读取或写入，或序列化对象。

`java.nio.file`包为文件和文件系统I/O提供了广泛的支持。这是一个非常全面的API，但关键切入点如下：

- `Path`类具有操作路径的方法。
- `Files`类具有文件操作的方法，例如移动，复制，删除，以及用于检索和设置文件属性的方法。
- `FileSystem`类有多种方法可用于获取有关文件系统的信息。

有关`NIO.2`的更多信息，请访问 [OpenJDK: NIO](http://openjdk.java.net/projects/nio/) 项目网站。此站点包含`NIO.2`提供的功能的资源，这些功能超出了本教程的范围，例如多播，异步I/O和创建自己的文件系统实现。

## 并发

计算机用户理所当然地认为他们的系统一次可以做多件事。他们假设他们可以继续在文字处理器中工作，而其他应用程序则下载文件，管理打印队列和流式传输音频。即使是单个应用程序通常也希望一次完成多个任务。例如，流式音频应用程序必须同时从网络读取数字音频，解压缩，管理播放和更新其显示。即使文字处理器应始终准备好响应键盘和鼠标事件，无论重新格式化文本或更新显示有多繁忙。可以执行此类操作的软件称为并发软件。

Java平台的设计初衷是为了支持并发编程，在Java编程语言和Java类库中提供基本的并发支持。从5.0版开始，Java平台还包含高级并发API。本课程介绍了平台的基本并发支持，并总结了`java.util.concurrent`包中的一些高级API。

### 进程和线程

在并发编程中，有两个基本的执行单元：进程和线程。在Java编程语言中，并发编程主要涉及线程。但是，进程也很重要。

计算机系统通常具有许多活动进程和线程。即使在只有一个执行核心的系统中也是如此，只不过在任何给定时刻只有一个线程实际执行。通过称为时间切片的OS功能，在进程和线程之间共享单个核的处理时间。

对于具有多个处理器或具有多个执行核心的处理器的计算机系统来说，并发极大地增强了系统并发执行进程和线程的能力 - 但即使在没有多个处理器或执行核心的简单系统上也可以实现并发。

**进程**

进程具有自包含的执行环境。进程通常具有完整的私有基本运行时资源集：特别是，每个进程都有自己的内存空间。

进程通常被视为程序或应用程序的同义词。但是，用户看到的单个应用程序实际上可能是一组协作进程。为了促进进程之间的通信，大多数操作系统都支持进程间通信（IPC）资源，例如管道和套接字。IPC不仅用于同一系统上的进程之间的通信，而且还用于不同系统上的进程。

Java虚拟机的大多数实现都作为单个进程运行。Java应用程序可以使用`ProcessBuilder`对象创建其他进程。多进程应用程序超出了本课程的范围。

**线程**

线程有时被称为轻量级进程。进程和线程都提供执行环境，但创建新线程所需的资源比创建新进程要少。

线程存在于进程中 - 每个进程至少有一个线程。线程共享进程的资源，包括内存和打开文件。这使得有效但可能有问题的通信成为可能。

多线程执行是Java平台的基本特性。每个应用程序至少有一个线程 - 或几个，如果你算上所谓的“系统”线程，它们执行内存管理和信号处理等操作。但是从应用程序员的角度来看，你只从一个线程开始，称为主线程。该线程具有创建其他线程的能力，我们将在下一节中进行演示。

### `Thread `对象

每个线程都与`Thread`类的实例相关联。使用`Thread`对象创建并发应用程序有两种基本策略。

- 要直接控制线程创建和管理，只需在每次应用程序需要启动异步任务时实例化`Thread`。
- 要从应用程序的其余部分抽象线程管理，请将应用程序的任务传递给*执行器*。

本节介绍`Thread`对象的使用。执行器与其他 [高级并发对象](https://docs.oracle.com/javase/tutorial/essential/concurrency/highlevel.html) 共同讨论。

#### 创建和启动线程

创建`Thread`实例的应用程序必须提供将在该线程中运行的代码。有两种方法可以做到这一点：

- *提供一个Runnable对象* [`Runnable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html) 接口定义了一个单独的方法`run`， 意味着包含在线程中执行的代码。 `Runnable`对象传递给`Thread`constructor，如 [`HelloRunnable`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/HelloRunnable.java) 示例：

  ```java
  public class HelloRunnable implements Runnable {

      public void run() {
          System.out.println("Hello from a thread!");
      }

      public static void main(String args[]) {
          (new Thread(new HelloRunnable())).start();
      }

  }
  ```

- *Thread 的子类* `Thread`类本身实现`Runnable`，尽管它的`run`方法什么都不做。应用程序可以子类化`Thread`，提供自己的`run`实现，如 [`HelloRunnable`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/HelloRunnable.java) 示例。

  ```java
  public class HelloThread extends Thread {

      public void run() {
          System.out.println("Hello from a thread!");
      }

      public static void main(String args[]) {
          (new HelloThread()).start();
      }

  }
  ```

请注意，两个示例都调用`Thread.start`以启动新线程。

你应该使用哪个方法？使用`Runnable`对象是更通用的，因为`Runnable`对象可以子类化除了`Thread`之外的类。第二个习惯用法在简单的应用程序中更容易使用，但受限于你的任务类必须是`Thread`的子类。本课重点介绍第一种方法，它将`Runnable`任务与执行任务的`Thread`对象分开。这种方法不仅更灵活，而且适用于后面介绍的高级线程管理API。

`Thread`类定义了许多对线程管理有用的方法。这些包括`static`方法，它们提供有关调用方法的线程的信息或影响其状态。从管理线程和`Thread`对象所涉及的其他线程调用其他方法。我们将在以下部分中研究其中一些方法。

#### 暂停执行与睡眠

`Thread.sleep`导致当前线程暂停执行指定的时间段。这是使处理器时间可用于应用程序的其他线程或可能在计算机系统上运行的其他应用程序的有效方法。`sleep`方法也可用于调度，如下面的示例所示，并等待具有被理解为具有时间要求的职责的另一个线程，如稍后部分中的`SimpleThreads`示例。

存在两个重载版本的`sleep`：一个指定睡眠时间为毫秒，另一个指定睡眠时间为纳秒。但是，这些睡眠时间并不能保证精确，因为它们受到底层操作系统提供的基础设施的限制。此外，睡眠周期可以通过中断终止，我们将在后面的部分中看到。在任何情况下，您都不能假设调用`sleep`会在指定的时间段内暂停该线程。

 [`SleepMessages`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SleepMessages.java) 示例使用`sleep`以四秒为间隔打印消息：

```java
public class SleepMessages {
    public static void main(String args[])
        throws InterruptedException {
        String importantInfo[] = {
            "Mares eat oats",
            "Does eat oats",
            "Little lambs eat ivy",
            "A kid will eat ivy too"
        };

        for (int i = 0;
             i < importantInfo.length;
             i++) {
            //Pause for 4 seconds
            Thread.sleep(4000);
            //Print a message
            System.out.println(importantInfo[i]);
        }
    }
}
```

请注意，`main`声明它会抛出`InterruptedException`。这是一个异常，当当前线程处于`sleep`状态时，另一个线程在中断当前线程时抛出。由于此应用程序尚未定义另一个导致中断的线程，因此无需捕获`InterruptedException`。

#### 中断

*中断*是一个给线程的指示，告诉它应该停止正在做的事情并做其他事情。由程序员决定线程如何响应中断，但线程终止是很常见的。这是本课程中强调的用法。

线程通过调用`Thread`对象上的 [`interrupt`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#interrupt--) 来发送中断，以便线程被中断。为使中断机制正常工作，被中断的线程必须支持自己的中断。

**支持中断**

线程如何支持自己的中断？这取决于它目前正在做什么。如果线程经常调用抛出`InterruptedException`的方法，它只会在捕获该异常后从`run`方法返回。例如，假设`SleepMessages`示例中的核心消息循环位于线程的`Runnable`对象的`run`方法中。然后可以按如下方式修改它以支持中断：

```java
for (int i = 0; i < importantInfo.length; i++) {
    // Pause for 4 seconds
    try {
        Thread.sleep(4000);
    } catch (InterruptedException e) {
        // We've been interrupted: no more messages.
        return;
    }
    // Print a message
    System.out.println(importantInfo[i]);
}
```

许多抛出`InterruptedException`的方法（例如`sleep`）被设计为取消当前操作并在收到中断时立即返回。

如果一个线程长时间没有调用抛出`InterruptedException`的方法怎么办？它必须定期调用`Thread.interrupted`，如果收到中断，则返回`true`。 例如：

```java
for (int i = 0; i < inputs.length; i++) {
    heavyCrunch(inputs[i]);
    if (Thread.interrupted()) {
        // We've been interrupted: no more crunching.
        return;
    }
}
```

在这个简单的例子中，代码只是测试中断并退出线程（如果已收到）。在更复杂的应用程序中，抛出`InterruptedException`可能更有意义：

```java
if (Thread.interrupted()) {
    throw new InterruptedException();
}
```

这允许中断处理代码集中在`catch`子句中。

**中断状态标识**

中断机制使用称为*中断状态*的内部标志来实现。调用`Thread.interrupt`设置此标志。当线程通过调用静态方法`Thread.interrupted`来检查中断时，将清除中断状态。非静态`isInterrupted`方法，由一个线程用于查询另一个线程的中断状态，不会更改中断状态标志。

按照惯例，任何通过抛出`InterruptedException`退出的方法都会在执行此操作时清除中断状态。但是，通过另一个线程调用`interrupt`，总是可以立即再次设置中断状态。

#### `Joins`

`join`方法允许一个线程等待另一个线程的完成。如果`t`是其线程当前正在执行的`Thread`对象，

```java
t.join();
```

导致当前线程暂停执行，直到`t`的线程终止。`join`过载允许程序员指定等待时长。但是，与`sleep`一样，`join`依赖于操作系统进行计时，因此您不应该假设`join`将等待您指定的时间。

与`sleep`一样，`join`通过响应`InterruptedException`退出的方式来响应中断。

#### 线程的简单示例

以下示例汇总了本节的一些概念。`SimpleThreads`由两个线程组成。第一个是每个Java应用程序都有的主线程。主线程从`Runnable`对象`MessageLoop`创建一个新线程，并等待它完成。如果`MessageLoop`线程需要很长时间才能完成，主线程会中断它。

`MessageLoop`线程打印出一系列消息。如果在打印完所有消息之前中断，`MessageLoop`线程将打印一条消息并退出。

```java
public class SimpleThreads {

    // Display a message, preceded by
    // the name of the current thread
    static void threadMessage(String message) {
        String threadName =
            Thread.currentThread().getName();
        System.out.format("%s: %s%n",
                          threadName,
                          message);
    }

    private static class MessageLoop
        implements Runnable {
        public void run() {
            String importantInfo[] = {
                "Mares eat oats",
                "Does eat oats",
                "Little lambs eat ivy",
                "A kid will eat ivy too"
            };
            try {
                for (int i = 0;
                     i < importantInfo.length;
                     i++) {
                    // Pause for 4 seconds
                    Thread.sleep(4000);
                    // Print a message
                    threadMessage(importantInfo[i]);
                }
            } catch (InterruptedException e) {
                threadMessage("I wasn't done!");
            }
        }
    }

    public static void main(String args[])
        throws InterruptedException {

        // Delay, in milliseconds before
        // we interrupt MessageLoop
        // thread (default one hour).
        long patience = 1000 * 60 * 60;

        // If command line argument
        // present, gives patience
        // in seconds.
        if (args.length > 0) {
            try {
                patience = Long.parseLong(args[0]) * 1000;
            } catch (NumberFormatException e) {
                System.err.println("Argument must be an integer.");
                System.exit(1);
            }
        }

        threadMessage("Starting MessageLoop thread");
        long startTime = System.currentTimeMillis();
        Thread t = new Thread(new MessageLoop());
        t.start();

        threadMessage("Waiting for MessageLoop thread to finish");
        // loop until MessageLoop
        // thread exits
        while (t.isAlive()) {
            threadMessage("Still waiting...");
            // Wait maximum of 1 second
            // for MessageLoop thread
            // to finish.
            t.join(1000);
            if (((System.currentTimeMillis() - startTime) > patience)
                  && t.isAlive()) {
                threadMessage("Tired of waiting!");
                t.interrupt();
                // Shouldn't be long now
                // -- wait indefinitely
                t.join();
            }
        }
        threadMessage("Finally!");
    }
}
```

### 同步

线程主要通过共享对字段的访问和字段表示的对象引用进行通信。这种通信形式非常有效，但可能会出现两种错误：*线程干扰*和*内存一致性错误*。防止这些错误所需的工具是*同步*。

但是，同步可能会引入*线程争用*，当两个或多个线程同时尝试访问同一资源，并导致Java运行时更慢地执行一个或多个线程，甚至暂停执行时，就会发生这种情况。[饥饿和活锁](https://docs.oracle.com/javase/tutorial/essential/concurrency/starvelive.html) 是线程争用的形式。有关更多信息，请参阅 [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 部分。

本章节包含以下主题：

- [线程干扰](https://docs.oracle.com/javase/tutorial/essential/concurrency/interfere.html) 描述了当多个线程访问共享数据时错误如何产生。
- [内存一致性错误](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html) 描述由共享内存的不一致视图导致的错误。
- [同步方法](https://docs.oracle.com/javase/tutorial/essential/concurrency/syncmeth.html) 描述了一个简单的惯用方法，可以有效解决线程干扰和内存一致性错误。
- [隐式锁和同步](https://docs.oracle.com/javase/tutorial/essential/concurrency/locksync.html) 描述了更通用的同步习惯用法，并描述了基于隐式锁的同步方式。
- [原子访问](https://docs.oracle.com/javase/tutorial/essential/concurrency/atomic.html) 讨论了不会被其它线程干扰的操作的一般概念。

#### 线程干扰

考虑下面的简单的类 [`Counter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Counter.java)

```java
class Counter {
    private int c = 0;

    public void increment() {
        c++;
    }

    public void decrement() {
        c--;
    }

    public int value() {
        return c;
    }

}
```

`Counter` 的设计使得每次调用`increment` 都会将`c`加1，每次调用`decrement` 都会从`c`中减去1。但是，如果从多个线程引用`Counter`对象，则线程之间的干扰可能会阻止这种情况按预期发生。

当两个操作在不同的线程中运行但作用于相同的数据时，会发生干扰。这意味着这两个操作由多个步骤组成，并且步骤序列重叠。

对于`Counter`实例的操作似乎不可能发生交错，因为对`c`的两个操作都是单个简单的语句。但是，即使是简单的语句也可以由虚拟机转换为多个步骤。我们不会检查虚拟机采取的具体步骤 - 足以知道单个表达式`c++`可以分解为三个步骤：

1. 获取 `c`的当前值。
2. 将获取的值加1。
3. 将增加之后的值存储到变量 `c` 中。

表达式`c--`可以以相同的方式分解，除了第二步是减少而不是增量。

假设线程A在大约同一时间调用 `increment` ，线程B调用 `decrement`。如果`c`的初始值为0，则它们的交错操作可能遵循以下顺序：

1. 线程A：检索`c`。
2. 线程B：检索`c`。
3. 线程A：增加检索值；结果是1。
4. 线程B：减少检索值；结果是-1。
5. 线程A：将结果存储在`c`中；`c`现在是1。
6. 线程B：将结果存储在`c`中；`c`现在是-1。

线程A的结果丢失，被线程B覆盖。这种特殊的交错只是一种可能性。在不同情况下，可能是线程B的结果丢失，或者根本没有错误。因为它们是不可预测的，所以难以检测和修复线程干扰错误。

#### 内存一致性错误

当不同的线程具有应该是相同数据的不一致视图时，会发生内存一致性错误。内存一致性错误的原因很复杂，超出了本教程的范围。幸运的是，程序员不需要详细了解这些原因。所需要的只是避免它们的策略。

避免内存一致性错误的关键是理解 *happens-before* 关系。这种关系只是简单地保证一个特定语句的内存写入对另一个特定语句可见。要查看此内容，请考虑以下示例。假设定义并初始化了一个简单的`int`字段：

```
int counter = 0;
```

 `counter` 字段在两个线程A和B之间共享。假设线程A递增 `counter` ：

```
counter++;
```

然后，不久之后，线程B打印出 `counter`：

```
System.out.println(counter);
```

如果两个语句已在同一个线程中执行，则可以安全地假设打印出的值为“1”。但是如果这两个语句是在不同的线程中执行的，那么打印出的值可能是“0”，因为不能保证线程A对计数器的更改对于线程B是可见的 - 除非程序员已经在这两个语句之间建立了*happens-before*关系。

有几种行为可以建立*happens-before*关系。其中之一是同步，我们将在以下部分中看到。

我们已经看到了两种建立*happens-before*关系的行为。

- 当一个语句调用`Thread.start`时，与该语句具有*happens-before*关系的每个语句也与新线程执行的每个语句都有一个*happens-before*关系。 新线程可以看到导致创建新线程的代码的影响。
- 当一个线程终止并导致另一个线程中的`Thread.join`返回时，终止线程执行的所有语句与成功`join`后的所有语句都有一个*happens-before*关系。现在，执行`join`的线程可以看到线程中代码的效果。

可以创建*happens-before*关系的行为列表，参考 [ `java.util.concurrent` 包的摘要页面。](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html#MemoryVisibility)

#### 同步方法

Java编程语言提供了两种基本的同步习惯用法：*synchronized方法*和*synchronized语句*。两者中更复杂的是同步语句，将在下一章节中介绍。本节介绍同步方法。

要使方法同步，只需将`synchronized`关键字添加到其声明：

```java
public class SynchronizedCounter {
    private int c = 0;

    public synchronized void increment() {
        c++;
    }

    public synchronized void decrement() {
        c--;
    }

    public synchronized int value() {
        return c;
    }
}
```

如果`count` 是一个 `SynchronizedCounter`实例，则使得这些方法同步会有两方面影响：

- 首先，对同一对象的两个同步方法的调用不可能交错。当一个线程正在为对象执行同步方法时，所有其他线程调用同一对象的同步方法阻塞（暂停执行）直到第一个线程完成对象上的执行。
- 其次，当同步方法退出时，它会自动与同一对象的同步方法的任何后续调用建立*happens-before*关系。 这可以保证对所有线程都可以看到对象状态的更改。

请注意，构造函数无法同步 - 将`synchronized`关键字与构造函数一起使用是一种语法错误。同步构造函数没有意义，因为只有创建对象的线程在构造时才能访问它。

------

**警告：** 构造将在线程之间共享的对象时，要非常小心，保证对象的引用不会过早“泄漏”。例如，假设您要维护一个包含每个类实例的名为`instances`的`List`。您可能想要将以下行添加到构造函数中：

```java
instances.add(this);
```

但是其他线程可以在构造对象完成之前使用`instances`来访问对象。

------

同步方法启用了一种简单的策略来防止线程干扰和内存一致性错误：如果一个对象对多个线程可见，则对该对象变量的所有读取或写入都是通过同步方法完成的。（一个重要的例外：构造对象后无法修改`final`字段，一旦构造了对象，就可以通过非同步方法安全地读取）这种策略是有效的，但是可能会带来 [liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 问题，就像我们稍后将看到的那样。

#### 内在锁和同步

同步是围绕被称为*内部锁*或*监视器锁*的内部实体构建的。（API规范通常将此实体简称为“监视器”。）内部锁在同步的两个方面都发挥作用：强制对对象状态进行独占访问，并建立对可见性至关重要的*happens-before*关系。

每个对象都有一个与之关联的内在锁。按照惯例，需要对对象字段进行独占和一致访问的线程必须在访问对象之前*获取*对象的内部锁，然后在完成它们时*释放*内部锁。一个线程在获得锁定和释放锁定之间被称为*拥有*内在锁。只要一个线程拥有一个内部锁，没有其他线程可以获得相同的锁。另一个线程在尝试获取锁时将阻塞。

当线程释放内部锁时，在该操作与同一锁的任何后续*获取*之间建立*happens-before*关系。

**同步方法中的锁**

当线程调用`synchronized`方法时，它会自动获取该方法对象的内部锁，并在方法返回时释放它。即使返回是由未捕获的异常引起的，也会发生锁定释放。

您可能想知道在调用静态同步方法时会发生什么，因为静态方法与类相关联，而不是与对象相关联。在这种情况下，线程获取与该类关联的`Class`对象的内部锁。因此，对类的静态字段的访问由与该类的任何实例的锁不同的锁控制。

**同步语句**

创建同步代码的另一种方法是使用`synchronized`语句。与`synchronized`方法不同，`synchronized`语句必须指定提供内部锁的对象：

```java
public void addName(String name) {
    synchronized(this) {
        lastName = name;
        nameCount++;
    }
    nameList.add(name);
}
```

在此示例中，`addName`方法需要将更改同步到`lastName`和`nameCount`，但还需要避免同步其他对象方法的调用。（从同步代码调用其他对象的方法可能会产生在 [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 部分中描述的问题。）如果没有`synchronized`语句，则必须有一个单独的，不同步的方法，其唯一目的是调用`nameList.add`。

同步语句对于通过细粒度同步提高并发性也很有用。例如，假设类`MsLunch`有两个从不一起使用的实例字段`c1`和`c2`。必须同步这些字段的所有更新，但没有理由阻止`c1`的更新与`c2`的更新交错 - 这样做会通过创建不必要的阻塞来降低并发性。我们创建两个对象仅用于提供锁，而不是使用同步方法或以其他方式使用与`this`关联的锁。

```java
public class MsLunch {
    private long c1 = 0;
    private long c2 = 0;
    private Object lock1 = new Object();
    private Object lock2 = new Object();

    public void inc1() {
        synchronized(lock1) {
            c1++;
        }
    }

    public void inc2() {
        synchronized(lock2) {
            c2++;
        }
    }
}
```

谨慎使用此方式。您必须绝对确保对受影响字段的访问交替进行是否安全。

**可重入同步**

回想一下，线程无法获取另一个线程拥有的锁。但是一个线程可以获得它已经拥有的锁。允许线程多次获取相同的锁可启用*可重入同步*。这描述了一种情况，其中同步代码直接或间接地调用也包含同步代码的方法，并且两组代码使用相同的锁。在没有可重入同步的情况下，同步代码必须采取许多额外的预防措施，以避免线程导致自身阻塞。

#### 原子操作

在编程中，原子操作是一次有效发生的动作。原子操作不能在中间停止：它要么完全发生，要么根本不发生。在操作完成之前，原子操作的副作用是不可见的。

我们已经看到增量表达式（例如`c++`）没有描述原子操作。即使非常简单的表达式也可以定义可以分解为其他操作的复杂操作。但是，您可以指定原子操作：

- 读取和写入对于引用变量和大多数基本数据类型变量（除`long`和`double`之外的所有类型）都是原子的。
- 对于声明为`volatile`的所有变量（包括`long`和`double`变量），读取和写入都是原子的。

原子操作不能交错，因此可以使用它们而不必担心线程干扰。但是，这并不能消除所有同步原子操作的需要，因为仍然可能存在内存一致性错误。使用`volatile`变量可降低内存一致性错误的风险，因为对`volatile`变量的任何写入都会建立与之后读取同一变量的*happens-before*关系。这意味着对`volatile`变量的更改始终对其他线程可见。更重要的是，它还意味着当线程读取`volatile`变量时，它不仅会看到`volatile`的最新更改，还会看到导致更改的代码的副作用。

使用简单的原子变量访问比通过同步代码访问这些变量更有效，但程序员需要更加小心以避免内存一致性错误。额外的努力是否值得取决于应用程序的大小和复杂性。

 [`java.util.concurrent`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html)包中的某些类提供了不依赖于同步的原子方法。我们将在 [高级并发对象](https://docs.oracle.com/javase/tutorial/essential/concurrency/highlevel.html) 一节中讨论它们。

### 活性

并发应用程序及时执行的能力被称为其*活性*。本节描述了最常见的活性问题，即 [死锁](https://docs.oracle.com/javase/tutorial/essential/concurrency/deadlock.html) ，并继续简要描述其他两个活动问题，[饥饿和活锁](https://docs.oracle.com/javase/tutorial/essential/concurrency/starvelive.html) 。

#### 死锁

*死锁*描述了两个或多个线程永远被阻塞，等待彼此的情况。这是一个例子。

Alphonse 和 Gaston 是朋友，也很有礼貌的信徒。严格的礼貌规则是，当你向朋友鞠躬时，你必须保持鞠躬，直到你的朋友有机会还礼。不幸的是，这条规则没有考虑到两个朋友可能同时互相鞠躬的可能性。这个示例应用程序`Deadlock`模拟了这种可能性：

```java
public class Deadlock {
    static class Friend {
        private final String name;
        public Friend(String name) {
            this.name = name;
        }
        public String getName() {
            return this.name;
        }
        public synchronized void bow(Friend bower) {
            System.out.format("%s: %s"
                + "  has bowed to me!%n", 
                this.name, bower.getName());
            bower.bowBack(this);
        }
        public synchronized void bowBack(Friend bower) {
            System.out.format("%s: %s"
                + " has bowed back to me!%n",
                this.name, bower.getName());
        }
    }

    public static void main(String[] args) {
        final Friend alphonse =
            new Friend("Alphonse");
        final Friend gaston =
            new Friend("Gaston");
        new Thread(new Runnable() {
            public void run() { alphonse.bow(gaston); }
        }).start();
        new Thread(new Runnable() {
            public void run() { gaston.bow(alphonse); }
        }).start();
    }
}
```

当`Deadlock`运行时，两个线程在尝试调用`bowBack`时极有可能会阻塞。两个块都不会结束，因为每个线程都在等待另一个线程退出 `bow`。

#### 饥饿和活锁

与死锁相比，饥饿和活锁不是常见的问题，但仍然是并发软件的每个设计者都可能遇到的问题。

**饥饿**

*Starvation*描述了一种情况，即线程无法获得对共享资源的正常访问，并且无法继续运行。当“贪婪”线程使共享资源长时间不可用时，就会发生这种情况。例如，假设一个对象提供了一个通常需要很长时间才能返回的同步方法。如果一个线程经常调用此方法，则需要对同一对象进行频繁同步访问的其他线程就会经常被阻塞。

**活锁**

线程通常用于响应另一个线程的操作。如果另一个线程的操作也是对另一个线程的操作的响应，则可能导致活锁。与死锁一样，活锁线程无法继续运行。但是，线程没有被阻塞 - 他们只是太忙于相互回应以恢复工作。这相当于两个试图在走廊里互相通过的人：Alphonse向左移动让Gaston通过，而Gaston向右移动让Alphonse通过。看到他们仍然互相阻挡，Alphone向右移动，而Gaston向左移动。他们还在互相阻挡，所以......

### 守卫块

线程通常必须协调他们的行为。最常见的协调习语是*guarded block*。这样的块开始于在块可以继续之前轮询必须为真的条件。要正确执行此操作，需要执行许多步骤。

假设，例如`guardedJoy`是一种方法，在另一个线程设置了共享变量`joy`之前，该方法不能继续。理论上，这种方法可以简单地循环直到满足条件，但是该循环是浪费的，因为它在等待时连续执行。

```java
public void guardedJoy() {
    // Simple loop guard. Wastes
    // processor time. Don't do this!
    while(!joy) {}
    System.out.println("Joy has been achieved!");
}
```

更有效的防护是调用 [`Object.wait`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#wait--) 来挂起当前线程。在另一个线程发出可能发生某些特殊事件的通知之前，`wait`的调用不会返回 - 尽管不一定是此线程正在等待的事件：

```java
public synchronized void guardedJoy() {
    // This guard only loops once for each special event, which may not
    // be the event we're waiting for.
    while(!joy) {
        try {
            wait();
        } catch (InterruptedException e) {}
    }
    System.out.println("Joy and efficiency have been achieved!");
}
```

------

**注意：** 始终在测试等待条件的循环内调用`wait`。不要假设中断是针对您正在等待的特定条件，或者该条件仍然是真的。

------

像许多暂停执行的方法一样，`wait`会抛出`InterruptedException`。在这个例子中，我们可以忽略该异常 - 我们只关心`joy`的值。

为什么这个版本的`guardedJoy`是同步的？假设`d`是我们用来调用`wait`的对象，当一个线程调用`d.wait`时，它必须拥有`d`的内部锁 - 否则抛出错误。在`synchronized`方法中调用`wait`是获取内部锁的一种简单方法。

当调用`wait`时，线程释放锁并暂停执行。在将来的某个时间，另一个线程将获取相同的锁并调用 [`Object.notifyAll`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#notifyAll--) ，通知等待该锁的所有线程发生了重要的事情：

```java
public synchronized notifyJoy() {
    joy = true;
    notifyAll();
}
```

在第二个线程释放锁之后的一段时间，第一个线程重新获取锁并通过从 `wait` 调用返回来恢复。

------

**注意：** 有第二个通知方法`notify`，它唤醒单个线程。因为`notify`不允许您指定被唤醒的线程，所以它仅在大规模并行应用程序中有用 - 即具有大量线程的程序，所有程序都执行类似的杂务。在这样的应用程序中，您不关心哪个线程被唤醒。

------

让我们使用保护块来创建`Producer-Consumer`应用程序。这种应用程序在两个线程之间共享数据：*生成器*，创建数据，以及使用数据的*消费者*。两个线程使用共享对象进行通信。协调是必不可少的：消费者线程不得在生产者线程交付之前尝试检索数据，并且如果消费者未检索到旧数据，则生产者线程不得尝试传递新数据。

在此示例中，数据是一系列文本消息，通过 [`Drop`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Drop.java) 类型的对象共享：

```java
public class Drop {
    // Message sent from producer
    // to consumer.
    private String message;
    // True if consumer should wait
    // for producer to send message,
    // false if producer should wait for
    // consumer to retrieve message.
    private boolean empty = true;

    public synchronized String take() {
        // Wait until message is
        // available.
        while (empty) {
            try {
                wait();
            } catch (InterruptedException e) {}
        }
        // Toggle status.
        empty = true;
        // Notify producer that
        // status has changed.
        notifyAll();
        return message;
    }

    public synchronized void put(String message) {
        // Wait until message has
        // been retrieved.
        while (!empty) {
            try { 
                wait();
            } catch (InterruptedException e) {}
        }
        // Toggle status.
        empty = false;
        // Store message.
        this.message = message;
        // Notify consumer that status
        // has changed.
        notifyAll();
    }
}
```

 [`Producer`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Producer.java) 中定义的生产者线程发送一系列相似的消息。字符串“DONE”表示已发送所有消息。为了模拟真实世界应用程序的不可预测性，生产者线程在消息之间暂停随机时间间隔。

```java
import java.util.Random;

public class Producer implements Runnable {
    private Drop drop;

    public Producer(Drop drop) {
        this.drop = drop;
    }

    public void run() {
        String importantInfo[] = {
            "Mares eat oats",
            "Does eat oats",
            "Little lambs eat ivy",
            "A kid will eat ivy too"
        };
        Random random = new Random();

        for (int i = 0;
             i < importantInfo.length;
             i++) {
            drop.put(importantInfo[i]);
            try {
                Thread.sleep(random.nextInt(5000));
            } catch (InterruptedException e) {}
        }
        drop.put("DONE");
    }
}
```

在 [`Consumer`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Consumer.java) 中定义的消费者线程只是检索消息并将其打印出来，直到它检索到“DONE”字符串。该线程也会暂停随机时间间隔。

```java
import java.util.Random;

public class Consumer implements Runnable {
    private Drop drop;

    public Consumer(Drop drop) {
        this.drop = drop;
    }

    public void run() {
        Random random = new Random();
        for (String message = drop.take();
             ! message.equals("DONE");
             message = drop.take()) {
            System.out.format("MESSAGE RECEIVED: %s%n", message);
            try {
                Thread.sleep(random.nextInt(5000));
            } catch (InterruptedException e) {}
        }
    }
}
```

最后，这是在 [`ProducerConsumerExample`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/ProducerConsumerExample.java) 中定义的主线程，它启动生产者和消费者线程。

```java
public class ProducerConsumerExample {
    public static void main(String[] args) {
        Drop drop = new Drop();
        (new Thread(new Producer(drop))).start();
        (new Thread(new Consumer(drop))).start();
    }
}
```

------

**注意：** `Drop`类的编写是为了演示保护块。为避免重新发明轮子，请在尝试编写自己的数据共享对象之前检查J [Java Collections Framework](https://docs.oracle.com/javase/tutorial/collections/index.html) 中的现有数据结构。

------

### 不可变对象

如果一个对象的状态在构造后不能改变，则该对象被认为是不可变的。最大程度上依赖不可变对象被广泛接受为创建简单，可靠代码的合理策略。

不可变对象在并发应用程序中特别有用。由于它们不能改变状态，因此它们不会被线程干扰破坏或在不一致状态下被观察到。

程序员通常不愿意使用不可变对象，因为他们担心创建新对象的成本而不是更新对象。对象创建的影响经常被高估，并且可以通过与不可变对象相关联的一些效率来抵消。这些包括由于垃圾收集而减少的开销，以及消除保护可变对象免于损坏所需的代码。

以下小节采用其实例可变的类，并从中派生出具有不可变实例的类。通过这样做，它们为这种转换提供了一般规则，并展示了不可变对象的一些优点。

#### 同步类示例

[`SynchronizedRGB`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SynchronizedRGB.java) 类定义了表示颜色的对象。每个对象将颜色表示为代表主要颜色值的三个整数和一个给出颜色名称的字符串。

```java
public class SynchronizedRGB {

    // Values must be between 0 and 255.
    private int red;
    private int green;
    private int blue;
    private String name;

    private void check(int red,
                       int green,
                       int blue) {
        if (red < 0 || red > 255
            || green < 0 || green > 255
            || blue < 0 || blue > 255) {
            throw new IllegalArgumentException();
        }
    }

    public SynchronizedRGB(int red,
                           int green,
                           int blue,
                           String name) {
        check(red, green, blue);
        this.red = red;
        this.green = green;
        this.blue = blue;
        this.name = name;
    }

    public void set(int red,
                    int green,
                    int blue,
                    String name) {
        check(red, green, blue);
        synchronized (this) {
            this.red = red;
            this.green = green;
            this.blue = blue;
            this.name = name;
        }
    }

    public synchronized int getRGB() {
        return ((red << 16) | (green << 8) | blue);
    }

    public synchronized String getName() {
        return name;
    }

    public synchronized void invert() {
        red = 255 - red;
        green = 255 - green;
        blue = 255 - blue;
        name = "Inverse of " + name;
    }
}
```

必须小心使用`SynchronizedRGB`以避免在不一致的状态下被看到。例如，假设一个线程执行以下代码：

```java
SynchronizedRGB color =
    new SynchronizedRGB(0, 0, 0, "Pitch Black");
...
int myColorInt = color.getRGB();      //Statement 1
String myColorName = color.getName(); //Statement 2
```

如果另一个线程在语句1之后但在语句2之前调用`color.set`，则`myColorInt`的值将与`myColorName`的值不匹配。为了避免这种结果，必须将两个语句绑定在一起：

```java
synchronized (color) {
    int myColorInt = color.getRGB();
    String myColorName = color.getName();
} 
```

这种不一致只适用于可变对象 - 对于不可变版本的`SynchronizedRGB`而言，这不是问题。

#### 定义不可变对象的策略

以下规则定义了用于创建不可变对象的简单策略。并非所有标记为“不可变”的类都遵循这些规则。这并不一定意味着这些课程的创造者是草率的 - 他们可能有充分的理由相信他们的类实例在创建后永远不会改变。但是，这种策略需要复杂的分析，不适合初学者。

1. 不要提供“setter”方法 - 通过字段引用修改字段或对象的方法。
2. 使所有字段成为`final`和`private`的。
3. 不允许子类重写方法。最简单的方法是将类声明为`final`。 更复杂的方法是使私有构造函数并在工厂方法中构造实例。
4. 如果实例字段包含对可变对象的引用，则不允许更改这些对象：
   - 不要提供修改可变对象的方法。
   - 不要共享对可变对象的引用。永远不要存储对传递给构造函数的外部可变对象的引用。如有必要，创建副本并存储对副本的引用。同样，必要时创建内部可变对象的副本，以避免在方法中返回原始对象。

将此策略应用于`SynchronizedRGB`会导致以下步骤：

1. 本课程中有两种`setter`方法。第一个，`set`，任意转换对象，并且在类的不可变版本中没有位置。第二个，`invert`，可以通过让它创建一个新对象而不是修改现有对象来进行适配。
2. 所有字段都已`private`；他们进一步被标记为`final`的。
3. 这个类本身被宣布为`final` 的。
4. 只有一个字段引用一个对象，该对象本身是不可变的。因此，不需要防止改变“包含的”可变对象的状态的保护措施。

在这些更改之后，我们有 [`ImmutableRGB`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/ImmutableRGB.java)：

```java
final public class ImmutableRGB {

    // Values must be between 0 and 255.
    final private int red;
    final private int green;
    final private int blue;
    final private String name;

    private void check(int red,
                       int green,
                       int blue) {
        if (red < 0 || red > 255
            || green < 0 || green > 255
            || blue < 0 || blue > 255) {
            throw new IllegalArgumentException();
        }
    }

    public ImmutableRGB(int red,
                        int green,
                        int blue,
                        String name) {
        check(red, green, blue);
        this.red = red;
        this.green = green;
        this.blue = blue;
        this.name = name;
    }


    public int getRGB() {
        return ((red << 16) | (green << 8) | blue);
    }

    public String getName() {
        return name;
    }

    public ImmutableRGB invert() {
        return new ImmutableRGB(255 - red,
                       255 - green,
                       255 - blue,
                       "Inverse of " + name);
    }
}
```

### 高级并发对象

到目前为止，本课程重点关注从一开始就是Java平台一部分的低级API。这些API适用于非常基本的任务，但更高级的任务需要更高级别的构建块。对于充分利用当今多处理器和多核系统的大规模并发应用程序来说尤其如此。

在本节中，我们将介绍Java平台5.0版中引入的一些高级并发功能。大多数这些功能都在新的`java.util.concurrent`包中实现。Java Collections Framework中还有新的并发数据结构。

- [锁对象](https://docs.oracle.com/javase/tutorial/essential/concurrency/newlocks.html) 支持锁定习惯用语并简化许多并发程序。
- [执行器](https://docs.oracle.com/javase/tutorial/essential/concurrency/executors.html) 定义用于启动和管理线程的高级API。`java.util.concurrent`提供的执行器实现提供适用于大规模应用程序的线程池管理。
- [并发集合](https://docs.oracle.com/javase/tutorial/essential/concurrency/collections.html) 使管理大量数据更容易，并可以大大减少同步需求。
- [原子变量](https://docs.oracle.com/javase/tutorial/essential/concurrency/atomicvars.html) 具有最小化同步和帮助避免内存一致性错误的功能。
- [`ThreadLocalRandom`](https://docs.oracle.com/javase/tutorial/essential/concurrency/threadlocalrandom.html) (in JDK 7) 提供从多个线程有效生成伪随机数功能。

#### 锁对象

同步代码依赖于简单的可重入锁。这种锁易于使用，但有许多限制。[`java.util.concurrent.locks`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/package-summary.html) 包支持更复杂的锁定习语。我们不会详细介绍这个包，而是将重点放在其最基本的接口 [`Lock`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/Lock.html) 上。

`Lock`对象非常类似于同步代码使用的隐式锁。与隐式锁一样，一次只有一个线程可以拥有一个`Lock`对象。锁对象还通过其关联的 [`Condition`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/Condition.html) 对象支持 `wait/notify` 机制。

`Lock`对象优于隐式锁的最大优点是它们能够退出获取锁的尝试。如果锁定立即不可用或超时（如果指定），则`tryLock`方法退出。如果另一个线程在获取锁之前发送中断，则`lockInterruptibly`方法将退出。

让我们使用`Lock`对象来解决我们在 [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 中看到的死锁问题。当朋友即将鞠躬时，Alphonse 和 Gaston 已经训练自己能够注意到对方何时也会鞠躬。我们通过要求`Friend`对象必须在继续执行鞠躬之前获取两个参与者的锁来对此进行建模。以下是改进模型`Safelock`的源代码。为了证明这个习语的多样性，我们假设 Alphonse 和 Gaston 如此迷恋他们新发现的安全鞠躬能力，他们不停相互鞠躬：

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
import java.util.Random;

public class Safelock {
    static class Friend {
        private final String name;
        private final Lock lock = new ReentrantLock();

        public Friend(String name) {
            this.name = name;
        }

        public String getName() {
            return this.name;
        }

        public boolean impendingBow(Friend bower) {
            Boolean myLock = false;
            Boolean yourLock = false;
            try {
                myLock = lock.tryLock();
                yourLock = bower.lock.tryLock();
            } finally {
                if (! (myLock && yourLock)) {
                    if (myLock) {
                        lock.unlock();
                    }
                    if (yourLock) {
                        bower.lock.unlock();
                    }
                }
            }
            return myLock && yourLock;
        }
            
        public void bow(Friend bower) {
            if (impendingBow(bower)) {
                try {
                    System.out.format("%s: %s has"
                        + " bowed to me!%n", 
                        this.name, bower.getName());
                    bower.bowBack(this);
                } finally {
                    lock.unlock();
                    bower.lock.unlock();
                }
            } else {
                System.out.format("%s: %s started"
                    + " to bow to me, but saw that"
                    + " I was already bowing to"
                    + " him.%n",
                    this.name, bower.getName());
            }
        }

        public void bowBack(Friend bower) {
            System.out.format("%s: %s has" +
                " bowed back to me!%n",
                this.name, bower.getName());
        }
    }

    static class BowLoop implements Runnable {
        private Friend bower;
        private Friend bowee;

        public BowLoop(Friend bower, Friend bowee) {
            this.bower = bower;
            this.bowee = bowee;
        }
    
        public void run() {
            Random random = new Random();
            for (;;) {
                try {
                    Thread.sleep(random.nextInt(10));
                } catch (InterruptedException e) {}
                bowee.bow(bower);
            }
        }
    }
            

    public static void main(String[] args) {
        final Friend alphonse =
            new Friend("Alphonse");
        final Friend gaston =
            new Friend("Gaston");
        new Thread(new BowLoop(alphonse, gaston)).start();
        new Thread(new BowLoop(gaston, alphonse)).start();
    }
}
```

#### 执行器

在前面的所有示例中，由新的线程（由其`Runnable`对象定义）和线程本身（由`Thread`对象定义）完成的任务之间存在紧密的联系。这适用于小型应用程序，但在大型应用程序中，将线程管理和创建与应用程序的其余部分分开是有意义的。封装这些函数的对象称为执行器。以下小节详细描述了执行器。

- [执行器接口](https://docs.oracle.com/javase/tutorial/essential/concurrency/exinter.html) 定义三个执行器对象类型。
- [线程池](https://docs.oracle.com/javase/tutorial/essential/concurrency/pools.html) 是最常见的执行器实现类型。
- [Fork/Join](https://docs.oracle.com/javase/tutorial/essential/concurrency/forkjoin.html) 是一个利用多个处理器的框架（JDK 7中的新增功能）。

##### 执行器接口

`java.util.concurrent` 包定义了三个执行器接口：

- `Executor`，支持启动新任务的简单接口。
- `ExecutorService` ，`Executor` 的子接口，添加了生命周期管理的特性，管理单个任务和执行器本身。
- `ScheduledExecutorService` ，`ExecutorService` 的子接口，支持 `Futrue` 和/或任务的周期性执行。

通常，引用执行器对象的变量被声明为这三种接口类型之一，而不是执行器类类型。

**`Executor` 接口**

[`Executor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html) 接口提供单个方法`execute`，旨在成为常见线程创建习惯用语的替代方法。如果`r`是`Runnable`对象，并且`e`是`Executor`对象，则可以替换

```java
(new Thread(r)).start();
```

为

```java
e.execute(r);
```

但是， `execute` 的定义不太具体。低级习语创建一个新线程并立即启动它。根据`Executor`实现，`execute`可以执行相同的操作，但更有可能使用现有的工作线程来运行`r`，或者将`r`放在队列中以等待工作线程变为可用。（我们将在 [线程池](https://docs.oracle.com/javase/tutorial/essential/concurrency/pools.html) 部分中描述工作线程。）

`java.util.concurrent`中的执行器实现旨在充分利用更高级的`ExecutorService`和`ScheduledExecutorService`接口，尽管它们也可以与基本`Executor`接口一起使用。

**`ExecutorService` 接口**

[`ExecutorService`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html) 接口使用类似但更通用的 `submit` 方法补充 `execute` 。与`execute`一样，`submit`接受`Runnable`对象，但也接受 [`Callable`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Callable.html) 对象，这些对象允许任务返回一个值。`submit`方法返回一个`Future`对象，该对象用于检索`Callable`返回值并管理`Callable`和`Runnable`任务的状态。

`ExecutorService`还提供了提交大量`Callable`对象的方法。最后，`ExecutorService`提供了许多用于管理执行器关闭的方法。为了支持立即关闭，任务应该正确处理 [中断](https://docs.oracle.com/javase/tutorial/essential/concurrency/interrupt.html)  。

**`ScheduledExecutorService` 接口**

[`ScheduledExecutorService`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledExecutorService.html) i接口使用`schedule`补充其父`ExecutorService`的方法，该方法在指定的延迟后执行`Runnable`或`Callable`任务。此外，接口定义了`scheduleAtFixedRate`和`scheduleWithFixedDelay`，它们以定义的间隔重复执行指定的任务。

##### 线程池

`java.util.concurrent`中的大多数执行器实现都使用由工作线程组成的线程池。这种线程与它执行的`Runnable`和`Callable`任务分开存在，通常用于执行多个任务。

使用工作线程可以最大限度地减少由于线程创建而产生线程对象使用大量内存，而在大型应用程序中，分配和释放许多线程对象会产生大量的内存管理开销。

一种常见类型的线程池是固定大小线程池。这种类型的池始终具有指定数量的线程运行；如果某个线程仍在使用时以某种方式终止，它将自动替换为新线程。任务通过内部队列提交到线程池中，只要有多个活动任务而不是线程，该队列就会保存额外的任务。

固定大小线程池的一个重要优点是使用它的应用程序可以优雅地降级。要理解这一点，请考虑一个Web服务器应用程序，其中每个HTTP请求都由一个单独的线程处理。如果应用程序只是为每个新的HTTP请求创建一个新线程，并且系统接收的请求数超过它可以立即处理的数量，那么当所有这些线程的开销超过系统容量时，应用程序将突然停止响应所有请求。使用固定大小的线程池，由于可以创建的线程数量有限制，应用程序不会像请求进入时那样快速地为HTTP请求提供服务，但它将在系统可以维持的时间内尽快为它们提供服务。

创建使用固定大小线程池的执行器的一种简单方法是在 [`java.util.concurrent.Executors`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html) 中调用[`newFixedThreadPool`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newFixedThreadPool-int-) 工厂方法。此类还提供以下工厂方法：

- [`newCachedThreadPool`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newCachedThreadPool-int-) 方法使用可扩展线程池创建执行器。此执行器适用于启动许多短期任务的应用程序。
- [`newSingleThreadExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newSingleThreadExecutor-int-) 方法创建一次执行单个任务的执行器。
- 几个工厂方法是上述执行器的`ScheduledExecutorService`版本。

如果上述工厂方法提供的执行器都不满足您的需要，则构造 [`java.util.concurrent.ThreadPoolExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html) 或者 [`java.util.concurrent.ScheduledThreadPoolExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledThreadPoolExecutor.html) 的实例将为您提供其他选项。

##### Fork/Join

fork/join框架是`ExecutorService`接口的一个实现，可帮助您利用多个处理器。它专为可以递归分解成小块的工作而设计。 目标是使用所有可用的处理能力来提高应用程序的性能。

与任何`ExecutorService`实现一样，fork/join框架将任务分配给线程池中的工作线程。fork/join框架是独特的，因为它使用了 *work-stealing* 算法。用完成任务的工作线程可以从仍然忙碌的其他线程中窃取任务。

fork/join框架的中心是 [`ForkJoinPool`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinPool.html) 类，它是`AbstractExecutorService`类的扩展。`ForkJoinPool`实现了核心工作窃取算法，可以执行 [`ForkJoinTask`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinTask.html) 进程。

**基本使用**

使用fork/join框架的第一步是编写执行一部分工作的代码。您的代码应类似于以下伪代码：

```
if (my portion of the work is small enough)
  do the work directly
else
  split my work into two pieces
  invoke the two pieces and wait for the results
```

将此代码包装在`ForkJoinTask`子类中，通常使用其更专业的类型之一， [`RecursiveTask`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/RecursiveTask.html) （可以返回结果）或 [`RecursiveAction`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/RecursiveAction.html) 。

在`ForkJoinTask`子类准备就绪后，创建表示要完成的所有工作的对象，并将其传递给`ForkJoinPool`实例的`invoke()`方法。

**图片模糊示例**

为了帮助您了解fork/join框架的工作原理，请考虑以下示例。假设您想模糊图像。原始源图像由整数数组表示，其中每个整数包含单个像素的颜色值。模糊的目标图像也由与源相同大小的整数数组表示。

通过一次一个像素地处理源阵列来完成模糊。每个像素的平均周围像素（红色，绿色和蓝色分量被平均），结果放在目标数组中。由于图像是大型数组，因此此过程可能需要很长时间。通过使用fork/join框架实现算法，您可以利用多处理器系统上的并发处理。 这是一个可能的实现：

```java
public class ForkBlur extends RecursiveAction {
    private int[] mSource;
    private int mStart;
    private int mLength;
    private int[] mDestination;
  
    // Processing window size; should be odd.
    private int mBlurWidth = 15;
  
    public ForkBlur(int[] src, int start, int length, int[] dst) {
        mSource = src;
        mStart = start;
        mLength = length;
        mDestination = dst;
    }

    protected void computeDirectly() {
        int sidePixels = (mBlurWidth - 1) / 2;
        for (int index = mStart; index < mStart + mLength; index++) {
            // Calculate average.
            float rt = 0, gt = 0, bt = 0;
            for (int mi = -sidePixels; mi <= sidePixels; mi++) {
                int mindex = Math.min(Math.max(mi + index, 0),
                                    mSource.length - 1);
                int pixel = mSource[mindex];
                rt += (float)((pixel & 0x00ff0000) >> 16)
                      / mBlurWidth;
                gt += (float)((pixel & 0x0000ff00) >>  8)
                      / mBlurWidth;
                bt += (float)((pixel & 0x000000ff) >>  0)
                      / mBlurWidth;
            }
          
            // Reassemble destination pixel.
            int dpixel = (0xff000000     ) |
                   (((int)rt) << 16) |
                   (((int)gt) <<  8) |
                   (((int)bt) <<  0);
            mDestination[index] = dpixel;
        }
    }
  
  ...

```

现在，您实现了抽象的`compute()`方法，该方法可以直接执行模糊或将其拆分为两个较小的任务。简单的数组长度阈值有助于确定是执行模糊还是拆分工作。

```java
protected static int sThreshold = 100000;

protected void compute() {
    if (mLength < sThreshold) {
        computeDirectly();
        return;
    }
    
    int split = mLength / 2;
    
    invokeAll(new ForkBlur(mSource, mStart, split, mDestination),
              new ForkBlur(mSource, mStart + split, mLength - split,
                           mDestination));
}
```

如果以前的方法在`RecursiveAction`类的子类中，那么将任务设置为在`ForkJoinPool`中运行是很简单的，并涉及以下步骤：

1. 创建一个代表要完成的所有工作的任务。

   ```java
   // source image pixels are in src
   // destination image pixels are in dst
   ForkBlur fb = new ForkBlur(src, 0, src.length, dst);
   ```

2. 创建将运行任务的`ForkJoinPool`。

   ```java
   ForkJoinPool pool = new ForkJoinPool();
   ```

3. 执行任务。

   ```java
   pool.invoke(fb);
   ```

有关完整源代码（包括创建目标图像文件的一些额外代码），请参阅 [`ForkBlur`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/ForkBlur.java) 示例。

**标准实现**

除了使用fork/join框架来实现在多处理器系统上同时执行的任务的自定义算法（例如上一节中的`ForkBlur.java`示例）之外，Java SE中的一些通用的功能已经使用 fork/join框架。Java SE 8中引入的一个这样的实现由 [`java.util.Arrays`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html) 类用于其`parallelSort()`方法。这些方法类似于`sort()`，但通过fork/join框架利用并发性。 在多处理器系统上运行时，大型数组的并行排序比顺序排序更快。但是，这些方法如何利用fork/join框架超出了Java Tutorials的范围。有关此信息，请参阅Java API文档。

fork/join框架的另一个实现由`java.util.streams`包中的方法使用，该包是为Java SE 8发行版规划的 [Project Lambda](http://openjdk.java.net/projects/lambda/) 的一部分。 有关更多信息，请参阅 [Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) 部分。

#### 并发集合

`java.util.concurrent`包中包含许多Java Collections Framework的附加内容。很容易通过提供的集合接口进行分类：

- [`BlockingQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BlockingQueue.html) 定义先进先出数据结构，当您尝试添加元素到满队列或从空队列中检索时，该数据结构会阻塞或超时。
- [`ConcurrentMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentMap.html) 是`java.util.Map`的子接口，它定义了有用的原子操作。仅当键存在时，这些操作才会删除或替换键值对，或仅在键不存在时才添加键值对。这些操作原子化有助于避免同步。`ConcurrentMap`的标准通用实现是 [`ConcurrentHashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html) ，它是 [`HashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) 的并发模拟。
- [`ConcurrentNavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentNavigableMap.html) 是`ConcurrentMap`的子接口，支持近似匹配。`ConcurrentNavigableMap`的标准通用实现是 [`ConcurrentSkipListMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentSkipListMap.html) ，它是 [`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) 的并发模拟。

所有这些集合通过定义将对象添加到集合的操作与访问或删除该对象的后续操作之间的*happens-before*关系来帮助避免[内存一致性错误](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html) 。

#### 原子变量

[`java.util.concurrent.atomic`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/package-summary.html) 包定义了支持单个变量的原子操作的类。所有类都有`get`和`set`方法，类似于对`volatile`变量的读写操作。也就是说，一个`set`与相关变量的任何后续`get`具有*happens-before*关系。原子`compareAndSet`方法也具有这些内存一致性功能，适用于整数原子变量的简单原子算法也是如此。

要查看如何使用此包，让我们返回我们最初用于演示线程干扰的 [`Counter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Counter.java) 类：

```java
class Counter {
    private int c = 0;

    public void increment() {
        c++;
    }

    public void decrement() {
        c--;
    }

    public int value() {
        return c;
    }

}
```

使计数器免受线程干扰的一种方法是使其方法同步，如在 [`SynchronizedCounter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SynchronizedCounter.java) 中：

```java
class SynchronizedCounter {
    private int c = 0;

    public synchronized void increment() {
        c++;
    }

    public synchronized void decrement() {
        c--;
    }

    public synchronized int value() {
        return c;
    }

}
```

对于这个简单的类，同步是可接受的解决方案。但对于更复杂的类，我们可能希望避免不必要的同步对活动的影响。使用`AtomicInteger`替换`int`字段允许我们在不使用同步的情况下防止线程干扰，如在 [`AtomicCounter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/AtomicCounter.java) 中：

```java
import java.util.concurrent.atomic.AtomicInteger;

class AtomicCounter {
    private AtomicInteger c = new AtomicInteger(0);

    public void increment() {
        c.incrementAndGet();
    }

    public void decrement() {
        c.decrementAndGet();
    }

    public int value() {
        return c.get();
    }

}
```

#### 并发随机数

在JDK 7中，[`java.util.concurrent`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html) 包含一个类 [`ThreadLocalRandom`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadLocalRandom.html) ，用于期望使用来自多个线程或`ForkJoinTasks`的随机数的应用程序。

对于并发访问，使用`ThreadLocalRandom`而不是`Math.random()`可以减少争用，并最终提高性能。

您需要做的就是调用`ThreadLocalRandom.current()`，然后调用其中一个方法来检索随机数。 这是一个例子：

```java
int r = ThreadLocalRandom.current() .nextInt(4, 77);
```

### 扩展阅读

- *Concurrent Programming in Java: Design Principles and Pattern (2nd Edition)* by Doug Lea. A comprehensive work by a leading expert, who's also the architect of the Java platform's concurrency framework.
- *Java Concurrency in Practice* by Brian Goetz, Tim Peierls, Joshua Bloch, Joseph Bowbeer, David Holmes, and Doug Lea. A practical guide designed to be accessible to the novice.
- *Effective Java Programming Language Guide (2nd Edition)* by Joshua Bloch. Though this is a general programming guide, its chapter on threads contains essential "best practices" for concurrent programming.
- *Concurrency: State Models & Java Programs (2nd Edition)*, by Jeff Magee and Jeff Kramer. An introduction to concurrent programming through a combination of modeling and practical examples.
- *Java Concurrent Animated:* Animations that show usage of concurrency features.

## 平台环境

应用程序在平台环境中运行，该平台环境由底层操作系统，Java虚拟机，类库以及启动应用程序时提供的各种配置数据定义。本课程描述了应用程序用于检查和配置其平台环境的一些API。包括三个部分：

- [Configuration Utilities](https://docs.oracle.com/javase/tutorial/essential/environment/config.html) 描述用于访问部署应用程序时提供的配置数据的API，或者由应用程序的用户访问的API。
- [System Utilities](https://docs.oracle.com/javase/tutorial/essential/environment/system.html) 描述了`System`和`Runtime`类中定义的各种API。
- [PATH and CLASSPATH](https://docs.oracle.com/javase/tutorial/essential/environment/paths.html) 描述用于配置JDK开发工具和其他应用程序的环境变量。

### 配置工具

本节介绍一些帮助应用程序访问其启动上下文的配置实用程序。

#### 属性

*属性*是作为*键/值对*管理的配置值。在每个键值对中，键和值都是 `String` 值。键并用于检索值，就像变量名用于检索变量的值一样。例如，能够下载文件的应用程序可能使用名为“download.lastDirectory”的属性来跟踪上次下载使用的目录。

为了管理属性，可以创建 [`java.util.Properties`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html) 实例。这个类提供了如下方法：

- 从数据流中加载键值对到 `Properties` 对象中。
- 根据键检索一个值。
- 列出所有的键和它们对应的值。
- 枚举所有的键。
- 保存属性到数据流中。

有关数据流的介绍，参考 [Basic I/O](https://docs.oracle.com/javase/tutorial/essential/io/index.html) 课程中的 [I/O Streams](https://docs.oracle.com/javase/tutorial/essential/io/streams.html) 章节。

`Properties` 扩展了 [`java.util.Hashtable`](https://docs.oracle.com/javase/8/docs/api/java/util/Hashtable.html) 。从 `Hashtable` 继承来的一些方法支持如下行为：

- 检测特定的键或者值是否在 `Properties` 对象中。
- 获取当前的键值对数量。
- 删除一个键和它对应的值。
- 添加一个键值对到 `Properties` 列表中。
- 枚举所有的值或者他们的键。
- 通过键检索一个值。
- 检测 `Properties` 对象是否为空。

------

**安全注意事项：** 访问属性需要获得当前安全经理的批准。假定本节中的示例代码段位于独立应用程序中，默认情况下，它们没有安全管理器。applet 中的相同代码可能无法运行，具体取决于运行它的浏览器。有关applet安全性限制的信息，请参阅 [Java Applets](https://docs.oracle.com/javase/tutorial/deployment/applet/index.html) 课程中 [可以做什么和不能做什么](https://docs.oracle.com/javase/tutorial/deployment/applet/security.html) 。

------

`System`类维护一个`Properties`对象，该对象定义当前工作环境的配置。有关这些属性的更多信息，请参阅 [系统属性](https://docs.oracle.com/javase/tutorial/essential/environment/sysprop.html) 。 本节的其余部分介绍了如何使用属性来管理应用程序配置。

**应用生命周期中的属性**

下图说明了典型应用程序如何在执行过程中使用`Properties`对象管理其配置数据。

![Possible lifecycle of a Properties object](https://docs.oracle.com/javase/tutorial/figures/essential/environment-1loads.gif)

- `Starting Up`
  前三个框中给出的操作在应用程序启动时发生。首先，应用程序将默认属性从一个众所周知的位置加载到`Properties`对象中。通常，默认属性与应用程序的`.class`和其他资源文件一起存储在磁盘上的文件中。
  接下来，应用程序创建另一个`Properties`对象，并加载从上次运行应用程序时保存的属性。许多应用程序基于每个用户存储属性，因此在此步骤中加载的属性通常位于此应用程序在用户主目录中维护的特定目录中的特定文件中。最后，应用程序使用默认和记住的属性来初始化自身。
  这里的关键是一致性。应用程序必须始终将属性加载并保存到同一位置，以便下次执行时可以找到它们。
- `Running`
  在执行应用程序期间，用户可能会在“首选项”窗口中更改某些设置，并更新 `Properties` 对象以反映这些更改。如果要在将来的会话中记住用户更改，则必须保存它们。
- `Exiting`
  退出时，应用程序将属性保存到其已知位置，以便在下次启动应用程序时再次加载。

**设置属性对象**

以下Java代码执行上一节中描述的前两个步骤：加载默认属性并加载记住的属性：

```java
. . .
// create and load default properties
Properties defaultProps = new Properties();
FileInputStream in = new FileInputStream("defaultProperties");
defaultProps.load(in);
in.close();

// create application properties with default
Properties applicationProps = new Properties(defaultProps);

// now load properties 
// from last invocation
in = new FileInputStream("appProperties");
applicationProps.load(in);
in.close();
. . .
```

首先，应用程序设置默认的`Properties`对象。如果未在其他位置显式设置值，则此对象包含要使用的属性集。然后，load方法从名为`defaultProperties`的磁盘上的文件中读取默认值。

接下来，应用程序使用不同的构造函数来创建第二个`Properties`对象，`applicationProps`，其默认值包含在`defaultProps`中。在检索属性时，默认值开始起作用。如果在`applicationProps`中找不到该属性，则搜索其默认列表。

最后，代码从名为`appProperties`的文件中将一组属性加载到`applicationProps`中。此文件中的属性是上次调用时从应用程序保存的属性，如下一节中所述。

**保存属性**

以下示例使用`Properties.store`写出上一个示例中的应用程序属性。每次都不需要保存默认属性，因为它们永远不会更改。

```java
FileOutputStream out = new FileOutputStream("appProperties");
applicationProps.store(out, "---No Comment---");
out.close();
```

`store`方法需要一个流来写入，以及一个字符串，它在输出的头部用作注释。

**获取属性信息**

一旦应用程序设置了它的`Properties`对象，就可以查询对象以获取有关它包含的各种键和值的信息。应用程序在启动后从`Properties`对象获取信息，以便它可以根据用户做出的选择进行初始化。`Properties`类有几种获取属性信息的方法：

- `contains(Object value)` 和 `containsKey(Object key)`
  如果值或键在`Properties`对象中，则返回`true`。`Properties`从`Hashtable`继承了这些方法。因此，它们接受`Object`参数，但只应使用`String`值。
- `getProperty(String key)` 和 `getProperty(String key, String default)`
  返回指定属性的值。第二个版本提供默认值。如果未找到键，则返回默认值。
- `list(PrintStream s)` 和 `list(PrintWriter w)`
  将所有属性写入指定的流或编写器。这对调试很有用。
- `elements()`, `keys()`, 和 `propertyNames()`
  返回一个`Enumeration`，它包含`Properties`对象中包含的键或值（由方法名称表示）。`keys`方法只返回对象本身的键；`propertyNames`方法也返回默认属性的键。
- `stringPropertyNames()`
  与`propertyNames`类似，但返回一个`Set<String>`，并且只返回其中键和值都是字符串的属性名称。请注意，`Set`对象不支持`Properties`对象，因此一个对象的更改不会影响另一个。
- `size()`
  返回当前键/值对的数量。

**设置属性**

用户在执行期间与应用程序的交互可能会影响属性设置。这些更改应该反映在`Properties`对象中，以便在应用程序退出时保存它们（并调用`store`方法）。以下方法更改`Properties`对象中的属性：

- `setProperty(String key, String value)`
  将键/值对放在`Properties`对象中。
- `remove(Object key)`
  删除与键关联的键/值对。

------

**注意：** 上面描述的一些方法在`Hashtable`中定义，因此接受除`String`以外的键和值参数类型。始终使用`String`表示键和值，即使该方法允许其他类型。也不要在`Properties`对象上调用`Hashtable.set`或`Hastable.setAll`；总是使用`Properties.setProperty`。

------

#### 命令行参数

Java应用程序可以从命令行接受任意数量的参数。这允许用户在启动应用程序时指定配置信息。

用户在调用应用程序时输入命令行参数，并在要运行的类的名称后指定它们。例如，假设一个名为`Sort`的Java应用程序对文件中的行进行排序。要对名为`friends.txt`的文件中的数据进行排序，用户将输入：

```
java Sort friends.txt
```

启动应用程序时，运行时系统通过`String`数组将命令行参数传递给应用程序的`main`方法。在前面的示例中，命令行参数传递给包含单个`String`：`“friends.txt”`的数组给`Sort`程序。

**回显命令行参数**

[`Echo`](https://docs.oracle.com/javase/tutorial/essential/environment/examples/Echo.java) 示例将命令行参数打印到控制台：

```java
public class Echo {
    public static void main (String[] args) {
        for (String s: args) {
            System.out.println(s);
        }
    }
}
```

以下示例显示用户如何运行`Echo`。用户输入以斜体显示。

```
java Echo Drink Hot Java
Drink
Hot
Java
```

请注意，应用程序单独显示每个单词 - `Drink`，`Hot`和`Java`。这是因为空格字符分隔了命令行参数。要将`Drink`，`Hot`和`Java`解释为单个参数，用户可以通过将它们括在引号内来加入它们。

```
java Echo "Drink Hot Java"
Drink Hot Java
```

**转化数字命令行参数**

如果应用程序需要支持数字命令行参数，则它必须将表示数字的`String`参数（例如“34”）转换为数字值。这是一个将命令行参数转换为`int`的代码片段：

```java
int firstArg;
if (args.length > 0) {
    try {
        firstArg = Integer.parseInt(args[0]);
    } catch (NumberFormatException e) {
        System.err.println("Argument" + args[0] + " must be an integer.");
        System.exit(1);
    }
}
```

如果`args[0]`的格式无效，`parseInt`会抛出`NumberFormatException`。所有的`Number`类 - `Integer`，`Float`，`Double`等等 - 都有`parseXXX`方法，它们将表示数字的`String`转换为它们类型的对象。

#### 其他配置工具

以下是一些其他配置实用程序的摘要。

*Preferences API*允许应用程序在依赖于实现的后备存储中存储和检索配置数据。支持异步更新，并且多个线程甚至多个应用程序可以安全地更新同一组首选项。有关更多信息，请参阅  [Preferences API Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/preferences/index.html) 。

部署在*JAR*包中的应用程序使用清单来描述存档的内容。有关更多信息，请参阅 [Packaging Programs in JAR Files](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html) 课程。

*Java Web Start应用程序*的配置包含在*JNLP*文件中。有关更多信息，请参阅 [Java Web Start](https://docs.oracle.com/javase/tutorial/deployment/webstart/index.html) 课程。

*Java Plug-in applet*的配置部分取决于用于在网页中嵌入applet的HTML标记。这些标记可以包含 `<applet>`, `<object>`, `<embed>`, 和 `<param>`，具体取决于applet和浏览器。有关更多信息，请参阅 [Java Applets](https://docs.oracle.com/javase/tutorial/deployment/applet/index.html) 课程。

 [`java.util.ServiceLoader`](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html) 类提供了一个简单的服务提供者工具。服务提供者是服务的实现 - 一组众所周知的接口和（通常是抽象的）类。服务提供者中的类通常实现接口并子类化服务中定义的类。可以将服务提供程序安装为扩展（请参阅 [The Extension Mechanism](https://docs.oracle.com/javase/tutorial/ext/index.html) ）。通过将提供者添加到类路径或通过其他特定于平台的方式，也可以使提供者可用。

### 系统工具

 [`System`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html) 类实现了许多系统实用程序。其中一些已在上一节 [Configuration Utilities](https://docs.oracle.com/javase/tutorial/essential/environment/config.html) 中介绍过。本节介绍一些其他系统实用程序。

#### 命令行 I/O 对象

`System` 提供了几个预定义的I/O对象，这些对象在Java应用程序中非常有用，可以从命令行启动。它们实现了大多数操作系统提供的标准I/O流，以及用于输入密码的控制台对象。有关更多信息，请参阅 [Basic I/O](https://docs.oracle.com/javase/tutorial/essential/io/index.html) 课程中 [I/O from the Command Line](https://docs.oracle.com/javase/tutorial/essential/io/cl.html) 。

#### 系统属性

在 [Properties](https://docs.oracle.com/javase/tutorial/essential/environment/properties.html) 中，我们检查了应用程序可以使用`Properties`对象来维护其配置的方式。Java平台本身使用`Properties`对象来维护自己的配置。`System`类维护一个`Properties`对象，该对象描述当前工作环境的配置。系统属性包括有关当前用户，Java运行时的当前版本以及用于分隔文件路径名的组件的字符的信息。

下表描述了一些最重要的系统属性。

| Key                 | Meaning                                  |
| ------------------- | ---------------------------------------- |
| `"file.separator"`  | Character that separates components of a file path. This is "`/`" on UNIX and "`\`" on Windows. |
| `"java.class.path"` | Path used to find directories and JAR archives containing class files. Elements of the class path are separated by a platform-specific character specified in the `path.separator` property. |
| `"java.home"`       | Installation directory for Java Runtime Environment (JRE) |
| `"java.vendor"`     | JRE vendor name                          |
| `"java.vendor.url"` | JRE vendor URL                           |
| `"java.version"`    | JRE version number                       |
| `"line.separator"`  | Sequence used by operating system to separate lines in text files |
| `"os.arch"`         | Operating system architecture            |
| `"os.name"`         | Operating system name                    |
| `"os.version"`      | Operating system version                 |
| `"path.separator"`  | Path separator character used in `java.class.path` |
| `"user.dir"`        | User working directory                   |
| `"user.home"`       | User home directory                      |
| `"user.name"`       | User account name                        |

------

**安全性考虑：**  [Security Manager](https://docs.oracle.com/javase/tutorial/essential/environment/security.html) 可以限制对系统属性的访问。这通常是applet中的一个问题，它无法读取某些系统属性，也无法编写任何系统属性。有关在applet中访问系统属性的更多信息，请参阅 [Doing More With Java Rich Internet Applications](https://docs.oracle.com/javase/tutorial/deployment/doingMoreWithRIA/index.html) 课程中的 [System Properties](https://docs.oracle.com/javase/tutorial/deployment/doingMoreWithRIA/properties.html) 。

------

**读取系统属性**

`System`类有两个用于读取系统属性的方法：`getProperty`和`getProperties`。

`System`类有两个不同版本的`getProperty`。两者都检索参数列表中指定的属性的值。两个`getProperty`方法中较简单的方法是一个参数，一个属性键。例如，要获取`path.separator`的值，请使用以下语句：

```java
System.getProperty("path.separator");
```

`getProperty`方法返回一个包含该属性值的字符串。如果该属性不存在，则此版本的`getProperty`返回`null`。

另一个版本的`getProperty`需要两个`String`参数：第一个参数是要查找的键，第二个参数是如果找不到键或者没有值则返回的默认值。例如，以下对`getProperty`的调用会查找名为`subliminal.message`的`System`属性。这不是一个有效的系统属性，因此这个方法不是返回`null`，而是返回作为第二个参数提供的默认值：“`Buy StayPuft Marshmallows！`”

```java
System.getProperty("subliminal.message", "Buy StayPuft Marshmallows!");
```

`System`类提供的访问属性值的最后一个方法是`getProperties`方法，它返回一个 [`Properties`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html) 对象。该对象包含一组完整的系统属性定义。

**写入系统属性**

要修改现有的系统属性集，请使用`System.setProperties`。此方法采用已初始化为包含要设置的属性的`Properties`对象。此方法使用`Properties`对象表示的新集合替换整个系统属性集。

------

**警告：** 更改系统属性具有潜在危险，应谨慎处理。启动后不会重读许多系统属性，这些属性仅供参考。更改某些属性可能会产生意外的副作用。

------

下一个例子，[`PropertiesTest`](https://docs.oracle.com/javase/tutorial/essential/environment/examples/PropertiesTest.java)，创建一个 `Properties` 对象并从 [`myProperties.txt`](https://docs.oracle.com/javase/tutorial/essential/environment/examples/myProperties.txt) 初始化它。

```java
subliminal.message=Buy StayPuft Marshmallows!
```

`PropertiesTest` 接下来使用 `System.setProperties` 来安装新的 `Properties` 对象作为当前系统属性集合。

```java
import java.io.FileInputStream;
import java.util.Properties;

public class PropertiesTest {
    public static void main(String[] args)
        throws Exception {

        // set up new properties object
        // from file "myProperties.txt"
        FileInputStream propFile =
            new FileInputStream( "myProperties.txt");
        Properties p =
            new Properties(System.getProperties());
        p.load(propFile);

        // set the system properties
        System.setProperties(p);
        // display new properties
        System.getProperties().list(System.out);
    }
}
```

注意`PropertiesTest`如何创建`Properties`对象，`p`，它被用作`setProperties`的参数：

```java
Properties p = new Properties(System.getProperties());
```

此语句使用当前系统属性集初始化新属性对象`p`，在这个小应用程序的情况下，它是由运行时系统初始化的属性集。然后，应用程序从文件`myProperties.txt`将其他属性加载到`p`中，并将系统属性设置为`p`。这具有将`myProperties.txt`中列出的属性添加到运行时系统在启动时创建的属性集的效果。请注意，应用程序可以创建`p`而不使用任何默认的`Properties`对象，如下所示：

```java
Properties p = new Properties();
```

另请注意，系统属性的值可以被覆盖！例如，如果`myProperties.txt`包含以下行，则将覆盖`java.vendor`系统属性：

```java
java.vendor=Acme Software Company
```

通常，请注意不要覆盖系统属性。

`setProperties`方法更改当前正在运行的应用程序的系统属性集。这些变化并不持久。也就是说，更改应用程序中的系统属性不会影响将来对此解释程序或任何其他应用程序的Java解释程序的调用。运行时系统每次启动时都会重新初始化系统属性。如果要保持对系统属性的更改，则应用程序必须在退出之前将值写入某个文件，并在启动时再次读取它们。

#### 安全管理器

*安全管理器*是定义应用程序安全策略的对象。此策略指定不安全或敏感的操作。安全策略不允许的任何操作都会导致抛出 [`SecurityException`](https://docs.oracle.com/javase/8/docs/api/java/lang/SecurityException.html) 。应用程序还可以查询其安全管理器以发现允许的操作。

通常，Web applet与浏览器或Java Web Start插件提供的安全管理器一起运行。其他类型的应用程序通常在没有安全管理器的情况下运行，除非应用程序本身定义一个。否则 如果没有安全管理器，则该应用程序没有安全策略，其运行没有任何限制。

本节介绍应用程序如何与现有安全管理器进行交互。有关更多详细信息，包括有关如何设计安全管理器的信息，请参阅 [Security Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/index.html) 。

**与安全管理器交互**

安全管理器是 [`SecurityManager`](https://docs.oracle.com/javase/8/docs/api/java/lang/SecurityManager.html) 类型的对象；要获取对此对象的引用，请调用`System.getSecurityManager`。

```java
SecurityManager appsm = System.getSecurityManager();
```

如果没有安全管理器，则此方法返回`null`。

一旦应用程序具有对安全管理器对象的引用，它就可以请求执行特定事务的权限。标准库中的许多类都是这样做的。例如，以退出状态终止Java虚拟机的`System.exit`调用`SecurityManager.checkExit`以确保当前线程具有关闭应用程序的权限。

`SecurityManager`类定义了许多用于验证其他类型操作的其他方法。例如，`SecurityManager.checkAccess`验证线程访问，`SecurityManager.checkPropertyAccess`验证对指定属性的访问。每个操作或一组操作都有自己的 `check*XXX*()` 方法。

此外， `check*XXX*()` 方法的集合表示已经受到安全管理器保护的操作集。通常，应用程序不必直接调用任何 `check*XXX*()` 方法。

**识别安全违规**

在没有安全管理器的情况下，许多常规操作在使用安全管理器运行时都会抛出`SecurityException`。即使在调用未记录为抛出`SecurityException`的方法时也是如此。例如，请考虑以下用于读取文件的代码：

```java
reader = new FileReader("xanadu.txt");
```

在缺少安全管理器的情况下，如果`xanadu.txt`存在且可读，则此语句无错误地执行。但是假设此语句插入到Web applet中，该applet通常在不允许文件输入的安全管理器下运行。可能会导致以下错误消息：

```shell
appletviewer fileApplet.html
Exception in thread "AWT-EventQueue-1" java.security.AccessControlException: access denied (java.io.FilePermission characteroutput.txt write)
        at java.security.AccessControlContext.checkPermission(AccessControlContext.java:323)
        at java.security.AccessController.checkPermission(AccessController.java:546)
        at java.lang.SecurityManager.checkPermission(SecurityManager.java:532)
        at java.lang.SecurityManager.checkWrite(SecurityManager.java:962)
        at java.io.FileOutputStream.<init>(FileOutputStream.java:169)
        at java.io.FileOutputStream.<init>(FileOutputStream.java:70)
        at java.io.FileWriter.<init>(FileWriter.java:46)
...
```

请注意，在这种情况下抛出的特定异常 [`java.security.AccessControlException`](https://docs.oracle.com/javase/8/docs/api/java/security/AccessControlException.html) 是`SecurityException`的子类。

#### 系统中的其它方法

本节介绍了前面几节中未介绍的`System`中的一些方法。

`arrayCopy`方法有效地在数组之间复制数据。有关更多信息，请参阅 [Language Basics](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/index.html) 课程中的 [Arrays](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html) 。

 [`currentTimeMillis`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#currentTimeMillis--) 和 [`nanoTime`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#nanoTime--) 方法可用于测量应用程序执行期间的时间间隔。要以毫秒为单位测量时间间隔，请在间隔的开始和结束时调用`currentTimeMillis`两次，并减去从第二次调用返回的第一个值。同样，调用`nanoTime`两次测量纳秒单位的时间间隔。

------

**注意：** `currentTimeMillis`和`nanoTime`的准确性受操作系统提供的时间服务的限制。不要假设`currentTimeMillis`精确到最接近的毫秒，或者`nanoTime`精确到最接近的纳秒。此外，`currentTimeMillis`和`nanoTime`都不应用于确定当前时间。使用高级方法，例如 [`java.util.Calendar.getInstance`](https://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html#getInstance--) 。

------

 [`exit`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#exit-int-) 方法使Java虚拟机关闭，并使用参数指定的整数退出状态码。退出状态码可用于启动应用程序的进程。按照惯例，退出状态码为`0`表示应用程序正常终止，而任何其他值都是错误代码。

### PATH 和 CLASSPATH

本节介绍如何在Microsoft Windows，Solaris和Linux上使用`PATH`和`CLASSPATH`环境变量。有关最新信息，请参阅安装Java Development Kit（JDK）软件包中随附的安装说明。

安装软件后，JDK目录将具有如下所示的结构。

![JDK directory structure](https://docs.oracle.com/javase/tutorial/figures/essential/environment-directories.gif)

`bin`目录包含编译器和启动器。

**更新 PATH 环境变量 (Microsoft Windows)**

您可以在不设置`PATH`环境变量的情况下正常运行Java应用程序。或者为了方便，您可以选择设置该变量值。

如果希望能够从任何目录方便地运行可执行文件（`javac.exe`，`java.exe`，`javadoc.exe`等）而无需键入命令的完整路径，请设置`PATH`环境变量。如果未设置`PATH`变量，则需要在每次运行时指定可执行文件的完整路径，例如：

```
C:\Java\jdk1.7.0\bin\javac MyClass.java
```

`PATH`环境变量是由分号`;`分隔的一系列目录。Microsoft Windows从左到右依次查找`PATH`目录中的程序。一次只能在路径中为JDK创建一个`bin`目录（第一个后面的那些目录被忽略），因此如果已存在一个，则可以更新该特定条目。

以下是`PATH`环境变量的示例：

```
C:\Java\jdk1.7.0\bin;C:\Windows\System32\;C:\Windows\;C:\Windows\System32\Wbem
```

永久设置`PATH`环境变量非常有用，因为在重新启动后它将保持不变。要永久更改`PATH`变量，请使用“控制面板”中的“系统”图标。具体过程因Windows版本而异：

Windows XP

1. 选择开始，选择控制面板。双击“系统”，然后选择“高级”选项卡。
2. 单击“环境变量”。在“系统变量”中，找到`PATH`环境变量并选择它。单击编辑。如果`PATH`环境变量不存在，请单击“新建”。
3. 在“编辑系统变量”（或“新建系统变量”）窗口中，指定`PATH`环境变量的值。单击确定。单击“确定”关闭所有剩余窗口。

Windows Vista:

1. 在桌面上，右键单击“我的电脑”图标。
2. 从上下文菜单中选择“属性”。
3. 单击“高级”选项卡（Vista中的“高级系统设置”链接）。
4. 单击“环境变量”。在“系统变量”中，找到`PATH`环境变量并选择它。单击编辑。如果`PATH`环境变量不存在，请单击“新建”。
5. 在“编辑系统变量”（或“新建系统变量”）窗口中，指定PATH环境变量的值。单击确定。单击“确定”关闭所有剩余窗口。

Windows 7:

1. 在桌面上，右键单击“计算机”图标。
2. 从上下文菜单中选择“属性”。
3. 单击“高级系统设置”链接。
4. 单击“环境变量”。在“系统变量”中，找到`PATH`环境变量并选择它。单击编辑。如果`PATH`环境变量不存在，请单击“新建”。
5. 在“编辑系统变量”（或“新建系统变量”）窗口中，指定`PATH`环境变量的值。单击确定。单击“确定”关闭所有剩余窗口。

------

**注意：** 从控制面板编辑时，您可能会看到与以下内容类似的`PATH`环境变量：

```
%JAVA_HOME%\bin;%SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem
```

以百分号`％`括起来的变量是现有的环境变量。如果其中一个变量在“控制面板”的“环境变量”窗口中列出（例如 `JAVA_HOME`），则可以编辑其值。如果没有出现，那么它是操作系统定义的特殊环境变量。例如，`SystemRoot`是Microsoft Windows系统文件夹的位置。要获取环境变量的值，请在命令提示符处输入以下内容。（此示例获取`SystemRoot`环境变量的值）：

```
echo％SystemRoot％
```

------

**更新 PATH 变量(Solaris and Linux)**

您可以在不设置`PATH`变量的情况下运行JDK，也可以为了方便选择设置它。但是，如果希望能够从任何目录运行可执行文件（`javac`，`java`，`javadoc`等）而不必键入命令的完整路径，则应设置路径变量。如果未设置`PATH`变量，则需要在每次运行时指定可执行文件的完整路径，例如：

```
% /usr/local/jdk1.7.0/bin/javac MyClass.java
```

要确定`path`是否正确设置，请执行：

```
% java -version
```

这将打印java工具的版本，如果它可以找到它。如果版本较旧或者您收到错误 **java：Command not found** ，则说明 `path` 未正确设置。

要永久设置 `path` ，请在启动文件中设置路径。

对 C shell (`csh`)，编辑启动文件 `(~/.cshrc`)：

```
set path=(/usr/local/jdk1.7.0/bin $path)
```

对 `bash`，编辑启动文件 (`~/.bashrc`)：

```
PATH=/usr/local/jdk1.7.0/bin:$PATH
export PATH
```

对 `ksh` ，启动文件由环境变量命名，`ENV`，为了设置 `path` ：

```
PATH=/usr/local/jdk1.7.0/bin:$PATH
export PATH
```

对 `sh`，编辑配置文件 (`~/.profile`)：

```
PATH=/usr/local/jdk1.7.0/bin:$PATH
export PATH
```

然后加载启动文件并通过重复调用`java`命令验证路径是否已设置：

对 C shell (`csh`)：

```
% source ~/.cshrc
% java -version
```

对 `ksh`, `bash`, 或者 `sh` ：

```
% . /.profile
% java -version
```

**检查 CLASSPATH 变量（所有平台）**

`CLASSPATH`变量是告诉应用程序（包括JDK工具）查找用户类的一种方法。（属于JRE，JDK平台和扩展的类应该通过其他方式定义，例如引导类路径或扩展目录。）

指定类路径的首选方法是使用`-cp`命令行开关。这允许为每个应用程序单独设置`CLASSPATH`，而不会影响其他应用程序。设置`CLASSPATH`可能很棘手，应谨慎执行。

类路径的默认值为“.”，表示仅搜索当前目录。指定`CLASSPATH`变量或`-cp`命令行开关会覆盖此值。

要检查是否在Microsoft Windows NT/2000/XP上设置`CLASSPATH`，请执行以下命令：

```
C:> echo %CLASSPATH%
```

在 Solaris 或者 Linux 上，执行：

```
% echo $CLASSPATH
```

如果 `CLASSPATH` 没有设置，你将得到一个 **CLASSPATH: Undefined variable** 错误 (Solaris 或者 Linux) 或者是简单的 **%CLASSPATH%** (Microsoft Windows NT/2000/XP)。

要修改`CLASSPATH`，请使用与`PATH`变量相同的过程。

类路径通配符允许您在类路径中包含`.jar`文件的整个目录，而无需单独指定它们。有关更多信息（包括类路径通配符的说明）以及有关如何清理CLASSPATH环境变量的详细说明，请参阅 [Setting the Class Path](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/classpath.html) 技术说明。

## 正则表达式

本课程介绍如何使用`java.util.regex` API与正则表达式进行模式匹配。虽然此包接受的语法类似于 [Perl](http://www.perl.com/) 编程语言，但 Perl 的知识不是先决条件。本课程从基础知识开始，逐步构建以涵盖更高级的技术。

- [介绍](https://docs.oracle.com/javase/tutorial/essential/regex/intro.html)

  提供正则表达式的一般概述。它还介绍了构成此API的核心类。

- [测试套件](https://docs.oracle.com/javase/tutorial/essential/regex/test_harness.html)

  定义用于测试与正则表达式匹配的模式的简单应用程序。

- [字符串字面值](https://docs.oracle.com/javase/tutorial/essential/regex/literals.html)

  介绍基本模式匹配，元字符和引用。

- [Character 类](https://docs.oracle.com/javase/tutorial/essential/regex/char_classes.html)

  描述简单的字符类，否定，范围，联合，交叉和减法。

- [预定义 Character 类](https://docs.oracle.com/javase/tutorial/essential/regex/pre_char_classes.html)

  描述空白，字和数字字符等基本预定义字符类。

- [Quantifiers](https://docs.oracle.com/javase/tutorial/essential/regex/quant.html)

  解释贪婪，不情愿和占有量词用于匹配指定表达式`x`次。

- [Capturing Groups](https://docs.oracle.com/javase/tutorial/essential/regex/groups.html)

  说明如何将多个字符视为一个单元。

- [Boundary Matchers](https://docs.oracle.com/javase/tutorial/essential/regex/bounds.html)

  描述线，字和输入边界。

- [Pattern 类方法](https://docs.oracle.com/javase/tutorial/essential/regex/pattern.html)

  检查`Pattern`类的其他有用方法，并探索高级功能，例如使用标志进行编译和使用嵌入式标志表达式。

- [Matcher 类方法](https://docs.oracle.com/javase/tutorial/essential/regex/matcher.html)

  描述了`Matcher`类的常用方法。

- [PatternSyntaxException 类方法](https://docs.oracle.com/javase/tutorial/essential/regex/pse.html) 

  描述如何检查`PatternSyntaxException`。

- [附加资源](https://docs.oracle.com/javase/tutorial/essential/regex/resources.html)

  要阅读有关正则表达式的更多信息，请参阅本节以获取其他资源


### 介绍

**啥是正则表达式？**

*正则表达式*是一种基于集合中每个字符串共享的共同特征来描述一组字符串的方法。它们可用于搜索，编辑或操作文本和数据。 您必须学习特定的语法来创建正则表达式 - 这超出了Java编程语言的常规语法。正则表达式的复杂程度各不相同，但是一旦理解了它们的构造基础，您就能够解密（或创建）任何正则表达式。

本教程讲解 [`java.util.regex`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/package-summary.html) API支持的正则表达式语法，并提供了几个示例来说明各种对象如何交互。在正则表达式的世界中，有许多不同的风格可供选择，例如grep，Perl，Tcl，Python，PHP和awk。`java.util.regex` API中的正则表达式语法与Perl中的类似。

**如何在此包中表示正则表达式？**

`java.util.regex`包主要由三个类组成： [`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) ， [`Matcher`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html) ，和 [`PatternSyntaxException`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html) 。

- `Pattern`对象是正则表达式的编译表示。`Pattern`类不提供公共构造函数。要创建模式，必须首先调用 `public static compile` 方法之一，然后返回`Pattern`对象。这些方法接受正则表达式作为第一个参数；本教程的前几课将教你所需的语法。
- `Matcher`对象是解释模式并对输入字符串执行匹配操作的引擎。与`Pattern`类一样，`Matcher`也没有定义公共构造函数。通过在`Pattern`对象上调用`matcher`方法获取`Matcher`对象。
- `PatternSyntaxException`对象是未经检查的异常，表示正则表达式模式中的语法错误。

教程的最后几章详细介绍了这几个类。但首先，您必须了解实际构造正则表达式的方式。因此，下一节将介绍一个简单的测试工具，将重复使用它来探索其语法。

### 测试套件

本节定义了一个可重用的测试工具 [`RegexTestHarness.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/RegexTestHarness.java) ，用于探索此API支持的正则表达式构造。运行此代码的命令是`java RegexTestHarness` ， 不接受命令行参数。应用程序重复循环，提示用户输入正则表达式和输入字符串。使用此测试工具是可选的，但您可能会发现浏览以下页面中讨论的测试用例很方便。

```java
import java.io.Console;
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class RegexTestHarness {

    public static void main(String[] args){
        Console console = System.console();
        if (console == null) {
            System.err.println("No console.");
            System.exit(1);
        }
        while (true) {

            Pattern pattern = 
            Pattern.compile(console.readLine("%nEnter your regex: "));

            Matcher matcher = 
            pattern.matcher(console.readLine("Enter input string to search: "));

            boolean found = false;
            while (matcher.find()) {
                console.format("I found the text" +
                    " \"%s\" starting at " +
                    "index %d and ending at index %d.%n",
                    matcher.group(),
                    matcher.start(),
                    matcher.end());
                found = true;
            }
            if(!found){
                console.format("No match found.%n");
            }
        }
    }
}
```

在继续下一节之前，请保存并编译此代码，以确保您的开发环境支持所需的包。

### 字符串字面值

此API支持的最基本的模式匹配形式是字符串字面值的匹配。例如，如果正则表达式为`foo`且输入字符串为`foo`，则匹配将成功，因为字符串是相同的。尝试使用测试工具：

```
Enter your regex: foo
Enter input string to search: foo
I found the text foo starting at index 0 and ending at index 3.
```

匹配成功。请注意，虽然输入字符串长度为3个字符，但起始索引为0，结束索引为3。照惯例，范围包括起始索引而排除结束索引，如下图所示：

![The string literal foo, with numbered cells and index values.](https://docs.oracle.com/javase/tutorial/figures/essential/cells.gif)

字符串文字`foo`，带有单元格编号和索引值。

字符串中的每个字符都驻留在自己的单元格中，位置索引指向每个单元格。字符串“foo”从索引0开始，到索引3结束，即使字符本身只占用单元格0,1和2。

随后的匹配，你会发现一些重叠; 下一个匹配的起始索引与上一个匹配的结束索引相同：

```
Enter your regex: foo
Enter input string to search: foofoofoo
I found the text foo starting at index 0 and ending at index 3.
I found the text foo starting at index 3 and ending at index 6.
I found the text foo starting at index 6 and ending at index 9.
```

**元字符**

此API还支持许多影响模式匹配方式的特殊字符。将正则表达式更改为`cat`，输入字符串改为`cats`。输出如下：

```
Enter your regex: cat.
Enter input string to search: cats
I found the text cats starting at index 0 and ending at index 4.
```

即使输入字符串中不存在点“.”，匹配仍然成功。成功是因为点是元字符 - 由匹配器解释的具有特殊含义的字符。元字符“.” 表示“任何字符”，这就是本例中匹配成功的原因。

此 API 支持的元字符为：`<([{\^-=$!|]})?*+.>` 。

------

**注意：** 在某些情况下，上面列出的特殊字符不会被视为元字符。当您了解有关如何构造正则表达式的更多信息时，您将遇到此问题。但是，您可以使用此列表检查特定字符是否会被视为元字符。例如，字符`@`和`＃`从不带有特殊含义。

------

有两种方法可以强制将元字符视为普通字符：

- 在元字符前面加一个反斜杠，或者
- 将其放在 `\Q`（开始）和 `\E`（结束）内。

使用此技术时，`\Q`和`\E`可以放在表达式中的任何位置，前提是`\Q`首先出现。

### 字符类

如果浏览 [`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) 类规范，您将看到总结支持的正则表达式构造的表。在“字符类”部分中，您将找到以下内容：

| Construct       | Description                              |
| --------------- | ---------------------------------------- |
| `[abc]`         | a, b, or c (simple class)                |
| `[^abc]`        | Any character except a, b, or c (negation) |
| `[a-zA-Z]`      | a through z, or A through Z, inclusive (range) |
| `[a-d[m-p]]`    | a through d, or m through p: [a-dm-p] (union) |
| `[a-z&&[def]]`  | d, e, or f (intersection)                |
| `[a-z&&[^bc]]`  | a through z, except for b and c: [ad-z] (subtraction) |
| `[a-z&&[^m-p]]` | a through z, and not m through p: [a-lq-z] (subtraction) |

左侧列指定正则表达式构造，而右侧列描述每个构造将匹配的条件。

------

**注意：** 短语“character class”中的“class”一词不是指`.class`文件。在正则表达式的上下文中，*字符类*是括在方括号内的一组字符。它指定将成功匹配给定输入字符串中的单个字符的字符。

------

**简单类**

字符类的最基本形式是简单地将一组字符并排放在方括号内。例如，正则表达式`[bcr]at`将匹配单词“bat”，“cat”或“rat”，因为它定义了一个字符类（接受“b”，“c”或“r”）作为其第一个字符。

```
Enter your regex: [bcr]at
Enter input string to search: bat
I found the text "bat" starting at index 0 and ending at index 3.

Enter your regex: [bcr]at
Enter input string to search: cat
I found the text "cat" starting at index 0 and ending at index 3.

Enter your regex: [bcr]at
Enter input string to search: rat
I found the text "rat" starting at index 0 and ending at index 3.

Enter your regex: [bcr]at
Enter input string to search: hat
No match found.
```

在上面的示例中，只有当第一个字母与字符类定义的字符之一匹配时，整体匹配才会成功。

**Negation**

要匹配除列出的字符以外的所有字符，请在字符类的开头插入“`^`”元字符。这种技术称为*否定*。

```
Enter your regex: [^bcr]at
Enter input string to search: bat
No match found.

Enter your regex: [^bcr]at
Enter input string to search: cat
No match found.

Enter your regex: [^bcr]at
Enter input string to search: rat
No match found.

Enter your regex: [^bcr]at
Enter input string to search: hat
I found the text "hat" starting at index 0 and ending at index 3.
```

仅当输入字符串的第一个字符不包含字符类定义的任何字符时，匹配才会成功。

**Ranges**

有时您需要定义一个包含一系列值的字符类，例如字母“a到h”或数字“1到5”。要指定范围，只需在要匹配的第一个和最后一个字符之间插入“ - ”元字符，例如`[1-5]`或`[a-h]`。您还可以在类中将不同的范围放在彼此旁边，以进一步扩展匹配的可能性。例如，`[a-zA-Z]`将匹配字母表中的任何字母：a到z（小写）或A到Z（大写）。

以下是范围和否定的一些示例：

```
Enter your regex: [a-c]
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: [a-c]
Enter input string to search: b
I found the text "b" starting at index 0 and ending at index 1.

Enter your regex: [a-c]
Enter input string to search: c
I found the text "c" starting at index 0 and ending at index 1.

Enter your regex: [a-c]
Enter input string to search: d
No match found.

Enter your regex: foo[1-5]
Enter input string to search: foo1
I found the text "foo1" starting at index 0 and ending at index 4.

Enter your regex: foo[1-5]
Enter input string to search: foo5
I found the text "foo5" starting at index 0 and ending at index 4.

Enter your regex: foo[1-5]
Enter input string to search: foo6
No match found.

Enter your regex: foo[^1-5]
Enter input string to search: foo1
No match found.

Enter your regex: foo[^1-5]
Enter input string to search: foo6
I found the text "foo6" starting at index 0 and ending at index 4.
```

**Unions**

您还可以使用联合创建由两个或多个单独的字符类组成的单个字符类。要创建联合，只需将一个类嵌套在另一个类中，例如`[0-4 [6-8]]`。此特定联合创建一个与数字0,1,2,3,4,6,7和8匹配的单个字符类。

```
Enter your regex: [0-4[6-8]]
Enter input string to search: 0
I found the text "0" starting at index 0 and ending at index 1.

Enter your regex: [0-4[6-8]]
Enter input string to search: 5
No match found.

Enter your regex: [0-4[6-8]]
Enter input string to search: 6
I found the text "6" starting at index 0 and ending at index 1.

Enter your regex: [0-4[6-8]]
Enter input string to search: 8
I found the text "8" starting at index 0 and ending at index 1.

Enter your regex: [0-4[6-8]]
Enter input string to search: 9
No match found.
```

**Intersections**

要创建仅匹配其所有嵌套类共有的字符的单个字符类，请使用`&&`，如`[0-9&&[345]]`中所示。此特定交集创建单个字符类，仅匹配两个字符类共有的数字：3,4和5。

```
Enter your regex: [0-9&&[345]]
Enter input string to search: 3
I found the text "3" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[345]]
Enter input string to search: 4
I found the text "4" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[345]]
Enter input string to search: 5
I found the text "5" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[345]]
Enter input string to search: 2
No match found.

Enter your regex: [0-9&&[345]]
Enter input string to search: 6
No match found.
```

这是一个显示两个范围交集的示例：

```
Enter your regex: [2-8&&[4-6]]
Enter input string to search: 3
No match found.

Enter your regex: [2-8&&[4-6]]
Enter input string to search: 4
I found the text "4" starting at index 0 and ending at index 1.

Enter your regex: [2-8&&[4-6]]
Enter input string to search: 5
I found the text "5" starting at index 0 and ending at index 1.

Enter your regex: [2-8&&[4-6]]
Enter input string to search: 6
I found the text "6" starting at index 0 and ending at index 1.

Enter your regex: [2-8&&[4-6]]
Enter input string to search: 7
No match found.
```

**Subtraction**

最后，您可以使用减法来否定一个或多个嵌套字符类，例如`[0-9&&[^345]]`。此示例创建一个匹配0到9之间的所有字符类，但数字3,4和5除外。

```
Enter your regex: [0-9&&[^345]]
Enter input string to search: 2
I found the text "2" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 3
No match found.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 4
No match found.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 5
No match found.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 6
I found the text "6" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 9
I found the text "9" starting at index 0 and ending at index 1.
```

现在我们已经介绍了如何创建字符类，您可能需要在继续下一部分之前查看 [Character Classes table](https://docs.oracle.com/javase/tutorial/essential/regex/char_classes.html#CHART) 。

### 预定义字符类

[`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) API 包含若干有用的*预定义字符类*，它们提供了使用正则表达式的简便方法：

| Construct | Description                              |
| --------- | ---------------------------------------- |
| `.`       | Any character (may or may not match line terminators) |
| `\d`      | A digit: `[0-9]`                         |
| `\D`      | A non-digit: `[^0-9]`                    |
| `\s`      | A whitespace character: `[ \t\n\x0B\f\r]` |
| `\S`      | A non-whitespace character: `[^\s]`      |
| `\w`      | A word character: `[a-zA-Z_0-9]`         |
| `\W`      | A non-word character: `[^\w]`            |

在上表中，左侧列中的每个构造都是右侧列中字符类的简写。例如，`\d`表示数字范围（0-9），`\w`表示单词字符（任何小写字母，任何大写字母，下划线字符或任何数字）。尽可能使用预定义的类。它们使您的代码更易于阅读，并消除格式错误的字符类引入的错误。

以反斜杠开头的构造称为转义构造。我们在 [String Literals](https://docs.oracle.com/javase/tutorial/essential/regex/literals.html) 部分中预览了转义结构，其中我们提到使用反斜杠和`\Q`和`\E`作为引用。如果在字符串字面量中使用转义构造，则必须在反斜杠前面加上另一个反斜杠，以便编译字符串。 例如：

```
private final String REGEX = "\\d"; // a single digit
```

在这个例子中`\d`是正则表达式；编译代码需要额外的反斜杠。测试工具直接从控制台读取表达式，因此不需要额外的反斜杠。

以下示例演示了预定义字符类的使用。

```
Enter your regex: .
Enter input string to search: @
I found the text "@" starting at index 0 and ending at index 1.

Enter your regex: . 
Enter input string to search: 1
I found the text "1" starting at index 0 and ending at index 1.

Enter your regex: .
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: \d
Enter input string to search: 1
I found the text "1" starting at index 0 and ending at index 1.

Enter your regex: \d
Enter input string to search: a
No match found.

Enter your regex: \D
Enter input string to search: 1
No match found.

Enter your regex: \D
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: \s
Enter input string to search:  
I found the text " " starting at index 0 and ending at index 1.

Enter your regex: \s
Enter input string to search: a
No match found.

Enter your regex: \S
Enter input string to search:  
No match found.

Enter your regex: \S
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: \w
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: \w
Enter input string to search: !
No match found.

Enter your regex: \W
Enter input string to search: a
No match found.

Enter your regex: \W
Enter input string to search: !
I found the text "!" starting at index 0 and ending at index 1.

```

在前三个例子中，正则表达式很简单。（“点”元字符）表示“任何字符”。因此，在所有三种情况下（随机选择的`@`字符，数字和字母）匹配成功。其余示例均使用 [Predefined Character Classes table](https://docs.oracle.com/javase/tutorial/essential/regex/pre_char_classes.html#CHART) 表中的单个正则表达式构造。您可以参考此表来确定每个匹配背后的逻辑：

- `\d` 匹配所有数字
- `\s` 匹配空格
- `\w` 匹配单词字符

或者，大写字母意思相反：

- `\D` 匹配非数字
- `\S` 匹配非空格
- `\W` 匹配非单词字符

### Quantifiers

*量词*允许您指定要匹配的出现次数。为方便起见，下面介绍了描述贪婪，不情愿和占有量词的Pattern API规范的三个部分。乍一看，似乎量词`X?`，`X??` 和`X?+`完全相同，因为它们都承诺匹配“X，一次或根本不匹配”。有一些细微的实现差异，将在本节末尾解释。

| Greedy   | Reluctant | Possessive | Meaning                                  |
| -------- | --------- | ---------- | ---------------------------------------- |
| `X?`     | `X??`     | `X?+`      | `X`, once or not at all                  |
| `X*`     | `X*?`     | `X*+`      | `X`, zero or more times                  |
| `X+`     | `X+?`     | `X++`      | `X`, one or more times                   |
| `X{n}`   | `X{n}?`   | `X{n}+`    | `X`, exactly *n* times                   |
| `X{n,}`  | `X{n,}?`  | `X{n,}+`   | `X`, at least *n* times                  |
| `X{n,m}` | `X{n,m}?` | `X{n,m}+`  | `X`, at least *n* but not more than *m* times |

让我们通过创建三个不同的正则表达式来开始我们对贪婪量词的看法：字母“a”后跟`?`，`*`或`+`。让我们看看当这些表达式针对空输入字符串`“”`进行测试时会发生什么：

```
Enter your regex: a?
Enter input string to search: 
I found the text "" starting at index 0 and ending at index 0.

Enter your regex: a*
Enter input string to search: 
I found the text "" starting at index 0 and ending at index 0.

Enter your regex: a+
Enter input string to search: 
No match found.
```

**0-长度匹配**

在上面的例子中，匹配在前两种情况下是成功的，因为表达式`a?`和`a*`都允许字母a出现零次。您还会注意到开始和结束索引都是零，这与我们到目前为止看到的任何示例都不同。空输入字符串`“”`没有长度，因此测试只是匹配索引0处的任何内容。此类匹配称为零长度匹配。在以下几种情况下可能发生零长度匹配：在空输入字符串中，在输入字符串的开头，在输入字符串的最后一个字符之后，或在输入字符串的任意两个字符之间。零长度匹配很容易识别，因为它们始终在相同的索引位置开始和结束。

让我们通过几个例子来探索零长度匹配。将输入字符串更改为单个字母“a”，您会注意到一些有趣的内容：

```
Enter your regex: a?
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.
I found the text "" starting at index 1 and ending at index 1.

Enter your regex: a*
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.
I found the text "" starting at index 1 and ending at index 1.

Enter your regex: a+
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.
```

所有三个量词都找到了字母“a”，但前两个也在索引1处找到了零长度匹配；也就是说，在输入字符串的最后一个字符之后。请记住，匹配器将字符“a”视为位于索引0和索引1之间的单元格中，并且我们的测试工具循环直到它无法再找到匹配项。根据所使用的量词，最后一个字符后索引处“无”的存在可能触发也可能不触发匹配。

现在将输入字符串更改为连续五个字母“a”，您将获得以下内容：

```
Enter your regex: a?
Enter input string to search: aaaaa
I found the text "a" starting at index 0 and ending at index 1.
I found the text "a" starting at index 1 and ending at index 2.
I found the text "a" starting at index 2 and ending at index 3.
I found the text "a" starting at index 3 and ending at index 4.
I found the text "a" starting at index 4 and ending at index 5.
I found the text "" starting at index 5 and ending at index 5.

Enter your regex: a*
Enter input string to search: aaaaa
I found the text "aaaaa" starting at index 0 and ending at index 5.
I found the text "" starting at index 5 and ending at index 5.

Enter your regex: a+
Enter input string to search: aaaaa
I found the text "aaaaa" starting at index 0 and ending at index 5.
```

表达式`a?` 找到每个字符的单独匹配，因为它匹配“a”出现零或一次。表达式`a*`找到两个单独的匹配：第一个匹配中的所有字母“a”，然后是索引5处的最后一个字符后的零长度匹配。最后，`a+`匹配所有出现的字母“a” ，忽略最后一个索引处“无”的存在。

此时，如果前两个量词遇到“a”以外的字母，您可能想知道结果会是什么。例如，如果遇到字母“b”会发生什么，如“ababaaaab”？

我们来看看：

```
Enter your regex: a?
Enter input string to search: ababaaaab
I found the text "a" starting at index 0 and ending at index 1.
I found the text "" starting at index 1 and ending at index 1.
I found the text "a" starting at index 2 and ending at index 3.
I found the text "" starting at index 3 and ending at index 3.
I found the text "a" starting at index 4 and ending at index 5.
I found the text "a" starting at index 5 and ending at index 6.
I found the text "a" starting at index 6 and ending at index 7.
I found the text "a" starting at index 7 and ending at index 8.
I found the text "" starting at index 8 and ending at index 8.
I found the text "" starting at index 9 and ending at index 9.

Enter your regex: a*
Enter input string to search: ababaaaab
I found the text "a" starting at index 0 and ending at index 1.
I found the text "" starting at index 1 and ending at index 1.
I found the text "a" starting at index 2 and ending at index 3.
I found the text "" starting at index 3 and ending at index 3.
I found the text "aaaa" starting at index 4 and ending at index 8.
I found the text "" starting at index 8 and ending at index 8.
I found the text "" starting at index 9 and ending at index 9.

Enter your regex: a+
Enter input string to search: ababaaaab
I found the text "a" starting at index 0 and ending at index 1.
I found the text "a" starting at index 2 and ending at index 3.
I found the text "aaaa" starting at index 4 and ending at index 8.
```

即使字母“b”出现在单元格1,3和8中，输出也会在这些位置报告零长度匹配。正则表达式`a?`不是专门寻找字母“b”；它只是在寻找字母“a”的存在（或缺少）。如果量词允许匹配“a”零次，则输入字符串中不是“a”的任何内容都将显示为零长度匹配。根据前面示例中讨论的规则匹配剩余的"a"。

要准确匹配模式n次，只需在大括号内指定一组数字：

```
Enter your regex: a{3}
Enter input string to search: aa
No match found.

Enter your regex: a{3}
Enter input string to search: aaa
I found the text "aaa" starting at index 0 and ending at index 3.

Enter your regex: a{3}
Enter input string to search: aaaa
I found the text "aaa" starting at index 0 and ending at index 3.
```

这里，正则表达式`a{3}`正在搜索连续三次出现的字母“a”。第一个测试失败，因为输入字符串没有足够的匹配。第二个测试在输入字符串中包含3个a，它会触发匹配。第三个测试也触发匹配，因为在输入字符串的开头恰好有3个a。接下来的任何事情都与第一次匹配无关。如果该模式应该在该位置之后再次出现，则会触发后续匹配：

```
Enter your regex: a{3}
Enter input string to search: aaaaaaaaa
I found the text "aaa" starting at index 0 and ending at index 3.
I found the text "aaa" starting at index 3 and ending at index 6.
I found the text "aaa" starting at index 6 and ending at index 9.
```

要求模式至少出现n次，请在数字后面添加逗号：

```
Enter your regex: a{3,}
Enter input string to search: aaaaaaaaa
I found the text "aaaaaaaaa" starting at index 0 and ending at index 9.
```

使用相同的输入字符串，此测试只找到一个匹配项，因为连续的9个a满足“至少”3个a的需要。

最后，要指定出现次数的上限，请在大括号内添加第二个数字：

```
Enter your regex: a{3,6} // find at least 3 (but no more than 6) a's in a row
Enter input string to search: aaaaaaaaa
I found the text "aaaaaa" starting at index 0 and ending at index 6.
I found the text "aaa" starting at index 6 and ending at index 9.
```

这里第一次匹配被迫停在6个字符的上限。第二次匹配包括遗留的任何内容，恰好是三个a  - 这次匹配允许的最小字符数。如果输入字符串是一个较短的字符，则不会有第二个匹配，因为只剩下两个a。

**捕获组和字符类与量词**

到目前为止，我们只对包含一个字符的输入字符串测试了量词。实际上，量词只能一次附加到一个字符，因此正则表达式“abc+”表示“a，后跟b，后跟c一次或多次”。这并不意味着“abc”一次或多次。但是，量词也可以附加到字符类和捕获组，例如`[abc]+`（a或b或c，一次或多次）或`(abc)+`（组“abc”，一次或多次）。

让我们通过连续三次指定组`(dog)`来说明。

```
Enter your regex: (dog){3}
Enter input string to search: dogdogdogdogdogdog
I found the text "dogdogdog" starting at index 0 and ending at index 9.
I found the text "dogdogdog" starting at index 9 and ending at index 18.

Enter your regex: dog{3}
Enter input string to search: dogdogdogdogdogdog
No match found.
```

这里第一个例子找到三个匹配，因为量词适用于整个捕获组。但是，删除括号并且匹配失败，因为量词`{3}`现在仅适用于字母“g”。

同样，我们可以将量词应用于整个字符类：

```
Enter your regex: [abc]{3}
Enter input string to search: abccabaaaccbbbc
I found the text "abc" starting at index 0 and ending at index 3.
I found the text "cab" starting at index 3 and ending at index 6.
I found the text "aaa" starting at index 6 and ending at index 9.
I found the text "ccb" starting at index 9 and ending at index 12.
I found the text "bbc" starting at index 12 and ending at index 15.

Enter your regex: abc{3}
Enter input string to search: abccabaaaccbbbc
No match found.
```

这里量词`{3}`适用于第一个例子中的整个字符类，但仅适用于第二个中的字母“c”。

**贪婪、不情愿和占有量词之间的不同**

贪婪，不情愿和占有量词之间存在细微差别。

贪心量词被认为是“贪婪的”，因为它们在尝试第一次匹配之前强制匹配器读入或吃掉整个输入字符串。如果第一次匹配尝试（整个输入字符串）失败，匹配器将输入字符串后退一个字符并再次尝试，重复该过程直到找到匹配项或者没有剩余字符可以退出。根据表达式中使用的量词，它将尝试匹配的最后一件事是1或0个字符。

然而，不情愿的量词采用相反的方法：它们从输入字符串的开头开始，然后不情愿地一次吃一个字符寻找匹配。他们尝试的最后一件事是整个输入字符串。

最后，占有量词总是占用整个输入字符串，尝试一次（并且只有一次）匹配。与贪婪的量词不同，占有量词永远不会退缩，即使这样做也会使整体匹配成功。

为了说明，请考虑输入字符串`xfooxxxxxxfoo`。

```
Enter your regex: .*foo  // greedy quantifier
Enter input string to search: xfooxxxxxxfoo
I found the text "xfooxxxxxxfoo" starting at index 0 and ending at index 13.

Enter your regex: .*?foo  // reluctant quantifier
Enter input string to search: xfooxxxxxxfoo
I found the text "xfoo" starting at index 0 and ending at index 4.
I found the text "xxxxxxfoo" starting at index 4 and ending at index 13.

Enter your regex: .*+foo // possessive quantifier
Enter input string to search: xfooxxxxxxfoo
No match found.
```

第一个例子使用贪心量词`.*`来找到“任何字符”，零次或多次，然后是字母`“f” “o” “o”`。因为量词是贪婪的，所以表达式的`.*`部分首先会占用整个输入字符串。此时，整体表达式匹配不能成功，因为已经消耗了最后三个字母（`“f” “o” “o”`）。因此，匹配器一次缓慢地退回一个字母，直到最右边的“foo”被反刍到，此时匹配成功并且搜索结束。

然而，第二个例子是不情愿的，所以它首先消耗“没有”。因为“foo”没有出现在字符串的开头，所以它被强制吞下第一个字母（“x”），这会在0和4处触发第一个匹配。我们的测试工具继续前进直到输入字符串耗尽。它在4和13找到另一次匹配。

第三个例子找不到匹配，因为量词是占有性的。在这种情况下，整个输入字符串由`.*+`消耗，不留下任何东西以满足表达式末尾的“foo”。使用占有量词来表示你想要抓住所有东西而不会退缩的情况；在没有立即找到匹配的情况下，它将胜过等效的贪心量词。

### 捕获组

在上一节中，我们看到了量词如何附加到一个字符，字符类或捕获组。但到目前为止，我们还没有详细讨论过捕获组的概念。

捕获组是将多个字符视为一个单元的一种方法。它们是通过将要分组的字符放在一组括号中来创建的。例如，正则表达式`(dog)`创建一个包含字母“d”“o”和“g”的组。与捕获组匹配的输入字符串部分将保存在内存中，以便以后通过反向引用进行调用（如下面的 [反向引用](https://docs.oracle.com/javase/tutorial/essential/regex/groups.html#backref) 一节中所述）。

**编号**

如 [`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)  API中所述，捕获组通过从左到右计算它们的左括号来编号。例如，在表达式 `((A)(B(C)))`中，有四个这样的组：

1. `((A)(B(C)))`
2. `(A)`
3. `(B(C))`
4. `(C)`

要查找表达式中存在多少个组，请在匹配器对象上调用`groupCount`方法。`groupCount`方法返回一个`int`，显示匹配器模式中存在的捕获组数。在此示例中，`groupCount`将返回数字`4`，表示该模式包含4个捕获组。

还有一个特殊组，即组0，它始终代表整个表达式。该组未包含在`groupCount`报告的总数中。以 `(?`开头的组是纯粹的非捕获组，不捕获文本而不计入组总数。（稍后将在 [Methods of the Pattern Class](https://docs.oracle.com/javase/tutorial/essential/regex/pattern.html) 部分中看到非捕获组的示例。）

了解组的编号很重要，因为一些`Matcher`方法接受一个`int`，指定一个特定的组号作为参数：

- [`public int start(int group)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#start-int-): 返回在上一个匹配操作期间由给定组捕获的子序列的起始索引。
- [`public int end (int group)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#end-int-): 返回在上一个匹配操作期间由给定组捕获的子序列的最后一个字符的索引加1。
- [`public String group (int group)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#group-int-): 返回在上一个匹配操作期间由给定组捕获的输入子序列。

**反向引用**

与捕获组匹配的输入字符串部分保存在内存中，以便以后通过反向引用进行调用。在正则表达式中将反向引用指定为反斜杠（`\`），后跟一个数字，指示要调用的组的编号。例如，表达式（`\d\d`）定义了一个匹配行中两个数字的捕获组，可以通过反向引用`\1`在表达式中稍后调用。

要匹配任何2位数字，后跟完全相同的两位数字，您可以使用`(\d\d)\1`作为正则表达式：

```
Enter your regex: (\d\d)\1
Enter input string to search: 1212
I found the text "1212" starting at index 0 and ending at index 4.
```

如果更改最后两位数，则匹配将失败：

```
Enter your regex: (\d\d)\1
Enter input string to search: 1234
No match found.
```

对于嵌套捕获组，反向引用的工作方式完全相同：指定反斜杠后跟要调用的组的编号。

### 边界匹配

到目前为止，我们只关心在特定输入字符串中的某个位置是否找到匹配项。我们从不关心匹配发生在输入字符串的哪个位置。

通过使用边界匹配器指定此类信息，可以使模式匹配更精确。例如，您可能对查找特定单词感兴趣，但前提是它出现在行的开头或结尾。或者您可能想知道匹配是在单词边界上还是在上一次匹配结束时发生。

下表列出并解释了所有边界匹配器。

| Boundary Construct | Description                              |
| ------------------ | ---------------------------------------- |
| `^`                | The beginning of a line                  |
| `$`                | The end of a line                        |
| `\b`               | A word boundary                          |
| `\B`               | A non-word boundary                      |
| `\A`               | The beginning of the input               |
| `\G`               | The end of the previous match            |
| `\Z`               | The end of the input but for the final terminator, if any |
| `\z`               | The end of the input                     |

以下示例演示了边界匹配器`^`和`$`的使用。如上所述，`^`匹配行的开头，`$`匹配结束。

```
Enter your regex: ^dog$
Enter input string to search: dog
I found the text "dog" starting at index 0 and ending at index 3.

Enter your regex: ^dog$
Enter input string to search:       dog
No match found.

Enter your regex: \s*dog$
Enter input string to search:             dog
I found the text "            dog" starting at index 0 and ending at index 15.

Enter your regex: ^dog\w*
Enter input string to search: dogblahblah
I found the text "dogblahblah" starting at index 0 and ending at index 11.
```

第一个示例是成功的，因为模式占用整个输入字符串。第二个示例失败，因为输入字符串在开头包含额外的空格。第三个示例指定一个表达式，该表达式允许无限制的空格，后面是行尾的“dog”。第四个例子要求“dog”出现在一行的开头，后跟无限数量的单词字符。

要检查模式是否在单词边界上开始和结束（与较长字符串中的子字符串相对），可在任一侧使用`\b`；例如，`\bdog\b` 。

```
Enter your regex: \bdog\b
Enter input string to search: The dog plays in the yard.
I found the text "dog" starting at index 4 and ending at index 7.

Enter your regex: \bdog\b
Enter input string to search: The doggie plays in the yard.
No match found.
```

要匹配非单词边界上的表达式，请使用`\B`代替：

```
Enter your regex: \bdog\B
Enter input string to search: The dog plays in the yard.
No match found.

Enter your regex: \bdog\B
Enter input string to search: The doggie plays in the yard.
I found the text "dog" starting at index 4 and ending at index 7.
```

要求匹配仅在上一个匹配结束时发生，请使用`\G`：

```
Enter your regex: dog 
Enter input string to search: dog dog
I found the text "dog" starting at index 0 and ending at index 3.
I found the text "dog" starting at index 4 and ending at index 7.

Enter your regex: \Gdog 
Enter input string to search: dog dog
I found the text "dog" starting at index 0 and ending at index 3.
```

这里第二个例子只找到一个匹配，因为第二次出现的“dog”不会在上一个匹配结束时开始。

### Pattern 类的方法

到目前为止，我们只使用测试工具以最基本的形式创建`Pattern`对象。本节探讨高级技术，例如使用标志创建模式和使用嵌入式标志表达式。它还探讨了我们尚未讨论的一些其他有用的方法。

**使用标志创建 Pattern**

`Pattern`类定义了一个备用 `compile` 方法，它接受一组影响模式匹配方式的标志。 `flags`参数是一个位掩码，可能包含以下任何公共静态字段：

- [`Pattern.CANON_EQ`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#CANON_EQ) 启用规范等效。指定此标志时，当且仅当它们的完整规范分解匹配时，才认为两个字符匹配。例如，当指定此标志时，表达式 `"a\u030A"`将匹配字符串 `"\u00E5"` 。默认情况下，匹配不会将规范等效考虑在内。 指定此标志可能会导致性能下降。
- [`Pattern.CASE_INSENSITIVE`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#CASE_INSENSITIVE) 启用不区分大小写的匹配。默认情况下，不区分大小写的匹配假定只匹配 US-ASCII 字符集中的字符。通过将 UNICODE_CASE 标志与此标志一起指定，可以启用 Unicode 感知的不区分大小写的匹配。也可以通过嵌入式标志表达式 `(?i)` 启用不区分大小写的匹配。指定此标志可能会略微降低性能。
- [`Pattern.COMMENTS`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#COMMENTS) 允许模式中的空格和注释。在此模式下，将忽略空格，并忽略以`＃`开头的嵌入式注释，直到行结束。也可以通过嵌入式标志表达式 `(?x)` 启用注释模式。
- [`Pattern.DOTALL`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#DOTALL) 启用 dotall 模式。在 dotall 模式中，表达式`.`匹配任何字符，包括行终止符。默认情况下，此表达式与行终止符不匹配。也可以通过嵌入式标志表达式`(?s)`启用 dotall 模式。（s是“单行”模式的助记符，这是在Perl中的叫法。）
- [`Pattern.LITERAL`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#LITERAL) 启用模式的文字解析。指定此标志后，指定模式的输入字符串将被视为文字字符序列。输入序列中的元字符或转义序列将没有特殊含义。当与此标志一起使用时，标志`CASE_INSENSITIVE`和`UNICODE_CASE`保持对匹配的影响。其他标志变得多余。没有用于启用文字解析的嵌入标志字符。
- [`Pattern.MULTILINE`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#MULTILINE) 启用多行模式。 在多行模式中，表达式`^`和`$`分别在行终止符之后或输入序列的末尾之前匹配。默认情况下，这些表达式仅在整个输入序列的开头和结尾处匹配。也可以通过嵌入式标志表达式 `(?m)` 启用多行模式。
- [`Pattern.UNICODE_CASE`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#UNICODE_CASE) 启用支持 Unicode 的大小写折叠。指定此标志后，由`CASE_INSENSITIVE`标志启用时，不区分大小写的匹配将以与 Unicode 标准一致的方式完成。默认情况下，不区分大小写的匹配假定只匹配 US-ASCII 字符集中的字符。也可以通过嵌入式标志表达式 `(?u)` 启用支持 Unicode 的大小写折叠。指定此标志可能会导致性能下降。
- [`Pattern.UNIX_LINES`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#UNIX_LINES) 启用 UNIX 行模式。在此模式下，只有'\n'行终止符在`.`，`^`和`$`的行为中被识别。UNIX 行模式也可以通过嵌入式标志表达式 `(?d)` 启用。

在以下步骤中，我们将修改测试工具[`RegexTestHarness.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/RegexTestHarness.java) 以创建具有不区分大小写匹配的模式。

首先，修改代码以调用`compile`的备用版本：

```
Pattern pattern = 
Pattern.compile(console.readLine("%nEnter your regex: "),
Pattern.CASE_INSENSITIVE);
```

然后编译并运行测试工具以获得以下结果：

```
Enter your regex: dog
Enter input string to search: DoGDOg
I found the text "DoG" starting at index 0 and ending at index 3.
I found the text "DOg" starting at index 3 and ending at index 6.
```

正如您所看到的，字符串文字“dog”匹配两种情况，无论是否大小写。要编译具有多个标志的模式，请使用按位 OR 运算符“`|`”分隔要包含的标志。为清楚起见，以下代码示例对正则表达式进行硬编码，而不是从控制台中读取它：

```
pattern = Pattern.compile("[az]$", Pattern.MULTILINE | Pattern.UNIX_LINES);
```

您也可以指定一个`int`变量：

```
final int flags = Pattern.CASE_INSENSITIVE | Pattern.UNICODE_CASE;
Pattern pattern = Pattern.compile("aa", flags);
```

**内嵌标志表达式**

也可以使用*嵌入的标志表达式*启用各种标志。嵌入式标志表达式是`compile`方法的双参数版本的替代，并且在正则表达式本身中指定。以下示例使用原始测试工具 [`RegexTestHarness.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/RegexTestHarness.java) 和嵌入式标志表达式 `(?i)` 来启用不区分大小写的匹配。

```
Enter your regex: (?i)foo
Enter input string to search: FOOfooFoOfoO
I found the text "FOO" starting at index 0 and ending at index 3.
I found the text "foo" starting at index 3 and ending at index 6.
I found the text "FoO" starting at index 6 and ending at index 9.
I found the text "foO" starting at index 9 and ending at index 12.
```

无论大小写，所有匹配再次成功。

与`Pattern`的可公开访问字段对应的嵌入式标志表达式如下表所示：

| Constant                   | Equivalent Embedded Flag Expression |
| -------------------------- | ----------------------------------- |
| `Pattern.CANON_EQ`         | None                                |
| `Pattern.CASE_INSENSITIVE` | `(?i)`                              |
| `Pattern.COMMENTS`         | `(?x)`                              |
| `Pattern.MULTILINE`        | `(?m)`                              |
| `Pattern.DOTALL`           | `(?s)`                              |
| `Pattern.LITERAL`          | None                                |
| `Pattern.UNICODE_CASE`     | `(?u)`                              |
| `Pattern.UNIX_LINES`       | `(?d)`                              |

**使用`matches(String,CharSequence) `方法**

`Pattern`类定义了一个方便的 [`matches`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#matches-java.lang.String-java.lang.CharSequence-) 方法，允许您快速检查给定输入字符串中是否存在模式。与所有公共静态方法一样，您应该通过其类名调用 `matches` ，例如`Pattern.matches("\\d","1");` 。在此示例中，该方法返回`true`，因为数字“1”与正则表达式`\d`匹配。

**使用`split(String)`方法**

 [`split`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#split-java.lang.CharSequence-) 方法是一个很好的工具，用于收集位于匹配模式两侧的文本。如下面 [`SplitDemo.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/SplitDemo.java) 中所示， `split` 方法可以从字符串`one:two:three:four:five`中提取单词`one two three four five`：

```
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class SplitDemo {

    private static final String REGEX = ":";
    private static final String INPUT =
        "one:two:three:four:five";
    
    public static void main(String[] args) {
        Pattern p = Pattern.compile(REGEX);
        String[] items = p.split(INPUT);
        for(String s : items) {
            System.out.println(s);
        }
    }
}

```

```
OUTPUT:

one
two
three
four
five

```

为简单起见，我们匹配了字符串字面值冒号（`:`)而不是复杂的正则表达式。由于我们仍在使用`Pattern`和`Matcher`对象，因此您可以使用`split`来获取位于任何正则表达式两侧的文本。这是一个相同的例子， [`SplitDemo2.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/SplitDemo2.java) ，修改为在数字上拆分：

```
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class SplitDemo2 {

    private static final String REGEX = "\\d";
    private static final String INPUT =
        "one9two4three7four1five";

    public static void main(String[] args) {
        Pattern p = Pattern.compile(REGEX);
        String[] items = p.split(INPUT);
        for(String s : items) {
            System.out.println(s);
        }
    }
}

OUTPUT:

one
two
three
four
five
```

**其它有用方法**

您可能会发现以下方法也有一些用处：

- [`public static String quote(String s)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#quote-java.lang.String-) 返回指定`String`的文字模式`String`。此方法生成一个`String`，可用于创建一个与`String`匹配的`Pattern`，就像它是一个文字模式一样。输入序列中的元字符或转义序列将没有特殊含义。
- [`public String toString()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#toString--) 返回此模式的`String`表示形式。这是编译此模式的正则表达式。

**`java.lang.String`中的模式方法等价物**

`java.lang.String`中也存在正则表达式支持，它们是几种模仿`java.util.regex.Pattern`行为的方法。为方便起见，下面介绍了API的主要摘录。

- [`public boolean matches(String regex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#matches-java.lang.String-): 判断此字符串是否与给定的正则表达式匹配。调用`*str*.matches(*regex*)`

  方法会产生与表达式`Pattern.matches(*regex*, *str*)`完全相同的结果。

- [`public String[] split(String regex, int limit)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#split-java.lang.String-int-): 将字符串拆分为给定正则表达式的匹配项。调用 方法 `*str*.split(*regex*, *n*)` 会得到与 `Pattern.compile(*regex*).split(*str*, *n*)` 一样的结果。

- [`public String[] split(String regex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#split-java.lang.String-): 将此字符串拆分为给定正则表达式的匹配项。 此方法与调用具有给定表达式且limit参数为零的双参数split方法的方法相同。结果数组中不包括尾随空字符串。

还有一个替换方法，用一个`CharSequence`替换另一个：

- [`public String replace(CharSequence target,CharSequence replacement)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#replace-java.lang.CharSequence-java.lang.CharSequence-): 将与该文字目标序列匹配的此字符串的每个子字符串替换为指定的文字替换序列。替换从字符串的开头到结尾，例如，在字符串“aaa”中将“aa”替换为“b”将导致“ba”而不是“ab”。


### Matcher 类的方法

本节介绍`Matcher`类的一些有用的附加方法。为方便起见，下面列出的方法根据功能进行分组。

**Index 方法**

*Index 方法* 提供有用的索引值，精确显示在输入字符串中找到匹配的位置：

- [`public int start()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#start--): 返回上一个匹配的起始索引。
- [`public int start(int group)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#start-int-): 返回在上一个匹配操作期间由给定组捕获的子序列的起始索引。
- [`public int end()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#end--): 返回最后一个字符匹配后的偏移量。
- [`public int end(int group)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#end-int-): 返回在上一个匹配操作期间由给定组捕获的子序列的最后一个字符之后的偏移量。

**Study 方法**

*Study 方法* 检查输入字符串并返回一个布尔值，指示是否找到该模式。

- [`public boolean lookingAt()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#lookingAt--): 尝试将输入序列（从区域的开头开始）与模式匹配。
- [`public boolean find()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#find--): 尝试查找与模式匹配的输入序列的下一个子序列。
- [`public boolean find(int start)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#find-int-): 重置此匹配器，然后尝试从指定的索引处开始查找与模式匹配的输入序列的下一个子序列。
- [`public boolean matches()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#matches--): 尝试将整个区域与模式匹配。

**替换方法**

*Replacement 方法* 用来替换输入字符串中的字符很有用。

- [`public Matcher appendReplacement(StringBuffer sb, String replacement)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#appendReplacement-java.lang.StringBuffer-java.lang.String-): 实现非尾部的附加和替换步骤。
- [`public StringBuffer appendTail(StringBuffer sb)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#appendTail-java.lang.StringBuffer-): 实现尾部追加和替换步骤。
- [`public String replaceAll(String replacement)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#replaceAll-java.lang.String-): 将具有给定替换字符串的模式匹配的输入序列的每个子序列替换。
- [`public String replaceFirst(String replacement)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#replaceFirst-java.lang.String-): 将具有给定替换字符串的模式匹配的输入序列的第一个子序列替换。
- [`public static String quoteReplacement(String s)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#quoteReplacement-java.lang.String-): 返回指定`String`的文字替换`String`。此方法生成一个`String`，它将作为`Matcher`类的`appendReplacement`方法中的文字替换。生成的字符串将匹配`s`中作为文字序列处理的字符序列。斜杠（`'\'`）和美元符号（`'$'`）将没有特殊含义。

**使用 `start` 和 `end` 方法**

下面是一个示例 [`MatcherDemo.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/MatcherDemo.java) ，它计算输入字符串中“dog”一词出现的次数。

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MatcherDemo {

    private static final String REGEX =
        "\\bdog\\b";
    private static final String INPUT =
        "dog dog dog doggie dogg";

    public static void main(String[] args) {
       Pattern p = Pattern.compile(REGEX);
       //  get a matcher object
       Matcher m = p.matcher(INPUT);
       int count = 0;
       while(m.find()) {
           count++;
           System.out.println("Match number "
                              + count);
           System.out.println("start(): "
                              + m.start());
           System.out.println("end(): "
                              + m.end());
      }
   }
}
```

```
OUTPUT:

Match number 1
start(): 0
end(): 3
Match number 2
start(): 4
end(): 7
Match number 3
start(): 8
end(): 11
```

您可以看到此示例使用单词边界来确保字母`“d” “o” “g”`不仅仅是较长单词中的子字符串。它还提供了有关输入字符串中匹配发生位置的一些有用信息。`start`方法返回上一个匹配操作期间给定组捕获的子序列的起始索引，`end`返回匹配的最后一个字符的索引加1。

**使用 `matches` 和 `lookingAt` 方法**

`matches`和`lookingAt`方法都尝试将输入序列与模式匹配。然而，不同之处在于`matches`需要匹配整个输入序列，而`lookingAt`则不需要。两种方法总是从输入字符串的开头开始。这是完整的代码， [`MatchesLooking.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/MatchesLooking.java)：

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MatchesLooking {

    private static final String REGEX = "foo";
    private static final String INPUT =
        "fooooooooooooooooo";
    private static Pattern pattern;
    private static Matcher matcher;

    public static void main(String[] args) {
   
        // Initialize
        pattern = Pattern.compile(REGEX);
        matcher = pattern.matcher(INPUT);

        System.out.println("Current REGEX is: "
                           + REGEX);
        System.out.println("Current INPUT is: "
                           + INPUT);

        System.out.println("lookingAt(): "
            + matcher.lookingAt());
        System.out.println("matches(): "
            + matcher.matches());
    }
}
```

```
Current REGEX is: foo
Current INPUT is: fooooooooooooooooo
lookingAt(): true
matches(): false
```

**使用 `replaceFirst(String)` 和 `replaceAll(String)`**

`replaceFirst`和`replaceAll`方法替换与给定正则表达式匹配的文本。正如其名称所示，`replaceFirst`替换第一次出现，`replaceAll`替换所有出现。这是 [`ReplaceDemo.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/ReplaceDemo.java) 代码：

```java
import java.util.regex.Pattern; 
import java.util.regex.Matcher;

public class ReplaceDemo {
 
    private static String REGEX = "dog";
    private static String INPUT =
        "The dog says meow. All dogs say meow.";
    private static String REPLACE = "cat";
 
    public static void main(String[] args) {
        Pattern p = Pattern.compile(REGEX);
        // get a matcher object
        Matcher m = p.matcher(INPUT);
        INPUT = m.replaceAll(REPLACE);
        System.out.println(INPUT);
    }
}
```

```
OUTPUT: The cat says meow. All cats say meow.
```

在第一个版本中，所有出现的`dog`都被`cat`取代。但为何停在这里？您可以替换匹配任何正则表达式的文本，而不是替换像`dog`一样的简单文字。此方法的API声明“给定正则表达式 `a*b`，输入`aabfooaabfooabfoob`和替换字符串 `-`，在该表达式的匹配器上调用此方法将产生字符串`-foo-foo-foo-`。

[`ReplaceDemo2.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/ReplaceDemo2.java) ：

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;
 
public class ReplaceDemo2 {
 
    private static String REGEX = "a*b";
    private static String INPUT =
        "aabfooaabfooabfoob";
    private static String REPLACE = "-";
 
    public static void main(String[] args) {
        Pattern p = Pattern.compile(REGEX);
        // get a matcher object
        Matcher m = p.matcher(INPUT);
        INPUT = m.replaceAll(REPLACE);
        System.out.println(INPUT);
    }
}
```

```
OUTPUT: -foo-foo-foo-
```

要仅替换模式的第一个匹配项，只需调用`replaceFirst`而不是`replaceAll`。它接受相同的参数。

**使用`appendReplacement(StringBuffer,String)` 和 `appendTail(StringBuffer)`**

`Matcher`类还提供了`appendReplacement`和`appendTail`方法来替换文本。以下示例 [`RegexDemo.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/RegexDemo.java) 使用这两种方法来实现与`replaceAll`相同的效果。

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class RegexDemo {
 
    private static String REGEX = "a*b";
    private static String INPUT = "aabfooaabfooabfoob";
    private static String REPLACE = "-";
 
    public static void main(String[] args) {
        Pattern p = Pattern.compile(REGEX);
        Matcher m = p.matcher(INPUT); // get a matcher object
        StringBuffer sb = new StringBuffer();
        while(m.find()){
            m.appendReplacement(sb,REPLACE);
        }
        m.appendTail(sb);
        System.out.println(sb.toString());
    }
}
```

```
OUTPUT: -foo-foo-foo- 
```

**`java.lang.String` 中 Matcher 类方法的等效方法**

为方便起见，`String`类也模仿了几个`Matcher`方法：

- [`public String replaceFirst(String regex, String replacement)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#replaceFirst-java.lang.String-java.lang.String-): 将此字符串匹配到给定正则表达式的第一个子串替换为给定替换字符串。调用 `*str*.replaceFirst(*regex*, *repl*)` 将得到与表达式`Pattern.compile(*regex*).matcher(*str*).replaceFirst(*repl*)` 相同的结果。
- [`public String replaceAll(String regex, String replacement)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#replaceAll-java.lang.String-java.lang.String-): 将此字符串匹配到给定正则表达式的所有子串替换为给定替换字符串。调用 `*str*.replaceAll(*regex*, *repl*)` 将得到与表达式 `Pattern.compile(*regex*).matcher(*str*).replaceAll(*repl*)` 相同的结果。

### PatternSyntaxException 类的方法

[`PatternSyntaxException`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html) 是未经检查的异常，表示正则表达式模式中的语法错误。`PatternSyntaxException`类提供以下方法来帮助您确定出错的地方：

- [`public String getDescription()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html#getDescription--): 获取错误的描述。
- [`public int getIndex()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html#getIndex--): 获取错误索引。
- [`public String getPattern()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html#getPattern--): 检索错误的正则表达式模式。
- [`public String getMessage()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html#getMessage--): 返回一个多行字符串，其中包含语法错误及其索引的描述，错误的正则表达式模式以及模式中错误索引的可视表示。

以下源代码 [`RegexTestHarness2.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/RegexTestHarness2.java) 更新了我们的测试工具以检查格式错误的正则表达式：

```java
import java.io.Console;
import java.util.regex.Pattern;
import java.util.regex.Matcher;
import java.util.regex.PatternSyntaxException;

public class RegexTestHarness2 {

    public static void main(String[] args){
        Pattern pattern = null;
        Matcher matcher = null;

        Console console = System.console();
        if (console == null) {
            System.err.println("No console.");
            System.exit(1);
        }
        while (true) {
            try{
                pattern = 
                Pattern.compile(console.readLine("%nEnter your regex: "));

                matcher = 
                pattern.matcher(console.readLine("Enter input string to search: "));
            }
            catch(PatternSyntaxException pse){
                console.format("There is a problem" +
                               " with the regular expression!%n");
                console.format("The pattern in question is: %s%n",
                               pse.getPattern());
                console.format("The description is: %s%n",
                               pse.getDescription());
                console.format("The message is: %s%n",
                               pse.getMessage());
                console.format("The index is: %s%n",
                               pse.getIndex());
                System.exit(0);
            }
            boolean found = false;
            while (matcher.find()) {
                console.format("I found the text" +
                    " \"%s\" starting at " +
                    "index %d and ending at index %d.%n",
                    matcher.group(),
                    matcher.start(),
                    matcher.end());
                found = true;
            }
            if(!found){
                console.format("No match found.%n");
            }
        }
    }
}
```

要运行此测试，请输入 `?i)foo` 作为正则表达式。这个错误是程序员忘记嵌入式标志表达式 `(?i)`中的左括号的常见情况。这样做会产生以下结果：

```
Enter your regex: ?i)
There is a problem with the regular expression!
The pattern in question is: ?i)
The description is: Dangling meta character '?'
The message is: Dangling meta character '?' near index 0
?i)
^
The index is: 0
```

从这个输出中，我们可以看到语法错误是索引0处的悬空元字符（问号）。缺少左括号是罪魁祸首。

### Unicode 支持

从JDK 7版本开始，正则表达式模式匹配扩展了支持 Unicode 6.0 的功能。

- [匹配特定的代码点](https://docs.oracle.com/javase/tutorial/essential/regex/unicode.html#matchingSpecific)
- [Unicode字符属性](https://docs.oracle.com/javase/tutorial/essential/regex/unicode.html#properties)

**匹配特定的代码点**

您可以使用格式`\uFFFF`格式的转义序列匹配特定的 Unicode 代码点，其中`FFFF`是您要匹配的代码点的十六进制值。例如，`\u6771`匹配东方的汉字符。

或者，您可以使用 Perl 样式的十六进制表示法指定代码点，`\x{...}`。 例如：

```
String hexPattern = "\x{" + Integer.toHexString(codePoint) + "}";
```

**Unicode字符属性**

除了其值之外，每个 Unicode 字符都具有某些属性或属性。您可以将属于特定类别的单个字符与表达式 `\p{*prop*}`进行匹配。您可以将不属于特定类别的单个字符与表达式 `\P{*prop*}`进行匹配。

支持的三种属性类型是脚本，块和“常规”类别。

### Scripts

要确定代码点是否属于特定脚本，可以使用`script` 关键字或`sc`短格式，例如`\p{script=Hiragana}`。或者，您可以在脚本名称前加上字符串`Is`，例如`\p{IsHiragana}`。

`Pattern`支持的有效脚本名称是 [`UnicodeScript.forName`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeScript.html#forName-java.lang.String-) 接受的名称。

### Blocks

可以使用`block`关键字或`blk`短格式指定块，例如`\p{block=Mongolian}`。或者，您可以在块名称前加上字符串 `In`，例如 `\p{InMongolian}`。

`Pattern`支持的有效块名称是 [`UnicodeBlock.forName`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html#forName-java.lang.String-)接受的块名称。

### General Category

可以使用可选前缀`Is`指定类别。例如，`IsL` 匹配 Unicode 字母的类别。也可以使用`general_categorykeyword`或短格式`gc`指定类别。例如，可以使用`general_category = Lu`或`gc = Lu`匹配大写字母。

支持的类别是由 [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 类指定的版本中的 [The Unicode Standard](http://www.unicode.org/unicode/standard/standard.html) 类别。

### 附加资源

现在您已经完成了关于正则表达式的课程，您可能会发现您的主要参考资料将是以下类的API文档：[`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html),[`Matcher`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html), 和 [`PatternSyntaxException`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html) 。

为了更准确地描述正则表达式构造的行为，我们建议您阅读Jeffrey E. F.Friedl撰写的 [*Mastering Regular Expressions*](http://www.amazon.com/exec/obidos/ASIN/0596002890/javasoftsunmicroA/) 一书。

