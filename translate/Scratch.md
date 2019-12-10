#### 3.1.3 目的地管理

作为 `ConnectionFactory` 实例的目的地，是可以在 JNDI 中存储和检索的 JMS 管理的对象。在配置 Spring 应用程序上下文时，可以使用 JNDI `JndiObjectFactoryBean` 工厂类或 `<jee:jndi-lookup>` 对对象对 JMS 目的地的引用执行依赖项注入。但是，如果应用程序中有大量目的地，或者 JMS 提供程序具有独特的高级目的地管理功能，则此策略通常很麻烦。这种高级目的地管理的示例包括动态目的地的创建或对目的地的分层名称空间的支持。 `JmsTemplate` 将目的地名称的解析委托给实现 `DestinationResolver` 接口的 JMS 目的地对象。 `DynamicDestinationResolver` 是 `JmsTemplate` 所使用的默认实现，并且可以解析动态目的地。还提供了 `JndiDestinationResolver` 以充当 JNDI 中包含的目的地的服务定位器，并且可以选择降级到 `DynamicDestinationResolver` 中包含的行为。

通常，仅在运行时才知道 JMS 应用程序中使用的目的地，因此，在部署应用程序时无法通过管理方式创建。这通常是因为在交互的系统组件之间存在共享的应用程序逻辑，这些组件根据已知的命名约定在运行时创建目的地。即使创建动态目的地不属于 JMS 规范的一部分，但大多数供应商都提供了此功能。动态目的地是使用用户定义的名称创建的，该名称将它们与临时目的地区分开来，并且通常未在 JNDI 中注册。各个提供者之间用于创建动态目的地的 API 有所不同，因为与目的地关联的属性是特定于供应商的。但是，供应商有时会做出一个简单的实现选择，就是忽略 JMS 规范中的警告，并使用方法 `TopicSession` `createTopic(String topicName)` 或 `QueueSession` `createQueue(String queueName)` 方法来实现。使用默认目的地属性创建一个新目的地。然后，取决于供应商的实现，`DynamicDestinationResolver `也可以创建一个物理目的地，而不仅仅是解析一个目的地。

布尔属性 `pubSubDomain` 用于在知道正在使用哪个 `JMS` 域的情况下配置 `JmsTemplate`。默认情况下，此属性的值为 `false`，表示将使用点对点域，`Queues`。这个属性（由 `JmsTemplate` 使用）通过 `DestinationResolver` 接口的实现确定动态目的地解析的行为。

您还可以通过属性 `defaultDestination` 将 `JmsTemplate` 配置为默认目的地。默认目的地是带有不引用特定目的地的发送和接收操作。

