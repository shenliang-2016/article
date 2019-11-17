## 1.8 Application server-specific integration

Spring 的事务抽象基本上是与应用服务器无关的。此外，Spring 的 `JtaTransactionManager` 类 (可以有选择地执行 JNDI lookup 为了 JTA `UserTransaction` 和 `JtaTransactionManager` 对象) 自动探测后续类的位置，该位置不同应用服务器不尽相同。可以访问 JTA `TransactionManager` 允许增强事务语义－特别地，支持事务挂起。参考 [`JtaTransactionManager`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/transaction/jta/JtaTransactionManager.html) 文档获取更多细节。

Spring 的 `JtaTransactionManager` 是运行在 Java EE 应用服务器上的标准选择，被认为可以工作在所有常见服务器上。高级功能，比如事务挂起，也可以在许多服务器上的工作 (包括 GlassFish, JBoss, 以及 Geronimo) 而不需要任何特殊配置。不过，为了事务挂起和更多高级集成的完整支持，Spring 包含了为 WebLogic Server 和 WebSphere 专门提供的特殊适配器。这些适配器将在随后章节中讨论。

对标准场景来所，包含 WebLogic Server 和 WebSphere ，考虑使用方便的 `<tx:jta-transaction-manager/>` 配置元素。当配置该元素时，它会自动探测底层的服务器并选择该平台上最佳的可用事务管理器。这就意味着你不需要显式配置特定于服务器的适配器类 (接下来的章节中讨论)。它们是会被自动选择的，如果没有合适的选择，标准的 `JtaTransactionManager` 就会作为默认的降级后备。

### 1.8.1 IBM WebSphere

在 WebSphere 6.1.0.9 以及更高版本的服务器上，推荐使用的 Spring JTA 事务管理器是 `WebSphereUowTransactionManager` 。这个特殊的适配器使用 IBM 的 `UOWManager` API，它在 WebSphere Application Server 6.1.0.9 及更高版本上可用。使用该适配器，Spring 驱动的事务挂起 (挂起以及由 `PROPAGATION_REQUIRES_NEW` 恢复为初始化状态) 得到 IBM 的官方支持。

### 1.8.2 Oracle WebLogic Server

在 WebLogic Server 9.0 及更高版本服务器上，我们通常使用 `WebLogicJtaTransactionManager` 替代 `JtaTransactionManager` 类。这个特定于 WebLogic 的 `JtaTansactionManager` 类的子类在 WebLogic 管理的事务环境下支持 Spring 的事务定义的完整能力，而不仅限于标准的 JTA 语义。包含事务名称，每个事务的隔离级别，以及在所有情况下正确地恢复事务。

## 1.9 常见问题解决方案

本节描述一些常见问题的解决方案。

### 1.9.1 为特定 `DataSource` 使用错误的事务管理器

基于你的事务性技术选择和实际需求使用正确的 `PlatformTransactionManager` 实现。使用正确的情况下，Spring 框架仅仅提供直截了当和可移植的抽象。如果你使用全局事务，你必须使用 `org.springframework.transaction.jta.JtaTransactionManager` 类 (或者它的 [application server-specific subclass](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-application-server-integration) 的子类) 来执行所有事务性操作。否则，事务基础设施尝试在此类资源上执行局部事务，比如容器 `DataSource` 实例。此类局部事务没有意义，良好的应用服务器将它们当作是错误。

## 1.10 更多资源

有关 Spring 框架事务支持的更多信息，参考：

- [Distributed transactions in Spring, with and without XA](https://www.javaworld.com/javaworld/jw-01-2009/jw-01-spring-transactions.html) 是 JavaWorld 的一个演示，Spring 的 David Syer 指导您完成 Spring 应用程序中七个分布式事务模式，其中三个使用 XA，四个不使用 XA。
- [*Java Transaction Design Strategies*](https://www.infoq.com/minibooks/JTDS) 是 [InfoQ](https://www.infoq.com/) 上的一本书，其中提供了有关 Java 事务的详细介绍。 它还包括有关如何通过 Spring Framework 和 EJB3 配置和使用事务的端到端示例。

