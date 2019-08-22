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

# JDBC™ 数据库访问

JDBC™ API 的设计目标是保持简单。这意味着 JDBC 使得所有的数据库任务变得简单。本课程带领你通过使用 JDBC 的实例来执行普通的 SQL 语句，以及执行数据库应用的常见任务。

本课程分为以下部分：

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**JDBC 介绍**](https://docs.oracle.com/javase/tutorial/jdbc/overview/index.html) 列出 JDBC 特性，描述 JDBC 体系结构，SQL 命令和关系数据库概念综述。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**JDBC 基础**](https://docs.oracle.com/javase/tutorial/jdbc/basics/index.html) 涵盖 JDBC API，包含在 Java™ SE 6 版本中。

完成第一部分学习后，你将知道如何使用基本的 JDBC API 来创建表，向表中插入数据，查询表，检索查询结果，以及更新表等。在此过程中，你将学习如何使用简单语句和预编译语句，同时你将看到一个存储过程的例子。你也将学到如何执行事务以及如何捕获异常和警告。

## JDBC 介绍

JDBC API 是可以访问任何类型的表格式的数据的 Java API，特别是存储在 [关系数据库](https://docs.oracle.com/javase/tutorial/jdbc/overview/index.html#relational) 中的数据。

JDBC 帮助你编写 Java 程序来管理以下三类程序活动：

* 连接数据源，比如数据库
* 发送查询和更新语句到数据库
* 检索并处理来自数据库的作为你的查询的响应的查询结果

下面的简单代码片段展示了这三个步骤的例子：

```java
public void connectToAndQueryDatabase(String username, String password) {

    Connection con = DriverManager.getConnection(
                         "jdbc:myDriver:myDatabase",
                         username,
                         password);

    Statement stmt = con.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT a, b, c FROM Table1");

    while (rs.next()) {
        int x = rs.getInt("a");
        String s = rs.getString("b");
        float f = rs.getFloat("c");
    }
}
```

此代码片段实例化一个 `DriverManager` 对象来连接到一个数据库驱动并登录到数据库中，实例化一个 `Statement` 对象运输你的 SQL 查询到数据库，实例化一个 `ResultSet` 对象来获取你的查询结果，并执行一个简单的 `while` 循环，获取并显示那些结果。

**JDBC 产品组件**

JDBC 包含四个组件：

1. **JDBC API** — JDBC™ API 提供了编程方式通过 Java™ 编程语言访问关系数据的能力。使用 JDBC API，程序能够执行 SQL 语句，检索结果，并反向传播更改到数据源。JDBC API 可以在异质的分布式环境中同时与多个数据源交互。

   JDBC API 是 Java 平台的一部分，该平台包含 *Java™ Standard Edition* (Java™ SE ) 和 *Java™ Enterprise Edition* (Java™ EE)。JDBC 4.0 API 被分为两个包： `java.sql` 和 `javax.sql` 。两个包都包含在 Java SE 和 Java EE 平台中。

2. **JDBC Driver Manager** —  JDBC `DriverManager` 类定义了能够将 Java 程序连接到 JDBC 驱动的类。`DriverManager` 从来就是 JDBC 架构的核心。它非常精简。

   标准扩展包 `javax.naming` 和 `javax.sql` 使得你可以使用在 *Java Naming and Directory Interface*™ (JNDI) 命名服务中注册的 `DataSource` 对象来建立与数据源的连接。您可以使用任一连接机制，但建议尽可能使用DataSource对象。

3. **JDBC Test Suite** —  JDBC driver 测试套件帮助你确定 JDBC 驱动将运行你的程序。这些测试并不全面或详尽，但它们确实运用了 JDBC API 中的许多重要功能。

4. **JDBC-ODBC Bridge** —  Java Software bridge 通过 ODBC 驱动程序提供 JDBC 访问。请注意，您需要将 ODBC 二进制代码加载到使用此驱动程序的每台客户端计算机上。因此，ODBC 驱动程序最适用于客户端安装不是主要问题的公司网络，或者适用于以三层体系结构用 Java 编写的应用程序服务器代码。

此课程使用这四个 JDBC 组件中的前两个连接到数据库，然后构建一个使用 SQL 命令与测试关系数据库通信的Java程序。最后两个组件用于特定环境以测试 web 应用程序，或与 ODBC 敏感的 DBMS 进行通信。

### JDBC 体系结构

JDBC API 同时支持两层或者三层数据库访问过程模型。

![The DBMS-proprietary protocol provides two-way communication between the client machine and the database server](https://docs.oracle.com/javase/tutorial/jdbc/overview/intro.anc2.gif)

Figure 1: 数据访问的两层体系结构

在两层模型中，Java 程序直接与数据源交互。这就需要 JDBC 驱动能够与被访问的特定数据源进行通信。一个用户的命令被交付给该数据库或者其他数据源，同时那些语句的结果被回送给用户。数据源可以位于别的机器上，用户通过网络进行连接。这被称为客户端/服务器配置，用户的机器作为客户端，数据源所在的机器作为服务器。网络可以是内联网，例如，连接公司内的员工，也可以是因特网。

在三层模型中，命令被发送到服务的“中间层”，然后将命令发送到数据源。数据源处理命令并将结果发送回中间层，然后中间层将它们发送给用户。MIS 主管发现三层模型非常具有吸引力，因为中间层可以保持对访问的控制以及可以对公司数据进行的更新。另一个优点是它简化了应用程序的部署。最后，在许多情况下，三层架构可以提供性能优势。

![The DBMS-proprietary protocol provides two-way communication between the database server and the server machine. HTTP, RMI, CORBA or other calls provide two way communication between the server machine and the client machine](https://docs.oracle.com/javase/tutorial/jdbc/overview/intro.anc1.gif)

Figure 2: 数据访问的三层体系结构

直到最近，中间层通常用 C 或 C++ 等语言编写，这些语言提供了足够高的性能。然而，随着优化编译器的引入，将 Java 字节码转换为高效的机器特定代码和诸如 Enterprise JavaBeans™ 的技术，Java 平台正迅速成为中间层开发的标准平台。这是一个很大的优势，可以利用 Java 的健壮性，多线程和安全功能。

随着企业越来越多地使用 Java 编程语言编写服务器代码，JDBC API 在三层体系结构的中间层中越来越多地被使用。使 JDBC 成为服务器技术的一些功能是它支持连接池，分布式事务和断开连接的行集。JDBC API也允许从 Java 中间层访问数据源。

