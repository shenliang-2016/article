### 字符类

如果浏览 [`Pattern`](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) 类规范，您将看到总结支持的正则表达式构造的表。在“字符类”部分中，您将找到以下内容：

| Construct       | Description                              |
| --------------- | ---------------------------------------- |
| `[abc]`         | a, b, or c (simple class)                |
| `[^abc]`        | Any character except a, b, or c (negation) |
| `[a-zA-Z]`      | a through z, or A through Z, inclusive (range) |
| `[a-d[m-p]]`    | a through d, or m through p: [a-dm-p] (union) |
| `[a-z&&[def]]`  | d, e, or f (intersection)                |
| `[a-z&&[^bc]]`  | a through z, except for b and c: [ad-z] (subtraction) |
| `[a-z&&[^m-p]]` | a through z, and not m through p: [a-lq-z] (subtraction) |

左侧列指定正则表达式构造，而右侧列描述每个构造将匹配的条件。

----

**注意：** 短语“character class”中的“class”一词不是指`.class`文件。在正则表达式的上下文中，*字符类*是括在方括号内的一组字符。它指定将成功匹配给定输入字符串中的单个字符的字符。

----

**简单类**

字符类的最基本形式是简单地将一组字符并排放在方括号内。例如，正则表达式`[bcr]at`将匹配单词“bat”，“cat”或“rat”，因为它定义了一个字符类（接受“b”，“c”或“r”）作为其第一个字符。

```
Enter your regex: [bcr]at
Enter input string to search: bat
I found the text "bat" starting at index 0 and ending at index 3.

Enter your regex: [bcr]at
Enter input string to search: cat
I found the text "cat" starting at index 0 and ending at index 3.

Enter your regex: [bcr]at
Enter input string to search: rat
I found the text "rat" starting at index 0 and ending at index 3.

Enter your regex: [bcr]at
Enter input string to search: hat
No match found.
```

在上面的示例中，只有当第一个字母与字符类定义的字符之一匹配时，整体匹配才会成功。

**Negation**

要匹配除列出的字符以外的所有字符，请在字符类的开头插入“`^`”元字符。这种技术称为*否定*。

```
Enter your regex: [^bcr]at
Enter input string to search: bat
No match found.

Enter your regex: [^bcr]at
Enter input string to search: cat
No match found.

Enter your regex: [^bcr]at
Enter input string to search: rat
No match found.

Enter your regex: [^bcr]at
Enter input string to search: hat
I found the text "hat" starting at index 0 and ending at index 3.
```

仅当输入字符串的第一个字符不包含字符类定义的任何字符时，匹配才会成功。

**Ranges**

有时您需要定义一个包含一系列值的字符类，例如字母“a到h”或数字“1到5”。要指定范围，只需在要匹配的第一个和最后一个字符之间插入“ - ”元字符，例如`[1-5]`或`[a-h]`。您还可以在类中将不同的范围放在彼此旁边，以进一步扩展匹配的可能性。例如，`[a-zA-Z]`将匹配字母表中的任何字母：a到z（小写）或A到Z（大写）。

以下是范围和否定的一些示例：

```
Enter your regex: [a-c]
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.

Enter your regex: [a-c]
Enter input string to search: b
I found the text "b" starting at index 0 and ending at index 1.

Enter your regex: [a-c]
Enter input string to search: c
I found the text "c" starting at index 0 and ending at index 1.

Enter your regex: [a-c]
Enter input string to search: d
No match found.

Enter your regex: foo[1-5]
Enter input string to search: foo1
I found the text "foo1" starting at index 0 and ending at index 4.

Enter your regex: foo[1-5]
Enter input string to search: foo5
I found the text "foo5" starting at index 0 and ending at index 4.

Enter your regex: foo[1-5]
Enter input string to search: foo6
No match found.

Enter your regex: foo[^1-5]
Enter input string to search: foo1
No match found.

Enter your regex: foo[^1-5]
Enter input string to search: foo6
I found the text "foo6" starting at index 0 and ending at index 4.
```

**Unions**

您还可以使用联合创建由两个或多个单独的字符类组成的单个字符类。要创建联合，只需将一个类嵌套在另一个类中，例如`[0-4 [6-8]]`。此特定联合创建一个与数字0,1,2,3,4,6,7和8匹配的单个字符类。

```
Enter your regex: [0-4[6-8]]
Enter input string to search: 0
I found the text "0" starting at index 0 and ending at index 1.

Enter your regex: [0-4[6-8]]
Enter input string to search: 5
No match found.

Enter your regex: [0-4[6-8]]
Enter input string to search: 6
I found the text "6" starting at index 0 and ending at index 1.

Enter your regex: [0-4[6-8]]
Enter input string to search: 8
I found the text "8" starting at index 0 and ending at index 1.

Enter your regex: [0-4[6-8]]
Enter input string to search: 9
No match found.
```

**Intersections**

要创建仅匹配其所有嵌套类共有的字符的单个字符类，请使用`&&`，如`[0-9&&[345]]`中所示。此特定交集创建单个字符类，仅匹配两个字符类共有的数字：3,4和5。

```
Enter your regex: [0-9&&[345]]
Enter input string to search: 3
I found the text "3" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[345]]
Enter input string to search: 4
I found the text "4" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[345]]
Enter input string to search: 5
I found the text "5" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[345]]
Enter input string to search: 2
No match found.

Enter your regex: [0-9&&[345]]
Enter input string to search: 6
No match found.
```

这是一个显示两个范围交集的示例：

```
Enter your regex: [2-8&&[4-6]]
Enter input string to search: 3
No match found.

Enter your regex: [2-8&&[4-6]]
Enter input string to search: 4
I found the text "4" starting at index 0 and ending at index 1.

Enter your regex: [2-8&&[4-6]]
Enter input string to search: 5
I found the text "5" starting at index 0 and ending at index 1.

Enter your regex: [2-8&&[4-6]]
Enter input string to search: 6
I found the text "6" starting at index 0 and ending at index 1.

Enter your regex: [2-8&&[4-6]]
Enter input string to search: 7
No match found.
```

**Subtraction**

最后，您可以使用减法来否定一个或多个嵌套字符类，例如`[0-9&&[^345]]`。此示例创建一个匹配0到9之间的所有字符类，但数字3,4和5除外。

```
Enter your regex: [0-9&&[^345]]
Enter input string to search: 2
I found the text "2" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 3
No match found.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 4
No match found.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 5
No match found.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 6
I found the text "6" starting at index 0 and ending at index 1.

Enter your regex: [0-9&&[^345]]
Enter input string to search: 9
I found the text "9" starting at index 0 and ending at index 1.
```

现在我们已经介绍了如何创建字符类，您可能需要在继续下一部分之前查看 [Character Classes table](https://docs.oracle.com/javase/tutorial/essential/regex/char_classes.html#CHART) 。

