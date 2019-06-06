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

