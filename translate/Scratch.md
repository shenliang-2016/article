# RMI

Java 远程方法调用 (RMI) 系统允许运行在一个 Java 虚拟机中的对象调用运行在另一个 Java 虚拟机中的对象。RMI 为使用 Java 语言编写的程序提供了远程通信。

------

**注意：** 如果你想要与一个现存的 IDL 程序通信，那么你应该使用 Java IDL 而不是 RMI。

------

本课程提供了 RMI 系统的简要介绍，然后深入一个完整的客户端/服务器示例，该示例使用了 RMI 的独特能力在运行时加载并执行用户自定义的任务。例子中的服务器实现了通用计算引擎，客户端使用它来计算 ![the pi symbol](https://docs.oracle.com/javase/tutorial/figures/rmi/pi.gif) 的值。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**RMI 应用概览**](https://docs.oracle.com/javase/tutorial/rmi/overview.html) 描述 RMI 系统并列出它的优点。另外，此章节提供了由客户端和服务器构成的典型 RMI 应用的描述。同时介绍了一些重要的术语。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**编写 RMI 服务器**](https://docs.oracle.com/javase/tutorial/rmi/server.html) 深入计算引擎服务器代码。本章节将教会你如何设计实现一个 RMI 服务器。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**创建客户端程序**](https://docs.oracle.com/javase/tutorial/rmi/client.html) 分析一个可能的计算引擎客户端，并以其为例展示了一个 RMI 客户端的重要特性。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**编译并运行示例**](https://docs.oracle.com/javase/tutorial/rmi/example.html) 向你展示如何编译并运行计算引擎服务器和客户端。

