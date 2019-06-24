### 预定义字符类

[`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) API 包含若干有用的*预定义字符类*，它们提供了使用正则表达式的简便方法：

| Construct | Description                              |
| --------- | ---------------------------------------- |
| `.`       | Any character (may or may not match line terminators) |
| `\d`      | A digit: `[0-9]`                         |
| `\D`      | A non-digit: `[^0-9]`                    |
| `\s`      | A whitespace character: `[ \t\n\x0B\f\r]` |
| `\S`      | A non-whitespace character: `[^\s]`      |
| `\w`      | A word character: `[a-zA-Z_0-9]`         |
| `\W`      | A non-word character: `[^\w]`            |

在上表中，左侧列中的每个构造都是右侧列中字符类的简写。例如，`\d`表示数字范围（0-9），`\w`表示单词字符（任何小写字母，任何大写字母，下划线字符或任何数字）。尽可能使用预定义的类。它们使您的代码更易于阅读，并消除格式错误的字符类引入的错误。

以反斜杠开头的构造称为转义构造。我们在 [String Literals](https://docs.oracle.com/javase/tutorial/essential/regex/literals.html) 部分中预览了转义结构，其中我们提到使用反斜杠和`\Q`和`\E`作为引用。如果在字符串字面量中使用转义构造，则必须在反斜杠前面加上另一个反斜杠，以便编译字符串。 例如：

```
private final String REGEX = "\\d"; // a single digit
```

在这个例子中`\d`是正则表达式；编译代码需要额外的反斜杠。测试工具直接从控制台读取表达式，因此不需要额外的反斜杠。

以下示例演示了预定义字符类的使用。

```
Enter your regex: .
Enter input string to search: @
I found the text "@" starting at index 0 and ending at index 1.

Enter your regex: . 
Enter input string to search: 1
I found the text "1" starting at index 0 and ending at index 1.

Enter your regex: .
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: \d
Enter input string to search: 1
I found the text "1" starting at index 0 and ending at index 1.

Enter your regex: \d
Enter input string to search: a
No match found.

Enter your regex: \D
Enter input string to search: 1
No match found.

Enter your regex: \D
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: \s
Enter input string to search:  
I found the text " " starting at index 0 and ending at index 1.

Enter your regex: \s
Enter input string to search: a
No match found.

Enter your regex: \S
Enter input string to search:  
No match found.

Enter your regex: \S
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: \w
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: \w
Enter input string to search: !
No match found.

Enter your regex: \W
Enter input string to search: a
No match found.

Enter your regex: \W
Enter input string to search: !
I found the text "!" starting at index 0 and ending at index 1.

```

在前三个例子中，正则表达式很简单。（“点”元字符）表示“任何字符”。因此，在所有三种情况下（随机选择的`@`字符，数字和字母）匹配成功。其余示例均使用 [Predefined Character Classes table](https://docs.oracle.com/javase/tutorial/essential/regex/pre_char_classes.html#CHART) 表中的单个正则表达式构造。您可以参考此表来确定每个匹配背后的逻辑：

- `\d` 匹配所有数字
- `\s` 匹配空格
- `\w` 匹配单词字符

或者，大写字母意思相反：

- `\D` 匹配非数字
- `\S` 匹配非空格
- `\W` 匹配非单词字符