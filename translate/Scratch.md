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

 -  `d`将整数值格式化为十进制值。
 -  `f`将浮点值格式化为十进制值。
 -  `n`输出特定于平台的行终结符。

以下是其他一些转换：

 -  `x`将整数格式化为十六进制值。
 -  `s`将任何值格式化为字符串。
 -  `tB`将整数格式化为特定于语言环境的月份名称。

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

