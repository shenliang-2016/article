# Apache Tomcat 8

**Version 8.5.37, Dec 12 2018**

----

## 文档索引

----

### 介绍

这是关于 Apache Tomcat Servlet/JSP 容器的文档的顶层切入点。Apache Tomcat 8.5 版本实现了来自 [Java Community Process](https://www.jcp.org/) 的 Servlet 3.1 和 JavaServer Pages 2.3 规范，同时包含很多附件特性，使得它成为开发和部署 web 应用和 web 服务的有用平台。

### Apache Tomcat 用户指南

1. [**介绍**](https://tomcat.apache.org/tomcat-8.5-doc/introduction.html)－Apache Tomcat 的简要的、高层次的概览。
2. [**安装**](https://tomcat.apache.org/tomcat-8.5-doc/setup.html)－如何在各种平台上安装并运行 Apache Tomcat。
3. [**第一个 web 应用**](https://tomcat.apache.org/tomcat-8.5-doc/appdev/index.html)－关于在 Servlet 规范中定义的 web 应用相关概念的介绍。包含 web 应用源代码基本组织结构，web 应用归档文件的结构，以及对 web 应用部署描述器文件````/WEB-INF/web.xml````的介绍。
4. [**部署器**](https://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html)－操作 Apache Tomcat 部署器来部署、预编译以及校验 web 应用。
5. [**管理器**](https://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html)－在 Apache Tomcat 运行状态下，操作管理器 web 应用进行应用的部署、卸载以及重新部署。
6. [**主机管理器**](https://tomcat.apache.org/tomcat-8.5-doc/host-manager-howto.html)－在 Apache Tomcat 运行状态下，操作主机管理器 web 应用进行虚拟主机的添加和删除。
7. [**领域和访问控制**](https://tomcat.apache.org/tomcat-8.5-doc/realm-howto.html)－描述如何配置应用中使用的领域（关于用户名、密码以及它们关联的角色等数据的数据库），以使用容器管理的安全机制。
8. [**安全管理器**](https://tomcat.apache.org/tomcat-8.5-doc/security-manager-howto.html)－配置和使用一个 Java 安全管理器以支持对 web 应用行为的细粒度控制。
9. [**JNDI 资源**](https://tomcat.apache.org/tomcat-8.5-doc/jndi-resources-howto.html)－在提供给每个应用的 JNDI 命名上下文中配置标准资源和客户资源。
10. [**JDBC 数据源**](http://tomcat.apache.org/tomcat-8.5-doc/jndi-datasource-examples-howto.html)－配置一个 JNDI 数据源和一个数据库连接池。支持大部分流行数据库。
11. [**类加载**](http://tomcat.apache.org/tomcat-8.5-doc/class-loader-howto.html)－关于类加载机制的信息，包括你应该将应用类放在哪里以保证它们是可见的。
12. [**JSPs**](http://tomcat.apache.org/tomcat-8.5-doc/jasper-howto.html)－关于 Jasper 的配置信息，已经 JSP 编译器的使用。
13. [**SSL/TLS**](http://tomcat.apache.org/tomcat-8.5-doc/ssl-howto.html)－安装和配置 SSL/TLS 支持，由此你的 Apache Tomcat 将支持使用````https````协议的请求。
14. [**SSI**](http://tomcat.apache.org/tomcat-8.5-doc/ssi-howto.html)－在 Apache Tomcat 中使用服务端包含。
15. [**CGI**](http://tomcat.apache.org/tomcat-8.5-doc/cgi-howto.html) - 在 Apache Tomcat 中使用 CGIs 。
16. [**代理支持**](http://tomcat.apache.org/tomcat-8.5-doc/proxy-howto.html) - 配置 Apache Tomcat 以工作在代理服务器背后 (或者作为代理服务器的 web 服务器背后)。
17. [**MBeans 描述器**](http://tomcat.apache.org/tomcat-8.5-doc/mbeans-descriptors-howto.html) - 为客户化组件配置 MBean 描述器文件。
18. [**默认 Servlet**](http://tomcat.apache.org/tomcat-8.5-doc/default-servlet.html) - 配置默认 servlet 和客户化目录列表。
19. [**Apache Tomcat 集群**](http://tomcat.apache.org/tomcat-8.5-doc/cluster-howto.html) - 在 Apache Tomcat 环境中开启会话复制。
20. [**负载均衡器**](http://tomcat.apache.org/tomcat-8.5-doc/balancer-howto.html) - 配置、使用和扩展负载均衡应用。
21. [**连接器**](http://tomcat.apache.org/tomcat-8.5-doc/connectors.html) - Apache Tomcat 中可用的连接器，以及本地 web 服务器。
22. [**监控和管理**](http://tomcat.apache.org/tomcat-8.5-doc/monitoring.html) - 开启 JMX 远程支持，使用工具监控和管理 Apache Tomcat。
23. [**日志**](http://tomcat.apache.org/tomcat-8.5-doc/logging.html) - 配置 Apache Tomcat 中的日志。
24. [**Apache 可移植运行时**](http://tomcat.apache.org/tomcat-8.5-doc/apr.html) - 使用 APR 提供更高性能、可扩展性以及与本地服务器技术更好的可集成性。
25. [**虚拟主机**](http://tomcat.apache.org/tomcat-8.5-doc/virtual-hosting-howto.html) - 在 Apache Tomcat 中配置虚拟主机。
26. [**高级 IO**](http://tomcat.apache.org/tomcat-8.5-doc/aio.html) - 超越传统的阻塞式 IO 的扩展。
27. [**附加组件**](http://tomcat.apache.org/tomcat-8.5-doc/extras.html) - 获取附加的可选组件。
28. [**通过 Maven 使用 Tomcat 类库**](http://tomcat.apache.org/tomcat-8.5-doc/maven-jars.html) - 通过 Maven 获取 Tomcat jars 。
29. [**安全考虑**](http://tomcat.apache.org/tomcat-8.5-doc/security-howto.html) - 关于 Apache Tomcat 的安全选项。
30. [**Windows 服务**](http://tomcat.apache.org/tomcat-8.5-doc/windows-service-howto.html) - 作为 Microsoft Windows 服务运行 Tomcat 。
31. [**Windows 身份认证**](http://tomcat.apache.org/tomcat-8.5-doc/windows-auth-howto.html) - 配置 Tomcat 以使用集成的 Windows 认证机制。
32. [**高并发 JDBC 连接池**](http://tomcat.apache.org/tomcat-8.5-doc/jdbc-pool.html) - 配置 Tomcat 以使用改进的 JDBC 连接池。
33. [**WebSocket 支持**](http://tomcat.apache.org/tomcat-8.5-doc/web-socket-howto.html) - 为 Apache Tomcat 开发 WebSocket 应用。
34. [**URL 重写**](http://tomcat.apache.org/tomcat-8.5-doc/rewrite.html) - 使用基于正则表达式的重写机制进行提交 URL 和主机地址的重写。

### 参考

负责安装、配置和维护 Apache Tomcat 服务器的系统管理员需要参考以下文档：

* [**Release notes**](http://tomcat.apache.org/tomcat-8.5-doc/RELEASE-NOTES.txt)－此版本 Apache Tomcat 发布的周知问题。
* [**Apache Tomcat Server 配置参考文档**](http://tomcat.apache.org/tomcat-8.5-doc/config/index.html)－描述可能被写入 Apache Tomcat ````conf/server.xml````文件的所有可用的元素和属性的参考文档。
* [**JK 文档**](https://tomcat.apache.org/connectors-doc/index.html)－关于 JK 本地服务器连接器的完整文档和操作手册，被 Apache HTTPd 、IIS 等其它服务器用于连接 Apache Tomcat 服务器。
* Servlet 3.1 [**规范**](http://jcp.org/aboutJava/communityprocess/final/jsr340/index.html) and [**Javadoc**](http://docs.oracle.com/javaee/7/api/javax/servlet/package-summary.html)
* JSP 2.3 [**规范**](https://jcp.org/aboutJava/communityprocess/mrel/jsr245/index2.html) and [**Javadoc**](http://docs.oracle.com/javaee/7/api/javax/servlet/jsp/package-summary.html)
* EL 3.0 [**规范**](https://jcp.org/aboutJava/communityprocess/final/jsr341/index.html) and [**Javadoc**](http://docs.oracle.com/javaee/7/api/javax/el/package-summary.html)
* WebSocket 1.1 [**规范**](https://jcp.org/aboutJava/communityprocess/mrel/jsr356/index.html) and [**Javadoc**](http://docs.oracle.com/javaee/7/api/javax/websocket/package-summary.html)
* JASPIC 1.1 [**规范**](https://jcp.org/aboutJava/communityprocess/mrel/jsr196/index.html) and [**Javadoc**](http://docs.oracle.com/javaee/7/api/javax/security/auth/message/package-summary.html)

### Apache Tomcat 开发者

以下资料可供想要为 Apache Tomcat 项目贡献代码的开发者参考。

- [**从源代码构建**](http://tomcat.apache.org/tomcat-8.5-doc/building.html) - 下载 Apache Tomcat 源代码和相关依赖包的必须步骤，以及从源代码构建一个二进制发布包。
- [**修改纪录**](http://tomcat.apache.org/tomcat-8.5-doc/changelog.html) - Apache Tomcat 变化的所有细节纪录。
- [**状态**](https://wiki.apache.org/tomcat/TomcatVersions) - Apache Tomcat 开发状态。
- [**开发者**](http://tomcat.apache.org/tomcat-8.5-doc/developers.html) - Apache Tomcat 活跃开发者列表。
- [**功能规范**](http://tomcat.apache.org/tomcat-8.5-doc/funcspecs/index.html) - 对作为 Apache Tomcat 一部分的 *Catalina* servlet 容器的需求规范。
- [**Javadocs**](http://tomcat.apache.org/tomcat-8.5-doc/api/index.html) - Apache Tomcat 内部的 Javadoc API 文档。
- [**Apache Tomcat 架构**](http://tomcat.apache.org/tomcat-8.5-doc/architecture/index.html) - Apache Tomcat 服务器架构文档。

----

## 介绍

----

### 内容列表

- [介绍](http://tomcat.apache.org/tomcat-8.5-doc/introduction.html#Introduction)
- [术语](http://tomcat.apache.org/tomcat-8.5-doc/introduction.html#Terminology)
- [目录和文件](http://tomcat.apache.org/tomcat-8.5-doc/introduction.html#Directories_and_Files)
- CATALINA_HOME and CATALINA_BASE
  1. [为什么使用 CATALINA_BASE](http://tomcat.apache.org/tomcat-8.5-doc/introduction.html#Why_Use_CATALINA_BASE)
  2. [CATALINA_BASE 的内容](http://tomcat.apache.org/tomcat-8.5-doc/introduction.html#Contents_of_CATALINA_BASE)
  3. [如何使用 CATALINA_BASE](http://tomcat.apache.org/tomcat-8.5-doc/introduction.html#How_to_Use_CATALINA_BASE)
- [配置 Tomcat](http://tomcat.apache.org/tomcat-8.5-doc/introduction.html#Configuring_Tomcat)
- [何处寻求帮助](http://tomcat.apache.org/tomcat-8.5-doc/introduction.html#Where_to_Go_for_Help)

### 介绍

作为系统管理员和应用开发者，在开始工作之前有一些重要的信息需要了解。此文档提供了 Tomcat 容器背后的一些重要概念和术语的简要介绍。同时，也给出了求助地址。

### 术语

阅读此文档过程中，你将会遇到大量的术语，某些专用于 Tomcat ，另外一些由 [Servlet and JSP 规范](https://wiki.apache.org/tomcat/Specifications) 定义。

* **context**－简而言之，一个 Context 就是一个 web 应用。

如果各位发现需要添加到此章节中的术语，请告诉我们。

### 目录和文件

以下是 tomcat 的一些关键目录：

* **/bin**－启动、关闭以及其它脚本。````*.sh````文件（对 Unix 系统）与````*.bat````文件（对 Windows 系统）的功能是相同的。因为 Win32 命令行工具缺少某些功能，此目录下还有一些附加文件。
* **/conf**－配置文件和相关的 DTDs。此处最重要的文件是````server.xml````。该文件是容器的主配置文件。
* **/logs**－默认的日志文件在这里。
* **/webapps**－你的 web 应用放在这里。

### CATALINA_HOME 和 CATALINA_BASE

贯穿整个文档，多处出现下面两个参数的引用：

* **CATALINA_HOME**：表示你的 Tomcat 安装的根目录。比如````/home/tomcat/apache-tomcat-9.0.10````或者````c:\Program Files\apache-tomcat-9.0.10````。
* **CATALINA_BASE**：表示一个特定 Tomcat 实例的运行时的配置文件的根目录。如果你想要在一台物理机器上运行多个 Tomcat 实例，就需要使用````CATALINA_BASE````属性。

如果你将这两个属性设置为不同的位置，````CATALINA_HOME````路径下包含静态资源，比如````.jar````文件，或者二进制文件。````CATALINA_BASE````路径包含配置文件，日志文件，部署的应用，以及其它运行时需要的文件。

#### 为什么要使用````CATALINA_BASE````

默认情况下，````CATALINA_HOME````和````CATALINA_BASE````指向相同的文件目录。当你需要在一台物理机器上运行多个 Tomcat 实例时就需要手动设定````CATALINA_BASE````属性。这样做可以有以下好处：

* 方便管理升级新版本的 Tomcat 。因为所有共享同一个````CATALINA_HOME````的多个实例都共享同一集合的````.jar````文件和二进制文件，你可以很方便地将这些文件升级到新版本，这个变化马上就会传播到共用同一个````CATALINA_HOME````目录的所有 Tomcat 实例。
* 避免相同的静态````.jar````文件的重复。
* 分享某些设置的可能性，比如````setenv```` shell 或者 bat 脚本文件（取决于你的操作系统）。

#### ````CATALINA_BASE```` 目录的内容

在你开始使用````CATALINA_BASE````之前，首先考虑并创建````CATALINA_BASE````所使用的目录树。注意，如果你没有创建这些推荐目录，Tomcat 就会自动创建。如果这些必要的目录创建失败，比如由于文件夹权限问题，Tomcat 要么启动失败，要么功能不正常。

考虑下列目录：

* ````bin````目录和````setenv.sh````、````setenv.bat````以及````tomcat-juli.jar````文件。

  推荐：否

  查找顺序：首先检查````CATALINA_BASE````，然后是加载````CATALINA_HOME````。

* ````lib````目录和需要被添加到````classpath````中的额外的资源。

  推荐：是，如果你的应用依赖于扩展类库。

  查找顺序：首先检查````CATALINA_BASE````，然后是加载````CATALINA_HOME````。

* ````logs````目录，存放特定实例的日志文件。

  推荐：是

* ````webapps````目录，Tomcat 从该目录自动加载 web 应用。

  推荐：是，如果你想要部署应用。

  查找顺序：只用````CATALINA_BASE````

* ````work````目录，包含部署的 web 应用的临时工作目录。

  推荐：是

* ````temp````目录，包含 JVM 使用的临时文件。

  推荐：是

我们推荐你不要修改````tomcat-juli.jar````文件。然而，如果你需要使用自己的日志实现，你就可以为特定的 Tomcat 实例替换位于````CATALINA_BASE````目录下的````tomcat-juli.jar````文件。

我们同时推荐你将````CATALINA_HOME/conf````目录下的所有的配置文件复制到````CATALINA_BASE/conf/````目录。免得````CATALINA_BASE````目录下缺失某个配置文件，而````CATALINA_HOME````目录下也没有备份。这样就可能导致失败。

最小化系统中，````CATALINA_BASE````必须包含：

* ````conf/server.xml````
* ````conf/web.xml````

这些文件都包含在````conf````目录下。否则，Tomcat 将启动失败，或者功能不正常。

更多的高级配置信息，可以参考 [RUNNING.txt ](https://tomcat.apache.org/tomcat-9.0-doc/RUNNING.txt) 文件。

#### 如何使用````CATALINA_BASE````

````CATALINA_BASE````属性是一个环境变量。你可以在执行 Tomcat 启动脚本之前设定改属性。比如：

* Unix：````CATALINA_BASE=/tmp/tomcat_base1 bin/catalina.sh start````
* Windows：````CATALINA_BASE=C:\tomcat_base1 bin/catalina.bat start````

### 配置 Tomcat

本节将帮助你熟悉配置容器过程中用到的基本信息。

配置文件中的所有信息都在容器启动时读取，这就意味着配置文件的任何修改都需要重启容器才能生效。

### 何处寻求帮助？

尽管我们尽量保证此文档书写清晰而且易于理解，然而还是无法避免有所遗漏。下面列出一些网址和邮件列表可能会提供帮助。

注意，某些问题和解决方案在 Tomcat 不同的主版本之间是不同的。当你在网上搜索解决方案时，某些文档并不一定是关于 Tomcat 8 的，可能仅仅是对更早版本有效。

* 此文档－大多数文档将列出潜在的问题。确保通读相关文档将为你节省很多时间和精力。当然，在网络上搜索问题的答案永远是最方便的方式。
* [Tomcat FAQ](https://wiki.apache.org/tomcat/FAQ)
* [Tomcat WIKI](https://wiki.apache.org/tomcat/)
* Tomcat FAQ at [jGuru](http://www.jguru.com/faq/home.jsp?topic=Tomcat)
* Tomcat 邮件列表归档 - 大量Tomcat 邮件列表的站点归档。
* TOMCAT-USER 邮件列表， [订阅地址](https://tomcat.apache.org/lists.html)。
* TOMCAT-DEV 邮件列表， [订阅地址](https://tomcat.apache.org/lists.html). 这个列表保留了关于 Tomcat 自身开发的讨论。关于 Tomcat 配置，开发和部署应用过程中可能遇到的问题，其中的答案可能要比 TOMCAT-USER 邮件列表中的更有针对性。

如果你认为文档中应该加入些什么内容，务必通过 Tomcat-DEV 邮件列表告诉我们。

----

## Tomcat 设置

----

### 内容列表

- [介绍](http://tomcat.apache.org/tomcat-8.5-doc/setup.html#Introduction)
- [Windows](http://tomcat.apache.org/tomcat-8.5-doc/setup.html#Windows)
- [Unix daemon](http://tomcat.apache.org/tomcat-8.5-doc/setup.html#Unix_daemon)

### 介绍

存在几种方式设置 Tomcat 以运行在不同的操作系统平台上。关于此设置的主要文档被称为 [RUNNING.txt](http://tomcat.apache.org/tomcat-8.5-doc/RUNNING.txt)。我们鼓励你直接研究该文件，如果下面的描述没有回答你的某些问题。

### Windows

通过 Windows 安装器在 Windows 操作系统上安装 Tomcat 是非常简单的。该安装器与其它的安装向导非常相似，仅仅包含很少有趣的元素。

* **安装为系统服务**：Tomcat 将被安装为一个 Windows 系统服务，无论选择的设置是什么。在组件设定页面上的选择框设定服务为````auto````启动模式，如此 Tomcat 就会在 Windows 系统启动时自动启动。为了优化安全性，该服务应该作为一个单独的用户运行，通过限制权限。

* **Java 位置**：安装器将提供一个默认的 JRE 用于运行该服务。安装器使用注册表来确定 Java 7 或者更高版本的 JRE 的安装根目录，或者是包含 JRE 作为其一部分的完整 JDK 的安装根目录。当运行在 64 位操作系统上时，安装器将首先寻找 64 位的 JRE ，只有当 64 位 JRE 不存在时才会寻找 32 位 JRE 。并不强制使用安装器找到的默认 JRE 。任何安装的 Java 7 或者更高版本的 JRE 都是可以使用的。

* **系统托盘按钮**：作为系统服务运行时，Tomcat 并不会作为按钮出现在系统托盘中。注意，如果在安装结束时选择直接运行 Tomcat ，则即使作为系统服务运行，系统托盘里还是会出现 Tomcat 按钮。

* **默认**：安装器使用的默认设置可以通过````/C=<config file>````命令行参数覆盖。配置文件使用````name=value````名值对形式，每行一个名值对。可用的配置项名称如下：

  * JavaHome
  * TomcatPortShutdown
  * TomcatPortHttp
  * TomcatPortAjp
  * TomcatMenuEntriesEnable
  * TomcatShortcurAllUsers
  * TomcatServiceDefaultName
  * TomcatServiceName
  * TomcatServiceFileName
  * TomcatServiceManagerFileName
  * TomcatAdminEnable
  * TomcatAdminUsername
  * TomcatAdminPassword
  * TomcatAdminRoles

  通过使用````/C=...````和````/s````以及````/D=````其实可以执行完整的配置 Apache Tomcat 无人安装。

* 参考 [Windows Service HOW-TO](http://tomcat.apache.org/tomcat-8.5-doc/windows-service-howto.html) 获取有关管理作为 Windows 系统服务的 Tomcat 的更多信息。

安装器将创建快捷方式用于启动和配置 Tomcat 。需要特别注意的是，只有当 Tomcat 处于运行状态时其管理应用才是可用的。

### Unix 守护进程

使用来自 commons-daemon 项目的 jsvc 工具，Tomcat 可以作为守护进程运行。jsvc 的源码压缩包已经被包含在 Tomcat 二进制文件中，因而是需要编译的。构建 jsvc 需要 C ANSI 编译器（比如 GCC），GNU Autoconf，以及一个 JDK。

运行脚本之前，环境变量````JAVA_HOME````应该被设定为 JDK 的根目录。另外，当调用````./configure````脚本时，JDK 的路径可以通过参数````--with-java````指定，形如````./configure --with-java=/usr/java````。

使用如下命令产生一个编译后的 jsvc 二进制文件，位于````$CATALINA_HOME/bin````文件夹下。此处假定使用了 GNU TAR，同时````CATALINA_HOME````环境变量指向 Tomcat 安装根目录。

注意，在 FreeBSD 操作系统中，应该使用 GNU make (gmake) ，而不是本地的 BSD make。

````shell
cd $CATALINA_HOME/bin
tar xvfz commons-daemon-native.tar.gz
cd commons-daemon-1.1.x-native-src/unix
./configure
make
cp jsvc ../..
cd ../..
````

接下来 Tomcat 可以通过以下命令作为守护进程运行：

````shell
CATALINA_BASE=$CATALINA_HOME
cd $CATALINA_HOME
./bin/jsvc \
    -classpath $CATALINA_HOME/bin/bootstrap.jar:$CATALINA_HOME/bin/tomcat-juli.jar \
    -outfile $CATALINA_BASE/logs/catalina.out \
    -errfile $CATALINA_BASE/logs/catalina.err \
    -Dcatalina.home=$CATALINA_HOME \
    -Dcatalina.base=$CATALINA_BASE \
    -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager \
    -Djava.util.logging.config.file=$CATALINA_BASE/conf/logging.properties \
    org.apache.catalina.startup.Bootstrap
````

当运行在 Java 9 平台上时，你需要在启动 jsvc 时额外指定下列参数以避免在关闭时的警告：

````shell
...
--add-opens=java.base/java.lang=ALL-UNNAMED \
--add-opens=java.base/java.io=ALL-UNNAMED \
--add-opens=java.rmi/sun.rmi.transport=ALL-UNNAMED \
...
````

你还需要指定````-jvm server````，如果 JVM 默认使用服务器 VM 而不是客户端 VM，这个问题在 OSX 上已经被发现过。

jsvc 还有其它有用参数，比如````-user````参数可以在守护进程初始化完成之后将其切换到另一个用户。这样一来就可以实现，以非特权用户启动 Tomcat 之后还可以随时使用特权端口。注意，如果你使用此选项同时作为 root 用户启动 Tomcat，你将需要关闭````org.apache.catalina.security.SecurityListener````检查，该检查会阻止以 root 用户身份启动 Tomcat 。

````jsvc --help````将返回完整的 jsvc 使用信息。特别地，````-debug````选项对调试 jsvc 运行问题非常有用。

````$CATALINA_HOME/bin/daemon.sh````文件可以被用来作为模版，用来通过 jsvc 在系统启动时从````/etc/init.d````自动启动 Tomcat 。

注意，为了以这种方式运行 Tomcat ，Commons-Daemon JAR 文件必须在你的运行时 classpath 下。Commons-Daemon JAR 文件位于 bootstrap.jar 的 manifest 文件的 Class-Path 入口，但是如果你仍然遇到关于Commons-Daemon 类的````ClassNotFoundException````或者````NoClassDefFoundError````，那就在启动 jsvc 时将Commons-Daemon JAR 文件添加到 -cp 参数中。

----

## 第一个 webapp

## Application Developer's Guide

**Version 8.5.37, Dec 12 2018**

----

## 内容索引

### 前言

此手册包含来自很多 Tomcat 项目开发者的共享。下面的作者贡献了主要部分：

* Craig R. McClanahan ([craigmcc@apache.org](mailto:craigmcc@apache.org))

### 内容索引

本手册内容分为以下章节：

* [**介绍**](http://tomcat.apache.org/tomcat-8.5-doc/appdev/introduction.html) - 此手册涵盖的信息的简要介绍，同时还有其它信息源的链接或者引用。
* [**安装**](http://tomcat.apache.org/tomcat-8.5-doc/appdev/installation.html) - 涵盖获取和安装必须的软件组件以使用 Tomcat 进行 web 应用开发。
* [**部署组织**](http://tomcat.apache.org/tomcat-8.5-doc/appdev/deployment.html) - 讨论由 Servlet API 规范定义的 web 应用的标准的文件目录结构，部署描述器文件，以及在你的开发环境中集成 Tomcat 的选项。
* [**源代码组织**](http://tomcat.apache.org/tomcat-8.5-doc/appdev/source.html) - 描述一种有用的方法来组织你的项目的源代码目录结构，同时介绍````build.xml````文件，Ant 根据该文件管理项目编译过程。
* [**开发过程**](http://tomcat.apache.org/tomcat-8.5-doc/appdev/processes.html) - 提供关于使用推荐的部署和源代码组织结构的典型的开发过程的简要描述。
* [**例子应用**](http://tomcat.apache.org/tomcat-8.5-doc/appdev/sample/) - 一个非常简单，而功能健全的例子应用，使用此手册中介绍的概念构建。你可以通过该例子应用练习使用相关技术。

## 介绍

### 概览

恭喜！你已经决定（或者被告知）学习如何利用 Servlets 和 JSP 页面构建 web 应用，同时选用了 Tomcat 服务器进行学习和开发。但是现在该干什么呢？

此手册是关于使用 Tomcat 来配置一个开发环境、组织你的源代码以及构建和测试你的应用的基本步骤的入门级介绍。这里不讨论 web 应用开发架构或者推荐的代码实践，也不会提供有关执行相关开发工具的深入介绍。附加信息的来源引用包含在接下来的章节中。

此手册中的讨论目标是使用文本编辑器和命令行工具进行应用开发和调试的开发者。因此，其中的推荐都非常通用，但是你应该可以很容易地将它们应用到 windows 或者 Unix 开发环境。如果你使用 IDE 工具，就需要分辨此处给出的建议是否适用于你的特定开发环境。

### 链接

下面的链接提供了访问对应在线资源的方式，包括文档和软件，对使用 Tomcat 进行应用开发非常有用。

* <https://jcp.org/aboutJava/communityprocess/mrel/jsr245/index2.html> - *JavaServer Pages (JSP) Specification, Version 2.3*。描述由 JSP 技术标准实现提供的编程环境。与 Servlet API Specification 相结合，本文档描述了包含的一个可移植的 API 页面。关于脚本、标签扩展以及 JSP 页面打包等的特定信息也是非常有用的。规范中包含了相应的 Javadoc API 文档，并随着 Tomcat 一同下载。
* <http://jcp.org/aboutJava/communityprocess/final/jsr340/index.html> - *Servlet API Specification, Version 3.1*。描述了所有声称遵循规范的所有 servlet 容器必须提供的编程环境。特别地，你将需要通过此文档理解 web 应用的目录结构和部署文件，将请求 URIs 映射到 servlet 的方法，容器管理的安全机制，以及应用部署描述器文件````web.xml````文件语法。规范中包含了相应的 Javadoc API 文档，并随着 Tomcat 一同下载。

## 安装

### 安装

为了使用 Tomcat 开发 web 应用，你必须首先安装它以及它所依赖的软件。下面列出必要的步骤。

#### JDK

Tomcat 8.5 被设计为运行在 Java SE 7 平台上。

多平台的兼容 JDK 可以从 <http://www.oracle.com/technetwork/java/javase/downloads/index.html>  获得。

#### Tomcat

Tomcat 服务器的二进制包下载地址 <https://tomcat.apache.org/>。此手册假定你使用的是 Tomcat 8 的最新发布版本。下载和安装过程的详细介绍参考 [这里](http://tomcat.apache.org/tomcat-8.5-doc/setup.html)。

在此手册剩余部分中，shell 脚本的例子假定你已经将 Tomcat 安装路径名设定为系统环境变量````CATALINA_HOME````。如果 Tomcat 已经被配置为多实例模式，每个实例都需要配置自己专门的````CATALINA_BASE````，当然这是可选的。

#### Ant

Ant 的二进制包下载地址 <https://ant.apache.org/>。此手册假定你使用的是 Ant 1.8 或者更高版本。这里的说明应该也是适用于其他版本的俄，不过并没有经过测试。

下载并安装 Ant。然后将安装目录中的````bin````目录添加到你的````PATH````环境变量中，按照你所使用的操作系统平台的设置方法。完成这一步设置之后，你就可以直接执行````ant````shell 命令。

#### CVS

除了上面提到的必须工具，强烈推荐你下载和安装源码控制系统，比如 CVS，用来维护构成你的应用的源代码的历史版本。除了服务端软件，你还需要对应的客户端软件来完成代码的签出和提交。

源码控制系统的详细介绍超出了本手册的范围，所以就不多说了……

## 部署

### 内容索引

- [背景](http://tomcat.apache.org/tomcat-8.5-doc/appdev/deployment.html#Background)
- [标准文件目录结构](http://tomcat.apache.org/tomcat-8.5-doc/appdev/deployment.html#Standard_Directory_Layout)
- [共享类库文件](http://tomcat.apache.org/tomcat-8.5-doc/appdev/deployment.html#Shared_Library_Files)
- [部署描述器文件](http://tomcat.apache.org/tomcat-8.5-doc/appdev/deployment.html#Web_Application_Deployment_Descriptor)
- [Tomcat 上下文描述器](http://tomcat.apache.org/tomcat-8.5-doc/appdev/deployment.html#Tomcat_Context_Descriptor)
- [在 Tomcat 上部署](http://tomcat.apache.org/tomcat-8.5-doc/appdev/deployment.html#Deployment_With_Tomcat)


### 背景

描述如何组织你的源代码目录结构之前，检查 web 应用的运行时组织结构是很有用的。在 Servlet API 规范 2.2 版本之前，服务器平台之间仅有很少的连贯性。然而，生成遵循 2.2 或者更高版本规范的服务器实现都必须接受标准格式的 web 应用归档包。后面我们会继续讨论。

一个 web 应用被定义为基于标准布局的目录和文件的层级结构。这个层级结构可以以尚未打包的形式被访问，彼时每个目录和文件都独立存在于文件系统中。也可以以打包之后的形式被访问，也就是众所周知的  Web ARchive 文件或者 WAR 文件形式。前者在开发过程中更有用，后者在你发布应用用于安装时更有用。

web 应用的顶层目录也就是你的应用的根目录。此处，你可以放置 HTML 文件和 JSP 页面来构成你的应用的用户界面。当系统管理员将你的应用部署到特定的服务器中时，他会配置一个````context path````给你的应用。因此，如果系统管理员将````/catalog````分配给你的应用作为````context path````，则 URI 指向````/catalog/index.html````的请求将从你的应用根目录中获取````index.html````文件。

### 标准目录布局

为了方便创建标准格式的 web 应用归档文件，传统的做法是将你的应用中的可执行文件（也就是 Tomcat 执行你的应用时实际使用的文件）按照 WAR 格式文件本身的要求组织起来。也就是说，你可以将以下内容放在你的应用的根文件目录中：

* **\*.html, \*.jsp, etc. ** - HTML 文件和 JSP 页面，连同其它必须对客户端浏览器可见的文件（比如 JavaScript, stylesheet 文件以及图片等）。在大型应用中，你可以将这些文件分门别类放入不同的子目录中。
* **/WEB-INF/web.xml** - 应用的部署描述器文件。这是一个 xml 文件，描述组成你的应用的 servlets 和其它组件，连同所有的初始化参数和你希望服务器可以向你保证的容器管理的安全约束。此文件将在后续章节中详细讨论。
* **/WEB-INF/classes** - 此目录包含你的应用必需的所有 Java 类文件（以及相关资源），包含 servlet 和非 servlet 类，它们没有被加入 JAR 包中。如果你的类文件被组织进入 Java 包中，你就必须将其反映在````/WEB-INF/classes````目录下的目录结构中。比如，名为````com.mycompany.mypackage.MyServlet````的 Java 类需要被存储在名为````/WEB-INF/classes/com/mycompany/mypackage/MyServlet.class````的类文件中。
* **/WEB-INF/lib/** - 此目录包含你的应用所需的 Java 类文件（以及相关资源）打包成的 JAR 文件。比如第三方类库或者 JDBC 驱动。

当你将应用安装到 Tomcat（或者其它 2.2 或更高版本的 Servlet 容器） 中，````/WEB-INF/classes````目录下的类文件，连同````/WEB-INF/lib/````目录下的 JAR 包中所有的类文件，都会对应用中的其它类可见。因此，如果你将所有的必需类库都放到同一个地方，你就可以很简单地安应用，而不需要修改系统 classpath。

这些信息很多都来自 Servlet API 规范 2.3 版本的第 9 章，可以参考以获取更多细节。

### 共享类库文件

跟大部分 servlet 容器一样，Tomcat 也支持安装类库 JAR 文件（或者未打包的类）的机制，同时使它们对所有安装的 web 应用可见（而不需要包含在 web 应用内部）。Tomcat 如何定位和共享这些类的细节描述放在 [Class Loader HOW-TO](http://tomcat.apache.org/tomcat-8.5-doc/class-loader-howto.html) 文档中。Tomcat 用来共享代码的通用目录是````$CATALINA_HOME/lib````。放在这里的 JAR 文件对 web 应用和 Tomcat 内部代码都是可见的。这里就很适合存放 web 应用和 Tomcat 都需要的 JDBC 驱动文件。

一个标准的 Tomcat 安装包含大量的开箱即用的共享类库，包括：

* Servlet 3.1 和 JSP 2.3 API，是编写 servlets 和 JavaServer Pages 的基础。

### 部署描述器文件

就像上面提到的，````/WEB-INF/web.xml````文件包含了应用的部署描述器。该文件扩展名表明，它是一个 xml 文件，定义了服务器需要知道的有关你的应用的所有信息（不包括````context path````，该属性由系统管理员在部署应用时分配）。

部署描述器文件的完整语法和语义由 Servlet API 规范 2.3 版本的第 13 章定义。随着时间推移，出现了很多开发工具可以用于创建和编辑部署描述器文件。在此基础上，开发工具会提供一个初始的 [basic web.xml file](http://tomcat.apache.org/tomcat-8.5-doc/appdev/web.xml.txt) 包含了其中每个元素的注解和目的描述。

注意：Servlet 规范包含了一个关于部署描述器文件的文档类型描述器（DTD），Tomcat 在处理你的应用中的````/WEB-INF/web.xml````文件时会强制执行这里定义的规则。特别地，你必须按照 DTD 定义的顺序将你的描述器元素放入部署描述器文件。

### Tomcat 上下文描述器

````/META-INF/context.xml````文件可以被用来定义 Tomcat 特定的配置选项，比如访问日志，数据源，会话管理配置等等。此文件必须包含一个上下文元素，它将被看作是 Host 元素的子元素，该 Host 元素对应于该 web 应用部署到其上的主机。[Tomcat configuration documentation](http://tomcat.apache.org/tomcat-8.5-doc/config/context.html) 包含了有关信息。

### 在 Tomcat 中部署

接下来的描述中使用变量名````$CATALINA_BASE````表示解析大多数项目路径时的根目录。如果你尚未为多实例的 Tomcat 配置各自的````CATALINA_BASE````目录，则````$CATALINA_BASE````就会被设置为````$CATALINA_HOME````的值，也就是你的 Tomcat 安装目录。

web 应用必须被部署到 Servlet 容器中才能执行，即使是在开发过程中。我们将描述如何使用 Tomcat 构建执行环境。web 应用可以通过如下任意一种方式部署到 Tomcat 中：

* 将未打包的目录层级结构复制到````$CATALINA_BASE/webapps/````目录的子目录下。Tomcat 将基于你选择的子目录名为你的应用分配一个 context path 。我们将使用我们在````build.xml````文件中构建的技术，因为这是开发过程中最快和最简单的部署方式。注意，安装或者升级你的应用之后需要重启 Tomcat。
* 将 web 应用归档包文件复制到````$CATALINA_BASE/webapp/````目录下。当 Tomcat 启动后，它将自动解压应用归档文件，然后执行应用。这种方式典型地用于安装由第三方提供商提供或者来自你的开发组的同事的附加应用到已经存在的 Tomcat 安装中。注意：如果你使用这种方法，同时希望随后升级你的应用，你就必须同时替换归档文件和解压后的文件夹，这样你的修改才会生效。
* 使用 Tomcat 管理 web 应用部署和卸载 web 应用。Tomcat 包含一个 web 应用，默认部署在````/manager````上下文路径下。它允许你在运行中的 Tomcat 上部署和卸载应用，而不需要重启。更多信息可参考 [Manager App HOW-TO](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html)。
* 使用你的构建脚本中的管理 Ant 任务。Tomcat 包含一系列为````Ant````构建工具定义的客户化任务，这些任务允许你自动化执行管理 web 应用。这些任务被用在 Tomcat 部署器中。
* 使用 Tomcat 部署器。Tomcat 包含一个集成了 Ant 任务的打包了的工具，可以在将应用部署到服务器之前自动预编译 JSPs。

将应用部署到其他 servlet 容器的方法可能各有不同，但是所有声称遵循 Servlet API 规范 2.2 或者更高版本的容器都被强制接受 web 应用归档文件。注意，其他容器并不强制接受解压后的目录结构，也不强制提供类库文件共享机制，不过这些特性通常都是可用的。

## 源代码组织

### 内容列表

- [目录结构](https://tomcat.apache.org/tomcat-8.5-doc/appdev/source.html#Directory_Structure)
  1. [扩展依赖](https://tomcat.apache.org/tomcat-8.5-doc/appdev/source.html#External_Dependencies)
- [源代码控制](https://tomcat.apache.org/tomcat-8.5-doc/appdev/source.html#Source_Code_Control)
- [BUILD.XML 配置文件](https://tomcat.apache.org/tomcat-8.5-doc/appdev/source.html#BUILD.XML_Configuration_File)

### 目录结构

下面描述中使用变量名````$CATALINA_BASE````表示解析相对路径时使用的根目录。如果你尚未为多个 Tomcat 实例分别指定````CATALINA_BASE````目录，则````$CATALINA_BASE````就会被设定为````CATALINA_HOME````的值，也即是你的 Tomcat 的安装路径。

本手册的一个关键的推荐做法就是将你的源代码目录结构与可部署应用的目录结构独立开来。保持这种独立性有以下好处：

* 源代码目录内容可以更容易管理、移动以及备份，因为所谓的“可执行”版本没有被源代码污染。
* 在仅仅只包含源代码的目录中更容易进行源代码控制。
* 部署层级结构独立时更容易选择可用于安装的应用的发布内容。

如我们即将看到的，````Ant````开发工具将以近乎无痛的方式创建和处理这些目录结构。

实际上，你几乎可以使用任何具体的目录和文件来组织你的应用的源代码。不过，下面的组织结构已经被证明是相当通用的，同时也是下面将要讨论的````build.xml````配置文件所期望的。所有这些组件都存在于应用的顶层工程源代码目录下面：

* **docs/** - 你的应用的文档，可用选用任意文件格式。
* **src/** - 产生 servlets、beans 及其它专属于你的应用的 Java 类的 Java 源代码文件。如果你的源代码被组织成包的形式（强烈推荐），则包层级结构就应该反映当前目录下的目录结构。
* **web/** - 对客户端可见的网站的静态内容 (HTML 页面, JSP 页面, JavaScript 文件, CSS 样式表文件, 以及图片) 。这个目录将是你的应用的根目录，所有这里的子目录都将反映在试图访问这些文件的请求的 URIs 中。
* **web/WEB-INF/** - 应用需要的特定配置文件，包括应用的部署描述器文件，你创建的客户化标签类库的描述器文件，以及其它你希望包含在应用中的其它资源文件。尽管此目录看起来是你的应用根目录的子目录，但是 Servlet 规范禁止客户端请求该目录以及其中文件。因此，这里很适合存放应用必需的敏感配置信息，比如数据库连接用户名和密码等。

在开发过程中，下面两个临时目录将会被创建：

* **build/** - 当你执行默认构建（````ant````）之后，该目录将包含应用的归档文件中包含的文件的完整拷贝。Tomcat 允许你以这种非打包目录形式部署应用，要么将该目录内容复制到````$CATALINA_BASE/webapps````目录，要么通过管理应用安装它。后者在开发过程中非常有用，稍后举例说明。
* **dist/** - 当你执行````ant dist````之后，此目录将被创建。它将创建你的应用的二进制发布文件的完整拷贝，包含你预先准备好的授权信息、文档以及 README 文件。

注意：这两个文件夹不应该加入源代码控制系统，因为在开发过程中会随时被删除和重建。同样的原因，你不应该在这些目录中对代码进行任何修改，因为所有修改都会在下一次构建后彻底丢失。

#### 扩展依赖

当你的应用需要来自其它项目或者包的 JAR 文件时，你会怎么办？最常见的例子就是你的应用需要包含 JDBC 驱动。

不同的开发者采取不同的策略应对此问题。比如将这些需要的包的拷贝加入所有需要它们的应用的源代码归档包中。然而，这将导致严重的管理问题，当你在许多应用中使用同一个 JAR 包，特别是当你需要更新这些 JAR 包时。

因此，我们推荐你不要将需要的包拷贝到源码归档文件中。更好的做法是，将这些扩展依赖的集成作为应用构建过程的一部分。采用这种方式，你就可以始终从系统管理员安装这些依赖包的源头自动获取合适的版本，而不需要每当这些扩展依赖改变时就升级你的应用。

在例子 Ant ````build.xml````文件中，我们将举例说明如何定义````build````属性以配置需要拷贝的文件的位置，而当这些文件发生变化时不需要修改````build.xml````文件。特定开发者使用的该构建属性可以为每个应用特殊设定，或者默认为开发者根目录中存储的默认构建属性。

很多情况下，你的开发环境系统管理员应该已经将必需的 JAR 文件安装到 Tomcat 的````lib````目录中。这样的话你自己就不会面对扩展依赖的问题。例子````build.xml````文件会自动创建包含这些文件的编译 classpath。

### 源代码控制

就像前面提到的，推荐你将所有组成你的应用的源代码文件和相关资源文件都通过类似 CVS 的源代码控制系统管理起来。如果你这么做了，源代码层级结构中的每个目录和文件都应该被注册和保存，除了那些自动生成的文件。如果你将二进制格式的文件也放到了源码控制系统中，请确保明确标记出来。

我们推荐你不要保存````build/````和````dist/````目录下的内容到源码控制系统中。通过创建在你的源代码顶层目录中````.cvsignore````文件可以告诉 CVS 忽略这些目录。该文件目录可以是：

````xml
build
dist
build.properties
````

这里包含````build.properties````文件的原因将在 [Processes](http://tomcat.apache.org/tomcat-8.5-doc/appdev/processes.html) 章节中解释。

### BUILD.XML 配置文件

我们将使用 **ant** 工具管理你的源代码的编译，同时创建部署层级结构。Ant 在构建文件控制下工作，该构建文件通常叫做````build.xml````，定义了构建过程的必要步骤。这个文件位于你的源代码顶级目录中，而且应该被你的源代码控制系统管理。

类似于 Makefile，该````build.xml````文件提供了若干````target````来支持可选的开发行为，比如创建相关的文档，清除部署根目录以便于从源码构建项目，或者创建 web 应用归档文件以便于发布应用。

----

## 部署

----

### 内容列表

- [介绍](http://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html#Introduction)
- [安装](http://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html#Installation)
- [上下文](http://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html#A_word_on_Contexts)
- [Tomcat 启动时部署](http://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html#Deployment_on_Tomcat_startup)
- [Tomcat 服务器运行时部署](http://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html#Deploying_on_a_running_Tomcat_server)
- [使用 Tomcat Manager 部署](http://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html#Deploying_using_the_Tomcat_Manager)
- [使用 Client Deployer Package 部署](http://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html#Deploying_using_the_Client_Deployer_Package)

### 介绍

所谓部署，就是将 web 应用安装到 Tomcat 服务器中的过程。

在 Tomcat 服务器上的应用部署可以通过很多种方法实现：

* 静态部署：Tomcat 启动之前就把 web 应用设置好。
* 动态部署：直接操作已经部署的应用（依赖自动部署特性），或者通过 Tomcat Manager web 应用远程操作应用。

[Tomcat Manager](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html) 是一个可以用来通过页面方式或者编程方式部署和管理 web 应用的应用。

有很多方法可以通过 Manager 应用执行部署。Apache Tomcat 为 Apache Ant 构建工具提供了相关任务。[Apache Tomcat Maven Plugin](https://tomcat.apache.org/maven-plugin.html) 项目提供了与 Apache Maven 的集成。同时还有叫做客户端部署器的工具，可以用来通过命令行提供额外的功能，比如编译和验证 web 应用，以及将 web 应用打包成 WAR 文件。

### 安装

对Tomcat 默认提供的开箱即用的 web 应用的静态安装方式没有任何强制性要求，也对通过 Tomcat Manager 部署功能也没有强制性要求，不过在 [Tomcat Manager manual](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html) 中对某些配置做了强制性要求。如果你想要使用 Tomcat Client Deployer （TCD）则无论如何都需要安装。

TCD 并没有包含在 Tomcat 核心发布版本中，因此必须手动单独下载。下载地址通常标识为 *apache-tomcat-8.5.x-deployer*。

TCD 需要 Apache Ant 1.6.2+ 和 Java 安装。你的系统中应该定义了````ANT_HOME````环境变量指向 Ant 安装根目录，````JAVA_HOME````环境变量指向 Java 安装目录。另外，你应确保 Ant 的````ant````命令和 Java 的````javac````命令都是可以从命令行执行的。

1. 下载 TCD 发布包；
2. 不需要将 TCD 解压到任何已经存在的 Tomcat 安装目录中，它可以解压到任意位置；
3. 查阅使用手册 [Tomcat Client Deployer](http://tomcat.apache.org/tomcat-8.5-doc/deployer-howto.html#Deploying_using_the_Client_Deployer_Package)。

### 上下文

当我们讨论 web 应用的部署时，必须理解 *Context* 术语。Tomcat 将 web 应用称为````Context````。

为了配置 Tomcat 中的 Context，一个 *Context Descriptor* 是必需的。上下文描述器就是一个简单的 XML 文件，其中包含 Tomcat 中有关上下文的配置，比如资源命名和会话管理配置。在 Tomcat 早期版本中，上下文描述去配置通常存储在 Tomcat 的主配置文件 *server.xml* 中（如今不推荐这种做法，不过仍然能用）。

上下文描述器不仅帮助 Tomcat 了解如何配置上下文，而且可以为诸如 Tomcat Manager 和 TCD 之类经常使用上下文描述器的工具执行它们各自的功能提供支持。

上下文描述器文件的位置：

1. ````$CATALINA_BASE/conf/[enginename]/[hostname]/[webappname].xml````
2. ````$CATALINA_BASE/webapps/[webappname]/META-INF/context.xml````

如果没有为上下文提供相应的描述器文件，则 Tomcat 将为上下文配置默认值。

### Tomcat 启动时部署

如果你不想使用 Tomcat Manager，或者 TCD，那么你就需要将你的应用静态部署到 Tomcat，然后再启动 Tomcat 。通过这种方式部署的应用的位置叫做````appBase````，每个主机都有各自特定的````appBase````。你可以将未打包的应用文件复制到该目录，或者将打包后的 WAR 文件复制过去。

位于主机（默认主机就是````localhost````）指定的特定````appBase````(默认的 appBase 是````$CATALINA_BASE/webapps````)目录下的 web 应用在 Tomcat 启动时将会被部署，如果主机的````deployOnStartup````属性是````true````。

这种情况下，Tomcat 启动时会发生如下的部署序列：

1. 所有上下文描述器将首先被部署；
2. 没有被任何上下文描述器引用的未打包的应用将接下来被部署，如果在````appBase````目录下存在相关的 WAR 包文件而且它又比未打包的应用更加新鲜，则未打包的目录将会被删除并且应用将会从该 WAR 包文件被重新部署。
3. WAR 包文件最后被部署。

### 在运行中的 Tomcat 上部署

你可以在运行中的 Tomcat 上部署应用。

如果主机的````autoDeploy````属性是````true````，则该主机将试图根据需要动态部署和升级应用。比如一个新的 WAR 包被放进````appBase````目录。为了做到这些，主机需要运行一套后台处理机制来获取相应的默认配置。

将````autoDeploy````设定为````true````之后运行中的 Tomcat 允许：

* 部署被复制到主机的````appBase````目录下的 WAR 文件。
* 部署被复制到主机的````appBase````目录下的未打包的 web 应用。
* 当新版本的 WAR 包出现时更新从该 WAR 包部署的应用。这种情况下未打包的 web 应用将被移除，同时 WAR 包会被重新解压。注意，如果主机的````unpackWARs````属性设定为````false````则 WAR 包就不会被解压，应用就只会简单地从 WAR 包被重新部署。
* 如果````WEB-INF/web.xml````文件或者任何其它定义为````WatchedResource````的资源文件更新时重新加载 web 应用。
* 当服务部署以来的额上下文描述器文件更新时重新部署 web 应用。
* 当应用使用的全局或者主机特定的上下文描述器文件更新时重新部署 web 应用。
* 当上下文描述器文件被添加到````$CATALINA_BASE/conf/[enginename]/[hostname]/````目录中时重新部署 web 应用。
* 当应用的根目录（docBase）被删除时卸载 web 应用。注意，在 Windows 系统下，假定````anti-locking````特性（参考上下文配置文档）是可用的，否则运行中的 web 应用的资源文件是不可能被删除的。

注意，web 应用的重新加载也可以被配置在加载器中，这样所有的被加载的类的修改都会被追踪。

### 使用 Tomcat Manager 部署

Tomcat Manager 有 [自己的使用手册](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html)。

### 使用客户端部署器包部署

最后，web 应用还可以通过 Tomcat 客户端部署器实现。这个包可以用于 web 应用的验证、编译、压缩为 WAR 包，以及将应用部署到开发环境或者生产环境的 Tomcat 服务器中。需要注意的是，该特性使用了 Tomcat Manager 因此需要保证目标 Tomcat 服务器处于运行中。

假定用户非常熟悉 Apache Ant 以使用 TCD。Apache Ant 是一个脚本化的构建工具。TCD 被预先跟使用的构建脚本打包在一起使用。只需要对 Apache Ant 的基本了解即可。

TCD 包含 Ant 任务、用于部署之前的 JSP 编译的 jasper 页面编译器、以及 web 应用上下文描述器验证任务。该验证任务（````org.apache.catalina.ant.ValidatorTask````类）只允许一个参数：未打包的应用的根目录。

TCD 以未打包的应用作为输入。通过部署器以编程方式部署的 web 应用可以包含一个上下文描述器，位于````/META-INF/context.xml````文件中。

TCD 包含一个随时可用的 Ant 脚本，具有以下目标：

* ````compile````(默认)：编译并验证 web 应用。可以用于单独安装的情形，而不需要一个运行中的 Tomcat 。被编译的应用将只运行在相应的 *Tomcat X.Y.Z* 发布版本上，当时并不保证能够运行在其它版本上，因为 Jasper 产生的代码依赖于它的运行时组件。还需要注意，此目标会同时自动编译位于应用的````WEB-INF/classes````目录下的所有 Java 源代码文件。
* ````deploy````：部署一个 web 应用（无论是否编译）到 Tomcat 服务器。
* ````undeploy````：卸载一个 web 应用。
* ````start````：启动 web 应用。
* ````reload````：重新加载 web 应用。
* ````stop````：停止 web 应用。

为了配置部署参数，在 TCD 安装根目录中创建````deployer.properties````文件，其中每行包含一个下列名值对：

* ````build````：将使用 build 文件夹，默认的，````${build}/webapp/${path}```` (````${build}````，默认指向````${basedir}/build````)。在````compile````目标执行结束之后，应用的 WAR 文件将会被放在````${build}/webapp/${path}.war````。
* ````webapp````：包含未打包的即将被编译和验证的应用的文件的目录。默认文件夹为````myapp````。
* ````path````：已经部署的 web 应用的上下文路径，默认为````/myapp````。
* ````url````：运行中的 Tomcat 服务器的 Tomcat Manager web 应用的绝对路径，将会被用于部署和卸载应用。默认情况下，部署器将会试图访问````localhost````上运行的 Tomcat 实例，位于````http://localhost:8080/manager/text````。
* ````username````：Tomcat Manager 用户名（用户应该拥有管理员脚本角色）。
* ````password````：Tomcat Manager 密码。

----

## Manager App 手册

----

### 内容列表

- [介绍](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Introduction)
- [配置 Manager 应用访问](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Configuring_Manager_Application_Access)
- [HTML 用户友好接口](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#HTML_User-friendly_Interface)
- [已支持的 Manager 命令](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Supported_Manager_Commands)
  1. [命令参数](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Common_Parameters)
  2. [远程部署新的 Application Archive (WAR) ](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Deploy_A_New_Application_Archive_(WAR)_Remotely)
  3. [从本地路径部署新的 Application](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Deploy_A_New_Application_from_a_Local_Path)
     1. [部署一个之前部署过的 webapp](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Deploy_a_previously_deployed_webapp)
     2. [通过 URL 部署目录或者 WAR](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Deploy_a_Directory_or_WAR_by_URL)
     3. [从 Host appBase 部署目录或者 War](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Deploy_a_Directory_or_War_from_the_Host_appBase)
     4. [使用上下文配置 ".xml" 文件进行部署](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Deploy_using_a_Context_configuration_%22.xml%22_file)
     5. [部署注意事项](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Deployment_Notes)
     6. [部署响应](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Deploy_Response)
  4. [当前已部署应用列表](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#List_Currently_Deployed_Applications)
  5. [重新加载一个已存在的应用](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Reload_An_Existing_Application)
  6. [操作系统和虚拟机参数列表](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#List_OS_and_JVM_Properties)
  7. [可用的全局 JNDI 资源列表](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#List_Available_Global_JNDI_Resources)
  8. [会话统计](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Session_Statistics)
  9. [会话超时](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Expire_Sessions)
  10. [启动一个已存在的应用](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Start_an_Existing_Application)
  11. [停止一个已存在的应用](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Stop_an_Existing_Application)
  12. [卸载一个已存在的应用](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Undeploy_an_Existing_Application)
  13. [寻找内存泄漏](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Finding_memory_leaks)
  14. [连接器 SSL/TLS 加密信息](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Connector_SSL/TLS_cipher_information)
  15. [连接器 SSL/TLS 凭证链信息](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Connector_SSL/TLS_certificate_chain_information)
  16. [连接器 SSL/TLS 信任凭证信息](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Connector_SSL/TLS_trusted_certificate_information)
  17. [重新加载 TLS 配置](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Reload_TLS_configuration)
  18. [线程内存镜像](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Thread_Dump)
  19. [虚拟机信息](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#VM_Info)
  20. [保存配置](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Save_Configuration)
- [服务器状态](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Server_Status)
- [使用 JMX Proxy Servlet](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Using_the_JMX_Proxy_Servlet)
  1. [什么是 JMX Proxy Servlet](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#What_is_JMX_Proxy_Servlet)
  2. [JMX 查询命令](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#JMX_Query_command)
  3. [JMX Get 命令](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#JMX_Get_command)
  4. [JMX Set 命令](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#JMX_Set_command)
  5. [JMX Invoke 命令](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#JMX_Invoke_command)
- [通过 Ant 执行 Manager 命令](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Executing_Manager_Commands_With_Ant)
  1. [任务输出捕获](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Tasks_output_capture)

### 介绍

在很多生产环境中，在不停止或者重启整个容器的情况下部署新的 web 应用或者卸载已经存在的应用是很有用的。另外，你能够请求一个已经存在的应用重新加载它自己，哪怕你在 Tomcat 服务器配置文件中并没有声明该应用是````reloadable````的。

为了支持这些能力，Tomcat 包含了一个 web 应用（默认安装在上下文路径````/manager````）来支持以下功能：

* 从上传的 WAR 包文件内容中部署一个新的 web 应用。
* 从服务器文件系统中部署一个新的 web 应用到指定上下文路径中。
* 列出当前已经部署的 web 应用，以及连接到这些 web 应用的所有活动会话。
* 重新加载已存在的 web 应用，以反映````/WEB-INF/classes````或者````/WEB-INF/lib````目录内容的变化。
* 列出操作系统和 Java 虚拟机参数值。
* 列出可用的全局 JNDI 资源，这些资源将被部署工具使用，以````<ResourceLink>````元素的形式预先准备在一个````<context>````部署描述中。
* 启动一个停止的应用（使其重新可用）。
* 停止一个已存在的应用（因此它会变为不可用），但是并不卸载它。
* 卸载一个已部署的应用，同时删除它的文件系统中的根目录（除非它是从文件系统部署的）。

默认的 Tomcat 安装包含该 Manager。将````manager.xml````上下文配置文件安装到````$CATALINA_BASE/conf/[enginename]/[hostname]````文件夹下就可以将一个 Manager 实例````Context````添加到新的主机中。下面是一个例子：

````xml
<Context privileged="true" antiResourceLocking="false"
         docBase="${catalina.home}/webapps/manager">
  <Valve className="org.apache.catalina.Valves.RemoteAddrValve"
         allow="127\.0\.0\.1"/>
</Context>
````

如果你的 Tomcat 被配置为支持多个虚拟主机（网站），你就需要为每个主机配置一个 Manager。

下面是使用 Manager 的三种方法：

* 作为一个自带用户界面的应用在浏览器中使用。举个例子，你可以在 URL 中用你的网站主机名````http://localhost:8080/manager/html````替换````localhost````。
* 最小版本使用 HTTP 请求仅仅适用于被系统管理员设置的脚本使用。请求作为请求 URI 的一部分给出，响应是简单的文本形式，很容易转化和处理。更多详情参见 [Supported Manager Commands](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Supported_Manager_Commands)。
* 一个方便的 Ant 构建工具（1.4版本及更高）的任务定义集合。更多信息参见 [Executing Manager Commands With Ant](http://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html#Executing_Manager_Commands_With_Ant)。

### 配置 Manager 应用访问

下面描述中使用变量名````$CATALINA_BASE````表示解析相对路径时使用的根目录。如果你尚未为多个 Tomcat 实例分别指定````CATALINA_BASE````目录，则````$CATALINA_BASE````就会被设定为````CATALINA_HOME````的值，也即是你的 Tomcat 的安装路径。

以默认配置安装运行 Tomcat 并且允许互联网上的任何人执行你的服务器上的 Manager 应用显然是相当不安全的。因此，使用该应用的用户必须认证他们的身份，使用属于````manager-xxx````角色的用户名和密码。进一步地，默认的用户文件（````$CATALINA_BASE/conf/tomcat-users.xml````）中并不包含属于该角色的用户名。因此，默认状态下访问 Manager 应用是不可能的。

你可以在 Manager 应用的````web.xml````文件中找到角色名称。可用的角色有：

* ````manager-gui````－可以访问 HTML 接口
* ````manager-status````－只可以访问````Server Status````页面
* ````manager-script````－可以访问此文档中描述的工具友好的纯文本接口，以及````Server Status````页面
* ````manager-jmx````－可以访问 JMX 代理接口和````Server Status````页面

HTML 接口是防 CSRF (跨站请求伪装) 攻击的，但是文本接口和 JMX 接口不是。这就意味着被允许访问文本接口和 JMX 接口的用户在通过浏览器访问 Manager 应用的时候就必须当心。为了维持 CSRF 防护：

* ​