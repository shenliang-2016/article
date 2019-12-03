### 4.4.3 Spring 驱动的 JPA 事务

> 强烈建议你先阅读 [Declarative transaction management](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative) 。

对于 JPA，推荐的策略是通过 JPA 的本地事务支持进行本地事务。Spring 的 `JpaTransactionManager` 提供了许多本地 JDBC 事务中已知的功能（例如，特定于事务的隔离级别和资源级别的只读优化），而不需要任何常规 JDBC 连接池（不需要 XA）。

Spring JPA 还允许已配置的 `JpaTransactionManager` 将 JPA 事务公开给访问同一 `DataSource` 的 JDBC 访问代码，前提是已注册的 `JpaDialect` 支持底层 JDBC `Connection` 的检索。Spring 为 EclipseLink 和 Hibernate JPA 实现提供了方言。有关 `JpaDialect` 机制的更多细节，请参考 [下一节](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-jpa-dialect)。

> 作为一种直接替代方案，Spring 的本机 `HibernateTransactionManager` 能够与 Spring Framework 5.1 和 Hibernate 5.2/5.3 及更高版本的 JPA 访问代码进行交互，以适应多种 Hibernate 规范并提供 JDBC 交互。与 `LocalSessionFactoryBean` 设置结合使用时特别有意义。有关详细信息，请参见 [用于JPA交互的本地Hibernate设置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-jpa-hibernate) 。

### 4.4.4 理解 `JpaDialect` 和 `JpaVendorAdapter`

作为高级功能，`JpaTransactionManager` 和 `AbstractEntityManagerFactoryBean` 的子类允许将自定义 `JPaDialect` 传递到 `jpaDialect` bean 属性中。`JpaDialect` 实现通常可以以特定于供应商的方式启用 Spring 支持的以下高级功能：

- 应用特定的事务语义（例如自定义隔离级别或事务超时）

- 检索事务性的 JDBC `Connection`（暴露给基于 JDBC 的 DAO）

- 从 `PersistenceExceptions` 到 Spring `DataAccessExceptions` 的高级翻译

这对于特殊的事务语义和异常的高级翻译特别有价值。默认实现（`DefaultJpaDialect`）不提供任何特殊功能，如果需要前面列出的功能，则必须指定适当的方言。

> 作为主要用于 Spring 功能齐全的 `LocalContainerEntityManagerFactoryBean` 设置的更广泛的提供程序适应工具，`JpaVendorAdapter` 将 `JpaDialect` 的功能与其他特定于提供程序的默认值结合在一起。指定 `HibernateJpaVendorAdapter` 或 `EclipseLinkJpaVendorAdapter` 是分别为 Hibernate 或 EclipseLink 自动配置 `EntityManagerFactory` 设置的最便捷方法。请注意，这些提供程序适配器主要设计用于与 Spring 驱动的事务管理一起使用（即，与 `JpaTransactionManager` 一起使用）。

参考 [`JpaDialect`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/orm/jpa/JpaDialect.html) 和 [`JpaVendorAdapter`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/orm/jpa/JpaVendorAdapter.html) 文档详细了解其操作以及如何在 Spring 的 JPA 支持中使用它们。

### 4.4.5 使用 JTA 事务管理配置 JPA

作为 `JpaTransactionManager` 的替代，Spring 还允许通过 JTA 在 Java EE 环境中或与独立事务协调器（例如 `Atomikos`）一起进行多资源事务协调。除了选择 Spring 的 `JtaTransactionManager` 而不是 `JpaTransactionManager` 之外，您还需要采取其他一些步骤：

- 基础的 JDBC 连接池需要具有 XA 功能，并且必须与事务协调器集成在一起。这在 Java EE 环境中通常很简单，通过 JNDI 公开了另一种类型的 `DataSource`。有关详细信息，请参见您的应用程序服务器文档。类似地，独立的事务协调器通常带有特殊的 XA 集成的 `DataSource` 实现。再次，检查其文档。

- 需要为 JTA 配置 JPA `EntityManagerFactory` 设置。这是特定于提供程序的，通常是通过在 `LocalContainerEntityManagerFactoryBean` 上将特殊属性指定为 `jpaProperties` 来实现的。对于 Hibernate，这些属性甚至是特定于版本的。有关详细信息，请参见 Hibernate 文档。
- Spring 的 `HibernateJpaVendorAdapter` 强制实施某些面向 Spring 的默认设置，例如连接释放模式 `on-close`，该模式与 Hibernate 5.0 中的 Hibernate 自己的默认设置匹配，但在 5.1/5.2中不再适用。对于 JTA 设置，请不要声明 `HibernateJpaVendorAdapter` 开头或关闭其 `prepareConnection` 标志。或者，将 Hibernate 5.2 的 `hibernate.connection.handling_mode` 属性设置为 `DELAYED_ACQUISITION_AND_RELEASE_AFTER_STATEMENT`，以恢复 Hibernate 自己的默认设置。请参阅 [使用 Hibernate 的虚假应用程序服务器警告](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-hibernate-invalid-jdbc-access-error) 以获取有关WebLogic的相关介绍。
- 另外，考虑从应用程序服务器本身获取 `EntityManagerFactory`（即通过 JNDI 查找，而不是在本地声明的  `LocalContainerEntityManagerFactoryBean`）。服务器提供的 `EntityManagerFactory` 在服务器配置中可能需要特殊定义（这使得部署的可移植性降低），但已针对服务器的 JTA 环境进行了设置。

### 4.4.6 JPA 交互的本机 Hibernate 设置和本机 Hibernate 事务

从 Spring Framework 5.1 和 Hibernate 5.2/5.3 开始，与 `HibernateTransactionManager` 相结合的本地 `LocalSessionFactoryBean` 设置允许与 `@PersistenceContext` 和其他 JPA 访问代码进行交互。现在 Hibernate `SessionFactory` 本地实现 JPA `EntityManagerFactory` 接口，而 Hibernate `Session` 处理的本地版本就是 JPA `EntityManager`。Spring 的 JPA 支持工具会自动检测本地的 Hibernate 会话。

因此，在许多情况下，这种本地 Hibernate 设置可以代替标准 JPA `LocalContainerEntityManagerFactoryBean` 和 `JpaTransactionManager` 组合，从而允许与同一本地事务中 `PersistenceContext EntityManager` 相关的 `SessionFactory.getCurrentSession()` 和 `HibernateTemplate` 进行交互。这样的设置还提供了更强的 `Hibernate` 集成和更大的配置灵活性，因为它不受 JPA 引导契约的约束。

在这种情况下，您不需要 `HibernateJpaVendorAdapter` 配置，因为 Spring 的本机 Hibernate 设置提供了更多功能（例如，自定义 Hibernate Integrator 设置，Hibernate 5.3 Bean 容器集成以及对只读事务的更强优化）。最后但并非最不重要的一点是，您还可以通过 `LocalSessionFactoryBuilder` 来表达本地 Hibernate 设置，并与 `@Bean` 样式配置无缝集成（不涉及 `FactoryBean`）。

> 就像 JPA `LocalContainerEntityManagerFactoryBean` 一样，`LocalSessionFactoryBean`和 `LocalSessionFactoryBuilder` 支持后台引导。有关简介，请参见 [Background Bootstrapping](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-jpa-setup-background)。
>
> 在 `LocalSessionFactoryBean` 上，可以通过 `bootstrapExecutor` 属性获得。在程序化的 `LocalSessionFactoryBuilder` 上，重载的 `buildSessionFactory` 方法带有一个引导执行程序参数。

