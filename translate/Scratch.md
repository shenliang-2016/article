### 3.1 使用 Spring JMS

本章节描述如何使用 Spring 的 JMS 组件。

#### 3.1.1 使用 `JmsTemplate`

 `JmsTemplate` 类是 JMS 核心包的中央类。它简化了 JMS 的使用，由于当发送消息或者同步接收消息时它处理了资源的创建和释放。

使用 `JmsTemplate` 的代码只需要实现回调接口以给它们一个明确定义的高层的契约。当由 `JmsTemplate` 中的调用代码提供一个 `Session` 时，`MessageCreator` 回调接口创建一条消息。为了允许更加复杂的 JMS API 的使用，`SessionCallback` 提供 JMS 会话，同时 `ProducerCallback` 暴露一个 `Session` 和 `MessageProducer` 对。

JMS API 暴露了两种类型的发送方法，一种采用交付模式，优先级和生存时间作为服务质量（QOS）参数，另一种不采用 QOS 参数并使用默认值。由于 `JmsTemplate` 具有许多发送方法，因此设置已作为 bean 属性公开的 QOS 参数，以避免重复发送方法。类似地，通过使用 `setReceiveTimeout` 属性设置同步接收调用的超时值。

一些 JMS 提供程序允许通过 `ConnectionFactory` 的配置来管理默认的 QOS 值。这样做的结果是，调用 `MessageProducer` 实例的 `send` 方法（`send(Destination destination, Message message)`）使用的 QOS 缺省值与 JMS 规范中指定的缺省值不同。因此，为了提供对 QOS 值的一致管理，必须通过将布尔属性 `isExplicitQosEnabled` 设置为 `true`，专门启用 `JmsTemplate` 以使用其自己的 QOS 值。

为了方便，`JmsTemplate` 同时暴露了一种基本的请求－回应操作，允许发送消息并在作为操作一部分而创建的一个临时队列上等待回应。

> 一旦配置完成，`JmsTemplate` 类的实例就是线程安全的。这一点很重要，因为这意味着你可以配置 `JmsTemplate` 的单个实例然后将其共享引用安全地注入到多个协作者中。需要明确的是，`JmsTemplate` 是有状态的，因为它维护了 `ConnectionFactory` 的引用，不过这里的状态并不是会话状态。

Spring 框架 4.1中，`JmsMessagingTemplate` 建立在 `JmsTemplate` 之上，提供了一种与消息抽象的集成－也就是 `org.springframework.messaging.Message`。这就允许你可以以通用的方式创建将要发送的消息。

#### 3.1.2 连接

`JmsTemplate` 需要 `ConnectionFactory` 引用。`ConnectionFactory` 是 JMS 规范的一部分，作为使用 JMS 的入口点。它被客户端应用用来作为使用 JMS 提供者创建连接的工厂，同时包装各种配置参数，其中许多参数都是特定于提供者的，比如 SSL 配置选项。

在 EJB 中使用 JMS 时，提供者提供 JMS 接口的实现，因而它们可以参与声明式事务管理以及执行连接和会话的池化。为了使用这种实现，Java EE 容器通常需要你在 EJB 或者 servlet 部署描述符文件中声明一个 JMS 连接工厂作为 `resource-ref` 。为了确保将这些功能能够与 EJB 中的 `JmsTemplate` 一起使用，客户端应用程序应确保其引用 `ConnectionFactory` 的托管实现。

##### 缓存消息资源

标准 API 调用创建许多中间对象。为了发送一条消息，下面的 API 调用过程会执行：

```
ConnectionFactory->Connection->Session->MessageProducer->send
```

在 `ConnectionFactory` 和 `Send` 操作之间，三个中间对象被创建然后销毁。为了优化资源使用并提升性能，Spring 提供了 `ConnectionFactory` 的两种实现。

##### 使用 `SingleConnectionFactory`

Spring 提供了一个 `ConnectionFactory` 接口的实现， `SingleConnectionFactory` 。该接口在所有的  `createConnection()` 调用上返回相同的 `Connection`，而忽略对 `close()` 的调用。这对于测试环境和独立环境非常有用，因此同一连接可用于可能跨越任意数量事务的多个 `JmsTemplate` 调用。`SingleConnectionFactory` 引用了通常来自 JNDI 的标准 `ConnectionFactory`。

##### 使用 `CachingConnectionFactory`

`CachingConnectionFactory` 扩展了 `SingleConnectionFactory` 的功能，并添加了 `Session`，`MessageProducer` 和 `MessageConsumer` 实例的缓存。初始缓存大小设置为 `1`。您可以使用 `sessionCacheSize` 属性来增加缓存会话的数量。请注意，实际缓存的会话数大于该数量，因为会话是基于其确认（应答）模式缓存的，因此，当将 `sessionCacheSize` 设置为 `1` 时，最多可以有四个缓存的会话实例（每个确认模式一个）。`MessageProducer` 和 `MessageConsumer` 实例被缓存在它们自己的会话中，并且在缓存时还考虑了生产者和使用者的唯一属性。`MessageProducers` 根据其目的地进行缓存。基于由目标，选择器，noLocal 传递标志和持久订阅名称（如果创建持久使用者）组成的键来缓存 `MessageConsumers`。

