### 介绍

**啥是正则表达式？**

*正则表达式*是一种基于集合中每个字符串共享的共同特征来描述一组字符串的方法。它们可用于搜索，编辑或操作文本和数据。 您必须学习特定的语法来创建正则表达式 - 这超出了Java编程语言的常规语法。正则表达式的复杂程度各不相同，但是一旦理解了它们的构造基础，您就能够解密（或创建）任何正则表达式。

本教程讲解 [`java.util.regex`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/package-summary.html) API支持的正则表达式语法，并提供了几个示例来说明各种对象如何交互。在正则表达式的世界中，有许多不同的风格可供选择，例如grep，Perl，Tcl，Python，PHP和awk。`java.util.regex` API中的正则表达式语法与Perl中的类似。

**如何在此包中表示正则表达式？**

`java.util.regex`包主要由三个类组成： [`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) ， [`Matcher`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html) ，和 [`PatternSyntaxException`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html) 。

 -  `Pattern`对象是正则表达式的编译表示。`Pattern`类不提供公共构造函数。要创建模式，必须首先调用 `public static compile` 方法之一，然后返回`Pattern`对象。这些方法接受正则表达式作为第一个参数；本教程的前几课将教你所需的语法。
 -  `Matcher`对象是解释模式并对输入字符串执行匹配操作的引擎。与`Pattern`类一样，`Matcher`也没有定义公共构造函数。通过在`Pattern`对象上调用`matcher`方法获取`Matcher`对象。
 -  `PatternSyntaxException`对象是未经检查的异常，表示正则表达式模式中的语法错误。

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

----

**注意：** 在某些情况下，上面列出的特殊字符不会被视为元字符。当您了解有关如何构造正则表达式的更多信息时，您将遇到此问题。但是，您可以使用此列表检查特定字符是否会被视为元字符。例如，字符`@`和`＃`从不带有特殊含义。

----

有两种方法可以强制将元字符视为普通字符：

 - 在元字符前面加一个反斜杠，或者
 - 将其放在 `\Q`（开始）和 `\E`（结束）内。

使用此技术时，`\Q`和`\E`可以放在表达式中的任何位置，前提是`\Q`首先出现。

