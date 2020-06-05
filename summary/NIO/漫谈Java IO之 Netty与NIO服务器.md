# [漫谈Java IO之 Netty与NIO服务器](https://www.cnblogs.com/xing901022/p/8678869.html)

> 前面介绍了基本的网络模型以及IO与NIO，那么有了NIO来开发非阻塞服务器，大家就满足了吗？有了技术支持，就回去追求效率，因此就产生了很多NIO的框架对NIO进行封装——这就是大名鼎鼎的Netty。

前几篇的内容，可以参考：

1. [网络IO的基本知识与概念](http://www.cnblogs.com/xing901022/p/8659436.html)
2. [普通IO以及BIO服务器](http://www.cnblogs.com/xing901022/p/8666147.html)
3. [NIO的使用与服务器Hello world](http://www.cnblogs.com/xing901022/p/8672418.html)
4. [Netty的使用与服务器Hello world](http://www.cnblogs.com/xing901022/p/8678869.html)

### 为什么要使用开源框架？

这个问题几乎可以当做废话，框架肯定要比一些原生的API封装了更多地功能，重复造轮子在追求效率的情况并不是明智之举。那么先来说说NIO有什么缺点吧：

1. NIO的类库和API还是有点复杂，比如Buffer的使用
2. Selector编写复杂，如果对某个事件注册后，业务代码过于耦合
3. 需要了解很多多线程的知识，熟悉网络编程
4. 面对断连重连、保丢失、粘包等，处理复杂
5. NIO存在BUG，根据网上言论说是selector空轮训导致CPU飙升，具体有兴趣的可以看看JDK的官网

那么有了这些问题，就急需一些大牛们开发通用框架来方便劳苦大众了。最致命的NIO框架就是MINA和Netty了，这里不得不说个小插曲：

先来看看**MINA**的主要贡献者：

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180330-150322.jpg)

再来看看**NETYY**的主要贡献者：

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180330-150316.jpg)

总结起来，有这么几点：

1. MINA和Netty的主要贡献者都是同一个人——Trustin lee，韩国Line公司的。
2. MINA于2006年开发，到14、15年左右，基本停止维护
3. Nety开始于2009年，目前仍由苹果公司的norman maurer在主要维护。
4. Norman Maurer是《Netty in Action》一书的作者

因此，如果让你选择你应该知道选择谁了吧。另外，MINA对底层系统要求功底更深，且国内Netty的氛围更好，有李林峰等人在大力宣传（《Netty权威指南》的作者）。

讲了一大堆的废话之后，总结来说就是——Netty有前途，学它准没错。

### Netty介绍

按照定义来说，Netty是一个异步、事件驱动的用来做高性能、高可靠性的网络应用框架。主要的优点有：

1. 框架设计优雅，底层模型随意切换适应不同的网络协议要求
2. 提供很多标准的协议、安全、编码解码的支持
3. 解决了很多NIO不易用的问题
4. 社区更为活跃，在很多开源框架中使用，如Dubbo、RocketMQ、Spark等

主要支持的功能或者特性有：
![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180330-151524.jpg)

1. 底层核心有：Zero-Copy-Capable Buffer，非常易用的灵拷贝Buffer（这个内容很有意思，稍后专门来说）；统一的API；标准可扩展的时间模型
2. 传输方面的支持有：管道通信（具体不知道干啥的，还请老司机指教）；Http隧道；TCP与UDP
3. 协议方面的支持有：基于原始文本和二进制的协议；解压缩；大文件传输；流媒体传输；protobuf编解码；安全认证；http和websocket

总之提供了很多现成的功能可以直接供开发者使用。

### Netty服务器小例子

基于Netty的服务器编程可以看做是Reactor模型：
![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180330-152213.jpg)
即包含一个接收连接的线程池（也有可能是单个线程，boss线程池）以及一个处理连接的线程池（worker线程池）。boss负责接收连接，并进行IO监听；worker负责后续的处理。为了便于理解Netty，直接看看代码:

```java
package cn.xingoo.book.netty.chap04;

import io.netty.bootstrap.ServerBootstrap;
import io.netty.buffer.ByteBuf;
import io.netty.buffer.Unpooled;
import io.netty.channel.*;
import io.netty.channel.nio.NioEventLoopGroup;
import io.netty.channel.socket.SocketChannel;
import io.netty.channel.socket.nio.NioServerSocketChannel;

import java.net.InetSocketAddress;
import java.nio.charset.Charset;

public class NettyNioServer {
    public void serve(int port) throws InterruptedException {
        final ByteBuf buffer = Unpooled.unreleasableBuffer(Unpooled.copiedBuffer("Hi\r\n", Charset.forName("UTF-8")));
		// 第一步，创建线程池
        EventLoopGroup bossGroup = new NioEventLoopGroup(1);
        EventLoopGroup workerGroup = new NioEventLoopGroup();

        try{
	        // 第二步，创建启动类
            ServerBootstrap b = new ServerBootstrap();
            // 第三步，配置各组件
            b.group(bossGroup, workerGroup)
                    .channel(NioServerSocketChannel.class)
                    .localAddress(new InetSocketAddress(port))
                    .childHandler(new ChannelInitializer<SocketChannel>() {
                        @Override
                        protected void initChannel(SocketChannel socketChannel) throws Exception {
                            socketChannel.pipeline().addLast(new ChannelInboundHandlerAdapter(){
                                @Override
                                public void channelActive(ChannelHandlerContext ctx) throws Exception {
                                    ctx.writeAndFlush(buffer.duplicate()).addListener(ChannelFutureListener.CLOSE);
                                }
                            });
                        }
                    });
            // 第四步，开启监听
            ChannelFuture f = b.bind().sync();
            f.channel().closeFuture().sync();
        } finally {
            bossGroup.shutdownGracefully().sync();
            workerGroup.shutdownGracefully().sync();
        }
    }

    public static void main(String[] args) throws InterruptedException {
        NettyNioServer server = new NettyNioServer();
        server.serve(5555);
    }
}
```

代码非常少，而且想要换成阻塞IO，只需要替换Channel里面的工厂类即可：

```java
public class NettyOioServer {
    public void serve(int port) throws InterruptedException {
        final ByteBuf buf = Unpooled.unreleasableBuffer(Unpooled.copiedBuffer("Hi\r\b", Charset.forName("UTF-8")));

        EventLoopGroup bossGroup = new OioEventLoopGroup(1);
        EventLoopGroup workerGroup = new OioEventLoopGroup();

        try{
            ServerBootstrap b = new ServerBootstrap();
            b.group(bossGroup, workerGroup)//配置boss和worker
                    .channel(OioServerSocketChannel.class) // 使用阻塞的SocketChannel
         ....
```

概括来说，在Netty中包含下面几个主要的组件：

- Bootstrap：netty的组件容器，用于把其他各个部分连接起来；如果是TCP的Server端，则为ServerBootstrap.
- Channel：代表一个Socket的连接
- EventLoopGroup：一个Group包含多个EventLoop，可以理解为线程池
- EventLoop：处理具体的Channel，一个EventLoop可以处理多个Channel
- ChannelPipeline：每个Channel绑定一个pipeline，在上面注册处理逻辑handler
- Handler：具体的对消息或连接的处理，有两种类型，Inbound和Outbound。分别代表消息接收的处理和消息发送的处理。
- ChannelFuture：注解回调方法

了解上面的基本组件后，就看一下几个重要的内容。

### Netty的Buffer和零拷贝

在Unix操作系统中，系统底层可以基于mmap实现内核空间和用户空间的内存映射。但是在Netty中并不是这个意思，它主要来自于下面几个功能：

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180330-153650.jpg)

1. 通过Composite和slice实现逻辑上的Buffer的组合和拆分，重新维护索引，避免内存拷贝过程。
2. 通过DirectBuffer申请堆外内存，避免用户空间的拷贝。不过堆外内存的申请和释放都很麻烦，推荐小心使用。关于堆外内存的一些研究，还可以参考执勤的分享：[Java堆外内存之突破JVM枷锁](http://www.cnblogs.com/xing901022/p/5215458.html) 以及 [Java直接内存与非直接内存性能测试](http://www.cnblogs.com/xing901022/p/5243657.html)
3. 通过FileRegion包装FileChannel，直接实现channel到channel的传输。

另外，Netty自己封装实现了ByteBuf，相比于Nio原生的ByteBuffer，API上更易用了；同时支持容量的动态扩容；另外还支持Buffer的池化，高效复用Buffer。

```java
public class ByteBufTest {
    public static void main(String[] args) {
        //创建bytebuf
        ByteBuf buf = Unpooled.copiedBuffer("hello".getBytes());
        System.out.println(buf);

        // 读取一个字节
        buf.readByte();
        System.out.println(buf);

        // 读取一个字节
        buf.readByte();
        System.out.println(buf);

        // 丢弃无用数据
        buf.discardReadBytes();
        System.out.println(buf);

        // 清空
        buf.clear();
        System.out.println(buf);

        // 写入
        buf.writeBytes("123".getBytes());
        System.out.println(buf);

        buf.markReaderIndex();
        System.out.println("mark:"+buf);

        buf.readByte();
        buf.readByte();
        System.out.println("read:"+buf);

        buf.resetReaderIndex();
        System.out.println("reset:"+buf);
    }
}
```

输出为：

```
UnpooledHeapByteBuf(ridx: 0, widx: 5, cap: 5/5)
UnpooledHeapByteBuf(ridx: 1, widx: 5, cap: 5/5)
UnpooledHeapByteBuf(ridx: 2, widx: 5, cap: 5/5)
UnpooledHeapByteBuf(ridx: 0, widx: 3, cap: 5/5)
UnpooledHeapByteBuf(ridx: 0, widx: 0, cap: 5/5)
UnpooledHeapByteBuf(ridx: 0, widx: 3, cap: 5/5)
mark:UnpooledHeapByteBuf(ridx: 0, widx: 3, cap: 5/5)
read:UnpooledHeapByteBuf(ridx: 2, widx: 3, cap: 5/5)
reset:UnpooledHeapByteBuf(ridx: 0, widx: 3, cap: 5/5)
```

有兴趣的可以看一下上一篇分享的ByteBuffer，对比一下，就能发现在Netty中通过独立的读写索引维护，避免读写模式的切换，更加方便了。

### Handler的使用

前面介绍了Handler包含了Inbound和Outbound两种，他们统一放在一个双向链表中：

![img](https://images.cnblogs.com/cnblogs_com/xing901022/1187174/o_Jietu20180330-154727.jpg)

当接收消息的时候，会从链表的表头开始遍历，如果是inbound就调用对应的方法；如果发送消息则从链表的尾巴开始遍历。那么上面途中的例子，接收消息就会输出：

```repl
InboundA --> InboundB --> InboundC
```

输出消息，则会输出：

```repl
OutboundC --> OutboundB --> OutboundA
```

这里有段代码，可以直接复制下来，试试看：

```java
package cn.xingoo.book.netty.pipeline;

import io.netty.bootstrap.ServerBootstrap;
import io.netty.buffer.ByteBuf;
import io.netty.buffer.Unpooled;
import io.netty.channel.*;
import io.netty.channel.nio.NioEventLoopGroup;
import io.netty.channel.socket.SocketChannel;
import io.netty.channel.socket.nio.NioServerSocketChannel;

import java.net.InetSocketAddress;
import java.net.SocketAddress;
import java.nio.charset.Charset;

/**
 * 注意：
 *
 * 1 ChannelOutboundHandler要在最后一个Inbound之前
 *
 */
public class NettyNioServerHandlerTest {

    final static ByteBuf buffer = Unpooled.unreleasableBuffer(Unpooled.copiedBuffer("Hi\r\n", Charset.forName("UTF-8")));

    public void serve(int port) throws InterruptedException {


        EventLoopGroup bossGroup = new NioEventLoopGroup(1);
        EventLoopGroup workerGroup = new NioEventLoopGroup();

        try{
            ServerBootstrap b = new ServerBootstrap();
            b.group(bossGroup, workerGroup)
                    .channel(NioServerSocketChannel.class)
                    .localAddress(new InetSocketAddress(port))
                    .childHandler(new ChannelInitializer<SocketChannel>() {
                        @Override
                        protected void initChannel(SocketChannel socketChannel) throws Exception {
                            ChannelPipeline pipeline = socketChannel.pipeline();
                            pipeline.addLast("1",new InboundA());
                            pipeline.addLast("2",new OutboundA());
                            pipeline.addLast("3",new InboundB());
                            pipeline.addLast("4",new OutboundB());
                            pipeline.addLast("5",new OutboundC());
                            pipeline.addLast("6",new InboundC());
                        }
                    });
            ChannelFuture f = b.bind().sync();
            f.channel().closeFuture().sync();
        } finally {
            bossGroup.shutdownGracefully().sync();
            workerGroup.shutdownGracefully().sync();
        }
    }

    public static void main(String[] args) throws InterruptedException {
        NettyNioServerHandlerTest server = new NettyNioServerHandlerTest();
        server.serve(5555);
    }

    private static class InboundA extends ChannelInboundHandlerAdapter {
        @Override
        public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
            ByteBuf buf = (ByteBuf)msg;
            System.out.println("InboundA read"+buf.toString(Charset.forName("UTF-8")));
            super.channelRead(ctx, msg);
        }
    }

    private static class InboundB extends ChannelInboundHandlerAdapter {
        @Override
        public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
            ByteBuf buf = (ByteBuf)msg;
            System.out.println("InboundB read"+buf.toString(Charset.forName("UTF-8")));
            super.channelRead(ctx, msg);
            // 从pipeline的尾巴开始找outbound
            ctx.channel().writeAndFlush(buffer);
        }
    }

    private static class InboundC extends ChannelInboundHandlerAdapter {
        @Override
        public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
            ByteBuf buf = (ByteBuf)msg;
            System.out.println("InboundC read"+buf.toString(Charset.forName("UTF-8")));
            super.channelRead(ctx, msg);
            // 这样会从当前的handler向前找outbound
            //ctx.writeAndFlush(buffer);
        }
    }

    private static class OutboundA extends ChannelOutboundHandlerAdapter {
        @Override
        public void write(ChannelHandlerContext ctx, Object msg, ChannelPromise promise) throws Exception {
            System.out.println("OutboundA write");
            super.write(ctx, msg, promise);
        }
    }

    private static class OutboundB extends ChannelOutboundHandlerAdapter {
        @Override
        public void write(ChannelHandlerContext ctx, Object msg, ChannelPromise promise) throws Exception {
            System.out.println("OutboundB write");
            super.write(ctx, msg, promise);
        }
    }

    private static class OutboundC extends ChannelOutboundHandlerAdapter {
        @Override
        public void write(ChannelHandlerContext ctx, Object msg, ChannelPromise promise) throws Exception {
            System.out.println("OutboundC write");
            super.write(ctx, msg, promise);
        }
    }
}
```

最后有一个TCP粘包的例子，有兴趣的也可以自己试一下，代码就不贴上来了，可以参考最后面的Github连接。

### 参考

1. [《Netty实战》](https://item.jd.com/12070975.html)
2. [《Netty权威指南》](https://item.jd.com/11681556.html)
3. [github代码链接](https://github.com/xinghalo/JDK-Learning/tree/master/src/cn/xingoo/book/netty2/chap5)

作者：[xingoo](http://www.cnblogs.com/xing901022)

出处：[http://www.cnblogs.com/xing901022](http://www.cnblogs.com/xing901022)

本文版权归作者和博客园共有。欢迎转载，但必须保留此段声明，且在文章页面明显位置给出原文连接！