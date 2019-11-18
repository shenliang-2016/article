# 2 DAO 支持

Spring 中的数据访问对象(DAO)支持的目标是使得可以很简单地以一致的方法使用数据访问技术，比如 JDBC，Hibernate 或者 JPA。这就允许你可以相当容易地在上述持久化技术之间进行切换，还允许你的代码无需考虑捕获特定于每种技术的异常。

## 2.1 一致性异常体系

Spring 提供了一种从特定技术的异常，比如 `SQLException` 向它自己的异常类体系转化的方便方式。Spring 的标准数据访问异常体系以 `DataAccessException` 为根异常。这些异常包装原始的异常，因此你不会有丢失任何具体错误信息的风险。

除了 JDBC 异常，Spring 还可以包装特定于 JPA 和 Hibernate 的异常，将它们转化到一个运行时异常集合。这就允许你在合适的层次处理大部分的不可恢复持久化异常，而不需要在你的 DAOs 中添加大量的异常声明和异常处理代码（不过，你当然可以在你需要的地方自行处理异常）。如前所属，JDBC 异常(包括特定于数据库方言的异常)都被转化到相同的异常体系，这就意味着你可以在一致性的编程模型下之行一些 JDBC 操作。

上面的讨论同样适用于各种 Spring 对各种 ORM 框架提供的支持中的各种模版类。如果你使用基于拦截器的类，应用必须自行处理 `HibernateExceptions` 和 `PersistenceExceptions` ，而不是将该任务委托给 `SessionFactoryUtils` 的 `convertHibernateAccessException(..)` 或者 `convertJpaAccessException()` 方法。这些方法将初始异常转化为兼容 `org.springframework.dao` 异常体系的异常。因为 `PersistenceException` 是不受检查的，它们也可以被抛出(不过，在异常方面牺牲了通用 DAO 抽象)。

下图展示了 Spring 提供的异常体系。(请注意，图中详细描述的类层次结构仅显示整个 `DataAccessException` 层次结构的子集)

![DataAccessException](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/DataAccessException.png)

