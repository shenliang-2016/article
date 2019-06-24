### Quantifiers

*量词*允许您指定要匹配的出现次数。为方便起见，下面介绍了描述贪婪，不情愿和占有量词的Pattern API规范的三个部分。乍一看，似乎量词`X?`，`X??` 和`X?+`完全相同，因为它们都承诺匹配“X，一次或根本不匹配”。有一些细微的实现差异，将在本节末尾解释。

| Greedy   | Reluctant | Possessive | Meaning                                  |
| -------- | --------- | ---------- | ---------------------------------------- |
| `X?`     | `X??`     | `X?+`      | `X`, once or not at all                  |
| `X*`     | `X*?`     | `X*+`      | `X`, zero or more times                  |
| `X+`     | `X+?`     | `X++`      | `X`, one or more times                   |
| `X{n}`   | `X{n}?`   | `X{n}+`    | `X`, exactly *n* times                   |
| `X{n,}`  | `X{n,}?`  | `X{n,}+`   | `X`, at least *n* times                  |
| `X{n,m}` | `X{n,m}?` | `X{n,m}+`  | `X`, at least *n* but not more than *m* times |

让我们通过创建三个不同的正则表达式来开始我们对贪婪量词的看法：字母“a”后跟`?`，`*`或`+`。让我们看看当这些表达式针对空输入字符串`“”`进行测试时会发生什么：

```
Enter your regex: a?
Enter input string to search: 
I found the text "" starting at index 0 and ending at index 0.

Enter your regex: a*
Enter input string to search: 
I found the text "" starting at index 0 and ending at index 0.

Enter your regex: a+
Enter input string to search: 
No match found.
```

**0-长度匹配**

在上面的例子中，匹配在前两种情况下是成功的，因为表达式`a?`和`a*`都允许字母a出现零次。您还会注意到开始和结束索引都是零，这与我们到目前为止看到的任何示例都不同。空输入字符串`“”`没有长度，因此测试只是匹配索引0处的任何内容。此类匹配称为零长度匹配。在以下几种情况下可能发生零长度匹配：在空输入字符串中，在输入字符串的开头，在输入字符串的最后一个字符之后，或在输入字符串的任意两个字符之间。零长度匹配很容易识别，因为它们始终在相同的索引位置开始和结束。

让我们通过几个例子来探索零长度匹配。将输入字符串更改为单个字母“a”，您会注意到一些有趣的内容：

```
Enter your regex: a?
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.
I found the text "" starting at index 1 and ending at index 1.

Enter your regex: a*
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.
I found the text "" starting at index 1 and ending at index 1.

Enter your regex: a+
Enter input string to search: a
I found the text "a" starting at index 0 and ending at index 1.
```

所有三个量词都找到了字母“a”，但前两个也在索引1处找到了零长度匹配；也就是说，在输入字符串的最后一个字符之后。请记住，匹配器将字符“a”视为位于索引0和索引1之间的单元格中，并且我们的测试工具循环直到它无法再找到匹配项。根据所使用的量词，最后一个字符后索引处“无”的存在可能触发也可能不触发匹配。

现在将输入字符串更改为连续五个字母“a”，您将获得以下内容：

```
Enter your regex: a?
Enter input string to search: aaaaa
I found the text "a" starting at index 0 and ending at index 1.
I found the text "a" starting at index 1 and ending at index 2.
I found the text "a" starting at index 2 and ending at index 3.
I found the text "a" starting at index 3 and ending at index 4.
I found the text "a" starting at index 4 and ending at index 5.
I found the text "" starting at index 5 and ending at index 5.

Enter your regex: a*
Enter input string to search: aaaaa
I found the text "aaaaa" starting at index 0 and ending at index 5.
I found the text "" starting at index 5 and ending at index 5.

Enter your regex: a+
Enter input string to search: aaaaa
I found the text "aaaaa" starting at index 0 and ending at index 5.
```

表达式`a?` 找到每个字符的单独匹配，因为它匹配“a”出现零或一次。表达式`a*`找到两个单独的匹配：第一个匹配中的所有字母“a”，然后是索引5处的最后一个字符后的零长度匹配。最后，`a+`匹配所有出现的字母“a” ，忽略最后一个索引处“无”的存在。

此时，如果前两个量词遇到“a”以外的字母，您可能想知道结果会是什么。例如，如果遇到字母“b”会发生什么，如“ababaaaab”？

我们来看看：

```
Enter your regex: a?
Enter input string to search: ababaaaab
I found the text "a" starting at index 0 and ending at index 1.
I found the text "" starting at index 1 and ending at index 1.
I found the text "a" starting at index 2 and ending at index 3.
I found the text "" starting at index 3 and ending at index 3.
I found the text "a" starting at index 4 and ending at index 5.
I found the text "a" starting at index 5 and ending at index 6.
I found the text "a" starting at index 6 and ending at index 7.
I found the text "a" starting at index 7 and ending at index 8.
I found the text "" starting at index 8 and ending at index 8.
I found the text "" starting at index 9 and ending at index 9.

Enter your regex: a*
Enter input string to search: ababaaaab
I found the text "a" starting at index 0 and ending at index 1.
I found the text "" starting at index 1 and ending at index 1.
I found the text "a" starting at index 2 and ending at index 3.
I found the text "" starting at index 3 and ending at index 3.
I found the text "aaaa" starting at index 4 and ending at index 8.
I found the text "" starting at index 8 and ending at index 8.
I found the text "" starting at index 9 and ending at index 9.

Enter your regex: a+
Enter input string to search: ababaaaab
I found the text "a" starting at index 0 and ending at index 1.
I found the text "a" starting at index 2 and ending at index 3.
I found the text "aaaa" starting at index 4 and ending at index 8.
```

即使字母“b”出现在单元格1,3和8中，输出也会在这些位置报告零长度匹配。正则表达式`a?`不是专门寻找字母“b”；它只是在寻找字母“a”的存在（或缺少）。如果量词允许匹配“a”零次，则输入字符串中不是“a”的任何内容都将显示为零长度匹配。根据前面示例中讨论的规则匹配剩余的"a"。

要准确匹配模式n次，只需在大括号内指定一组数字：

```
Enter your regex: a{3}
Enter input string to search: aa
No match found.

Enter your regex: a{3}
Enter input string to search: aaa
I found the text "aaa" starting at index 0 and ending at index 3.

Enter your regex: a{3}
Enter input string to search: aaaa
I found the text "aaa" starting at index 0 and ending at index 3.
```

这里，正则表达式`a{3}`正在搜索连续三次出现的字母“a”。第一个测试失败，因为输入字符串没有足够的匹配。第二个测试在输入字符串中包含3个a，它会触发匹配。第三个测试也触发匹配，因为在输入字符串的开头恰好有3个a。接下来的任何事情都与第一次匹配无关。如果该模式应该在该位置之后再次出现，则会触发后续匹配：

```
Enter your regex: a{3}
Enter input string to search: aaaaaaaaa
I found the text "aaa" starting at index 0 and ending at index 3.
I found the text "aaa" starting at index 3 and ending at index 6.
I found the text "aaa" starting at index 6 and ending at index 9.
```

要求模式至少出现n次，请在数字后面添加逗号：

```
Enter your regex: a{3,}
Enter input string to search: aaaaaaaaa
I found the text "aaaaaaaaa" starting at index 0 and ending at index 9.
```

使用相同的输入字符串，此测试只找到一个匹配项，因为连续的9个a满足“至少”3个a的需要。

最后，要指定出现次数的上限，请在大括号内添加第二个数字：

```
Enter your regex: a{3,6} // find at least 3 (but no more than 6) a's in a row
Enter input string to search: aaaaaaaaa
I found the text "aaaaaa" starting at index 0 and ending at index 6.
I found the text "aaa" starting at index 6 and ending at index 9.
```

这里第一次匹配被迫停在6个字符的上限。第二次匹配包括遗留的任何内容，恰好是三个a  - 这次匹配允许的最小字符数。如果输入字符串是一个较短的字符，则不会有第二个匹配，因为只剩下两个a。

**捕获组和字符类与量词**

到目前为止，我们只对包含一个字符的输入字符串测试了量词。实际上，量词只能一次附加到一个字符，因此正则表达式“abc+”表示“a，后跟b，后跟c一次或多次”。这并不意味着“abc”一次或多次。但是，量词也可以附加到字符类和捕获组，例如`[abc]+`（a或b或c，一次或多次）或`(abc)+`（组“abc”，一次或多次）。

让我们通过连续三次指定组`(dog)`来说明。

```
Enter your regex: (dog){3}
Enter input string to search: dogdogdogdogdogdog
I found the text "dogdogdog" starting at index 0 and ending at index 9.
I found the text "dogdogdog" starting at index 9 and ending at index 18.

Enter your regex: dog{3}
Enter input string to search: dogdogdogdogdogdog
No match found.
```

这里第一个例子找到三个匹配，因为量词适用于整个捕获组。但是，删除括号并且匹配失败，因为量词`{3}`现在仅适用于字母“g”。

同样，我们可以将量词应用于整个字符类：

```
Enter your regex: [abc]{3}
Enter input string to search: abccabaaaccbbbc
I found the text "abc" starting at index 0 and ending at index 3.
I found the text "cab" starting at index 3 and ending at index 6.
I found the text "aaa" starting at index 6 and ending at index 9.
I found the text "ccb" starting at index 9 and ending at index 12.
I found the text "bbc" starting at index 12 and ending at index 15.

Enter your regex: abc{3}
Enter input string to search: abccabaaaccbbbc
No match found.
```

这里量词`{3}`适用于第一个例子中的整个字符类，但仅适用于第二个中的字母“c”。

**贪婪、不情愿和占有量词之间的不同**

贪婪，不情愿和占有量词之间存在细微差别。

贪心量词被认为是“贪婪的”，因为它们在尝试第一次匹配之前强制匹配器读入或吃掉整个输入字符串。如果第一次匹配尝试（整个输入字符串）失败，匹配器将输入字符串后退一个字符并再次尝试，重复该过程直到找到匹配项或者没有剩余字符可以退出。根据表达式中使用的量词，它将尝试匹配的最后一件事是1或0个字符。

然而，不情愿的量词采用相反的方法：它们从输入字符串的开头开始，然后不情愿地一次吃一个字符寻找匹配。他们尝试的最后一件事是整个输入字符串。

最后，占有量词总是占用整个输入字符串，尝试一次（并且只有一次）匹配。与贪婪的量词不同，占有量词永远不会退缩，即使这样做也会使整体匹配成功。

为了说明，请考虑输入字符串`xfooxxxxxxfoo`。

```
Enter your regex: .*foo  // greedy quantifier
Enter input string to search: xfooxxxxxxfoo
I found the text "xfooxxxxxxfoo" starting at index 0 and ending at index 13.

Enter your regex: .*?foo  // reluctant quantifier
Enter input string to search: xfooxxxxxxfoo
I found the text "xfoo" starting at index 0 and ending at index 4.
I found the text "xxxxxxfoo" starting at index 4 and ending at index 13.

Enter your regex: .*+foo // possessive quantifier
Enter input string to search: xfooxxxxxxfoo
No match found.
```

第一个例子使用贪心量词`.*`来找到“任何字符”，零次或多次，然后是字母`“f” “o” “o”`。因为量词是贪婪的，所以表达式的`.*`部分首先会占用整个输入字符串。此时，整体表达式匹配不能成功，因为已经消耗了最后三个字母（`“f” “o” “o”`）。因此，匹配器一次缓慢地退回一个字母，直到最右边的“foo”被反刍到，此时匹配成功并且搜索结束。

然而，第二个例子是不情愿的，所以它首先消耗“没有”。因为“foo”没有出现在字符串的开头，所以它被强制吞下第一个字母（“x”），这会在0和4处触发第一个匹配。我们的测试工具继续前进直到输入字符串耗尽。它在4和13找到另一次匹配。

第三个例子找不到匹配，因为量词是占有性的。在这种情况下，整个输入字符串由`.*+`消耗，不留下任何东西以满足表达式末尾的“foo”。使用占有量词来表示你想要抓住所有东西而不会退缩的情况；在没有立即找到匹配的情况下，它将胜过等效的贪心量词。

