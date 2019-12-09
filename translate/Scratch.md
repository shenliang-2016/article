## 2 Enterprise JavaBeans (EJB) 集成

EJB 好像已经被业界抛弃……

## 3 JMS (Java Message Service)

Spring 提供了一个 JMS 集成框架用来简化 JMS API 的使用，非常类似于 Spring 的 JDBC 集成对 JDBC API 使用的简化。

JMS 可以粗略分成两个部分功能，称为消息生产和消息消费。`JmsTemplate` 类被用来生产消息和同步消息接收。对于类似于 Java EE 消息驱动 bean 样式的异步接收，Spring 提供了许多消息侦听器容器，可用于创建消息驱动 POJO（MDP）。Spring 还提供了一种声明式方法来创建消息侦听器。

`org.springframework.jms.core` 软件包提供了使用 JMS 的核心功能。它包含 JMS 模板类，该 JMS 模板类通过处理资源的创建和释放来简化 JMS 的使用，就像 `JdbcTemplate` 对 JDBC 所做的那样。Spring 模板类共有的设计原则是提供辅助方法来执行常见的操作，并且对于更复杂的用法，将处理任务的核心委托给用户实现的回调接口。 JMS 模板遵循相同的设计。这些类提供了各种便利的方法，用于发送消息，同步使用消息以及向用户公开 JMS 会话和消息生成器。

`org.springframework.jms.support` 包提供了 `JMSException` 转换功能。转换将检查的 `JMSException` 层次结构转换为未检查的异常的镜像层次结构。如果已检查的 `javax.jms.JMSException` 的提供者特定的子类存在，则将此异常包装在未检查的 `UncategorizedJmsException` 中。

`org.springframework.jms.support.converter` 包提供了 `MessageConverter` 抽象，可以在 Java 对象和 JMS 消息之间进行转换。

`org.springframework.jms.support.destination` 包提供了用于管理 JMS 目的地的各种策略，例如为 JNDI 中存储的目的地提供服务定位器。

`org.springframework.jms.annotation` 包通过使用 `@JmsListener` 提供了必要的基础设施来支持注解驱动的侦听器端点。

`org.springframework.jms.config` 包为` jms` 名称空间提供了解析器实现，并提供了 Java config 支持来配置监听器容器和创建监听器端点。

最后，`org.springframework.jms.connection` 包提供了适用于独立应用程序的 `ConnectionFactory` 的实现。它还包含 Spring 用于 JMS 的 `PlatformTransactionManager` 的实现（巧妙地名为 `JmsTransactionManager`）。这样可以将 JMS 作为事务资源无缝集成到 Spring 的事务管理机制中。

> 从 Spring Framework 5 开始，Spring 的 JMS 软件包完全支持 JMS 2.0，并要求在运行时提供 JMS 2.0 API。我们建议使用 JMS 2.0 兼容的提供程序。
>
> 如果您碰巧在系统中使用了较旧的消息代理，则可以尝试升级到适用于现有代理的 JMS 2.0 兼容驱动程序。或者，您也可以尝试针对基于 JMS 1.1 的驱动程序运行，只需将 JMS 2.0 API jar 放在类路径上，而仅对驱动程序使用兼容 JMS 1.1的API。Spring 的 JMS 支持默认情况下遵守 JMS 1.1 约定，因此通过相应的配置它确实支持这种情况。但是，请仅在过渡方案中考虑这一点。

