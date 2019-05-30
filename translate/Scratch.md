**替换字符串中的字符或者子串**

`String`类只有很少的方法可以将字符或子字符串插入到字符串中。通常，不需要它们：您可以通过连接从字符串中删除特定子字符串之后剩余的子字符串、或者要插入的子字符串来创建新字符串。

但是，`String`类确实有四种方法可以替换找到的字符或子字符串。 它们是：

| Method                                   | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| `String replace(char oldChar, char newChar)` | 返回一个新字符串，该字符串是使用`newChar`替换此字符串中所有出现的`oldChar`。 |
| `String replace(CharSequence target, CharSequence replacement)` | 将与该文字目标序列匹配的此字符串的每个子字符串替换为指定的文字替换序列。     |
| `String replaceAll(String regex, String replacement)` | 将给定替换的给定正则表达式匹配的此字符串的每个子字符串替换。           |
| `String replaceFirst(String regex, String replacement)` | 将给定替换的给定正则表达式匹配的此字符串的第一个子字符串替换。          |

**例子**

````java
public class Filename {
    private String fullPath;
    private char pathSeparator, 
                 extensionSeparator;

    public Filename(String str, char sep, char ext) {
        fullPath = str;
        pathSeparator = sep;
        extensionSeparator = ext;
    }

    public String extension() {
        int dot = fullPath.lastIndexOf(extensionSeparator);
        return fullPath.substring(dot + 1);
    }

    // gets filename without extension
    public String filename() {
        int dot = fullPath.lastIndexOf(extensionSeparator);
        int sep = fullPath.lastIndexOf(pathSeparator);
        return fullPath.substring(sep + 1, dot);
    }

    public String path() {
        int sep = fullPath.lastIndexOf(pathSeparator);
        return fullPath.substring(0, sep);
    }
}
````

下面的程序使用了上面的类：

````java
public class FilenameDemo {
    public static void main(String[] args) {
        final String FPATH = "/home/user/index.html";
        Filename myHomePage = new Filename(FPATH, '/', '.');
        System.out.println("Extension = " + myHomePage.extension());
        System.out.println("Filename = " + myHomePage.filename());
        System.out.println("Path = " + myHomePage.path());
    }
}
````

程序输出：

````shell
Extension = html
Filename = index
Path = /home/user
````

如下图所示，我们的`extension`方法使用`lastIndexOf`来定位文件名中最后一次出现的句点。然后`substring`使用`lastIndexOf`的返回值来提取文件扩展名 - 即从句点到字符串结尾的子字符串。此代码假定文件名中包含句点；如果文件名没有句点，则`lastIndexOf`返回 -1，`substring`方法抛出`StringIndexOutOfBoundsException`。

![The use of lastIndexOf and substring in the extension method in the Filename class.](https://docs.oracle.com/javase/tutorial/figures/java/objects-lastIndexOf.gif)

另请注意，`extension`方法使用`dot + 1`作为`substring`的参数。如果句点字符是字符串的最后一个字符，则`dot + 1`等于字符串的长度，该字符串大于字符串中的最大索引（因为索引从0开始）。这是`substring`的合法参数，因为该方法接受的索引等于但不大于字符串的长度，并将其解释为“字符串的结尾”。



