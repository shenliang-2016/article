### 自动装箱和拆箱

*自动装箱*是一种Java编译器自动执行的在基本数据类型和它们对应的对象包装类之间的转换机制。比如，将`int` 转换为`Integer`，`double`转换为`Double`，等等。如果这种转换反向进行，则被称为*自动拆箱*。

下面是一个自动装箱的最简单的例子：

```java
Character ch = 'a';
```

本章节中其它例子中用到了泛型。如果你对泛型语法还不熟悉，参考 [Generics (Updated)](https://docs.oracle.com/javase/tutorial/java/generics/index.html) 部分。

考虑下面的代码：

```java
List<Integer> li = new ArrayList<>();
for (int i = 1; i < 50; i += 2)
    li.add(i);
```

虽然您将`int`值作为基本类型而不是`Integer`对象添加到`li`，但代码会通过编译。因为`li`是`Integer`对象的列表，而不是`int`值列表，所以您可能想知道为什么Java编译器不会发出编译时错误。编译器不会生成错误，因为它从`i`创建一个`Integer`对象并将对象添加到`li`。因此，编译器在运行时将以前的代码转换为以下代码：

```java
List<Integer> li = new ArrayList<>();
for (int i = 1; i < 50; i += 2)
    li.add(Integer.valueOf(i));
```

将原始值（例如`int`）转换为相应包装类（`Integer`）的对象称为`autoboxing`。 当基本数据类型值为如下情况时，Java编译器应用自动装箱：

- 被作为参数传递给期望它对应的包装类型的方法时。
- 被赋值给对应的包装类型的变量时。

考虑下面的方法：

```java
public static int sumEven(List<Integer> li) {
    int sum = 0;
    for (Integer i: li)
        if (i % 2 == 0)
            sum += i;
        return sum;
}
```

由于求余数(`%`) 和一元加 (`+=`) 操作符不能应用于 `Integer` 对象，你可能会好奇为啥Java编译器在编译该方法时并没有抛出异常。因为它在运行时调用了 `intValue` 方法将 `Integer` 转换成了 `int` ：

```java
public static int sumEven(List<Integer> li) {
    int sum = 0;
    for (Integer i : li)
        if (i.intValue() % 2 == 0)
            sum += i.intValue();
        return sum;
}
```

将包装类型（`Integer`）的对象转换为其对应的原始（`int`）值称为自动拆箱。当包装类的对象是下列情况时，Java编译器应用拆箱：

 - 作为参数传递给期望相应基本数据类型值的方法。
 - 赋值给相应基本数据类型的变量。

`Unboxing`示例显示了其工作原理：

```java
import java.util.ArrayList;
import java.util.List;

public class Unboxing {

    public static void main(String[] args) {
        Integer i = new Integer(-8);

        // 1. Unboxing through method invocation
        int absVal = absoluteValue(i);
        System.out.println("absolute value of " + i + " = " + absVal);

        List<Double> ld = new ArrayList<>();
        ld.add(3.1416);    // Π is autoboxed through method invocation.

        // 2. Unboxing through assignment
        double pi = ld.get(0);
        System.out.println("pi = " + pi);
    }

    public static int absoluteValue(int i) {
        return (i < 0) ? -i : i;
    }
}
```

程序输出：

```shell
absolute value of -8 = 8
pi = 3.1416
```

自动装箱和拆箱使开发人员可以编写更清晰的代码，使其更易于阅读。下表列出了原始类型及其相应的包装类，Java编译器使用这些类进行自动装箱和拆箱：

| 基本数据类型  | 包装类型      |
| ------- | --------- |
| boolean | Boolean   |
| byte    | Byte      |
| char    | Character |
| float   | Float     |
| int     | Integer   |
| long    | Long      |
| short   | Short     |
| double  | Double    |

