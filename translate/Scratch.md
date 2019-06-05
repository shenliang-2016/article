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

**定义：**异常是一个事件，在程序执行过程中产生，打乱程序指令的正常执行流程。

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

* 捕获异常的`try`语句。`try`必须为异常提供处理程序，如 [捕获和处理异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/handling.html) 中所述。
* 一个方法，指定它可以抛出异常。该方法必须提供一个`throws`子句，列出异常，如 [指定方法引发的异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/declaring.html) 中所述。

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

