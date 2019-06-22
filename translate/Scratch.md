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

