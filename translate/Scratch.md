### 捕获组

在上一节中，我们看到了量词如何附加到一个字符，字符类或捕获组。但到目前为止，我们还没有详细讨论过捕获组的概念。

捕获组是将多个字符视为一个单元的一种方法。它们是通过将要分组的字符放在一组括号中来创建的。例如，正则表达式`(dog)`创建一个包含字母“d”“o”和“g”的组。与捕获组匹配的输入字符串部分将保存在内存中，以便以后通过反向引用进行调用（如下面的 [反向引用](https://docs.oracle.com/javase/tutorial/essential/regex/groups.html#backref) 一节中所述）。

**编号**

如 [`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)  API中所述，捕获组通过从左到右计算它们的左括号来编号。例如，在表达式 `((A)(B(C)))`中，有四个这样的组：

1. `((A)(B(C)))`
2. `(A)`
3. `(B(C))`
4. `(C)`

要查找表达式中存在多少个组，请在匹配器对象上调用`groupCount`方法。`groupCount`方法返回一个`int`，显示匹配器模式中存在的捕获组数。在此示例中，`groupCount`将返回数字`4`，表示该模式包含4个捕获组。

还有一个特殊组，即组0，它始终代表整个表达式。该组未包含在`groupCount`报告的总数中。以 `(?`开头的组是纯粹的非捕获组，不捕获文本而不计入组总数。（稍后将在 [Methods of the Pattern Class](https://docs.oracle.com/javase/tutorial/essential/regex/pattern.html) 部分中看到非捕获组的示例。）

了解组的编号很重要，因为一些`Matcher`方法接受一个`int`，指定一个特定的组号作为参数：

- [`public int start(int group)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#start-int-): 返回在上一个匹配操作期间由给定组捕获的子序列的起始索引。
- [`public int end (int group)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#end-int-): 返回在上一个匹配操作期间由给定组捕获的子序列的最后一个字符的索引加1。
- [`public String group (int group)`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Matcher.html#group-int-): 返回在上一个匹配操作期间由给定组捕获的输入子序列。

**反向引用**

与捕获组匹配的输入字符串部分保存在内存中，以便以后通过反向引用进行调用。在正则表达式中将反向引用指定为反斜杠（`\`），后跟一个数字，指示要调用的组的编号。例如，表达式（`\d\d`）定义了一个匹配行中两个数字的捕获组，可以通过反向引用`\1`在表达式中稍后调用。

要匹配任何2位数字，后跟完全相同的两位数字，您可以使用`(\d\d)\1`作为正则表达式：

```
Enter your regex: (\d\d)\1
Enter input string to search: 1212
I found the text "1212" starting at index 0 and ending at index 4.
```

如果更改最后两位数，则匹配将失败：

```
Enter your regex: (\d\d)\1
Enter input string to search: 1234
No match found.
```

对于嵌套捕获组，反向引用的工作方式完全相同：指定反斜杠后跟要调用的组的编号。

