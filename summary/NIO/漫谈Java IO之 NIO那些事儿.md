# [漫谈Java IO之 NIO那些事儿](https://www.cnblogs.com/xing901022/p/8672418.html)

> 前面一篇中已经介绍了基本IO的使用以及最简单的阻塞服务器的例子，本篇就来介绍下NIO的相关内容，前面的分享可以参考目录：

1. [网络IO的基本知识与概念](http://www.cnblogs.com/xing901022/p/8659436.html)
2. [普通IO以及BIO服务器](http://www.cnblogs.com/xing901022/p/8666147.html)
3. [NIO的使用与服务器Hello world](http://www.cnblogs.com/xing901022/p/8672418.html)
4. [Netty的使用与服务器Hello world](http://www.cnblogs.com/xing901022/p/8678869.html)

NIO，也叫做new-IO或者non-blocking-IO，就暂且理解为非阻塞IO吧。

### 为什么选择NIO

那么NIO相对于IO来说，有什么优势呢？总结来说：

1. IO是面向流的，数据只能从一端读取到另一端，不能随意读写。NIO则是面向缓冲区的，进行数据的操作更方便了。
2. IO是阻塞的，既浪费服务器的性能，也增加了服务器的风险；而NIO是非阻塞的。
3. NIO引入了IO多路复用器，效率上更高效了。

### NIO都有什么

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180329-134125.jpg)

那么NIO都提供了什么呢？

1. 基于缓冲区的双向管道，Channel和Buffer
2. IO多路复用器Selector
3. 更为易用的API

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180329-134053.jpg)

### Buffer的使用

在NIO中提供了各种不同的Buffer，最常用的就是ByteBuffer:

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180329-134819.jpg)

可以看到，他们都有几个比较重要的变量：

- capacity——容量，这个值是一开始申请就确定好的。类似c语言申请数组的大小。
- limit——剩余，在写模式下初始的时候等于capacity；在读模式下，等于最后一次写入的位置
- mark——标记位，标记一下position的位置，可以调用reset()方法回到这个位置。
- posistion——位置，写模式下表示开始写入的位置；读模式下表示开始读的位置

总结来说，NIO的Buffer有两种模式，读模式和写模式。刚上来就是写模式，使用flip()可以切换到读模式。

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180329-134902.jpg)

关于这几个位置的使用，可以参考下面的代码：

```java
public class ByteBufferTest {
    public static void main(String[] args) {

        ByteBuffer buffer = ByteBuffer.allocate(88);
        System.out.println(buffer);

        String value = "Netty权威指南";
        buffer.put(value.getBytes());
        System.out.println(buffer);

        buffer.flip();
        System.out.println(buffer);

        byte[] v = new byte[buffer.remaining()];
        buffer.get(v);

        System.out.println(buffer);
        System.out.println(new String(v));
    }
}
```

得到的输出为：

```
java.nio.HeapByteBuffer[pos=0 lim=88 cap=88]
java.nio.HeapByteBuffer[pos=17 lim=88 cap=88]
java.nio.HeapByteBuffer[pos=0 lim=17 cap=88]
java.nio.HeapByteBuffer[pos=17 lim=17 cap=88]
Netty权威指南
```

读者可以自己领会一下，这几个变量的含义。另外说明一点，如果遇到自己定义POJO类，就可以像这里的Buffer重载toString()方法，这样输出的时候就很方便了。

最后关于ByteBuffer在Channel中的使用，可以参考下面的代码：

```java
public class BufferTest {
    public static void main(String[] args) throws IOException {
        String file = "xxxx/test.txt";
        RandomAccessFile accessFile = new RandomAccessFile(file,"rw");
        FileChannel fileChannel = accessFile.getChannel();
        // 20个字节
        ByteBuffer buffer = ByteBuffer.allocate(20);
        int bytesRead = fileChannel.read(buffer);
        // buffer.put()也能写入buffer
        while(bytesRead!=-1){
            // 写切换到读
            buffer.flip();

            while(buffer.hasRemaining()){
                System.out.println((char)buffer.get());
            }

            // buffer.rewind()重新读
            // buffer.mark()标记position buffer.reset()恢复

            // 清除缓冲区
            buffer.clear();
            // buffer.compact(); 清楚读过的数据
            bytesRead = fileChannel.read(buffer);
        }
    }
}
```

这样，就熟悉了Channel和ByteBuffer的使用。接下来，看看服务器中的应用吧。

### NIO服务器例子

前面BIO的服务器，是来一个连接就创建一个新的线程响应。这里基于NIO的多路复用，可以这样写：

```java
import java.io.IOException;
import java.net.InetSocketAddress;
import java.net.ServerSocket;
import java.nio.ByteBuffer;
import java.nio.channels.SelectionKey;
import java.nio.channels.Selector;
import java.nio.channels.ServerSocketChannel;
import java.nio.channels.SocketChannel;
import java.util.Iterator;
import java.util.Set;

public class PlainNioServer {
    public void serve(int port) throws IOException {

        // 创建channel，并绑定监听端口
        ServerSocketChannel serverSocketChannel = ServerSocketChannel.open();
        serverSocketChannel.configureBlocking(false);
        ServerSocket ssocket = serverSocketChannel.socket();
        InetSocketAddress address = new InetSocketAddress(port);
        ssocket.bind(address);

        //创建selector,并将channel注册到selector
        Selector selector = Selector.open();
        serverSocketChannel.register(selector, SelectionKey.OP_ACCEPT);

        final ByteBuffer msg = ByteBuffer.wrap("Hi\r\b".getBytes());

        for(;;){
            try{
                selector.select();

            }catch (IOException e){
                e.printStackTrace();
                break;
            }

            Set<SelectionKey> readyKeys = selector.selectedKeys();
            Iterator<SelectionKey> iterator = readyKeys.iterator();

            while(iterator.hasNext()){
                SelectionKey key = iterator.next();
                iterator.remove();

                try{
                    if(key.isAcceptable()){
                        ServerSocketChannel server = (ServerSocketChannel)key.channel();
                        SocketChannel client=  server.accept();
                        client.configureBlocking(false);
                        client.register(selector, SelectionKey.OP_WRITE | SelectionKey.OP_READ, msg.duplicate());
                        System.out.println("accepted connection from "+client);
                    }

                    if(key.isWritable()){
                        SocketChannel client = (SocketChannel) key.channel();
                        ByteBuffer buffer = (ByteBuffer) key.attachment();
                        while(buffer.hasRemaining()){
                           if(client.write(buffer)==0){
                               break;
                           }
                        }
                        client.close();
                    }
                }catch (IOException e){
                    key.cancel();
                    try{
                        key.channel().close();
                    } catch (IOException ex){
                        ex.printStackTrace();
                    }
                }
            }

        }
    }

    public static void main(String[] args) throws IOException {
        PlainNioServer server = new PlainNioServer();
        server.serve(5555);
    }
}
```

这里抽象来说是下面的步骤：

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180329-140026.jpg)

1. 创建ServerSocketChannel并绑定端口
2. 创建Selector多路复用器，并注册Channel
3. 循环监听是否有感兴趣的事件发生selector.select();
4. 获得事件的句柄，并进行处理

其中Selector可以一次监听多个IO处理，效率就提高很多了。

作者：[xingoo](http://www.cnblogs.com/xing901022)

出处：[http://www.cnblogs.com/xing901022](http://www.cnblogs.com/xing901022)

本文版权归作者和博客园共有。欢迎转载，但必须保留此段声明，且在文章页面明显位置给出原文连接！