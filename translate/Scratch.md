# 4 对象－关系映射（ORM）数据访问

本节如何使用对象－关系映射（ORM）进行数据访问。

## 4.1 Spring 的 ORM 介绍

Spring Framework 支持与 Java Persistence API（JPA）集成，并支持用于资源管理，数据访问对象（DAO）实现和事务策略的本地 Hibernate。例如，对于 Hibernate，它具有一流的支持以及一些便捷的 IoC 功能，可解决许多典型的 Hibernate 集成问题。您可以通过依赖关系注入为 OR（对象关系）映射工具配置所有受支持的功能。它们可以参与 Spring 的资源和事务管理，并且符合 Spring 的通用事务和 DAO 异常层次结构。推荐的集成样式是针对普通的 Hibernate 或 JPA API 编写 DAO。

当您创建数据访问应用程序时，Spring 会显着增强您选择的 ORM 层。您可以根据需要利用尽可能多的集成支持，并且应该将这种集成工作与内部构建类似基础架构的成本和风险进行比较。不管使用哪种技术，您都可以像使用库一样使用许多 ORM 支持，因为所有内容都被设计为一组可重用的 JavaBean。Spring IoC 容器中的 ORM 有 助于配置和部署。因此，本节中的大多数示例都显示了 Spring 容器内部的配置。

使用 Spring 框架创建 ORM DAOs 的好处包括：

- **测试更简单。** Spring 的 IoC 方法使交换 Hibernate `SessionFactory` 实例，JDBC `DataSource` 实例，事务管理器和映射对象实现（如果需要）的实现和配置位置变得容易。反过来，这使得隔离每个与持久性相关的代码片段的测试变得容易得多。
- **通用的数据访问异常。** Spring 可以包装您的 ORM 工具中的异常，将它们从专有的（可能是受检查的）异常转换为通用的运行时 `DataAccessException` 层次结构。使用此功能，您可以仅在适当的层中处理大多数不可恢复的持久性异常，而不需要烦人的到处添加捕获，抛出和异常声明。您仍然可以根据需要捕获和处理异常。请记住，JDBC 异常（包括特定于 DB 的方言）也将转换为相同的层次结构，这意味着您可以在一致的编程模型中使用 JDBC 执行某些操作。
- **通用资源管理。** Spring 应用程序上下文可以处理 Hibernate `SessionFactory` 实例，JPA `EntityManagerFactory` 实例，JDBC `DataSource` 实例和其他相关资源的位置和配置。这使得这些值易于管理和更改。Spring 提供了对持久性资源的高效，便捷和安全的处理。例如，使用 Hibernate 的相关代码通常需要使用相同的 Hibernate `Session`，以确保效率和适当的事务处理。通过在Hibernate的 `SessionFactory` 中公开当前的 `Session`，Spring 可以使创建 `Session` 和透明地绑定到当前线程变得容易。因此，对于任何本地或 JTA 事务环境，Spring 都解决了典型的 Hibernate 使用中的许多长期问题。
- **集成事务管理。** 您可以通过 `@Transactional` 注解或通过在 XML 配置文件中显式配置事务 AOP 增强，以声明性的，面向方面的编程（AOP）样式的方法拦截器包装 ORM 代码。这两种情况下，都会为您处理事务语义和异常处理（回滚等）。如 [Resource and Transaction Management](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-resource-mngmnt) 中所述，还可以交换各种事务管理器，而不会影响您与 ORM 相关的代码。例如，您可以在两种情况下使用相同的完整服务（例如声明性事务）在本地事务和 JTA 之间进行交换。此外，与 JDBC 相关的代码可以与您用于执行 ORM 的代码完全事务性集成。这对于不适合 ORM（例如批处理和 BLOB 流）但仍需要与 ORM 操作共享常见事务的数据访问很有用。

> 要获得更全面的 ORM 支持，包括对 MongoDB 等替代数据库技术的支持，您可能需要查看 [Spring Data](https://projects.spring.io/spring-data/) 项目套件。如果您是 JPA 用户，请参阅 [https://spring.io](https://spring.io/) 中的 [使用JPA开始访问数据](https://spring.io/guides/gs/accessing-data-jpa/) 指南。

