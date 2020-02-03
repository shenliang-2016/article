#### 4.18.3. 使用 Java EE 管理的事务管理器

如果将 Spring Boot 应用程序打包为 `war` 或 `ear` 文件并将其部署到 Java EE 应用程序服务器，则可以使用应用程序服务器的内置事务管理器。Spring Boot 尝试通过查看常见的 JNDI 位置（例如 `java:comp/UserTransaction`，`java:comp/TransactionManager` 等）来自动配置事务管理器。如果您使用应用程序服务器提供的事务服务，则通常还需要确保所有资源都由服务器管理并通过 JNDI 公开。Spring Boot 尝试通过在 JNDI 路径（`java:/JmsXA` 或 `java:/XAConnectionFactory`）中查找 `ConnectionFactory` 来尝试自动配置 JMS，并且您可以使用 [`spring.datasource.jndi-name` 属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-connecting-to-a-jndi-datasource) 来配置您的 `DataSource`。

