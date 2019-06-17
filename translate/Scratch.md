#### 随机存取文件

*随机访问文件*允许对文件内容进行非顺序或随机访问。要随机访问文件，请打开文件，查找特定位置，然后读取或写入该文件。

使用 [`SeekableByteChannel`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html) 接口可以实现此功能。 `SeekableByteChannel`接口使用当前位置的概念扩展通道 I/O. 使用方法可以设置或查询位置，然后可以从该位置读取数据或将数据写入该位置。API由一些易于使用的方法组成：

- [`position`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#position--) – 返回通道的当前位置
- [`position(long)`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#position-long-) – 设定通道的当前位置
- [`read(ByteBuffer)`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#read-java.nio.ByteBuffer-) – 从通道读取字节进入缓冲区
- [`write(ByteBuffer)`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#write-java.nio.ByteBuffer-) – 将缓冲区中的字节写入通道
- [`truncate(long)`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/SeekableByteChannel.html#truncate-long-) – 切断文件（或者其它实体）与通道的联系

[使用通道 I/O 读取和写入文件](https://docs.oracle.com/javase/tutorial/essential/io/file.html#channelio)  展示了`Path.newByteChannel`方法返回`SeekableByteChannel`的实例。在默认文件系统上，您可以按原样使用该通道，也可以将其强制转换为 [`FileChannel`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/FileChannel.html) ，以便访问更高级的功能，例如将文件区域直接映射到内存中以便更快地访问，锁定文件区域，或从绝对位置读取和写入字节而不影响通道的当前位置。

以下代码段使用`newByteChannel`方法之一打开用于读取和写入的文件。返回的`SeekableByteChannel`将强制转换为`FileChannel`。然后，从文件的开头读取12个字节，字符串 "I was here!" 是在那个地方写的。文件中的当前位置移动到末尾，并附加从开头的12个字节。最后，字符串， "I was here!" 附加，并关闭文件上的通道。

```java
String s = "I was here!\n";
byte data[] = s.getBytes();
ByteBuffer out = ByteBuffer.wrap(data);

ByteBuffer copy = ByteBuffer.allocate(12);

try (FileChannel fc = (FileChannel.open(file, READ, WRITE))) {
    // Read the first 12
    // bytes of the file.
    int nread;
    do {
        nread = fc.read(copy);
    } while (nread != -1 && copy.hasRemaining());

    // Write "I was here!" at the beginning of the file.
    fc.position(0);
    while (out.hasRemaining())
        fc.write(out);
    out.rewind();

    // Move to the end of the file.  Copy the first 12 bytes to
    // the end of the file.  Then write "I was here!" again.
    long length = fc.size();
    fc.position(length-1);
    copy.flip();
    while (copy.hasRemaining())
        fc.write(copy);
    while (out.hasRemaining())
        fc.write(out);
} catch (IOException x) {
    System.out.println("I/O Exception: " + x);
}
```

