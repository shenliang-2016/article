##### 接收消息

当存在 Rabbit 基础设施时，可以使用 `@RabbitListener` 注解任何 bean 以创建侦听器端点。如果未定义 `RabbitListenerContainerFactory`，则会自动配置默认的 `SimpleRabbitListenerContainerFactory`，您可以使用 `spring.rabbitmq.listener.type` 属性切换到直接容器。如果定义了一个 `MessageConverter` 或 `MessageRecoverer` bean，它将自动与默认工厂关联。

以下示例组件在 `someQueue` 队列上创建一个侦听器端点：

```java
@Component
public class MyBean {

    @RabbitListener(queues = "someQueue")
    public void processMessage(String content) {
        // ...
    }

}
```

> 参考 [the Javadoc of `@EnableRabbit`](https://docs.spring.io/spring-amqp/docs/2.2.2.RELEASE/api/org/springframework/amqp/rabbit/annotation/EnableRabbit.html) 获取更多细节。

如果您需要创建更多的 `RabbitListenerContainerFactory` 实例，或者想要覆盖默认实例，Spring Boot 提供了 `SimpleRabbitListenerContainerFactoryConfigurer` 和 `DirectRabbitListenerContainerFactoryConfigurer`，您可以使用它们初始化具有相同设置的 `SimpleRabbitListenerContainerFactory` 和 `DirectRabbitListenerContainerFactory`  作为自动配置使用的工厂。

> 选择哪种容器都没有关系。 这两个 bean 通过自动配置公开。

例如，以下配置类公开了另一个使用特定 `MessageConverter` 的工厂：

```java
@Configuration(proxyBeanMethods = false)
static class RabbitConfiguration {

    @Bean
    public SimpleRabbitListenerContainerFactory myFactory(
            SimpleRabbitListenerContainerFactoryConfigurer configurer) {
        SimpleRabbitListenerContainerFactory factory =
                new SimpleRabbitListenerContainerFactory();
        configurer.configure(factory, connectionFactory);
        factory.setMessageConverter(myMessageConverter());
        return factory;
    }

}
```

然后，您可以在任何带有 `@RabbitListener` 注解的方法中使用工厂，如下所示：

```java
@Component
public class MyBean {

    @RabbitListener(queues = "someQueue", containerFactory="myFactory")
    public void processMessage(String content) {
        // ...
    }

}
```

您可以启用重试以处理侦听器引发异常的情况。默认情况下，使用 `RejectAndDontRequeueRecoverer`，但是您可以定义自己的 `MessageRecoverer`。重试用尽后，如果将代理配置为这样做，则消息将被拒绝并被丢弃或路由到死信队列。默认情况下，重试是禁用的。您还可以通过声明 `RabbitRetryTemplateCustomizer` bean 来以编程方式自定义 `RetryTemplate`。

> 默认情况下，如果禁用了重试，并且侦听器引发了异常，则会无限期地重试传递。您可以通过两种方式修改此行为：将 `defaultRequeueRejected` 属性设置为 `false`，以便尝试进行零次重新传递，或者抛出 `AmqpRejectAndDontRequeueException` 来指示应拒绝该消息。后者是启用重试并达到最大传递尝试次数时使用的机制。

