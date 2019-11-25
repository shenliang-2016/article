## 3.4 控制数据库连接

本节涵盖：

- [使用 `DataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-datasource)
- [使用 `DataSourceUtils`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-DataSourceUtils)
- [实现 `SmartDataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-SmartDataSource)
- [扩展 `AbstractDataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-AbstractDataSource)
- [使用 `SingleConnectionDataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-SingleConnectionDataSource)
- [使用 `DriverManagerDataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-DriverManagerDataSource)
- [使用 `TransactionAwareDataSourceProxy`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-TransactionAwareDataSourceProxy)
- [使用 `DataSourceTransactionManager`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-DataSourceTransactionManager)

### 3.4.1 使用 `DataSource`

Spring 通过 `DataSource` 获取数据库连接。`DataSource` 是 JDBC 规范的一部分，同时是一个通用的连接工厂。它允许容器或者框架向应用代码隐藏连接池和事务管理问题。作为开发者，你不需要了解数据库连接的具体细节。这是配置数据库的管理员的职责。你必须完成开发并测试代码的任务，但是你没有必要了解生产数据源是如何配置的。

当你使用 Spring 的 JDBC 层时，你可以从 JNDI 获取数据源，或者你可以配置第三方提供的连接池实现。流行的实现是 Apache Jakarta Commons DBCP 和 C3P0。Spring 发行版中的实现仅仅用于测试目的，并且没有提供池化实现。

本节使用 Spring 的 `DriverManagerDataSource` 实现，后续介绍另外几种实现。

> 你应该仅将 `DriverManagerDataSource` 类用于测试目的，因为它并未提供池化实现，因而当一个连接上到来多个请求时性能很差。

为了配置 `DriverManagerDataSource`：

1. 从 `DriverManagerDataSource` 获取一个连接，类似于你典型地获取一个 JDBC 连接那样。
2. 指定 JDBC 驱动的全限定类名以便于 `DriverManager` 可以加载该驱动类。
3. 提供一个特定于不同 JDBC 驱动的 URL。（参考你使用的驱动文档获取正确的值）
4. 提供用户名和密码以连接数据库。

下面的例子展示了如何在 Java 中配置 `DriverManagerDataSource` ：

```java
DriverManagerDataSource dataSource = new DriverManagerDataSource();
dataSource.setDriverClassName("org.hsqldb.jdbcDriver");
dataSource.setUrl("jdbc:hsqldb:hsql://localhost:");
dataSource.setUsername("sa");
dataSource.setPassword("");
```

下面的例子展示了对应的 XML 配置：

```xml
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

<context:property-placeholder location="jdbc.properties"/>
```

下面两个例子展示了 DBCP 和 C3P0 的连接性和配置。为了学习更多选项以控制连接池特性，参考相应连接池实现的产品文档。

下面的例子展示了 DBCP 配置：

```xml
<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

<context:property-placeholder location="jdbc.properties"/>
```

下面的例子展示了 C3P0 配置：

```xml
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" destroy-method="close">
    <property name="driverClass" value="${jdbc.driverClassName}"/>
    <property name="jdbcUrl" value="${jdbc.url}"/>
    <property name="user" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

<context:property-placeholder location="jdbc.properties"/>
```