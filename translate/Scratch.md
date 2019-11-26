### 3.6.7 如何定义 `SqlParameters`

要为 `SimpleJdbc` 类和 RDBMS 操作类（[Modeling JDBC Operations as Java Objects](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-object) 中介绍）定义参数，你可以使用 `SqlParameter` 或者它的一个子类。为了这样做，你通常在构造器中指定参数名称和 SQL 类型。使用 `java.sql.Type` 常量指定 SQL 类型。本节前文中我们看到过如下声明：

```java
new SqlParameter("in_id", Types.NUMERIC),
new SqlOutParameter("out_first_name", Types.VARCHAR),
```

第一行使用 `SqlParameter` 声明一个 IN 参数。你可以使用 IN 参数进行存储过程调用，或者用于使用 `SqlQuery` 或和它的子类进行查询（在 [Understanding `SqlQuery`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-SqlQuery) 中介绍）：

第二行使用 `SqlOutParameter` 声明一个 `out` 参数，该参数将被用于存储过程调用。同时还有一个包含 `InOut` 参数的 `SqlInOutParameter` (参数为存储过程提供一个 IN 值，同时也返回一个值)。

> 只有被声明为 `SqlParameter` 和 `SqlInOutParameter` 的参数才能被用来提供输入值。这一点不同于 `StoredProcedure` 类，(出于向后兼容的原因) 它允许被提供作为参数的输入值声明为 `SqlOutParameter` 。

对于 IN 参数，除了名称和 SQL 类型外，还可以为数值数据指定小数位，或者为自定义数据库类型指定类型名。对于 `out` 参数，您可以提供 `RowMapper` 来处理从 `REF` 游标返回的行的映射。另一个选择是指定一个 `SqlReturnType`，它提供了一个定义返回值的自定义处理的机会。

### 3.6.8 使用 `SimpleJdbcCall` 调用存储函数

可以使用与调用存储过程几乎相同的方式来调用存储函数，区别在于提供函数名而不是过程名。您可以在配置中使用 `withFunctionName` 方法，以指示您要调用函数，并且会为函数调用生成相应的字符串。专门的 `execute` 调用（`executeFunction`）用于执行函数，它以指定类型的对象的形式返回函数的返回值，这意味着您不必从结果映射中检索返回值。对于只有一个 `out` 参数的存储过程，也可以使用类似的便捷方法（名为 `executeObject` ）。以下示例（对于MySQL）基于一个名为 `get_actor_name` 的存储函数，该函数返回 actor 的全名：

```sql
CREATE FUNCTION get_actor_name (in_id INTEGER)
RETURNS VARCHAR(200) READS SQL DATA
BEGIN
    DECLARE out_name VARCHAR(200);
    SELECT concat(first_name, ' ', last_name)
        INTO out_name
        FROM t_actor where id = in_id;
    RETURN out_name;
END;
```

为了调用该函数，我们再次在初始化方法中创建一个 `SimpleJdbcCall` ，如下面例子所示：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcCall funcGetActorName;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
        jdbcTemplate.setResultsMapCaseInsensitive(true);
        this.funcGetActorName = new SimpleJdbcCall(jdbcTemplate)
                .withFunctionName("get_actor_name");
    }

    public String getActorName(Long id) {
        SqlParameterSource in = new MapSqlParameterSource()
                .addValue("in_id", id);
        String name = funcGetActorName.executeFunction(String.class, in);
        return name;
    }

    // ... additional methods
}
```

其中使用的 `executeFunction` 方法返回一个 `String`，包含函数调用返回的值。

### 3.6.9 从 `SimpleJdbcCall` 返回 `ResultSet` 或者 REF 游标

调用返回结果集的存储过程或函数有点棘手。一些数据库在 JDBC 结果处理期间返回结果集，而另一些数据库则需要显式注册的特定类型的 `out` 参数。两种方法都需要进行额外的处理才能遍历结果集并处理返回的行。通过 `SimpleJdbcCall`，您可以使用 `returningResultSet` 方法，并声明用于特定参数的 `RowMapper` 实现。如果在结果处理过程中返回了结果集，则没有定义任何名称，因此返回的结果必须与声明 `RowMapper` 实现的顺序匹配。指定的名称仍用于将处理后的结果列表存储在从 `execute` 语句返回的结果映射中。

下面的例子 (MySQL) 使用一个存储过程，该存储过程不使用 IN 参数，返回表 `t_actor` 中所有的行：

```sql
CREATE PROCEDURE read_all_actors()
BEGIN
 SELECT a.id, a.first_name, a.last_name, a.birth_date FROM t_actor a;
END;
```

为了调用此存储过程，你可以声明 `RowMapper`。由于你希望映射到的类遵循 JavaBean 规范，你可以使用 `BeanPropertyRowMapper` ，这个对象通过将需要映射到的类传入 `newInstance` 方法而创建。下面的例子展示了如何做：

```java
public class JdbcActorDao implements ActorDao {

    private SimpleJdbcCall procReadAllActors;

    public void setDataSource(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
        jdbcTemplate.setResultsMapCaseInsensitive(true);
        this.procReadAllActors = new SimpleJdbcCall(jdbcTemplate)
                .withProcedureName("read_all_actors")
                .returningResultSet("actors",
                BeanPropertyRowMapper.newInstance(Actor.class));
    }

    public List getActorsList() {
        Map m = procReadAllActors.execute(new HashMap<String, Object>(0));
        return (List) m.get("actors");
    }

    // ... additional methods
}
```

`execute` 调用传入一个空 `Map`，因为该调用不需要任何参数。然后 actors 列表就回从结果集中被检索出来并返回给调用者。