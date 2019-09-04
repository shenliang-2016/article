## JNDI 概述

Java命名和目录接口（JNDI）是一种应用程序编程接口（API），它为使用Java™编程语言编写的应用程序提供 [命名](https://docs.oracle.com/javase/tutorial/jndi/overview/naming.html) 和 [目录](https://docs.oracle.com/javase/tutorial/jndi/overview/dir.html) 功能。它被定义为独立于任何特定的目录服务实现。因此，可以以通用方式访问各种目录 - 新的，出现的和已经部署的目录。

**架构**

JNDI体系结构由API和服务提供者接口（SPI）组成。Java应用程序使用JNDI API来访问各种命名和目录服务。SPI允许透明地插入各种命名和目录服务，从而允许使用JNDI API的Java应用程序访问其服务。见下图：

![JNDI Architecture](https://docs.oracle.com/javase/tutorial/figures/jndi/jndiarch.gif)

**包**

JNDI包含在Java SE平台中。要使用JNDI，您必须具有JNDI类和一个或多个服务提供者。JDK包括以下命名/目录服务的服务提供者：

 - 轻量级目录访问协议（LDAP）
 - 公共对象请求代理体系结构（CORBA）公共对象服务（COS）名称服务
 - Java远程方法调用（RMI）注册表
 - 域名服务（DNS）

其它服务提供者可以从 [JNDI page](http://www.oracle.com/technetwork/java/jndi/index.html) 下载或者从各自厂商获得。

JNDI 被分为 5 个包：

- [javax.naming](https://docs.oracle.com/javase/tutorial/jndi/overview/naming.html)
- [javax.naming.directory](https://docs.oracle.com/javase/tutorial/jndi/overview/dir.html)
- [javax.naming.ldap](https://docs.oracle.com/javase/tutorial/jndi/overview/dir.html)
- [javax.naming.event](https://docs.oracle.com/javase/tutorial/jndi/overview/event.html)
- [javax.naming.spi](https://docs.oracle.com/javase/tutorial/jndi/overview/event.html)

接下面的部分简要介绍了各个 JNDI 包。

