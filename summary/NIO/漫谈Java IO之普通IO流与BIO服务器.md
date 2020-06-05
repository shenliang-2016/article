# [漫谈Java IO之普通IO流与BIO服务器](https://www.cnblogs.com/xing901022/p/8666147.html)

> 今天来复习一下基础IO，也就是最普通的IO。

1. [网络IO的基本知识与概念](http://www.cnblogs.com/xing901022/p/8659436.html)
2. [普通IO以及BIO服务器](http://www.cnblogs.com/xing901022/p/8666147.html)
3. [NIO的使用与服务器Hello world](http://www.cnblogs.com/xing901022/p/8672418.html)
4. [Netty的使用与服务器Hello world](http://www.cnblogs.com/xing901022/p/8678869.html)

## 输入流与输出流

Java的输入流和输出流，按照输入输出的单元不同，又可以分为字节流和字符流的。
![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180328-201414@2x.jpg)

JDK提供了很多输入流和输出流，比如：

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_IO%e6%b5%81%e7%9a%84%e5%85%b3%e7%b3%bb%e5%9b%be.png)

字节流可以按照不同的变量类型进行读写，而字符流则是基于字符编码的。不同的字符编码包含的字节数是不一样的，因此在使用字符流时，一定要注意编码的问题。

## 读写

### 字节的输入输出流操作

```java
// 字节输入流操作
InputStream input = new ByteArrayInputStream("abcd".getBytes());
int data = input.read();
while(data != -1){
    System.out.println((char)data);
    data = input.read();
}

// 字节输出流
ByteArrayOutputStream output = new ByteArrayOutputStream();
output.write("12345".getBytes());
byte[] ob = output.toByteArray();
```

### 字符的输入输出流操作

```java
// 字符输入流操作
Reader reader = new CharArrayReader("abcd".toCharArray());
data = reader.read();
while(data != -1){
    System.out.println((char)data);
    data = reader.read();
}
// 字符输出流
CharArrayWriter writer = new CharArrayWriter();
writer.write("12345".toCharArray());
char[] wc = writer.toCharArray();
```

### 关闭流

流打开后，相当于占用了一个文件的资源，需要及时的释放。传统的标准关闭的方式为：

```java
// 字节输入流操作
InputStream input = null;
try {
    input = new ByteArrayInputStream("abcd".getBytes());
    int data = input.read();
    while (data != -1) {
        System.out.println((char) data);
        // todo
        data = input.read();
    }
}catch(Exception e){
    // todo
}finally {
    if(input != null) {
        try {
            input.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

在JDK1.7后引入了try-with-resources的语法，可以在跳出try{}的时候直接自动释放：

```java
try(InputStream input1 = new ByteArrayInputStream("abcd".getBytes())){
   //

}catch (Exception e){
    //
}
```

## IOUtils

直接使用IO的API还是很麻烦的，网上的大多数教程都是各种while循环，操作很麻烦。其实apache common已经提供了一个工具类——IOUtils，可以方便的进行IO操作。

比如`IOUtils.readLines(is, Charset.forName("UTF-8"));`可以方便的按照一行一行读取.

## BIO阻塞服务器

基于原始的IO和Socket就可以编写一个最基本的BIO服务器。

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180328-202911@2x.jpg)

**概要：** 这个模型很简单，就是主线程（Acceptor）负责接收连接，然后开启新的线程专门负责连接处理客户端的请求。

```java
import io.netty.util.CharsetUtil;

import java.io.IOException;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class PlainOioServer {
    public void serve(int port) throws IOException {
        // 开启Socket服务器，并监听端口
        final ServerSocket socket = new ServerSocket(port);
        try{
            for(;;){
                // 轮训接收监听
                final Socket clientSocket = socket.accept();
                try {
                    Thread.sleep(500000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println("accepted connection from "+clientSocket);
                // 创建新线程处理请求
                new Thread(()->{
                   OutputStream out;
                   try{
                       out = clientSocket.getOutputStream();
                       out.write("Hi\r\n".getBytes(CharsetUtil.UTF_8));
                       out.flush();
                   } catch (IOException e) {
                       e.printStackTrace();
                   } finally {
                       try{
                           clientSocket.close();
                       } catch (IOException e) {
                           e.printStackTrace();
                       }
                   }
                }).start();
            }
        } catch (IOException e){
            e.printStackTrace();
        }
    }
    public static void main(String[] args) throws IOException {
        PlainOioServer server = new PlainOioServer();
        server.serve(5555);
    }
}
```

然后执行`telnet localhost 5555`，就能看到返回结果了。

这种阻塞模式的服务器，原理上很简单，问题也容易就暴露出来：

1. 服务端与客户端的连接相当于1:1，因此如果连接数上升，服务器的压力会很大
2. 如果主线程Acceptor阻塞，那么整个服务器将会阻塞，单点问题严重
3. 线程数膨胀后，整个服务器性能都会下降

改进的方式可以基于**线程池**或者**消息队列**，不过也存在一些问题：

1. 线程池的数量、消息队列后端服务器并发处理数，都是并发数的限制
2. 仍然存在Acceptor的单点阻塞问题

接下来，将会介绍基于Nio的非阻塞服务器模式，如果忘记什么是IO多路复用，可以回顾前面一篇分享。敬请期待吧...

作者：[xingoo](http://www.cnblogs.com/xing901022)

出处：[http://www.cnblogs.com/xing901022](http://www.cnblogs.com/xing901022)

本文版权归作者和博客园共有。欢迎转载，但必须保留此段声明，且在文章页面明显位置给出原文连接！