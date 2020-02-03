### 4.18. JTA 的分布式事务

Spring Boot 通过使用 [Atomikos](https://www.atomikos.com/) 或 [Bitronix](https://github.com/bitronix/btm) 嵌入式事务管理器，支持跨多个 XA 资源的分布式 JTA 事务。部署到合适的 Java EE 应用程序服务器时，还支持 JTA 事务。

检测到 JTA 环境后，将使用 Spring 的 `JtaTransactionManager` 来管理事务。自动配置的 JMS，DataSource 和 JPA Bean 已升级为支持 XA 事务。您可以使用标准的 Spring 习语（例如 `@Transactional`）来参与分布式事务。如果您在 JTA 环境中，但仍要使用本地事务，则可以将 `spring.jta.enabled` 属性设置为 `false`，以禁用 JTA 自动配置。

