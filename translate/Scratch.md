### 边界匹配

到目前为止，我们只关心在特定输入字符串中的某个位置是否找到匹配项。我们从不关心匹配发生在输入字符串的哪个位置。

通过使用边界匹配器指定此类信息，可以使模式匹配更精确。例如，您可能对查找特定单词感兴趣，但前提是它出现在行的开头或结尾。或者您可能想知道匹配是在单词边界上还是在上一次匹配结束时发生。

下表列出并解释了所有边界匹配器。

| Boundary Construct | Description                              |
| ------------------ | ---------------------------------------- |
| `^`                | The beginning of a line                  |
| `$`                | The end of a line                        |
| `\b`               | A word boundary                          |
| `\B`               | A non-word boundary                      |
| `\A`               | The beginning of the input               |
| `\G`               | The end of the previous match            |
| `\Z`               | The end of the input but for the final terminator, if any |
| `\z`               | The end of the input                     |

以下示例演示了边界匹配器`^`和`$`的使用。如上所述，`^`匹配行的开头，`$`匹配结束。

```
Enter your regex: ^dog$
Enter input string to search: dog
I found the text "dog" starting at index 0 and ending at index 3.

Enter your regex: ^dog$
Enter input string to search:       dog
No match found.

Enter your regex: \s*dog$
Enter input string to search:             dog
I found the text "            dog" starting at index 0 and ending at index 15.

Enter your regex: ^dog\w*
Enter input string to search: dogblahblah
I found the text "dogblahblah" starting at index 0 and ending at index 11.
```

第一个示例是成功的，因为模式占用整个输入字符串。第二个示例失败，因为输入字符串在开头包含额外的空格。第三个示例指定一个表达式，该表达式允许无限制的空格，后面是行尾的“dog”。第四个例子要求“dog”出现在一行的开头，后跟无限数量的单词字符。

要检查模式是否在单词边界上开始和结束（与较长字符串中的子字符串相对），可在任一侧使用`\b`；例如，`\bdog\b` 。

```
Enter your regex: \bdog\b
Enter input string to search: The dog plays in the yard.
I found the text "dog" starting at index 4 and ending at index 7.

Enter your regex: \bdog\b
Enter input string to search: The doggie plays in the yard.
No match found.
```

要匹配非单词边界上的表达式，请使用`\B`代替：

```
Enter your regex: \bdog\B
Enter input string to search: The dog plays in the yard.
No match found.

Enter your regex: \bdog\B
Enter input string to search: The doggie plays in the yard.
I found the text "dog" starting at index 4 and ending at index 7.
```

要求匹配仅在上一个匹配结束时发生，请使用`\G`：

```
Enter your regex: dog 
Enter input string to search: dog dog
I found the text "dog" starting at index 0 and ending at index 3.
I found the text "dog" starting at index 4 and ending at index 7.

Enter your regex: \Gdog 
Enter input string to search: dog dog
I found the text "dog" starting at index 0 and ending at index 3.
```

这里第二个例子只找到一个匹配，因为第二次出现的“dog”不会在上一个匹配结束时开始。

