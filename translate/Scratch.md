### 3.5 注解驱动的监听器端点

同步接收消息的最简单方法就是使用注解修饰的监听器端点基础设施。简而言之，它允许你暴露容器托管的 bean 的方法作为 JMS 监听器端点。下面的例子展示了如何使用：

```java
@Component
public class MyService {

    @JmsListener(destination = "myDestination")
    public void processOrder(String data) { ... }
}
```

上面例子的想法是，无论何时，只要 `javax.jms.Destinations.myDestination` 上有一条可用消息，则对应的 `processOrder` 方法就会被调用（这种情况下，使用 JMS 消息的内容，类似于 [`MessageListenerAdapter`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async-message-listener-adapter) 所提供的）。

通过使用 `JmsListenerContainerFactory` ，注解修饰的端点基础设施在幕后为每个注解修饰的方法创建一个消息监听器容器。这样的容器并不注册在应用上下文中，但是可以通过使用 `JmsListenerEndpointRegistry` bean 出于管理目的很容易地定位。

> `@JmsListener` 在 Java 8 中是一个可重复注解，因此你可以通过将额外的`@JmsListener` 注解添加到同一个方法上来声明该方法关联到多个 JMS 目的地。

#### 3.5.1 启用监听器端点注解

为了启用 `@JmsListener` 注解支持，你可以将 `@EnableJms` 添加到你的其中一个 `@Configuration` 类中，如下面例子所示：

```java
@Configuration
@EnableJms
public class AppConfig {

    @Bean
    public DefaultJmsListenerContainerFactory jmsListenerContainerFactory() {
        DefaultJmsListenerContainerFactory factory = new DefaultJmsListenerContainerFactory();
        factory.setConnectionFactory(connectionFactory());
        factory.setDestinationResolver(destinationResolver());
        factory.setSessionTransacted(true);
        factory.setConcurrency("3-10");
        return factory;
    }
}
```

默认情况下，基础设施会寻找名为 `jmsListenerContainerFactory` 的 bean 作为用来创建消息监听器容器的工厂的源。这种情况下（同时忽略了 JMS 基础设施配置），你可以使用 3 个核心线程、最多 10 个线程的线程池调用 `processOrder` 方法。

您可以自定义用于每个注解的监听器容器工厂，也可以通过实现 `JmsListenerConfigurer` 接口来显式配置默认值。仅当至少一个端点在没有特定容器工厂的情况下注册时，才需要使用默认值。请参阅实现 [`JmsListenerConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/annotation/JmsListenerConfigurer.html ) 的类的 Javadoc 以获取详细信息和示例。

如果你更喜欢 [XML configuration](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-namespace)，你可以使用 `<jms:annotation-driven>` 元素，如下面例子所示：

```xml
<jms:annotation-driven/>

<bean id="jmsListenerContainerFactory"
        class="org.springframework.jms.config.DefaultJmsListenerContainerFactory">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destinationResolver" ref="destinationResolver"/>
    <property name="sessionTransacted" value="true"/>
    <property name="concurrency" value="3-10"/>
</bean>
```

#### 3.5.2 编程式端点注册

`JmsListenerEndpoint` 提供了 JMS 端点的模型，并负责配置该模型的容器。基础设施除了通过 `JmsListener`  注解探测端点，还允许你编程式配置端点。下面的例子展示了如何做：

```java
@Configuration
@EnableJms
public class AppConfig implements JmsListenerConfigurer {

    @Override
    public void configureJmsListeners(JmsListenerEndpointRegistrar registrar) {
        SimpleJmsListenerEndpoint endpoint = new SimpleJmsListenerEndpoint();
        endpoint.setId("myJmsEndpoint");
        endpoint.setDestination("anotherQueue");
        endpoint.setMessageListener(message -> {
            // processing
        });
        registrar.registerEndpoint(endpoint);
    }
}
```

上面的例子中，我们使用 `SimpleJmsListenerEndpoint` ，它提供实际的 `MessageListener` 用于调用。不过，你也可以创建你自己的端点变体来描述自定义的调用机制。

注意，您可以完全不使用 `@JmsListener` ，而可以仅通过 `JmsListenerConfigurer` 以编程方式注册端点。

#### 3.5.3 注解的端点方法签名

目前为止，我们已经将简单的 `String` 注入你的端点，不过实际上它也可以是非常复杂的方法签名。下面的例子中，我们注入携带自定义首部字段的 `Order` ：

```java
@Component
public class MyService {

    @JmsListener(destination = "myDestination")
    public void processOrder(Order order, @Header("order_type") String orderType) {
        ...
    }
}
```

可以注入 JMS 监听器端点的主要元素如下：

- 原始的 `javax.jms.Message` 或者任何它的子类（前提是它与进入的消息类型匹配）。
- `javax.jms.Session` 用于对本地 JMS API 的可选访问（比如，为了发送自定义响应）。
- `org.springframework.messaging.Message` 表达进入的 JMS 消息。注意该消息同时包含自定义和标准首部字段（如由 `JmsHeaders` 定义的）。
- `@Header`-注解的方法参数以提取特定首部字段值，包括标准 JMS 首部字段。
- `@Headers`-注解的参数，必须还可以被分配给 `java.util.Map` 以访问所有首部字段。
- 不是支持的类型之一（`Message` 或 `Session`）的非注解元素被视为有效负载。您可以通过在 `@Payload` 中注解参数来使其明确。您还可以通过添加额外的 `@Valid` 来启用验证。

注入 Spring 的 `Message` 抽象的能力特别有用，它可以受益于存储在特定于传输的消息中的所有信息，而无需依赖于特定于传输的 API。以下示例显示了如何执行此操作：

```java
@JmsListener(destination = "myDestination")
public void processOrder(Message<Order> order) { ... }
```

方法参数的处理由 `DefaultMessageHandlerMethodFactory` 提供，您可以进一步对其进行自定义以支持其他方法参数。您也可以自定义转换和验证支持。

例如，如果我们想在处理 `Order` 之前确保其有效，则可以使用 `@Valid` 注解有效负载并配置必要的验证器，如以下示例所示：

```java
@Configuration
@EnableJms
public class AppConfig implements JmsListenerConfigurer {

    @Override
    public void configureJmsListeners(JmsListenerEndpointRegistrar registrar) {
        registrar.setMessageHandlerMethodFactory(myJmsHandlerMethodFactory());
    }

    @Bean
    public DefaultMessageHandlerMethodFactory myHandlerMethodFactory() {
        DefaultMessageHandlerMethodFactory factory = new DefaultMessageHandlerMethodFactory();
        factory.setValidator(myValidator());
        return factory;
    }
}
```

#### 3.5.4. Response Management

The existing support in [`MessageListenerAdapter`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async-message-listener-adapter) already lets your method have a non-`void` return type. When that is the case, the result of the invocation is encapsulated in a `javax.jms.Message`, sent either in the destination specified in the `JMSReplyTo` header of the original message or in the default destination configured on the listener. You can now set that default destination by using the `@SendTo` annotation of the messaging abstraction.

Assuming that our `processOrder` method should now return an `OrderStatus`, we can write it to automatically send a response, as the following example shows:

```
@JmsListener(destination = "myDestination")
@SendTo("status")
public OrderStatus processOrder(Order order) {
    // order processing
    return status;
}
```

> If you have several `@JmsListener`-annotated methods, you can also place the `@SendTo` annotation at the class level to share a default reply destination.

If you need to set additional headers in a transport-independent manner, you can return a `Message` instead, with a method similar to the following:

```
@JmsListener(destination = "myDestination")
@SendTo("status")
public Message<OrderStatus> processOrder(Order order) {
    // order processing
    return MessageBuilder
            .withPayload(status)
            .setHeader("code", 1234)
            .build();
}
```

If you need to compute the response destination at runtime, you can encapsulate your response in a `JmsResponse` instance that also provides the destination to use at runtime. We can rewrite the previous example as follows:

```
@JmsListener(destination = "myDestination")
public JmsResponse<Message<OrderStatus>> processOrder(Order order) {
    // order processing
    Message<OrderStatus> response = MessageBuilder
            .withPayload(status)
            .setHeader("code", 1234)
            .build();
    return JmsResponse.forQueue(response, "status");
}
```

Finally, if you need to specify some QoS values for the response such as the priority or the time to live, you can configure the `JmsListenerContainerFactory` accordingly, as the following example shows:

```
@Configuration
@EnableJms
public class AppConfig {

    @Bean
    public DefaultJmsListenerContainerFactory jmsListenerContainerFactory() {
        DefaultJmsListenerContainerFactory factory = new DefaultJmsListenerContainerFactory();
        factory.setConnectionFactory(connectionFactory());
        QosSettings replyQosSettings = new QosSettings();
        replyQosSettings.setPriority(2);
        replyQosSettings.setTimeToLive(10000);
        factory.setReplyQosSettings(replyQosSettings);
        return factory;
    }
}
```