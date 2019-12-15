### 3.6 JMS 命名空间支持

Spring 提供了 XML 命名空间支持以简化 JMS 配置。为了使用 JMS 命名空间元素，你v 要引用 JMS 规范文件。如下面例子所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:jms="http://www.springframework.org/schema/jms" 
        xsi:schemaLocation="
            http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/jms https://www.springframework.org/schema/jms/spring-jms.xsd">

    <!-- bean definitions here -->

</beans>
```

该命名空间由 3 中顶级元素组成：`<annotation-driven/>`, `<listener-container/>` 和 `<jca－listener-container/>`。`<annotation-driven/>` 启用注解驱动的监听器端点。`<listener-container/>` 和 `<jca-listener-container/>` 定义共享的监听器容器配置，同时可以包含 `<listener/>` 子元素。下面的例子展示了两个监听器的基本配置：

```xml
<jms:listener-container>

    <jms:listener destination="queue.orders" ref="orderService" method="placeOrder"/>

    <jms:listener destination="queue.confirmations" ref="confirmationLogger" method="log"/>

</jms:listener-container>
```

上面的例子等价于创建两个不同的监听器容器 bean 定义以及两个不同的 `MessageListenerAdapter` bean 定义，如  [Using `MessageListenerAdapter`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async-message-listener-adapter) 中所述。除了上面例子中展示的属性，`listener` 元素还可以包含若干可选属性。下表描述了所有可用属性：

| 属性                     | 描述                                                         |
| :----------------------- | :----------------------------------------------------------- |
| `id`                     | 托管监听器容器的 bean 名称。如果未指定，则自动生成 bean 名称。 |
| `destination` (required) | 监听器的目标名称，通过 `DestinationResolver` 策略进行解析。  |
| `ref` (required)         | 处理器对象 bean 名称。                                       |
| `method`                 | 将要调用的处理器方法名称。如果 `ref` 属性指向 `MessageListener` 或者 Spring `SessionAwareMessageListener` ，你可以忽略此属性。 |
| `response-destination`   | 向其发送响应消息的默认响应目标的名称。在请求消息中不包含 `JMSReplyTo` 字段的情况下适用。此目的地的类型由监听容器的 `response-destination-type` 属性确定。请注意，这仅适用于具有返回值的侦听器方法，为此，每个结果对象都将转换为响应消息。 |
| `subscription`           | 持久订阅的名称（如果有）。                                   |
| `selector`               | 此侦听器的可选消息选择器。                                   |
| `concurrency`            | 要启动此侦听器的并发会话或使用者的数量。该值可以是表示最大数的简单数字（例如，`5`），也可以是表示下限和上限的范围（例如，`3-5`）。请注意，指定的最小值仅是一个提示，在运行时可能会被忽略。默认值为容器提供的值。 |

`<listener-container/>` 元素也接受若干可选属性。这就允许自定义各种策略（比如，`taskExecutor` 和 `destinationResolver`）以及基本的 JMS 设定和资源引用。通过使用这些属性，你可以定义高度定制化的监听器容器，同时还能够从命名空间受益。

您可以通过指定要通过 `factory-id` 属性公开的 bean 的 `id` 来自动将此类设置公开为 `JmsListenerContainerFactory`，如以下示例所示：

```xml
<jms:listener-container connection-factory="myConnectionFactory"
        task-executor="myTaskExecutor"
        destination-resolver="myDestinationResolver"
        transaction-manager="myTransactionManager"
        concurrency="10">

    <jms:listener destination="queue.orders" ref="orderService" method="placeOrder"/>

    <jms:listener destination="queue.confirmations" ref="confirmationLogger" method="log"/>

</jms:listener-container>
```

下表描述了所有可用的属性。参考 [`AbstractMessageListenerContainer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/AbstractMessageListenerContainer.html) 类以及它的子类的文档，获取更多有关属性的细节。文档中还提供了有关事务选择以及消息重发场景的讨论。

| 属性                        | 描述                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| `container-type`            | 监听器容器的类型。可用的选择有 `default`, `simple`, `default102`, 或者 `simple102` (默认值是 `default`)。 |
| `container-class`           | 由全限定类名指定的自定义监听器容器实现类。默认是 Spring 的标准 `DefaultMessageListenerContainer` 或者 `SimpleMessageListenerContainer`， 根据 `container-type` 属性确定。 |
| `factory-id`                | 指定 `id` 暴露由作为 `JmsListenerContainerFactory` 的元素定义的设定以便它们可以被其它端点复用。 |
| `connection-factory`        | 指向 JMS `ConnectionFactory` bean 的引用（默认 bean 名称是 `connectionFactory`）。 |
| `task-executor`             | 对 JMS 侦听器调用程序的 Spring `TaskExecutor` 的引用。       |
| `destination-resolver`      | 对用于解析 JMS `Destination` 实例的 `DestinationResolver` 策略的引用。 |
| `message-converter`         | 对将 JMS 消息转换为侦听器方法参数的 `MessageConverter` 策略的引用。默认值为 `SimpleMessageConverter` 。 |
| `error-handler`             | 对用于处理在 `MessageListener` 执行期间可能发生的任何未捕获异常的 `ErrorHandler` 策略的引用。 |
| `destination-type`          | 此侦听器的 JMS 目标类型：`queue`， `topic`， `durableTopic`， `sharedTopic`，或者 `sharedDurableTopic`。这可能会启用容器的 `pubSubDomain`，`subscriptionDurable` 和 `subsubscribeShared` 属性。默认值为 `queue`（禁用这三个属性）。 |
| `response-destination-type` | 响应的 JMS 目标类型： `queue` 或者 `topic`。默认是 `destination-type` 属性的值。 |
| `client-id`                 | 此监听器容器的 JMS 客户端 ID。使用持久化订阅时你必须指定它。 |
| `cache`                     | JMS 资源的缓存级别：`none`， `connection`， `session`， `consumer`， 或者 `auto`。默认情况下（`auto`），缓存级别实际上是 `consumer`，除非已指定外部事务管理器。在这种情况下，有效的默认值为 `none`（假设 Java EE 风格的事务管理，`ConnectionFactory` 是一个 XA-感知池）。 |
| `acknowledge`               | 本地 JMS 确认模式：`auto`， `client`， `dups-ok`， 或者 `transacted`。值 `transacted` 激活了本地交易的 `Session` 。或者，您可以指定 `transaction-manager` 属性，稍后在表中进行描述。默认为 `auto`。 |
| `transaction-manager`       | 对外部 `PlatformTransactionManager`（通常是基于 XA 的事务协调器，例如 Spring 的 `JtaTransactionManager`）的引用。如果未指定，则使用本机确认（请参阅 `acknowledge` 属性）。 |
| `concurrency`               | 每个侦听器启动的并发会话或使用者的数量。它可以是表示最大值的简单数字（例如，`5`），也可以是表示上下限的范围（例如，`3-5`）。请注意，指定的最小值只是一个提示，在运行时可能会被忽略。 默认值为 `1`。如果是主题侦听器或队列顺序很重要，则应将并发限制为 `1`。考虑将其提升为一般队列。 |
| `prefetch`                  | 加载到单个会话中的最大消息数。请注意，增加此数字可能会导致并发消费者饥饿。 |
| `receive-timeout`           | 用于接受调用的超时时间（以毫秒为单位）。默认值为 `1000`（一秒）。`-1` 表示没有超时。 |
| `back-off`                  | 指定 `BackOff` 实例，用于计算两次恢复尝试之间的间隔。如果 `BackOffExecution` 实现返回 `BackOffExecution#STOP`，则侦听器容器不会进一步尝试恢复。设置此属性后，将忽略 `recovery-interval` 值。默认值为 `FixedBackOff`，间隔为 `5000` 毫秒（即 5秒）。 |
| `recovery-interval`         | 指定两次恢复尝试之间的时间间隔（以毫秒为单位）。它提供了一种方便的方法来创建具有指定间隔的 `FixedBackOff`。对于更多恢复选项，请考虑指定一个 `BackOff` 实例。缺省值为 5000 毫秒（即 5 秒）。 |
| `phase`                     | 此容器应在其中启动和停止的生命周期阶段。值越低，此容器启动越早，而其停止越晚。默认值为 `Integer.MAX_VALUE`，这意味着容器将尽可能晚地启动，并尽快停止。 |

使用 `jms` 模式支持配置基于 JCA 的侦听器容器非常相似，如以下示例所示：

```xml
<jms:jca-listener-container resource-adapter="myResourceAdapter"
        destination-resolver="myDestinationResolver"
        transaction-manager="myTransactionManager"
        concurrency="10">

    <jms:listener destination="queue.orders" ref="myMessageListener"/>

</jms:jca-listener-container>
```

下表描述了 JCA 变体的可用配置选项：

| 属性                        | 描述                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| `factory-id`                | 将此元素定义的设置公开为具有指定 ID 的 `JmsListenerContainerFactory`，以便其他端点重复使用。 |
| `resource-adapter`          | 对 JCA `ResourceAdapter` bean的引用（默认 bean 名称为 `resourceAdapter`）。 |
| `activation-spec-factory`   | `JmsActivationSpecFactory` 的引用。默认设置是自动检测 JMS 提供程序及其 `ActivationSpec` 类（参考 [`DefaultJmsActivationSpecFactory`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/endpoint/DefaultJmsActivationSpecFactory.html)）。 |
| `destination-resolver`      | 对用于解析 JMS 目标的 `DestinationResolver` 策略的引用。     |
| `message-converter`         | 对将 JMS 消息转换为侦听器方法参数的 `MessageConverter` 策略的引用。默认值为 `SimpleMessageConverter`。 |
| `destination-type`          | 此侦听器的 JMS 目标类型：`queue`， `topic`， `durableTopic`， `sharedTopic`，或者 `sharedDurableTopic`。这可能会启用容器的 `pubSubDomain`，`subscriptionDurable` 和 `subsubscribeShared` 属性。默认值为 `queue`（禁用这三个属性）。 |
| `response-destination-type` | 响应的 JMS 目标类型：`queue` 或 `topic`。默认值为 `destination-type` 属性的值。 |
| `client-id`                 | 此侦听器容器的JMS客户端ID。使用持久订阅时需要指定它。        |
| `acknowledge`               | 本地 JMS 确认模式：`auto`， `client`， `dups-ok`， 或者 `transacted`。值 `transacted` 激活了本地交易的 `Session` 。或者，您可以指定稍后描述的 `transaction-manager` 属性。默认为 `auto`。 |
| `transaction-manager`       | 对 Spring  `JtaTransactionManager` 或 `javax.transaction.TransactionManager` 的引用，用于为每个传入消息启动 XA 事务。如果未指定，则使用本机确认（请参阅 `acknowledge` 属性）。 |
| `concurrency`               | 每个侦听器启动的并发会话或使用者的数量。它可以是表示最大数的简单数字（例如， `5`），也可以是表示上下限的范围（例如，`3-5`）。请注意，指定的最小值只是一个提示，通常在运行时使用 JCA 侦听器容器时将被忽略。 预设值为 `1`。 |
| `prefetch`                  | 加载到单个会话中的最大消息数。请注意，增加此数字可能会导致并发消费者饥饿。 |

