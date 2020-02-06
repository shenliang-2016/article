### 4.22. Spring 集成

Spring Boot 为使用 [Spring Integration](https://spring.io/projects/spring-integration) 提供了许多便利，其中包括 `spring-boot-starter-integration` “Starter”。Spring Integration 在消息传递以及其他传输（例如 HTTP，TCP 等）上提供了抽象。如果 Spring Integration 在您的类路径中可用，则通过 `@EnableIntegration` 注解对其进行初始化。

Spring Boot 还配置了一些功能，这些功能由其他 Spring Integration 模块的存在触发。如果 `spring-integration-jmx` 也位于类路径中，则消息处理统计信息将通过 JMX 发布。如果 `spring-integration-jdbc` 可用，则可以在启动时创建默认的数据库模式，如以下行所示：

```properties
spring.integration.jdbc.initialize-schema=always
```

参考 [`IntegrationAutoConfiguration`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/integration/IntegrationAutoConfiguration.java) 和 [`IntegrationProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/integration/IntegrationProperties.java) 类获取更多细节。

默认情况下，如果存在 Micrometer `meterRegistry` bean，那么 Spring Integration 指标将由 Micrometer 管理。如果您希望使用传统的 Spring Integration 指标，请向应用程序上下文中添加一个 `DefaultMetricsFactory` bean。

