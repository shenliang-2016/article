#### 数据流

数据流支持原始数据类型值（`boolean`，`char`，`byte`，`short`，`int`，`long`，`float`和`double`）以及`String`值的二进制 I/O 。所有数据流都实现`DataInput`接口或`DataOutput`接口。本节重点介绍这些接口最广泛使用的实现 [`DataInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/DataInputStream.html) 和 [`DataOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html) 。

 [`DataStreams`](https://docs.oracle.com/javase/tutorial/essential/io/examples/DataStreams.java) 示例通过写出一组数据记录然后再次读取它们来演示数据流。每条记录包含三个与发票上的项目相关的值，如下表所示：

| Order in record | Data type | Data description | Output Method                  | Input Method                 | Sample Value     |
| --------------- | --------- | ---------------- | ------------------------------ | ---------------------------- | ---------------- |
| 1               | `double`  | Item price       | `DataOutputStream.writeDouble` | `DataInputStream.readDouble` | `19.99`          |
| 2               | `int`     | Unit count       | `DataOutputStream.writeInt`    | `DataInputStream.readInt`    | `12`             |
| 3               | `String`  | Item description | `DataOutputStream.writeUTF`    | `DataInputStream.readUTF`    | `"Java T-Shirt"` |

我们来看看`DataStreams`中的关键代码。首先，程序定义了一些常量，包含数据文件的名称和将写入的数据：

```java
static final String dataFile = "invoicedata";

static final double[] prices = { 19.99, 9.99, 15.99, 3.99, 4.99 };
static final int[] units = { 12, 8, 13, 29, 50 };
static final String[] descs = {
    "Java T-shirt",
    "Java Mug",
    "Duke Juggling Dolls",
    "Java Pin",
    "Java Key Chain"
};
```

然后`DataStreams`打开输出流。由于`DataOutputStream`只能作为现有字节流对象的包装器创建，因此`DataStreams`提供带缓冲的文件输出字节流。

```java
out = new DataOutputStream(new BufferedOutputStream(
              new FileOutputStream(dataFile)));
```

`DataStreams`写出记录并关闭输出流。

```java
for (int i = 0; i < prices.length; i ++) {
    out.writeDouble(prices[i]);
    out.writeInt(units[i]);
    out.writeUTF(descs[i]);
}
```

`writeUTF`方法以`UTF-8`的改进形式写出`String`值。这是一个可变宽度的字符编码，只需要一个字节表示常见的西方字符。

现在，`DataStreams`再次读回数据。首先，它必须提供输入流和变量来保存输入数据。与`DataOutputStream`一样，`DataInputStream`必须构造为字节流的包装器。

```java
in = new DataInputStream(new
            BufferedInputStream(new FileInputStream(dataFile)));

double price;
int unit;
String desc;
double total = 0.0;
```

现在，`DataStreams`可以读取流中的每条记录，报告它遇到的数据。

```java
try {
    while (true) {
        price = in.readDouble();
        unit = in.readInt();
        desc = in.readUTF();
        System.out.format("You ordered %d" + " units of %s at $%.2f%n",
            unit, desc, price);
        total += unit * price;
    }
} catch (EOFException e) {
}
```

请注意，`DataStreams`通过捕获 [`EOFException`](https://docs.oracle.com/javase/8/docs/api/java/io/EOFException.html)来检测文件结束条件，而不是测试无效的返回值。`DataInput`方法的所有实现都使用`EOFException`而不是返回值。

另请注意，`DataStream`中的每个特定`write`都与相应的特定`read`完全匹配。程序员需要确保输出类型和输入类型以这种方式匹配：输入流由简单的二进制数据组成，没有任何内容可以指示单个值的类型，或者它们在流中开始的位置。

`DataStreams`使用一种非常糟糕的编程技术：它使用浮点数来表示货币值。通常，浮点对于精确值是不利的。对于小数分数尤其不好，因为常见的数值（例如`0.1`）没有二进制表示。

表示货币值的正确类型是`java.math.BigDecimal`。不幸的是，`BigDecimal`是一种对象类型，因此它不适用于数据流。但是，`BigDecimal`将使用对象流，这将在下一节中介绍。