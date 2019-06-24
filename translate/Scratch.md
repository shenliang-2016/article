### PatternSyntaxException 类的方法

[`PatternSyntaxException`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html) 是未经检查的异常，表示正则表达式模式中的语法错误。`PatternSyntaxException`类提供以下方法来帮助您确定出错的地方：

- [`public String getDescription()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html#getDescription--): 获取错误的描述。
- [`public int getIndex()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html#getIndex--): 获取错误索引。
- [`public String getPattern()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html#getPattern--): 检索错误的正则表达式模式。
- [`public String getMessage()`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html#getMessage--): 返回一个多行字符串，其中包含语法错误及其索引的描述，错误的正则表达式模式以及模式中错误索引的可视表示。

以下源代码 [`RegexTestHarness2.java`](https://docs.oracle.com/javase/tutorial/essential/regex/examples/RegexTestHarness2.java) 更新了我们的测试工具以检查格式错误的正则表达式：

```java
import java.io.Console;
import java.util.regex.Pattern;
import java.util.regex.Matcher;
import java.util.regex.PatternSyntaxException;

public class RegexTestHarness2 {

    public static void main(String[] args){
        Pattern pattern = null;
        Matcher matcher = null;

        Console console = System.console();
        if (console == null) {
            System.err.println("No console.");
            System.exit(1);
        }
        while (true) {
            try{
                pattern = 
                Pattern.compile(console.readLine("%nEnter your regex: "));

                matcher = 
                pattern.matcher(console.readLine("Enter input string to search: "));
            }
            catch(PatternSyntaxException pse){
                console.format("There is a problem" +
                               " with the regular expression!%n");
                console.format("The pattern in question is: %s%n",
                               pse.getPattern());
                console.format("The description is: %s%n",
                               pse.getDescription());
                console.format("The message is: %s%n",
                               pse.getMessage());
                console.format("The index is: %s%n",
                               pse.getIndex());
                System.exit(0);
            }
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

要运行此测试，请输入 `?i)foo` 作为正则表达式。这个错误是程序员忘记嵌入式标志表达式 `(?i)`中的左括号的常见情况。这样做会产生以下结果：

```
Enter your regex: ?i)
There is a problem with the regular expression!
The pattern in question is: ?i)
The description is: Dangling meta character '?'
The message is: Dangling meta character '?' near index 0
?i)
^
The index is: 0
```

从这个输出中，我们可以看到语法错误是索引0处的悬空元字符（问号）。缺少左括号是罪魁祸首。

### Unicode 支持

从JDK 7版本开始，正则表达式模式匹配扩展了支持 Unicode 6.0 的功能。

- [匹配特定的代码点](https://docs.oracle.com/javase/tutorial/essential/regex/unicode.html#matchingSpecific)
- [Unicode字符属性](https://docs.oracle.com/javase/tutorial/essential/regex/unicode.html#properties)

**匹配特定的代码点**

您可以使用格式`\uFFFF`格式的转义序列匹配特定的 Unicode 代码点，其中`FFFF`是您要匹配的代码点的十六进制值。例如，`\u6771`匹配东方的汉字符。

或者，您可以使用 Perl 样式的十六进制表示法指定代码点，`\x{...}`。 例如：

```
String hexPattern = "\x{" + Integer.toHexString(codePoint) + "}";
```

**Unicode字符属性**

除了其值之外，每个 Unicode 字符都具有某些属性或属性。您可以将属于特定类别的单个字符与表达式 `\p{*prop*}`进行匹配。您可以将不属于特定类别的单个字符与表达式 `\P{*prop*}`进行匹配。

支持的三种属性类型是脚本，块和“常规”类别。

### Scripts

要确定代码点是否属于特定脚本，可以使用`script` 关键字或`sc`短格式，例如`\p{script=Hiragana}`。或者，您可以在脚本名称前加上字符串`Is`，例如`\p{IsHiragana}`。

`Pattern`支持的有效脚本名称是 [`UnicodeScript.forName`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeScript.html#forName-java.lang.String-) 接受的名称。

### Blocks

可以使用`block`关键字或`blk`短格式指定块，例如`\p{block=Mongolian}`。或者，您可以在块名称前加上字符串 `In`，例如 `\p{InMongolian}`。

`Pattern`支持的有效块名称是 [`UnicodeBlock.forName`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html#forName-java.lang.String-)接受的块名称。

### General Category

可以使用可选前缀`Is`指定类别。例如，`IsL` 匹配 Unicode 字母的类别。也可以使用`general_categorykeyword`或短格式`gc`指定类别。例如，可以使用`general_category = Lu`或`gc = Lu`匹配大写字母。

支持的类别是由 [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 类指定的版本中的 [The Unicode Standard](http://www.unicode.org/unicode/standard/standard.html) 类别。

### 附加资源

现在您已经完成了关于正则表达式的课程，您可能会发现您的主要参考资料将是以下类的API文档：[`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html),[`Matcher`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html), 和 [`PatternSyntaxException`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/PatternSyntaxException.html) 。

为了更准确地描述正则表达式构造的行为，我们建议您阅读Jeffrey E. F.Friedl撰写的 [*Mastering Regular Expressions*](http://www.amazon.com/exec/obidos/ASIN/0596002890/javasoftsunmicroA/) 一书。

