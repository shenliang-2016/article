### 3.4.2 使用 `DataSourceUtils`

`DataSourceUtils` 类是一个方便而且强大的帮助类，提供了 `static` 方法来从 JNDI 获取连接，如果需要，关闭连接。它支持线程绑定的连接以及，例如，`DataSourceTransactionManager` 。

### 3.4.3 实现 `SmartDataSource`

`SmartDataSource` 接口应该被那些能够提供关系数据库连接的类实现。它扩展 `DataSource` 接口以允许使用它的类查询给定的操作完成之后连接是否应该被关闭。当你需要复用连接是这种用法的有效的。

### 3.4.4 扩展 `AbstractDataSource`

`AbstractDataSource` 是一个Spring 的 `DataSource` 实现的 `abstract` 基类。它实现了所有 `DataSource` 实现的通用部分。你应该扩展 `AbstractDataSource` 类，如果你编写自己的 `DataSource` 实现。

### 3.4.5 使用 `SingleConnectionDataSource`

`SingleConnectionDataSource` 类是 `SmartDataSource` 接口的实现，包装了一个使用后不会被关闭的 `Connection` 。但是不具有多线程能力。

如果任何客户端代码调用假想中的池化连接（与使用持久化工具时一样）上的 `close` 方法，你应该将 `suppressClose` 属性设定为 `true` 。该设定返回一个关闭压抑 (close-suppressing) 代理包装物理连接。注意，此时你就不再能够将其转化为一个原生的 Oracle `Connection` 或者类似的对象。

`SingleConnectionDataSource` 主要是一个测试类。比如，它允许在应用服务器之外，结合一个简单的 JNDI 环境方便地编写测试代码。相对于 `DriverManagerDataSource` ，它始终复用相同的连接，避免了物理连接的额外创建。

### 3.4.6 使用 `DriverManagerDataSource`

`DriverManagerDataSource` 类是标准 `DataSource` 接口的实现，该接口通过 bean 属性配置普通的 JDBC 驱动程序，并每次都返回一个新的 `Connection`。

此实现对于 Java EE 容器外部的测试和独立部署环境非常有用，可以作为 Spring IoC 容器中的 `DataSource` Bean或与简单的 JNDI 环境结合使用。假想池的 `Connection.close()` 调用会关闭连接，因此任何 `DataSource` 感知的持久性代码都应该起作用。然而，即使在测试环境中，使用 JavaBean 风格的连接池（例如 `commons-dbcp`）也是如此容易，以至于总是比在 `DriverManagerDataSource` 上使用这样的连接池更为可取。

### 3.4.7 使用 `TransactionAwareDataSourceProxy`

`TransactionAwareDataSourceProxy` 是目标 `DataSource` 的代理。该代理包装目标 `DataSource` 以添加 Spring 管理的事务的敏感性。这个层面上，它类似于 Java EE 服务器提供的事务性的 `DataSource` 。

> 很少需要使用此类，除非必须调用已经存在的代码并传入标准的 JDBC `DataSource` 接口实现。在这种情况下，您仍然可以使该代码可用，同时使该代码参与 Spring 托管的事务。通常最好使用更高级别的资源管理抽象来编写自己的新代码，例如 `JdbcTemplate` 或 `DataSourceUtils`。

参考 [`TransactionAwareDataSourceProxy`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/datasource/TransactionAwareDataSourceProxy.html) 文档获取更多细节。

### 3.4.8 使用 `DataSourceTransactionManager`

`DataSourceTransactionManager` 类是用于单个 JDBC 数据源的 `PlatformTransactionManager` 实现。它将 JDBC 连接从指定的数据源绑定到当前正在执行的线程，可能允许每个数据源一个线程连接。

应用程序代码需要通过 `DataSourceUtils.getConnection(DataSource)` 来检索 JDBC 连接，而不是 Java EE 的标准 `DataSource.getConnection` 。它抛出未经检查的 `org.springframework.dao` 异常，而不是`SQLExceptions` 。所有框架类（例如 `JdbcTemplate`）都隐式使用此策略。如果不与该事务管理器一起使用，则查找策略的行为与普通策略完全相同。因此，可以在任何情况下使用它。

`DataSourceTransactionManager` 类支持自定义隔离级别和超时，这些级别和超时将作为适当的 JDBC 语句查询超时而应用。为了支持后者，应用程序代码必须使用 `JdbcTemplate` 或为每个创建的语句调用 `DataSourceUtils.applyTransactionTimeout(..)` 方法。

在单资源情况下，您可以使用此实现代替 `JtaTransactionManager`，因为它不需要容器支持 JTA。您可以坚持需要的连接查找模式，因为在两者之间进行切换只是配置问题。JTA不支持自定义隔离级别。

