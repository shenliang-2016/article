## 4.2 通用的 ORM 集成考量

本节重点介绍适用于所有 ORM 技术的注意事项。[Hibernate](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-hibernate) 部分提供了更多详细信息并显示了这些功能和具体情况下的配置。

Spring 的 ORM 集成的主要目标是清晰的应用程序分层（具有任何数据访问和事务技术）以及松散耦合应用程序对象–不再对数据访问或事务策略依赖业务服务，不再进行硬编码的资源查找，更多难以替换的单例，不再需要自定义服务注册表。最终目标是采用一种简单且一致的方法来连接应用程序对象，以使它们尽可能可重用，并且消除容器依赖。所有单独的数据访问功能都可以单独使用，但又可以与 Spring 的应用程序上下文概念很好地集成，从而提供基于 XML 的配置和对不需要 Spring 感知的纯 JavaBean 实例的交叉引用。在典型的 Spring 应用程序中，许多重要的对象是 JavaBean：数据访问模板，数据访问对象，事务管理器，使用数据访问对象和事务管理器的业务服务，Web 视图解析器，使用业务服务的 Web 控制器等等。

### 4.2.1 资源管理和事务管理

典型的业务应用程序中充斥着重复的资源管理代码。许多项目试图发明自己的解决方案，有时为了编程方便而牺牲了对故障的正确处理。Spring 提倡简单的解决方案来进行适当的资源处理，即通过在 JDBC 情况下进行模板化以及为 ORM 技术应用 AOP 拦截器来实现所谓的 IoC。

基础设施提供适当的资源处理，并将特定的 API 异常适当地转换为未经检查的基础设施异常层次结构。Spring 引入了 DAO 异常层次结构，适用于任何数据访问策略。对于直接 JDBC，[上一节](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-JdbcTemplate) 中提到的 `JdbcTemplate` 类 提供连接处理并将 `SQLException` 正确转换为 `DataAccessException` 层次结构，包括将特定于数据库的 SQL 错误代码转换为有意义的异常类。有关 ORM 技术，请参见 [下一节](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-exception-translation) 了解如何获得相同的异常转化的好处。

在事务管理方面，`JdbcTemplate` 类通过相应的 Spring 事务管理器挂接到 Spring 事务支持并支持 JTA 和 JDBC 事务。对于受支持的 ORM 技术，Spring 通过 Hibernate 和 JPA 事务管理器提供了 Hibernate 和 JPA 支持以及 JTA 支持。有关事务支持的详细信息，请参见 [事务管理](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction) 一章。

