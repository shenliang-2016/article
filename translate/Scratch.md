##### Artemis 支持

当 Spring Boot 检测到 [Artemis](https://activemq.apache.org/artemis/) 在类路径上可用时，它可以自动配置一个 `ConnectionFactory`。如果存在代理，则将自动启动和配置嵌入式代理（除非已明确设置 `mode` 属性）。支持的模式为 `embeded`（以明确要求使用嵌入式代理，并且如果代理在类路径上不可用，则会发生错误）和 `native`（使用 `netty` 传输协议连接到代理）。配置后者后，Spring Boot 会配置一个 `ConnectionFactory`，以默认设置连接到在本地计算机上运行的代理。

> 如果使用 `spring-boot-starter-artemis`，则将提供连接到现有 Artemis 实例所需的依赖项，以及与 JMS 集成的 Spring 基础结构。在您的应用程序中添加 `org.apache.activemq:artemis-jms-server` 可以使您使用嵌入式模式。

Artemis 配置由 `spring.artemis.*` 中的外部配置属性控制。例如，您可以在 `application.properties` 中声明以下部分：

```properties
spring.artemis.mode=native
spring.artemis.host=192.168.1.210
spring.artemis.port=9876
spring.artemis.user=admin
spring.artemis.password=secret
```

嵌入代理时，可以选择是否要启用持久性并列出应使其可用的目的地。可以将它们指定为以逗号分隔的列表，以使用默认选项创建它们，或者您可以定义类型为 `org.apache.activemq.artemis.jms.server.config.JMSQueueConfiguration` 或 `org.apache.activemq.artemis.jms.server.config.TopicConfiguration` 的 bean，分别用于高级队列和主题配置。

默认情况下，`CachingConnectionFactory` 将本机 `ConnectionFactory` 包装为明智的设置，您可以通过 `spring.jms.*` 中的外部配置属性来控制这些设置：

```properties
spring.jms.cache.session-cache-size=5
```

如果您想使用本机池，则可以通过向 `org.messaginghub:pooled-jms` 添加依赖项并相应地配置 `JmsPoolConnectionFactory` 来实现，如以下示例所示：

```properties
spring.artemis.pool.enabled=true
spring.artemis.pool.max-connections=50
```

参考 [`ArtemisProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jms/artemis/ArtemisProperties.java) 了解更多支持的选项。

不涉及 JNDI 查找，并且使用 Artemis 配置中的 `name` 属性或通过配置提供的名称来根据目的地名称解析目的地。

