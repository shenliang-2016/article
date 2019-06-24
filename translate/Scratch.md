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

