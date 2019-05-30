#### 

例如，下面的代码：

````java
// creates empty builder, capacity 16
StringBuilder sb = new StringBuilder();
// adds 9 character string at beginning
sb.append("Greetings");
````

将产生容量 16 长度 9 的字符串构建器：

![A string builder's length is the number of characters it contains; a string builder's capacity is the number of character spaces that have been allocated.](https://docs.oracle.com/javase/tutorial/figures/java/objects-stringBuffer.gif)

`StringBuilder`类拥有若干方法关于长度和容量，`String`类没有这些方法。

| 方法                                   | 描述                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| `void setLength(int newLength)`        | 设置字符序列的长度，如果 `newLength` 小于 `length()`，则字符序列的尾部字符将会被截断。如果 `newLength` 大于 `length()`， `null`字符就会被添加到字符序列之后。 |
| `void ensureCapacity(int minCapacity)` | 确保容量至少等于给定的最小值。                               |

很多操作 (比如 `append()`, `insert()`, 或者 `setLength()`) 能够增加字符串构建器中字符序列的长度，而结果 `length()` 可能会超过目前的 `capacity()`。当这种情况发生时，容量将会自动扩展。

**`StringBuilder` 操作**

`String`中不可用的`StringBuilder`上的主要操作是`append()`和`insert()`方法，它们被重载以接受任何类型的数据。每个都将其参数转换为字符串，然后将该字符串的字符追加或插入字符串生成器中的字符序列。`append`方法总是在现有字符序列的末尾添加这些字符，而`insert`方法在指定位置添加字符。

以下是`StringBuilder`类的一些方法。

| 方法                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `StringBuilder append(boolean b)`<br />`StringBuilder append(char c)`<br />`StringBuilder append(char[] str)`<br />`StringBuilder append(char[] str, int offset, int len)`<br />`StringBuilder append(double d)`<br />`StringBuilder append(float f)`<br />`StringBuilder append(int i)`<br />`StringBuilder append(long lng)`<br />`StringBuilder append(Object obj)`<br />`StringBuilder append(String s)` | 将参数追加到此字符串构建器。在附加操作发生之前，数据将转换为字符串。 |
| `StringBuilder delete(int start, int end)`<br />`StringBuilder deleteCharAt(int index)` | 第一种方法在`StringBuilder`的字符序列中删除从`start`到`end-1`（包括）的子序列。第二种方法删除位于`index`的字符。 |
| `StringBuilder insert(int offset, boolean b)`<br />`StringBuilder insert(int offset, char c)`<br />`StringBuilder insert(int offset, char[] str)`<br />`StringBuilder insert(int index, char[] str, int offset, int len)`<br />`StringBuilder insert(int offset, double d)`<br />`StringBuilder insert(int offset, float f)`<br />`StringBuilder insert(int offset, int i)`<br />`StringBuilder insert(int offset, long lng)`<br />`StringBuilder insert(int offset, Object obj)`<br />`StringBuilder insert(int offset, String s)` | 将第二个参数插入到字符串构建器中。第一个整数参数表示要在其中插入数据的索引。在插入操作发生之前，数据将转换为字符串。 |
| `StringBuilder replace(int start, int end, String s)`<br />`void setCharAt(int index, char c)` | 替换此字符串生成器中的指定字符。                             |
| `StringBuilder reverse()`                                    | 反转此字符串构建器中的字符序列。                             |
| `String toString()`                                          | 返回包含构建器中的字符序列的字符串。                         |

------

**注意：**您可以在`StringBuilder`对象上使用任何`String`方法，方法是首先使用`StringBuilder`类的`toString()`方法将字符串构建器转换为字符串。然后使用`StringBuilder(String str)`构造函数将字符串转换回字符串构建器。

------

**例子**

标题为“字符串”一节中列出的`StringDemo`程序是一个程序的示例，如果使用`StringBuilder`而不是`String`则该程序会更有效率。

`StringDemo`反转了回文。在这里，它再次出现：

```java
public class StringDemo {
    public static void main(String[] args) {
        String palindrome = "Dot saw I was Tod";
        int len = palindrome.length();
        char[] tempCharArray = new char[len];
        char[] charArray = new char[len];
        
        // put original string in an 
        // array of chars
        for (int i = 0; i < len; i++) {
            tempCharArray[i] = 
                palindrome.charAt(i);
        } 
        
        // reverse array of chars
        for (int j = 0; j < len; j++) {
            charArray[j] =
                tempCharArray[len - 1 - j];
        }
        
        String reversePalindrome =
            new String(charArray);
        System.out.println(reversePalindrome);
    }
}
```

程序输出：

```shell
doT saw I was toD
```

为了完成字符串反转，程序将字符串转换为字符数组（第一个`for`循环），将数组反转为第二个数组（第二个`for`循环），然后转换回字符串。

如果将`palindrome`字符串转换为字符串构建器，则可以在`StringBuilder`类中使用`reverse()`方法。它使代码更简单，更易于阅读：

```java
public class StringBuilderDemo {
    public static void main(String[] args) {
        String palindrome = "Dot saw I was Tod";
         
        StringBuilder sb = new StringBuilder(palindrome);
        
        sb.reverse();  // reverse it
        
        System.out.println(sb);
    }
}
```

程序输出：

```shell
doT saw I was toD
```

请注意，`println()`打印字符串构建器，如下所示：

```java
System.out.println(sb);
```

`sb.toString()`是隐式调用的，因为它与`println()`调用中的任何其他对象一样。

------

**注意：**还有一个与`StringBuilder`类完全相同的`StringBuffer`类，除了它的方法是同步的，它是线程安全的。线程将在关于并发的课程中讨论。

------

#### 字符和字符串小结

大多数情况下，如果使用单个字符值，则将使用原始`char`类型。但是，有时候需要使用`char`作为对象 - 例如，作为期望对象的方法参数。Java编程语言提供了一个*wrapper*类，为了这个目的，它将`char`包装在`Character`对象中。 `Character`类型的对象包含一个类型为`char`的字段。 这个[`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 类还提供了许多用于操作字符的有用类（即静态）方法。

字符串是一系列字符，广泛用于Java编程。在Java编程语言中，字符串是对象。 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 类有60多个方法和13个构造函数。

最常见的是，您如下创建一个字符串：

```shell
String s = "Hello world!";
```

而不是使用其中一个`String`构造函数。

`String`类有很多方法可以查找和检索子字符串；然后可以使用`+`连接运算符将它们轻松地重新组合成新的字符串。

`String`类还包括许多实用方法，其中包括`split()`，`toLowerCase()`，`toUpperCase()`和`valueOf()`。后一种方法在将用户输入字符串转换为数字时是必不可少的。`Number`子类还具有将字符串转换为数字的方法，反之亦然。

除了`String`类之外，还有一个[`StringBuilder`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html) 类。使用`StringBuilder`对象有时比使用字符串更有效。`StringBuilder`类提供了一些对字符串有用的方法，其中包括`reverse()`。但是，一般来说，`String`类有更多种方法。

可以使用`StringBuilder`构造函数将字符串转换为字符串构建器。可以使用`toString()`方法将字符串构建器转换为字符串。

