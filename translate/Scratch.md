下面是`String`类中其它操作字符串的一些方法：

| 方法                                       | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| `String[] split(String regex)`<br />`String[] split(String regex, int limit)` | 搜索由字符串参数（包含正则表达式）指定的匹配，并相应地将此字符串拆分为字符串数组。 可选的整数参数指定返回数组的最大大小。正则表达式在标题为“正则表达式”的课程中介绍。 |
| `CharSequence subSequence(int beginIndex, int endIndex) | 返回从`beginIndex`索引构造的新字符序列，直到`endIndex - 1`。 |
| `String trim()`                          | 返回此字符串的副本，其中删除了前导和尾随空格。                  |
| `String toLowerCase()`<br />`String toUpperCase()` | 返回转换为小写或大写的此字符串的副本。如果不需要转换，则这些方法返回原始字符串。 |

**字符串中搜索字符和子串**

以下是一些其他`String`方法，用于查找字符串中的字符或子字符串。`String`类提供了访问器方法，这些方法返回特定字符或子字符串的字符串中的位置：`indexOf()`和`lastIndexOf()`。`indexOf()`方法从字符串的开头向前搜索，而`lastIndexOf()`方法从字符串的末尾向后搜索。如果未找到字符或子字符串，`indexOf()`和`lastIndexOf()`将返回 -1。

`String`类还提供了一个搜索方法`contains`，如果字符串包含特定的字符序列，则返回`true`。当您只需要知道字符串包含字符序列时，请使用此方法，但精确位置并不重要。

下表描述了各种字符串搜索方法。

| 方法                                       | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| `int indexOf(int ch)`<br />`int lastIndexOf(int ch)` | 返回指定字符的第一个（最后一次）出现的下标位置。                 |
| `int indexOf(int ch, int fromIndex)`<br />`int lastIndexOf(int ch, int fromIndex)` | 返回指定字符的第一个（最后一次）出现的下标位置，从指定的下标位置向前（向后）搜索。 |
| `int indexOf(String str)`<br />`int lastIndexOf(String str)` | 返回指定子字符串的第一个（最后一次）出现的下标位置。               |
| `int indexOf(String str, int fromIndex)`<br />`int lastIndexOf(String str, int fromIndex)` | 返回指定子字符串的第一个（最后一次）出现的下标位置，从指定的下标位置向前（向后）搜索。 |
| `boolean contains(CharSequence s)`       | 如果字符串包含指定的字符序列，则返回`true`。                |

------

**Note:** `CharSequence` 是`String` 类实现的一个接口。因此，你可以将字符串作为 `contains()` 方法的参数。

------

