### 3.3.2 使用 `NamedParameterJdbcTemplate`

 `NamedParameterJdbcTemplate` 类相对于传统的编程式 JDBC 语句仅仅使用占位符 `'?'` 参数，支持了编程式 JDBC 语句使用命名参数的支持。 `NamedParameterJdbcTemplate` 类包装了一个 `JdbcTemplate` 并将很多工作委托给该 `JdbcTemplate` 。本节仅仅描述了 `NamedParameterJdbcTemplate` 区别于 `JdbcTemplate` 本身的部分－也就是，在编程式 JDBC 语句中使用命名参数。下面的例子展示了如何使用 `NamedParameterJdbcTemplate` ：

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActorsByFirstName(String firstName) {

    String sql = "select count(*) from T_ACTOR where first_name = :first_name";

    SqlParameterSource namedParameters = new MapSqlParameterSource("first_name", firstName);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

注意命名参数记号在配置给 `sql` 变量的值中和插入 `namedParameters` 变量的相映的值（类型是 `MapSqlParameterSource`）中的使用。

或者，你可以使用基于 `Map` 的形式将命名参数和相应的值传入 `NamedParameterJdbcTemplate` 实例。 `NamedParameterJdbcOperations` 暴露出来并由 `NamedParameterJdbcTemplate` 类实现的其他方法遵循相似的模式，不在这里讨论。

下面的例子展示了基于 `Map` 形式的使用：

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActorsByFirstName(String firstName) {

    String sql = "select count(*) from T_ACTOR where first_name = :first_name";

    Map<String, String> namedParameters = Collections.singletonMap("first_name", firstName);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters,  Integer.class);
}
```

有关 `NamedParameterJdbcTemplate` （以及同一个 Java 包中的其他类）的一个很好的特性是 `SqlParameterSource` 接口。你已经看到过一个该接口的实现的示例(`MapSqlParameterJdbcTemplate` 类) 。一个 `SqlParameterSource` 是一个 `NamedParameterJdbcTemplate` 中命名参数值的来源。`MapSqlParameterSource` 类是一个实现，是一个 `java.util.Map` 的适配器，其中的键是参数名称而值是参数值。

另一个 `SqlParameterSource` 实现是 `BeanPropertySqlParameterSource` 类。这个类包装任意 JavaBean (也就是一个遵循 [the JavaBean conventions](https://www.oracle.com/technetwork/java/javase/documentation/spec-136004.html) 的类的实例)，并且使用该被包装的 JavaBean 的属性作为命名参数值的来源。

下面的例子展示了一个典型的 JavaBean：

```java
public class Actor {

    private Long id;
    private String firstName;
    private String lastName;

    public String getFirstName() {
        return this.firstName;
    }

    public String getLastName() {
        return this.lastName;
    }

    public Long getId() {
        return this.id;
    }

    // setters omitted...

}
```

下面的例子使用 `NamedParameterJdbcTemplate` 来返回前面例子中展示的类的成员的数量：

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActors(Actor exampleActor) {

    // notice how the named parameters match the properties of the above 'Actor' class
    String sql = "select count(*) from T_ACTOR where first_name = :firstName and last_name = :lastName";

    SqlParameterSource namedParameters = new BeanPropertySqlParameterSource(exampleActor);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

记住， `NamedParameterJdbcTemplate` 类包装了一个经典的 `JdbcTemplate` 模版。如果你需要访问该包装的 `JdbcTemplate` 实例以访问只存在于该类中的功能，你可以使用 `getJdbcOperations()` 方法来通过 `JdbcOperations` 接口访问该包装的 `JdbcTemplate` 。

参考 [`JdbcTemplate` Best Practices](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-JdbcTemplate-idioms) 获取更多有关在应用上下文中使用 `NamedParameterJdbcTemplate` 类的指引。

