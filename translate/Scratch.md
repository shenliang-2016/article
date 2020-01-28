### 4.13. 消息

Spring 框架为与消息系统的集成提供了丰富的支持，从通过使用 `JmsTemplate` 来简化 JMS API 的使用，到异步接收消息的完整机车设施。Spring AMQP 提供了类似于高级消息队列协议的特性集合。Spring Boot 也提供了 `RabbitTemplate` 和 RabbitMQ 的自动配置选项。Spring WebSocket 本身包含 STOMP 消息支持，同时 Spring Boot 通过启动器和少量的自动配置支持该消息。Spring Boot 还支持 Apache Kafka。

#### 4.13.1. JMS

`javax.jms.ConnectionFactory` 接口提供了创建用于与 JMS 代理进行交互的 `javax.jms.Connection` 的标准方法。尽管 Spring 需要 `ConnectionFactory` 来与 JMS 一起使用，但是您通常不需要自己直接使用它，而可以依赖于更高级别的消息抽象。（有关详细信息，请参见 Spring Framework 参考文档的 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#jms)。）Spring Boot 还自动配置了必要的基础设施，以发送和接收消息。

##### ActiveMQ Support

当 [ActiveMQ](https://activemq.apache.org/) 在类路径上可用时，Spring Boot 也能够配置一个 `ConnectionFactory`。如果代理存在，则会自动配置（如果没有通过配置指定代理 URL）并启动一个内置代理。

> 如果你使用 `spring-boot-starter-activemq`，连接或者内置 ActiveMQ 实例所必需的依赖就都提供好了，它们作为 Spring 集成 JMS 的基础设施存在。

ActiveMQ 配置由 `spring.activemq.*` 中的外部配置属性控制。例如，您可以在 `application.properties` 中声明以下部分：

```properties
spring.activemq.broker-url=tcp://192.168.1.210:9876
spring.activemq.user=admin
spring.activemq.password=secret
```

默认情况下，`CachingConnectionFactory` 将本机 `ConnectionFactory` 包装为明智的设置，您可以通过 `spring.jms.*` 中的外部配置属性来控制这些设置：

```properties
spring.jms.cache.session-cache-size=5
```

如果您想使用本机池，则可以通过向 `org.messaginghub:pooled-jms` 添加依赖项并相应地配置 `JmsPoolConnectionFactory` 来实现，如以下示例所示：

```properties
spring.activemq.pool.enabled=true
spring.activemq.pool.max-connections=50
```

> 参考 [`ActiveMQProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jms/activemq/ActiveMQProperties.java) 了解更多支持的选项。你还可以注册任意数量实现了 `ActiveMQConnectionFactoryCustomizer` 的 beans 来实现更高级的定制化。

默认情况下，ActiveMQ 创建一个目的地（如果尚不存在），以便根据其提供的名称解析目的地。

