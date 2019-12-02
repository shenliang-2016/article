### 4.3.5 事务管理策略

`TransactionTemplate` 和 `TransactionInterceptor` 都将实际的事务处理委托给 `PlatformTransactionManager` 实例（可以是 `HibernateTransactionManager`（对于单个 Hibernate  `SessionFactory`）通过使用隐含的 `ThreadLocal` `Session` ），或者 Hibernate 应用程序的 `JtaTransactionManager`（代理到容器的 JTA 子系统）。您甚至可以使用自定义的 `PlatformTransactionManager` 实现。从本机 Hibernate 事务管理切换到 JTA（例如，面对应用程序的某些部署的分布式事务要求时）仅是配置问题。您可以将 Hibernate 事务管理器替换为 Spring 的 JTA 事务实现。事务划分和数据访问代码都无需更改即可工作，因为它们使用通用的事务管理 API。

对于跨多个 Hibernate 会话工厂的分布式事务，可以将 `JtaTransactionManager` 作为事务策略与多个 `LocalSessionFactoryBean` 定义结合使用。然后，每个 DAO 都会获得一个特定的 `SessionFactory` 引用，该引用传递到其相应的 bean 属性中。如果所有底层 JDBC 数据源都是事务性容器数据源，那么只要使用 `JtaTransactionManager` 作为策略，业务服务就可以在任何数量的 DAO 和任意数量的会话工厂之间划分事务。

`HibernateTransactionManager` 和 `JtaTransactionManager` 都允许使用 Hibernate 进行正确的 JVM 级别的缓存处理，而无需特定于容器的事务管理器查找或 JCA 连接器（如果您不使用 EJB 来启动事务）。

`HibernateTransactionManager` 可以将 Hibernate JDBC Connection 导出为特定 `DataSource` 的普通 JDBC 访问代码。此功能允许使用混合的 Hibernate 和 JDBC 数据访问进行高级事务划分，而无需 JTA，前提是您仅访问一个数据库。如果您通过 `LocalSessionFactoryBean` 类的 `dataSource` 属性使用 `DataSource` 设置了传入的 `SessionFactory`，则 `HibernateTransactionManager` 会自动将 Hibernate 事务公开为 JDBC 事务。或者，您可以通过 `HibernateTransactionManager` 类的 `dataSource` 属性显式指定应该公开其事务的 `DataSource`。

### 4.3.6 比较容器管理的和本地定义的资源

您可以在容器管理的 JNDI `SessionFactory` 和本地定义的 JNDI `SessionFactory` 之间切换，而无需更改任何一行应用程序代码。将资源定义保留在容器中还是在应用程序中本地保留，主要取决于您使用的事务策略。与 Spring 定义的本地 `SessionFactory` 相比，手动注册的 JNDI `SessionFactory` 没有任何好处。通过 Hibernate 的 JCA 连接器部署 `SessionFactory` 可以增加参与 Java EE 服务器的管理基础架构的附加价值，但是也仅此而已。

Spring 的事务支持不限于容器。当使用除 JTA 之外的任何其他策略配置时，事务支持还可以在独立或测试环境中工作。尤其是在单数据库事务的典型情况下，Spring 的单资源本地事务支持是 JTA 的轻量级功能强大的替代方案。当您使用本地 EJB 无状态会话 Bean 驱动事务时，即使您仅访问单个数据库并且仅使用无状态会话 Bean 通过容器管理的事务提供声明性事务，您也将依赖 EJB 容器和 JTA。以编程方式直接使用 JTA 还需要 Java EE 环境。就 JTA 本身和 JNDI `DataSource` 实例而言，JTA 不仅仅涉及容器依赖项。对于非 Spring 的，由 JTA 驱动的 Hibernate 事务，您必须使用 Hibernate JCA 连接器或额外的 Hibernate 事务代码，并将其 `TransactionManagerLookup` 配置为正确的 JVM 级别的缓存。

Spring 驱动的事务可以与本地定义的 Hibernate `SessionFactory` 一起工作，就像访问本地 JDBC `DataSource` 一样，只要它们访问单个数据库即可。因此，只有在分配了事务需求后，才需要使用 Spring 的 JTA 交易策略。JCA 连接器需要特定于容器的部署步骤，并且首先需要（显然）JCA 支持。与部署具有本地资源定义和 Spring 驱动的事务的简单 Web 应用程序相比，此配置需要更多的工作。另外，如果使用（例如）不提供 JCA 的 WebLogic Express，则通常需要容器的企业版。具有跨单个数据库的本地资源和事务的 Spring 应用程序可以在任何 Java EE Web 容器（没有 JTA，JCA 或 EJB）中运行，例如 Tomcat，Resin 甚至普通 Jetty。此外，您可以轻松地在桌面应用程序或测试套件中重用这样的中间层。

考虑到所有问题，如果您不使用 EJB，请坚持使用本地的 `SessionFactory` 设置和 Spring 的 `HibernateTransactionManager` 或 `JtaTransactionManager`。您将获得所有好处，包括适当的事务性 JVM 级别的缓存和分布式事务，而不会给容器部署带来不便。通过 JCA 连接器对 Hibernate `SessionFactory` 进行 JNDI 注册仅在与 EJB 结合使用时才增加价值。

### 4.3.7 Hibernate 虚假的应用程序服务器警告

在某些具有非常严格的 `XADataSource` 实现的 JTA 环境中（当前仅某些 WebLogic Server 和 WebSphere 版本），当配置 Hibernate 而不考虑该环境的 JTA `PlatformTransactionManager` 对象时，虚假警告或异常会显示在应用程序服务器日志中。这些警告或异常指示正在访问的连接不再有效或 JDBC 访问不再有效，这可能是因为事务不再有效。例如，这是 WebLogic 的实际异常：

```shell
java.sql.SQLException: The transaction is no longer active - status: 'Committed'. No
further JDBC access is allowed within this transaction.
```

您可以通过使 Hibernate 感知与之同步的JTA `PlatformTransactionManager` 实例（以及 Spring 实例）来解决此警告。您可以通过以下两种方式执行此操作：

- 如果在您的应用程序上下文中，您已经直接获取了JTA `PlatformTransactionManager` 对象（大概是通过 `JndiObjectFactoryBean` 或 `<jee:jndi-lookup>` 从 JNDI 获取）并将其提供给例如 Spring 的  `JtaTransactionManager`，则最简单的方法是指定对定义此 JTA `PlatformTransactionManager` 实例的 Bean 的引用，作为 `LocalSessionFactoryBean` 的 `jtaTransactionManager` 属性的值。然后，Spring 使对象可用于 Hibernate。
- 更可能的是，您还没有 JTA `PlatformTransactionManager` 实例，因为 Spring 的 `JtaTransactionManager` 可以自行找到它。因此，您需要配置 Hibernate 来直接查找 JTA `PlatformTransactionManager`。您可以通过在 Hibernate 配置中配置特定于应用程序服务器的 `TransactionManagerLookup` 类来实现此目的，如 Hibernate 手册中所述。

本节的其余部分描述了在 Hibernate 不感知 JTA `PlatformTransactionManager` 的情况下发生的事件序列。

如果未配置 Hibernate 对 JTA `PlatformTransactionManager` 的任何感知，则在 JTA 事务提交时会发生以下事件：

- JTA 事务提交。
- Spring 的 `JtaTransactionManager` 与 JTA 事务同步，因此它由 JTA 事务管理器通过 `afterCompletion` 回调进行回调。
- 在其他活动中，这种同步可以通过 Spring 的 Hibernate 的 `afterTransactionCompletion` 回调（用于清除 Hibernate 的缓存）触发 Spring 到 Hibernate 的回调，然后在 Hibernate 会话上进行显式的 `close()` 调用，这会使 Hibernate 尝试 `close()` JDBC连接。
- 在某些环境中，此 `Connection.close()` 调用随后触发警告或错误，因为应用程序服务器不再认为 `Connection` 是可用的，因为事务已经提交。

当 Hibernate 配置为具有 JTA `PlatformTransactionManager` 感知时，在提交 JTA 事务时会发生以下事件：

- JTA 事务已准备好提交。

- Spring 的 `JtaTransactionManager` 被同步到 JTA 事务，因此 JTA 事务管理器通过一次 `beforeCompletion` 回调回调了该事务。

- Spring 感知 Hibernate 本身已同步到 JTA 事务，并且其行为与先前方案不同。假设完全需要关闭 Hibernate `Session`，Spring 现在将其关闭。

- JTA 事务提交。

- Hibernate 已同步到 JTA 事务，因此 JTA 事务管理器通过 `afterCompletion` 回调来回调该事务，并且可以正确清除其缓存。

