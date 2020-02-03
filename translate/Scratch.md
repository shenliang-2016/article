#### 4.18.1. 使用 Atomikos 事务管理器

[Atomikos](https://www.atomikos.com/) 是一种流行的开源事务管理器，可以嵌入到您的 Spring Boot 应用程序中。您可以使用 `spring-boot-starter-jta-atomikos` 启动器引入相应的 Atomikos 库。Spring Boot 自动配置 Atomikos，并确保将适当的 `depends-on` 设置应用于您的 Spring bean，以保证正确的启动和关闭顺序。

默认情况下，Atomikos 事务日志将写入应用程序主目录（应用程序 jar 文件所在的目录）中的 `transaction-logs` 目录。您可以通过在 `application.properties` 文件中设置一个 `spring.jta.log-dir` 属性来定制该目录的位置。以 `spring.jta.atomikos.properties` 开头的属性也可以用于自定义 Atomikos 的 `UserTransactionServiceImp`。请参阅 [`AtomikosProperties` Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/jta/atomikos/AtomikosProperties.html) 了解更多细节。

> 为了确保多个事务管理器可以安全地协调同一资源管理器，必须为每个 Atomikos 实例配置一个唯一的 ID。默认情况下，此 ID 是运行 Atomikos 的计算机的 IP 地址。为了确保生产中的唯一性，应为应用程序的每个实例将 `spring.jta.transaction-manager-id` 属性配置为不同的值。

