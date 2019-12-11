#### 3.1.5 事务管理

Spring 提供了一个 `JmsTransactionManager` 来管理单个 JMS `ConnectionFactory` 的事务。这样，JMS 应用程序就可以利用 Spring 的托管事务功能，如 [Transaction Management section of the Data Access chapter](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction) 部分所述。`JmsTransactionManager` 执行本地资源事务，将来自指定 `ConnectionFactory` 的 JMS Connection/Session 对绑定到线程。`JmsTemplate` 会自动检测此类事务资源并对其进行相应的操作。

在 Java EE 环境中，`ConnectionFactory` 汇集了 `Connection` 和 `Session` 实例，因此可以有效地在事务之间重用这些资源。在独立环境中，使用 Spring 的 `SingleConnectionFactory` 会导致共享的 JMS `Connection`，并且每个事务都有自己独立的 `Session`。另外，考虑使用提供程序专用的池适配器，例如 ActiveMQ 的 `PooledConnectionFactory` 类。

您还可以将 `JmsTemplate` 和 `JtaTransactionManager` 和具有 XA 功能的 JMS `ConnectionFactory` 一起使用来执行分布式事务。请注意，这需要使用 JTA 事务管理器以及正确的 XA 配置的 `ConnectionFactory`。（请查看您的 Java EE 服务器或 JMS 提供者的文档。）

使用 JMS API 从 `Connection` 创建 `Session` 时，在托管和非托管事务环境中重用代码可能会造成混淆。这是因为 JMS API 只有一种工厂方法可以创建 `Session`，并且它需要事务和确认模式的值。在托管环境中，设置这些值是环境的事务基础设施的责任，因此，供应商对 JMS `Connection` 的包装将忽略这些值。在非托管环境中使用 `JmsTemplate` 时，可以通过使用 `sessionTransacted` 和 `sessionAcknowledgeMode` 属性来指定这些值。当将 `PlatformTransactionManager` 与 `JmsTemplate` 一起使用时，模板总是被赋予事务性 JMS `Session`。

