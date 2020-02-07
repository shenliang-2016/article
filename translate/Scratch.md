### 4.23. Spring Session

Spring Boot 提供了 [Spring Session](https://spring.io/projects/spring-session) 使用大部分种类的数据存储技术的自动配置。当构建 Servlet web 应用时，下面的数据存储会被自动配置：

- JDBC
- Redis
- Hazelcast
- MongoDB

当创建反应式 web 应用时，下面的数据存储能够被自动配置：

- Redis
- MongoDB

如果类路径上存在单个 Spring Session 模块，则 Spring Boot 会自动使用该存储实现。如果您有多个实现，则必须选择您希望用来存储会话的 [`StoreType`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/session/StoreType.java) 。例如，要将 JDBC 用作后端存储，可以按以下方式配置应用程序：

```properties
spring.session.store-type=jdbc
```

> 你可以通过将 `store-type` 设定为 `none` 来禁用 Spring Session。

每种存储都有特定的其他设置。例如，可以为 JDBC 存储定制表的名称，如以下示例所示：

```properties
spring.session.jdbc.table-name=SESSIONS
```

为了设置会话超时，您可以使用 `spring.session.timeout` 属性。如果未设置该属性，则自动配置将降级到使用 `server.servlet.session.timeout` 的值。