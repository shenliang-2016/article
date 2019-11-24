### 3.3.3 使用 `SQLExceptionTranslator`

`SQLExceptionTranslator` 是一个接口，被那些可以将 `SQLExceptions` 转化为 Spring 自己的 `org.springframework.dao.DataAccessException` 的类实现，这些类并不了解数据访问策略。这些实现可以是宽泛的 (比如，使用 JDBC 的 SQLState 编码) 或者是更精确的 (比如，使用 Oracle 错误编码)。

`SQLErrorCodeSQLExceptionTranslator` 是默认使用的 `SQLExceptionTranslator` 实现。该实现使用特定的提供者 (vendor) 编码。它比 `SQLState` 实现更加精确。错误编码转换基于一个名为 `SQLErrorCodes` 的 JavaBean 类持有的编码。该类由 `SQLErrorCodesFactory` 创建并填充，该类 (顾名思义) 就是一个基于名为 `sql-error-codes.xml` 的配置文件的内容创建 `SQLErrorCodes` 的工厂。该文件基于提供者编码和来自 `DatabaseMetaData` 的 `DatabaseProductName` 填充。你正在使用的具体数据库的编码会被使用。

`SQLErrorCodeSQLExceptionTranslator` 按照下列顺序应用匹配的规则：

1. 由子类实现的所有自定义转换。通常，会使用提供的具体 `SQLErrorCodeSQLExceptionTranslator` ，因此本规则不会应用。本规则只有当你确实提供了一个子类实现时才会应用。
2. 被作为 `SQLErrorCodes` 类的 `customSqlExceptionTranslator` 属性提供的任何自定义 `SQLExceptionTranslator` 实现。
3. 为一个匹配搜索 `CustomSQLErrorCodesTranslation` 类实例列表 (作为 `SQLErrorCodes` 类的 `customTranslations` 属性提供) 。
4. 错误编码匹配被应用。
5. 使用降级的转换器。`SQLExceptionSubclassTranslator` 是默认的降级转换器。如果该转换器不可用，下一个降级转换器是 `SQLStateSQLExceptionTranslator` 。

> 默认使用 `SQLErrorCodesFactory` 来定义 `Error` 编码和自定义的异常转换。它们被从类路径下的名为 `sql-error-codes.xml` 的文件中查找，匹配到的 `SQLErrorCodes` 实例的位置基于来自所使用的数据库的元数据的数据库名称。

你可以扩展 `SQLErrorCodeSQLExceptionTranslator`，如下面例子所示：

```java
public class CustomSQLErrorCodesTranslator extends SQLErrorCodeSQLExceptionTranslator {

    protected DataAccessException customTranslate(String task, String sql, SQLException sqlex) {
        if (sqlex.getErrorCode() == -12345) {
            return new DeadlockLoserDataAccessException(task, sqlex);
        }
        return null;
    }
}
```

前面的例子中，特定的错误编码 (`-12345`) 被转换，其他的错误由默认的转换器实现转换。为了使用该自定义转换器，你必须通过方法 `setExceptionTranslator` 将其传递给 `JdbcTemplate` ，同时你必须使用该 `JdbcTemplate` 进行所有需要转换器的数据访问过程。下面的例子展示了如何使用自定义转换器：

```java
private JdbcTemplate jdbcTemplate;

public void setDataSource(DataSource dataSource) {

    // create a JdbcTemplate and set data source
    this.jdbcTemplate = new JdbcTemplate();
    this.jdbcTemplate.setDataSource(dataSource);

    // create a custom translator and set the DataSource for the default translation lookup
    CustomSQLErrorCodesTranslator tr = new CustomSQLErrorCodesTranslator();
    tr.setDataSource(dataSource);
    this.jdbcTemplate.setExceptionTranslator(tr);

}

public void updateShippingCharge(long orderId, long pct) {
    // use the prepared JdbcTemplate for this update
    this.jdbcTemplate.update("update orders" +
        " set shipping_charge = shipping_charge * ? / 100" +
        " where id = ?", pct, orderId);
}
```

数据源被传递给自定义转换器以便于在 `sql-error-codes.xml` 文件中查找错误编码。

