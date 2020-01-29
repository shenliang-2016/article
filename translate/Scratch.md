#### 4.13.2. AMQP

高级消息队列协议（AMQP）是面向消息中间件的与平台无关的有线级别协议。Spring AMQP 项目将 Spring 的核心概念应用于基于 AMQP 的消息传递解决方案的开发。Spring Boot 为通过 RabbitMQ 使用 AMQP 提供了许多便利，包括 `spring-boot-starter-amqp` “Starter”。

##### RabbitMQ 支持

[RabbitMQ](https://www.rabbitmq.com/) 时一个轻量级的，可靠的，可扩展的，可移植的消息代理，基于 AMQP 协议。Spring 使用 `RabbitMQ` 来通过 AMQP 协议进行通信。

RabbitMQ 配置由 `spring.rabbitmq.*` 中的外部配置属性控制。例如，您可以在 `application.properties` 中声明以下部分：

```properties
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=admin
spring.rabbitmq.password=secret
```

另外，你可以使用 `addresses` 属性来配置相同的连接：

```properties
spring.rabbitmq.addresses=amqp://admin:secret@localhost
```

如果上下文中存在一个 `ConnectionNameStrategy` bean，它将被自动用来命名由自动配置的 `ConnectionFactory` 创建的连接。参见 [`RabbitProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/amqp/RabbitProperties.java) 以获取更多受支持的选项。

> 参考 [Understanding AMQP, the protocol used by RabbitMQ](https://spring.io/blog/2010/06/14/understanding-amqp-the-protocol-used-by-rabbitmq/) 获取更多细节。

##### 发送消息

Spring 的 `AmqpTemplate` 和 `AmqpAdmin` 都是自动配置的，你可以直接将其注入自己的 beans，如下面例子所示：

```java
import org.springframework.amqp.core.AmqpAdmin;
import org.springframework.amqp.core.AmqpTemplate;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    private final AmqpAdmin amqpAdmin;
    private final AmqpTemplate amqpTemplate;

    @Autowired
    public MyBean(AmqpAdmin amqpAdmin, AmqpTemplate amqpTemplate) {
        this.amqpAdmin = amqpAdmin;
        this.amqpTemplate = amqpTemplate;
    }

    // ...

}
```

> [`RabbitMessagingTemplate`](https://docs.spring.io/spring-amqp/docs/2.2.2.RELEASE/api/org/springframework/amqp/rabbit/core/RabbitMessagingTemplate.html) 可以通过类似方式注入。如果定义了 `MessageConverter` bean，它就会自动联系到自动配置的 `AmqpTemplate`。

如有必要，任何定义为 bean 的 `org.springframework.amqp.core.Queue` 都会自动用于在 RabbitMQ 实例上声明相应的队列。

要重试操作，可以在 `AmqpTemplate` 上启用重试（例如，在代理连接丢失的情况下）：

```properties
spring.rabbitmq.template.retry.enabled=true
spring.rabbitmq.template.retry.initial-interval=2s
```

默认是禁用重试的。你也可以通过声明 `RabbitRetryTemplateCustomizer` bean 来以编程方式自定义 `RetryTemplate` 。

