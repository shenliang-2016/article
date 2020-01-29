##### 接收消息

存在 JMS 基础设施时，可以使用 `@JmsListener` 注解任何 bean 以创建侦听器端点。如果未定义 `JmsListenerContainerFactory`，则会自动配置一个默认值。如果定义了 `DestinationResolver` 或 `MessageConverter` bean，则它们将自动关联到默认工厂。

默认情况下，默认工厂是事务性的。如果您在存在 `JtaTransactionManager` 的基础架构中运行，则默认情况下将其关联到侦听器容器。如果不是，则启用 `sessionTransacted` 标志。在后一种情况下，可以通过在侦听器方法（或其委托）上添加 `@Transactional` 来将本地数据存储事务与传入消息的处理相关联。这样可以确保本地事务完成后，传入消息得到确认。这还包括发送已在同一 JMS 会话上执行的响应消息。

以下组件在 `someQueue` 目标上创建侦听器端点：

```java
@Component
public class MyBean {

    @JmsListener(destination = "someQueue")
    public void processMessage(String content) {
        // ...
    }

}
```

> 参考 [the Javadoc of `@EnableJms`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/jms/annotation/EnableJms.html) 获取更多细节。

如果您需要创建更多的 `JmsListenerContainerFactory` 实例，或者想要覆盖默认实例，Spring Boot 提供了 `DefaultJmsListenerContainerFactoryConfigurer` ，您可以使用与自动配置相同的设置来初始化 `DefaultJmsListenerContainerFactory`。

例如，以下示例公开了另一个工厂，该工厂使用特定的 `MessageConverter`：

```java
@Configuration(proxyBeanMethods = false)
static class JmsConfiguration {

    @Bean
    public DefaultJmsListenerContainerFactory myFactory(
            DefaultJmsListenerContainerFactoryConfigurer configurer) {
        DefaultJmsListenerContainerFactory factory =
                new DefaultJmsListenerContainerFactory();
        configurer.configure(factory, connectionFactory());
        factory.setMessageConverter(myMessageConverter());
        return factory;
    }

}
```

然后，您可以在任何带有 `@JmsListener` 注解的方法中使用该工厂，如下所示：

```java
@Component
public class MyBean {

    @JmsListener(destination = "someQueue", containerFactory="myFactory")
    public void processMessage(String content) {
        // ...
    }

}
```