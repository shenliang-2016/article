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