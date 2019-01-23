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

* ***.html, *.jsp, etc. ** - HTML 文件和 JSP 页面，连同其它必须对客户端浏览器可见的文件（比如 JavaScript, stylesheet 文件以及图片等）。在大型应用中，你可以将这些文件分门别类放入不同的子目录中。
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

* 将未打包的目录层级结构复制到````$CATALINA_BASE/webapps/````目录的子目录下。