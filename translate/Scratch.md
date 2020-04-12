### 5.4. 通过 JMX 监控和管理

Java 管理扩展（JMX）提供了监视和管理应用程序的标准机制。默认情况下，此功能未启用，可以通过将配置属性 `spring.jmx.enabled` 设置为 `true` 来启用。默认情况下，Spring Boot 将管理端点作为 `org.springframework.boot` 域下的 JMX MBean 公开。

#### 5.4.1. 自定义 MBean 名称

MBean 的名称通常由端点的 `id` 生成。例如， `health` 端点公开为 `org.springframework.boot:type=Endpoint,name=Health`。

如果您的应用程序包含多个 Spring `ApplicationContext`，您可能会发现名称冲突。为了解决这个问题，可以将 `spring.jmx.unique-names` 属性设置为 `true`，以便 MBean 名称始终是唯一的。

您还可以自定义暴露端点的 JMX 域。以下设置显示了在 `application.properties` 中执行此操作的示例：

```properties
spring.jmx.unique-names=true
management.endpoints.jmx.domain=com.example.myapp
```

