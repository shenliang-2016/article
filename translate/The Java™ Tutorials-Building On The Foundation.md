# Java™教程

[主页](https://docs.oracle.com/javase/tutorial/index.html)

## Java教程学习路径

> Java教程是为JDK 8编写的。本页描述的示例和实践没有利用后续版本中引入的改进。

## 入门

- [入门](https://docs.oracle.com/javase/tutorial/getStarted/index.html) - 介绍Java技术和安装Java开发软件并使用它来创建简单程序的课程。
- [学习Java语言](https://docs.oracle.com/javase/tutorial/java/index.html) - 描述基本概念（如类，对象，继承，数据类型，泛型和包）的课程。
- [基本Java类](https://docs.oracle.com/javase/tutorial/essential/index.html) - 有关异常，基本输入/输出，并发，正则表达式和平台环境的课程。

## 基础

- [集合](https://docs.oracle.com/javase/tutorial/collections/index.html) - 使用和扩展Java集合框架的经验教训。
- [Lambda表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)：了解如何以及为何在应用程序中使用Lambda表达式。
- [聚合操作](https://docs.oracle.com/javase/tutorial/collections/streams/index.html)：探索聚合操作，流和Lambda表达式如何协同工作以提供强大的过滤功能。
- [JAR文件中的打包程序](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html) - 有关创建和签署JAR文件的课程。
- [国际化](https://docs.oracle.com/javase/tutorial/i18n/index.html) - 设计软件的介绍，以便可以轻松地适应（本地化）各种语言和区域。
- [反射](https://docs.oracle.com/javase/tutorial/reflect/index.html) - 表示（“反映”）当前Java虚拟机中的类，接口和对象的API。
- [安全性](https://docs.oracle.com/javase/tutorial/security/index.html) - Java平台功能，有助于保护应用程序免受恶意软
- [JavaBeans](https://docs.oracle.com/javase/tutorial/javabeans/index.html) - Java平台的组件技术。
- [扩展机制](https://docs.oracle.com/javase/tutorial/ext/index.html) - 如何使Java平台上运行的所有应用程序都可以使用自定义API。
- [泛型](https://docs.oracle.com/javase/tutorial/extra/generics/index.html) - 对类型系统的增强，支持对各种类型的对象的操作，同时提供编译时类型安全性。

## 客户端开发

- [JavaFX入门](http://www.oracle.com/pls/topic/lookup?ctx=javase80&id=JFXST804) - 一组示例应用程序，旨在帮助您开始使用常见的JavaFX任务
- [Scene Builder入门](http://www.oracle.com/pls/topic/lookup?ctx=javase80&id=JSBGS101) - 逐步向您展示如何使用JavaFX Scene Builder工具创建简单的问题跟踪应用程序。
- [使用Swing创建GUI](https://docs.oracle.com/javase/tutorial/uiswing/index.html) - 全面介绍Java平台上的GUI创建。
- [部署](https://docs.oracle.com/javase/tutorial/deployment/index.html) - 如何使用JAR文件打包应用程序和applet，并使用Java Web Start和Java Plug-in进行部署。
- [2D图形](https://docs.oracle.com/javase/tutorial/2d/index.html) - 如何在应用程序中显示和打印2D图形。
- [全屏独占模式API](https://docs.oracle.com/javase/tutorial/extra/fullscreen/index.html) - 如何编写更充分利用用户图形硬件的应用程序。

## 服务端开发

- [JDBC数据库访问](https://docs.oracle.com/javase/tutorial/jdbc/index.html) - 介绍用于Java应用程序与各种数据库和数据源之间的连接的API。
- [JMX](https://docs.oracle.com/javase/tutorial/jmx/index.html) - Java Management Extensions提供了一种管理应用程序，设备和服务等资源的标准方法。
- [JNDI](https://docs.oracle.com/javase/tutorial/jndi/index.html) - Java命名和目录接口支持访问DNS和LDAP等命名和目录服务。
- [JAXP](https://docs.oracle.com/javase/tutorial/jaxp/index.html) - 介绍用于XML处理的Java API（JAXP）1.4技术。
- [RMI](https://docs.oracle.com/javase/tutorial/rmi/index.html) - 远程方法调用API允许对象调用在另一个Java虚拟机上运行的对象的方法。
- [并发](https://docs.oracle.com/javase/tutorial/essential/concurrency/index.html) - Java平台具有API，可帮助您开发多线程程序。


# 集合

本节介绍Java Collections Framework。在这里，您将了解集合是什么以及如何使您的工作更轻松，程序更好。您将了解构成Java Collections Framework的核心元素 - 接口，实现，聚合操作和算法。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**介绍**](https://docs.oracle.com/javase/tutorial/collections/intro/index.html) 告诉您什么是集合，以及它们如何使您的工作更轻松，您的程序更好。您将了解构成集合框架的核心元素：接口，实现和算法。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**接口**](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html) 描述了核心集合接口，它是Java Collections Framework的核心和灵魂。您将学习有效使用这些接口的一般准则，包括何时使用哪个接口。您还将学习每个接口的习惯用法，以帮助您充分利用接口。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**Aggregate Operations**](https://docs.oracle.com/javase/tutorial/collections/streams/index.html) iterate over collections on your behalf, which enable you to write more concise and efficient code that process elements stored in collections.

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**实现**](https://docs.oracle.com/javase/tutorial/collections/implementations/index.html) 描述了JDK的通用集合实现，并告诉您何时使用哪个实现。您还将了解包装器实现，它为通用实现添加功能。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**算法**](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html) 描述了JDK提供的用于对集合进行操作的多态算法。运气好的话，你再也不用写自己的排序程序了！

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**自定义实现**](https://docs.oracle.com/javase/tutorial/collections/custom-implementations/index.html) 告诉你为什么你可能想要编写自己的集合实现（而不是使用JDK提供的一个通用实现），以及你如何去做。使用JDK的抽象集合实现很容易！

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**互操作性**](https://docs.oracle.com/javase/tutorial/collections/interoperability/index.html) 告诉您集合框架如何与早于将集合添加到Java之前的API进行互操作。此外，它还告诉您如何设计新的API，以便它们可以与其他新API无缝地互操作。

## 介绍

集合（有时称为容器）只是一个将多个元素组合到一个单元中的对象。集合用于存储，检索，操作和传递聚合数据。通常，它们表示形成自然组的数据项，例如扑克牌（卡片集合），邮件文件夹（字母集合）或电话目录（名称到电话号码的映射）。如果您使用过Java编程语言 - 或者只使用其他任何编程语言 - 那么您已经熟悉了集合。

**什么是集合框架？**

集合框架是用于表示和操作集合的统一体系结构。所有集合框架都包含以下内容：

 - 接口：这些是表示集合的抽象数据类型。接口允许独立于其表示的细节来操纵集合。在面向对象语言中，接口通常形成层次结构。
 - 实现：这些是集合接口的具体实现。实质上，它们是可重用的数据结构。
 - 算法：这些是对实现集合接口的对象执行有用计算（如搜索和排序）的方法。算法被认为是多态的：也就是说，相同的方法可以用于适当的集合接口的许多不同实现。实质上，算法是可重用的功能。

除了Java Collections Framework之外，最着名的集合框架示例是C++标准模板库（STL）和Smalltalk的集合层次结构。从历史上看，集合框架相当复杂，这使得它们具有陡峭的学习曲线的声誉。我们相信Java Collections Framework打破了这一传统，因为您将在本章中自学。

**Java Collections Framework 的好处**

Java Collections Framework提供以下好处：

- **减少编程工作：** 通过提供有用的数据结构和算法，Collections Framework可以让您专注于程序的重要部分，而不是使其工作所需的低级“管道”。通过促进不相关API之间的互操作性，Java Collections Framework使您无需编写适配器对象或转换代码来连接API。
- **提高程序速度和质量：** 集合框架提供有用数据结构和算法的高性能，高质量实现。每个接口的各种实现是可互换的，因此可以通过切换集合实现来轻松调整程序。因为您没有编写自己的数据结构的苦差事，所以您将有更多的时间投入到改进程序的质量和性能上。
- **允许不相关的API之间的互操作性：** 集合接口是通过其API来回传递集合的本地语言。如果我的网络管理API提供了一组节点名称，并且您的GUI工具包需要一组列标题，那么我们的API将无缝地互操作，即使它们是独立编写的。
- **减少学习和使用新API的工作量：** 许多API自然地在输入上收集集合并将它们作为输出提供。过去，每个这样的API都有一个专门用于操作其集合的小型子API。这些专用集合子API之间几乎没有一致性，因此您必须从头开始学习每一个，并且在使用它们时很容易出错。随着标准集合接口的出现，问题就消失了。
- **减少设计新API的工作量：** 这是之前优势的另一面。设计人员和实施人员每次创建依赖于集合的API时都不必重新发明轮子；相反，他们可以使用标准的集合接口。
- **促进软件重用：** 符合标准集合接口的新数据结构本质上是可重用的。对于实现这些接口的对象进行操作的新算法也是如此。

## 接口

