### 转化非 Unicode 文本

在Java编程语言中，`char`值表示Unicode字符。Unicode是一种支持世界主要语言的16位字符编码。您可以在[Unicode Consortium网站](http://www.unicode.org/) 上了解有关Unicode标准的更多信息。

很少有文本编辑器支持Unicode文本输入。我们用来编写本节代码示例的文本编辑器仅支持ASCII字符，限制为7位。为了表示不能用ASCII表示的Unicode字符，例如 ö，我们使用了`\uXXXX`转义序列。转义序列中的每个“X”都是十六进制数字。以下示例显示如何使用转义序列表示 ö 字符：

```java
String str = "\u00F6";
char c = '\u00F6';
Character letter = new Character('\u00F6');
```

世界各地的系统使用各种字符编码。目前，这些编码很少符合Unicode。因为您的程序需要Unicode中的字符，所以它从系统获取的文本数据必须转换为Unicode，反之亦然。当文本文件的编码与Java虚拟机的默认文件编码匹配时，文本文件中的数据将自动转换为Unicode。您可以通过使用它创建`OutputStreamWriter`并询问其规范名称来识别默认文件编码：

```java
OutputStreamWriter out = new OutputStreamWriter(new ByteArrayOutputStream());
System.out.println(out.getEncoding());
```

如果默认文件编码与您要处理的文本数据的编码不同，则必须自己执行转换。处理来自其他国家/地区或计算平台的文本时，您可能需要执行此操作。

本节讨论用于将非Unicode文本转换为Unicode的API。在使用这些API之前，您应该验证是否支持要转换为Unicode的字符编码。支持的字符编码列表不是Java编程语言规范的一部分。因此，API支持的字符编码可能随平台而变化。要查看Java Development Kit支持哪些编码，请参阅 [Supported Encodings](https://docs.oracle.com/javase/8/docs/technotes/guides/intl/encoding.doc.html) 文档。

下面的内容描述了将非Unicode文本转换为Unicode的两种技术。您可以将非Unicode字节数组转换为`String`对象，反之亦然。或者，您可以在Unicode字符流和非Unicode文本的字节流之间进行转换。

**[字节编码和字符串](https://docs.oracle.com/javase/tutorial/i18n/text/string.html)**

本节介绍如何将非Unicode字节数组转换为`String`对象，反之亦然。

**[字符和字节流](https://docs.oracle.com/javase/tutorial/i18n/text/stream.html)**

在本节中，您将学习如何在Unicode字符流和非Unicode文本字节流之间进行转换。

#### 字节编码和字符串

如果字节数组包含非Unicode文本，则可以使用`String`构造函数方法之一将文本转换为Unicode。相反，您可以使用`String.getBytes`方法将`String`对象转换为非Unicode字符的字节数组。调用这些方法之一时，请将编码标识符指定为其中一个参数。

下面的示例将在UTF-8和Unicode之间转换字符。UTF-8是Unicode的传输格式，对UNIX文件系统是安全的。该示例的完整源代码位于文件[`StringConverter.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/StringConverter.java) 中。

`StringConverter`程序首先创建一个包含Unicode字符的`String`：

```java
String original = new String("A" + "\u00ea" + "\u00f1" + "\u00fc" + "C");
```

打印时，名为`original`的`String`显示为：

```
AêñüC
```

要将`String`对象转换为UTF-8，请调用`getBytes`方法并将相应的编码标识符指定为参数。 `getBytes`方法返回UTF-8格式的字节数组。要从非Unicode字节数组创建`String`对象，请使用`encoding`参数调用`String`构造函数。进行这些调用的代码包含在`try`块中，以防指定的编码不受支持：

```java
try {
    byte[] utf8Bytes = original.getBytes("UTF8");
    byte[] defaultBytes = original.getBytes();

    String roundTrip = new String(utf8Bytes, "UTF8");
    System.out.println("roundTrip = " + roundTrip);
    System.out.println();
    printBytes(utf8Bytes, "utf8Bytes");
    System.out.println();
    printBytes(defaultBytes, "defaultBytes");
} 
catch (UnsupportedEncodingException e) {
    e.printStackTrace();
}
```

`StringConverter`程序打印出`utf8Bytes`和`defaultBytes`数组中的值以演示一个重要的点：转换后的文本的长度可能与源文本的长度不同。一些Unicode字符转换为单个字节，其他字符转换为成两字节或三字节字节。

`printBytes`方法通过调用`byteToHex`方法显示字节数组，该方法在源文件中定义，[`UnicodeFormatter.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/UnicodeFormatter.java) 。这是`printBytes`方法：

```java
public static void printBytes(byte[] array, String name) {
    for (int k = 0; k < array.length; k++) {
        System.out.println(name + "[" + k + "] = " + "0x" +
            UnicodeFormatter.byteToHex(array[k]));
    }
}
```

接下来是`printBytes`方法的输出。请注意，在两个数组中，只有第一个和最后一个字节A和C字符相同：

```
utf8Bytes[0] = 0x41
utf8Bytes[1] = 0xc3
utf8Bytes[2] = 0xaa
utf8Bytes[3] = 0xc3
utf8Bytes[4] = 0xb1
utf8Bytes[5] = 0xc3
utf8Bytes[6] = 0xbc
utf8Bytes[7] = 0x43
defaultBytes[0] = 0x41
defaultBytes[1] = 0xea
defaultBytes[2] = 0xf1
defaultBytes[3] = 0xfc
defaultBytes[4] = 0x43
```

#### 字符和字节流

`java.io`包提供了允许您在Unicode字符流和非Unicode文本的字节流之间进行转换的类。使用 [`InputStreamReader`](https://docs.oracle.com/javase/8/docs/api/java/io/InputStreamReader.html) 类，您可以将字节流转换为字符流。使用 [`OutputStreamWriter`](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStreamWriter.html) 类将字符流转换为字节流。下图说明了转换过程：

![This figure represents the conversion process](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-6.gif)

创建`InputStreamReader`和`OutputStreamWriter`对象时，指定要转换的字节编码。例如，要将UTF-8编码的文本文件转换为Unicode，您可以创建一个`InputStreamReader`，如下所示：

```java
FileInputStream fis = new FileInputStream("test.txt");
InputStreamReader isr = new InputStreamReader(fis, "UTF8");
```

如果省略编码标识符，`InputStreamReader`和`OutputStreamWriter`依赖于默认编码。您可以通过调用`getEncoding`方法来确定`InputStreamReader`或`OutputStreamWriter`使用的编码，如下所示：

```java
InputStreamReader defaultReader = new InputStreamReader(fis);
String defaultEncoding = defaultReader.getEncoding();
```

下面的示例向您展示了如何使用`InputStreamReader`和`OutputStreamWriter`类执行字符集转换。此示例的完整源代码位于[`StreamConverter.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/StreamConverter.java) 中。该程序显示日文字符。在尝试之前，请验证系统上是否安装了相应的字体。如果您使用的是与1.1版兼容的JDK软件，请复制`font.properties`文件，然后将其替换为`font.properties.ja`文件。

`StreamConverter`程序将一个Unicode字符序列从`String`对象转换为以UTF-8编码的字节的`FileOutputStream`。执行转换的方法称为`writeOutput`：

```java
static void writeOutput(String str) {
    try {
        FileOutputStream fos = new FileOutputStream("test.txt");
        Writer out = new OutputStreamWriter(fos, "UTF8");
        out.write(str);
        out.close();
    } 
    catch (IOException e) {
        e.printStackTrace();
    }
}
```

`readInput`方法从`writeOutput`方法创建的文件中读取以UTF-8编码的字节。 `InputStreamReader`对象将UTF-8中的字节转换为Unicode，并将结果返回给`String`。 `readInput`方法如下：

```java
static String readInput() {
    StringBuffer buffer = new StringBuffer();
    try {
        FileInputStream fis = new FileInputStream("test.txt");
        InputStreamReader isr = new InputStreamReader(fis, "UTF8");
        Reader in = new BufferedReader(isr);
        int ch;
        while ((ch = in.read()) > -1) {
            buffer.append((char)ch);
        }
        in.close();
        return buffer.toString();
    } 
    catch (IOException e) {
        e.printStackTrace();
        return null;
    }
}
```

`StreamConverter`程序的`main`方法调用`writeOutput`方法来创建以UTF-8编码的字节文件。 `readInput`方法读取相同的文件，将字节转换回Unicode。 这是`main`方法的源代码：

```java
public static void main(String[] args) {
    String jaString = new String("\u65e5\u672c\u8a9e\u6587\u5b57\u5217");
    writeOutput(jaString); 
    String inputString = readInput();
    String displayString = jaString + " " + inputString;
    new ShowString(displayString, "Conversion Demo");
}
```

原始字符串（`jaString`）应该与新创建的字符串（`inputString`）相同。为了显示两个字符串是相同的，程序将它们连接起来并用`ShowString`对象显示它们。 `ShowString`类显示带有`Graphics.drawString`方法的字符串。该类的源代码位于 [`ShowString.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ShowString.java) 中。当`StreamConverter`程序实例化`ShowString`时，会出现以下窗口。显示的字符重复验证两个字符串是否相同：

![This is a screens hot of the StreamConverter program](https://docs.oracle.com/javase/tutorial/figures/i18n/conversion.gif)

