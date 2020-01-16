### 4.10. 使用 SQL 数据库

 [Spring Framework](https://spring.io/projects/spring-framework) 提供了使用 SQL 数据库的丰富支持，从使用 `JdbcTemplate` 的直接 JDBC 访问到诸如 Hibernate 的完善的 "对象关系映射" 技术。 [Spring Data](https://spring.io/projects/spring-data) 提供了另一个级别的功能：直接从接口创建 `Repository` 实现，并使用约定从你的方法名称生成查询。

#### 4.10.1. 配置数据库

Java 的 `javax.sql.DataSource` 接口提供使用数据库连接的标准方法。传统上，`DataSource` 使用一个 `URL` 和一些凭证来建立数据库连接。

> 参考 [the “How-to” section](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-configure-a-datasource) 了解更多高级示例，其中一些是关于如何完全控制数据库配置。

##### 内置数据库支持

使用内存内置数据库来开发应用程序通常很方便。显然，内存数据库不提供持久存储。您需要在应用程序启动时填充数据库，并准备在应用程序结束时丢弃数据。

> “How-to” 章节包含 [section on how to initialize a database](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-database-initialization) 。

Spring Boot 可以自动配置内置 [H2](https://www.h2database.com/)，[HSQL](http://hsqldb.org/) 和 [Derby](https://db.apache.org/derby/) 数据库。您无需提供任何连接 URL。您只需要包含要使用的内置数据库的构建依赖项即可。

> 如果您在测试中使用此功能，则可能会注意到，整个测试套件将重复使用同一数据库，而不管您使用的应用程序上下文有多少。如果要确保每个上下文都有一个单独的内置数据库，则应将 `spring.datasource.generate-unique-name` 设置为 `true`。

比如，典型的 POM 依赖应该是：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.hsqldb</groupId>
    <artifactId>hsqldb</artifactId>
    <scope>runtime</scope>
</dependency>
```

> 您需要依赖于 `spring-jdbc` 才能自动配置内置数据库。在这个例子中，它是通过 `spring-boot-starter-data-jpa` 传递的。

> 如果出于某种原因确实为内置数据库配置了连接 URL，请务必确保禁用了数据库的自动关闭功能。如果您使用的是 H2，则应使用 `DB_CLOSE_ON_EXIT=FALSE`。如果使用 HSQLDB，则应确保不使用 `shutdown=true`。通过禁用数据库的自动关闭功能，Spring Boot 可以控制何时关闭数据库，从而确保一旦不再需要访问数据库时就可以进行自动关闭。

