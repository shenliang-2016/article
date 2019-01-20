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

