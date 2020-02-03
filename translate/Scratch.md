#### 4.18.2. 使用 Bitronix 事务管理器

[Bitronix](https://github.com/bitronix/btm) 是一种流行的开源 JTA 事务管理器实现。您可以使用 `spring-boot-starter-jta-bitronix` 启动器将适当的 Bitronix 依赖项添加到您的项目中。与 Atomikos 一样，Spring Boot 自动配置 Bitronix 并对您的 bean 进行后处理，以确保启动和关闭顺序正确。

默认情况下，Bitronix 事务日志文件（`part1.btm` 和 `part2.btm`）被写入应用程序主目录中的 `transaction-logs` 目录。您可以通过设置 `spring.jta.log-dir` 属性来定制该目录的位置。以 `spring.jta.bitronix.properties` 开头的属性也绑定到 `bitronix.tm.Configuration` bean上，以实现完全自定义。有关详细信息，请参见 [Bitronix文档](https://github.com/bitronix/btm/wiki/Transaction-manager-configuration)。

> 为了确保多个事务管理器可以安全地协调同一资源管理器，必须为每个 Bitronix 实例配置唯一的 ID。默认情况下，此 ID 是运行 Bitronix 的计算机的 IP 地址。为了确保生产中的唯一性，应为应用程序的每个实例将 `spring.jta.transaction-manager-id` 属性配置为不同的值。

