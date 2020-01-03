#### 4.1.11. 管理特性

通过指定 `spring.application.admin.enabled` 属性，可以为应用程序启用与管理员相关的功能。这暴露了 MBeanServer平台上的 [`SpringApplicationAdminMXBean`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/admin/SpringApplicationAdminMXBean.java) 。您可以使用此功能来远程管理 Spring Boot 应用程序。此功能对于任何服务包装器实现也可能很有用。

> 如果您想知道应用程序在哪个 HTTP 端口上运行，请使用 `local.server.port` 键获取属性。

