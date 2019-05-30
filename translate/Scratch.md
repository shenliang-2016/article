#### 比较字符串和部分字符串

`String` 类包含大量方法用来比较字符串或者部分字符串。下面列出了这些方法：

| Method                                   | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| `boolean endsWith(String suffix)`<br />`boolean startsWith(String prefix)` | 返回 `true` 如果字符串以参数给出的字符串结尾或者开头。          |
| `boolean startsWith(String prefix, int offset)` | 考察从索引偏移量`offset`开始的字符串，如果它以指定为参数的子字符串开头，则返回`true`。 |
| `int compareTo(String anotherString)`    | 按字典顺序比较两个字符串。返回一个整数，指示此字符串是大于（结果是> 0），等于（结果是= 0）还是小于（结果是<0）参数。 |
| `int compareToIgnoreCase(String str)`    | 按字典顺序比较两个字符串，忽略大小写的差异。返回一个整数，指示此字符串是大于（结果是> 0），等于（结果是= 0）还是小于（结果是<0）参数。 |
| `boolean equals(Object anObject)`        | 当且仅当参数是`String`对象时才返回`true`，该`String`对象表示与此对象相同的字符序列。 |
| `boolean equalsIgnoreCase(String anotherString)` | 当且仅当参数是`String`对象时才返回`true`，该对象表示与此对象相同的字符序列，忽略大小写的差异。 |
| `boolean regionMatches(int toffset, String other, int ooffset, int len)` | 测试此字符串的指定区域是否与`String`参数的指定区域匹配。`Region`的长度为`len`，从此字符串的索引`toffset`开始，另一个字符串的`ooffset`开始。 |
| `boolean regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len)` | 测试此字符串的指定区域是否与`String`参数的指定区域匹配。`Region`的长度为`len`，从此字符串的索引`toffset`开始，另一个字符串的`ooffset`开始。`boolean`参数指示是否应忽略大小写；如果为`true`，则在比较字符时忽略大小写。 |
| `boolean matches(String regex)`          | 测试此字符串是否与指定的正则表达式匹配。正则表达式在标题为“正则表达式”的课程中讨论。 |

下面的程序，`RegionMatchesDemo`，使用 `regionMatches` 方法在一个字符串中搜索另一个字符串：

````java
public class RegionMatchesDemo {
    public static void main(String[] args) {
        String searchMe = "Green Eggs and Ham";
        String findMe = "Eggs";
        int searchMeLength = searchMe.length();
        int findMeLength = findMe.length();
        boolean foundIt = false;
        for (int i = 0; 
             i <= (searchMeLength - findMeLength);
             i++) {
           if (searchMe.regionMatches(i, findMe, 0, findMeLength)) {
              foundIt = true;
              System.out.println(searchMe.substring(i, i + findMeLength));
              break;
           }
        }
        if (!foundIt)
            System.out.println("No match found.");
    }
}
````

这个程序的输出是`Eggs`。

程序逐步遍历`searchMe`引用的字符串。对于每个字符，程序调用`regionMatches`方法来确定以当前字符开头的子字符串是否与程序正在查找的字符串匹配。

#### `StringBuilder` 类

`StringBuilder`对象与`String`对象类似，只是它们可以被修改。在内部，这些对象被视为包含一系列字符的可变长度数组。在任何时候，可以通过方法调用来改变序列的长度和内容。

除非`StringBuilder`在更简单的代码（参见本节末尾的示例程序）或更好的性能方面具有优势的场景，否则应始终使用字符串。例如，如果需要连接大量字符串，则附加到`StringBuilder`对象会更有效率。

**长度和容量**

与`String`类一样，`StringBuilder`类有一个`length()`方法，该方法返回构建器中字符序列的长度。

与字符串不同，每个字符串构建器也具有容量，即已分配的字符空间数。 `capacity()`方法返回的容量始终大于或等于长度（通常大于），并将根据需要自动扩展以适应字符串构建器的添加。

| 构造器                               | 描述                                       |
| --------------------------------- | ---------------------------------------- |
| `StringBuilder()`                 | 创建容量为16的空字符串构建器。(包含16个空元素)               |
| `StringBuilder(CharSequence cs)`  | 构建一个字符串构建器包含参数 `CharSequence`给出的字符，同时还在后面跟着16个空元素。 |
| `StringBuilder(int initCapacity)` | 创建一个具有特定初始容量的空字符串构建器。                    |
| `StringBuilder(String s)`         | 创建一个字符串构建器，它包含参数给出的特定字符串，同时在后面跟随16个空元素。  |