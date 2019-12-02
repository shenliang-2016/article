### 4.3.5 事务管理策略

`TransactionTemplate` 和 `TransactionInterceptor` 都将实际的事务处理委托给 `PlatformTransactionManager` 实例（可以是 `HibernateTransactionManager`（对于单个 Hibernate  `SessionFactory`）通过使用隐含的 `ThreadLocal` `Session` ），或者 Hibernate 应用程序的 `JtaTransactionManager`（代理到容器的 JTA 子系统）。您甚至可以使用自定义的 `PlatformTransactionManager` 实现。从本机 Hibernate 事务管理切换到 JTA（例如，面对应用程序的某些部署的分布式事务要求时）仅是配置问题。您可以将 Hibernate 事务管理器替换为 Spring 的 JTA 事务实现。事务划分和数据访问代码都无需更改即可工作，因为它们使用通用的事务管理 API。

对于跨多个 Hibernate 会话工厂的分布式事务，可以将 `JtaTransactionManager` 作为事务策略与多个 `LocalSessionFactoryBean` 定义结合使用。然后，每个 DAO 都会获得一个特定的 `SessionFactory` 引用，该引用传递到其相应的 bean 属性中。如果所有底层 JDBC 数据源都是事务性容器数据源，那么只要使用 `JtaTransactionManager` 作为策略，业务服务就可以在任何数量的 DAO 和任意数量的会话工厂之间划分事务。



Both `HibernateTransactionManager` and `JtaTransactionManager` allow for proper JVM-level cache handling with Hibernate, without container-specific transaction manager lookup or a JCA connector (if you do not use EJB to initiate transactions).

`HibernateTransactionManager` can export the Hibernate JDBC `Connection` to plain JDBC access code for a specific `DataSource`. This ability allows for high-level transaction demarcation with mixed Hibernate and JDBC data access completely without JTA, provided you access only one database. `HibernateTransactionManager` automatically exposes the Hibernate transaction as a JDBC transaction if you have set up the passed-in `SessionFactory` with a `DataSource` through the `dataSource` property of the `LocalSessionFactoryBean` class. Alternatively, you can specify explicitly the `DataSource` for which the transactions are supposed to be exposed through the `dataSource` property of the `HibernateTransactionManager` class.

### 4.3.6 比较容器管理的和本地定义的资源

You can switch between a container-managed JNDI `SessionFactory` and a locally defined one without having to change a single line of application code. Whether to keep resource definitions in the container or locally within the application is mainly a matter of the transaction strategy that you use. Compared to a Spring-defined local `SessionFactory`, a manually registered JNDI `SessionFactory` does not provide any benefits. Deploying a `SessionFactory` through Hibernate’s JCA connector provides the added value of participating in the Java EE server’s management infrastructure, but does not add actual value beyond that.

Spring’s transaction support is not bound to a container. When configured with any strategy other than JTA, transaction support also works in a stand-alone or test environment. Especially in the typical case of single-database transactions, Spring’s single-resource local transaction support is a lightweight and powerful alternative to JTA. When you use local EJB stateless session beans to drive transactions, you depend both on an EJB container and on JTA, even if you access only a single database and use only stateless session beans to provide declarative transactions through container-managed transactions. Direct use of JTA programmatically also requires a Java EE environment. JTA does not involve only container dependencies in terms of JTA itself and of JNDI `DataSource` instances. For non-Spring, JTA-driven Hibernate transactions, you have to use the Hibernate JCA connector or extra Hibernate transaction code with the `TransactionManagerLookup` configured for proper JVM-level caching.

Spring-driven transactions can work as well with a locally defined Hibernate `SessionFactory` as they do with a local JDBC `DataSource`, provided they access a single database. Thus, you need only use Spring’s JTA transaction strategy when you have distributed transaction requirements. A JCA connector requires container-specific deployment steps, and (obviously) JCA support in the first place. This configuration requires more work than deploying a simple web application with local resource definitions and Spring-driven transactions. Also, you often need the Enterprise Edition of your container if you use, for example, WebLogic Express, which does not provide JCA. A Spring application with local resources and transactions that span one single database works in any Java EE web container (without JTA, JCA, or EJB), such as Tomcat, Resin, or even plain Jetty. Additionally, you can easily reuse such a middle tier in desktop applications or test suites.

All things considered, if you do not use EJBs, stick with local `SessionFactory` setup and Spring’s `HibernateTransactionManager` or `JtaTransactionManager`. You get all of the benefits, including proper transactional JVM-level caching and distributed transactions, without the inconvenience of container deployment. JNDI registration of a Hibernate `SessionFactory` through the JCA connector adds value only when used in conjunction with EJBs.

### 4.3.7 Hibernate 虚假的应用程序服务器警告

In some JTA environments with very strict `XADataSource` implementations (currently only some WebLogic Server and WebSphere versions), when Hibernate is configured without regard to the JTA `PlatformTransactionManager` object for that environment, spurious warning or exceptions can show up in the application server log. These warnings or exceptions indicate that the connection being accessed is no longer valid or JDBC access is no longer valid, possibly because the transaction is no longer active. As an example, here is an actual exception from WebLogic:

```shell
java.sql.SQLException: The transaction is no longer active - status: 'Committed'. No
further JDBC access is allowed within this transaction.
```

You can resolve this warning by making Hibernate aware of the JTA `PlatformTransactionManager` instance, to which it synchronizes (along with Spring). You have two options for doing this:

- If, in your application context, you already directly obtain the JTA `PlatformTransactionManager` object (presumably from JNDI through `JndiObjectFactoryBean` or `<jee:jndi-lookup>`) and feed it, for example, to Spring’s `JtaTransactionManager`, the easiest way is to specify a reference to the bean that defines this JTA `PlatformTransactionManager` instance as the value of the `jtaTransactionManager` property for `LocalSessionFactoryBean.` Spring then makes the object available to Hibernate.
- More likely, you do not already have the JTA `PlatformTransactionManager` instance, because Spring’s `JtaTransactionManager` can find it itself. Thus, you need to configure Hibernate to look up JTA `PlatformTransactionManager` directly. You do this by configuring an application server-specific `TransactionManagerLookup` class in the Hibernate configuration, as described in the Hibernate manual.

The remainder of this section describes the sequence of events that occur with and without Hibernate’s awareness of the JTA `PlatformTransactionManager`.

When Hibernate is not configured with any awareness of the JTA `PlatformTransactionManager`, the following events occur when a JTA transaction commits:

- The JTA transaction commits.
- Spring’s `JtaTransactionManager` is synchronized to the JTA transaction, so it is called back through an `afterCompletion` callback by the JTA transaction manager.
- Among other activities, this synchronization can trigger a callback by Spring to Hibernate, through Hibernate’s `afterTransactionCompletion` callback (used to clear the Hibernate cache), followed by an explicit `close()` call on the Hibernate session, which causes Hibernate to attempt to `close()` the JDBC Connection.
- In some environments, this `Connection.close()` call then triggers the warning or error, as the application server no longer considers the `Connection` to be usable, because the transaction has already been committed.

When Hibernate is configured with awareness of the JTA `PlatformTransactionManager`, the following events occur when a JTA transaction commits:

- The JTA transaction is ready to commit.
- Spring’s `JtaTransactionManager` is synchronized to the JTA transaction, so the transaction is called back through a `beforeCompletion` callback by the JTA transaction manager.
- Spring is aware that Hibernate itself is synchronized to the JTA transaction and behaves differently than in the previous scenario. Assuming the Hibernate `Session` needs to be closed at all, Spring closes it now.
- The JTA transaction commits.
- Hibernate is synchronized to the JTA transaction, so the transaction is called back through an `afterCompletion` callback by the JTA transaction manager and can properly clear its cache.