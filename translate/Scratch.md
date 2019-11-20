## 3.3 使用 JDBC 核心类控制基本 JDBC 处理和 Error 处理

本节涵盖如何使用 JDBC 核心类控制基本 JDBC 处理，包含错误处理。包括以下主题：

- [使用 `JdbcTemplate`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-JdbcTemplate)
- [使用 `NamedParameterJdbcTemplate`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-NamedParameterJdbcTemplate)
- [使用 `SQLExceptionTranslator`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-SQLExceptionTranslator)
- [运行语句](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-statements-executing)
- [运行查询](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-statements-querying)
- [更新数据库](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-updates)
- [检索自动生成的键](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-auto-generated-keys)

### 3.3.1 使用 `JdbcTemplate`

`JdbcTemplate` 是 JDBC 核心包中的核心类。它处理资源的创建和释放，帮助你避免常见错误，比如忘记关闭连接。它执行核心 JDBC 流程的基本任务 (比如语句创建和执行等) ，应用代码提供 SQL 并提取结果。`JdbcTemplate` 类：

* 运行 SQL 查询
* 更新语句和存储过程调用
* 在 `ResultSet` 实例上执行迭代器，提取返回的参数
* 捕获 JDBC 异常并将它们转化为范型的，携带更多信息的，定义在 `org.springframework.dao` 包中的异常。(参考 [Consistent Exception Hierarchy](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#dao-exceptions) )

当你的代码使用 `JdbcTemplate` 时，你只需要实现回调接口，给予它们清楚定义的契约。由 `JdbcTemplate` 给定 `Connection` 后，`PreparedStatementCreator` 回调接口创建一个准备语句，提供 SQL 和所有必需的参数。`CallableStatementCreator` 接口完整类似的操作，它创建可调用语句。`RowCallbackHandler` 即可从 `ResultSet` 中提取值。

你可以直接使用 `DataSource` 引用实例化 `JdbcTemplate` 并在 DAO 实现中使用，还可以将它配置到 Spring IoC 容器中，并将其作为 bean 引用提供给 DAOs。

> `DataSource` 应该始终被配置为 Spring IoC 容器中的 bean 。在第一种情况下该 bean 被直接提供给服务。第二种情况，它被提供给准备模板。

由此类发出的所有 SQL 都会被记录在 `DEBUG` 级别的日志中，位于对应于模板实例的全限定类名的类别下 (典型地，`JdbcTempalte` ，但是如果你使用了自定义的 `JdbcTemplate` 子类，则会有所不同)。

后续的章节提供了一些使用 `JdbcTemplate` 的例子。这些例子并没有展示 `JdbcTemplate` 暴露出来的所有功能。参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/core/JdbcTemplate.html) 获取更多信息。

