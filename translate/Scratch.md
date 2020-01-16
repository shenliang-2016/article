##### 连接到生产数据库

生产数据库的连接也可以通过使用 `DataSource` 池来自动配置。Spring Boot 使用以下算法来选择特定的实现：

1. 我们更喜欢 [HikariCP](https://github.com/brettwooldridge/HikariCP) 的性能和并发性。如果有 HikariCP，我们总是选择它。

2. 否则，如果 Tomcat 池 `DataSource` 可用，我们将使用它。

3. 如果 HikariCP 和 Tomcat 池数据源均不可用，而 [Commons DBCP2](https://commons.apache.org/proper/commons-dbcp/) 可用，我们将使用它。

如果您使用 `spring-boot-starter-jdbc` 或 `spring-boot-starter-data-jpa` `starters`，则会自动获得对  `HikariCP` 的依赖。

> 您可以通过设置 `spring.datasource.type` 属性来完全绕过该算法，并指定要使用的连接池。如果您在 Tomcat 容器中运行应用程序，这一点尤其重要，因为默认情况下会提供 `tomcat-jdbc`。

> 额外连接池始终可以手动配置。如果定义自己的 `DataSource` bean，则不会进行自动配置。

数据源的配置由 `spring.datasource.*` 中的外部配置属性控制。例如，您可以在 `application.properties` 中声明以下部分：

```properties
spring.datasource.url=jdbc:mysql://localhost/test
spring.datasource.username=dbuser
spring.datasource.password=dbpass
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

> 您至少应通过设置 `spring.datasource.url` 属性来指定 URL。否则，Spring Boot 会尝试自动配置内置数据库。

> 您通常不需要指定 `driver-class-name`，因为 Spring Boot 可以从 `url` 中为大多数数据库推断出它。

> 对于要创建的 `DataSource` 池，我们需要能够验证有效的 `Driver` 类是否可用，因此我们在进行任何操作之前都要进行检查。换句话说，如果设置 `spring.datasource.driver-class-name=com.mysql.jdbc.Driver`，则该类必须是可加载的。

参见 [`DataSourceProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jdbc/DataSourceProperties.java) 以获取更多受支持的选项。这些是不管实际实现如何都起作用的标准选项。也可以通过使用各自的前缀（`spring.datasource.hikari.*`，`spring.datasource.tomcat.*` 和 `spring.datasource.dbcp2.*`）微调实现特定的设置。有关更多详细信息，请参阅所用连接池实现的文档。

例如，如果你使用 [Tomcat connection pool](https://tomcat.apache.org/tomcat-8.0-doc/jdbc-pool.html#Common_Attributes)，你可以自定义很多额外的设定，如下面例子所示：

```properties
# Number of ms to wait before throwing an exception if no connection is available.
spring.datasource.tomcat.max-wait=10000

# Maximum number of active connections that can be allocated from this pool at the same time.
spring.datasource.tomcat.max-active=50

# Validate the connection before borrowing it from the pool.
spring.datasource.tomcat.test-on-borrow=true
```

##### 连接到 JNDI 数据库

如果您将 Spring Boot 应用程序部署到 Application Server，则可能需要使用 Application Server 的内置功能来配置和管理 DataSource，并使用 JNDI 对其进行访问。

`spring.datasource.jndi-name` 属性可以替代 `spring.datasource.url`，`spring.datasource.username` 和 `spring.datasource.password` 属性来从特定的 JNDI 位置访问 `DataSource`。例如，`application.properties` 中的以下部分显示了如何访问 JBoss 作为定义的 `DataSource`：

```properties
spring.datasource.jndi-name=java:jboss/datasources/customers
```

