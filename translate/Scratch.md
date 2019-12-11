#### 3.1.4. Message Listener Containers

在 EJB 世界中，JMS 消息最常见的用途之一就是驱动消息驱动的 bean（MDB）。Spring 提供了一种解决方案，以不将用户绑定到 EJB 容器的方式创建消息驱动的 POJO（MDP）。（有关详细信息，请参见 [异步接收：消息驱动的POJO](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async)）自 Spring Framework 4.1 以来，可以使用 `@JmsListener` 注解修释端点方法。请参阅 [注解驱动的侦听器端点](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-annotated) 以了解更多详细信息。

消息侦听器容器用于从 JMS 消息队列接收消息，并驱动注入到其中的 `MessageListener`。侦听器容器负责消息接收的所有线程，并分派到侦听器中进行处理。消息侦听器容器是 MDP 与消息传递提供程序之间的中介，并负责注册接收消息，参与事务，资源获取和释放，异常转换等。这使您可以编写与接收消息（并可能响应消息）相关的（可能很复杂的）业务逻辑，并将样板 JMS 基础设施问题委托给框架。

Spring 中包含两种标准的 JMS 消息监听器容器，各自有不同的特性集。

- [`SimpleMessageListenerContainer`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-mdp-simple)
- [`DefaultMessageListenerContainer`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-mdp-default)

##### 使用 `SimpleMessageListenerContainer`

此消息侦听器容器是两种标准样式中的简单容器。它在启动时创建固定数量的 JMS 会话和使用者，使用标准 JMS `MessageConsumer.setMessageListener()` 方法注册侦听器，并将其留给 JMS 提供者来执行侦听器回调。此变体不允许动态适应运行时需求或参与外部管理的事务。在兼容性方面，它非常符合独立 JMS 规范的精神，但通常与 Java EE 的 JMS 限制不兼容。

> 尽管 `SimpleMessageListenerContainer` 不允许参与外部管理的事务，但它确实支持本机 JMS 事务。要启用此功能，可以将 `sessionTransacted` 标志切换为 `true`，或者在 XML 名称空间中将 `acknowledge` 属性设置为 `transacted`。然后，从您的侦听器抛出的异常会导致回滚，并重新传递消息。另外，请考虑使用 `CLIENT_ACKNOWLEDGE` 模式，该模式也可以在发生异常的情况下重新交付，但不使用事务处理的 `Session` 实例，因此在该模式中不包含事务协议中任何其他 `Session` 操作（例如发送响应消息）。

> 默认的 `AUTO_ACKNOWLEDGE` 模式无法提供适当的可靠性保证。当侦听器执行失败时消息会丢失（因为提供者会在侦听器调用后自动确认每条消息，没有异常会传播到提供者），或者在侦听器容器关闭时（可以通过设置 `acceptMessagesWhileStopping` 标志进行配置） 。确保出于可靠性需求（例如，为了可靠的队列处理和持久的主题订阅）使用事务处理的会话。

##### 使用 `DefaultMessageListenerContainer`

大多数情况下使用此消息侦听器容器。 与 `SimpleMessageListenerContainer` 相反，此容器变体允许动态适应运行时需求，并能够参与外部管理的事务。当使用 `JtaTransactionManager` 进行配置时，每个接收到的消息都会在 XA 事务中注册。结果，处理可以利用 XA 事务语义。该侦听器容器在对 JMS 提供程序的低要求，高级功能（例如参与外部管理的事务）以及与 Java EE 环境的兼容性之间取得了良好的平衡。

您可以自定义容器的缓存级别。请注意，当未启用缓存时，将为每个消息接收创建一个新的连接和一个新的会话。将其与具有高负载的非持久订阅结合使用可能会导致消息丢失。在这种情况下，请确保使用适当的缓存级别。

当节点关闭时，此容器还具有可恢复的功能。默认情况下，一个简单的 `BackOff` 实现每五秒钟重试一次。您可以为更细粒度的恢复选项指定一个自定义的 `BackOff` 实现。有关示例，请参见 `ExponentialBackOff` 文档了解更多细节。

> 就像它的兄弟（[`SimpleMessageListenerContainer`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-mdp-simple)）一样，`DefaultMessageListenerContainer ` 支持本机 JMS 事务，并允许自定义确认模式。如果对您的情况可行，则强烈建议在外部管理的事务上使用此方法，也就是说，如果 JVM 死亡，您可以偶尔接收重复的消息。业务逻辑中的自定义重复消息检测步骤可以涵盖这种情况，例如以业务实体存在检查或协议表检查的形式。任何这样的安排都比替代方案更为有效：用 XA 事务包装整个处理过程（通过使用 `JtaTransactionManager` 配置 `DefaultMessageListenerContainer`）来覆盖 JMS 消息的接收以及您的消息监听器业务逻辑的执行（包括数据库操作等）。

> 默认的 `AUTO_ACKNOWLEDGE` 模式无法提供适当的可靠性保证。当侦听器执行失败时消息会丢失（因为提供者会在侦听器调用后自动确认每条消息，没有异常会传播到提供者），或者在侦听器容器关闭时（可以通过设置 `acceptMessagesWhileStopping` 标志进行配置） 消息也会丢失。确保出于可靠性需求（例如，为了可靠的队列处理和持久的主题订阅）使用事务处理的会话。

