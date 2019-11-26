### 3.6.5 使用 `SimpleJdbcCall` 调用存储过程

`SimpleJdbcCall` 类使用数据库中的元数据来查找 `in` 和 `out` 参数的名称，因此你不需要显式声明它们。如果你喜欢，仍然可以显式声明它们，或者你的参数 (比如 `ARRAY` 或者 `STRUCT`) 无法自动影射到 Java 类。下面的第一个累字展示了一个简单的存储过程，从 MySQL 数据库返回 `VARCHAR` 和 `DATE` 格式的标量值。示例存储过程读取特定 actor 实体并以 `out` 参数的形式返回 `first_name`，`last_name`，以及 `birth_date` 列。下面的列表展示了第一个例子：

```sql
CREATE PROCEDURE read_actor (
    IN in_id INTEGER,
    OUT out_first_name VARCHAR(100),
    OUT out_last_name VARCHAR(100),
    OUT out_birth_date DATE)
BEGIN
    SELECT first_name, last_name, birth_date
    INTO out_first_name, out_last_name, out_birth_date
    FROM t_actor where id = in_id;
END;
```

`in_id` 参数包含你寻找的 actor 的 `id` 。`out` 参数返回从表里读取的数据。

你可以像声明 `SimpleJdbcInsert` 那样声明 `SimpleJdbcCall` 。你应该在你的数据访问层的实例化方法中实例化并配置该类。相比于 `StoredProcedure` 类，你不需要创建子类，也不需要声明那些可以在数据库元数据中找到的参数。下面的 `SimpleJdbcCall` 配置的例子使用了上面的存储过程(其中仅有的配置选项，除了 `DataSource` ，另外一个就是存储过程的名称)：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcCall procReadActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.procReadActor = new SimpleJdbcCall(dataSource)
                .withProcedureName("read_actor");
    }

    public Actor readActor(Long id) {
        SqlParameterSource in = new MapSqlParameterSource()
                .addValue("in_id", id);
        Map out = procReadActor.execute(in);
        Actor actor = new Actor();
        actor.setId(id);
        actor.setFirstName((String) out.get("out_first_name"));
        actor.setLastName((String) out.get("out_last_name"));
        actor.setBirthDate((Date) out.get("out_birth_date"));
        return actor;
    }

    // ... additional methods
}
```

你用来执行该调用的代码涉及到创建一个包含 IN 参数的 `SqlParameterSource` 。你必须匹配给定的输入值的名称到在存储过程中声明的参数名称。如果你使用元数据确定数据库对象应该如何对应到存储过程，则不需要这个匹配过程。源中为存储过程指定的内容不一定是存储过程在数据库中存储的方式。某些数据库将所有名称都转换为大写，有些使用小写，还有的使用指定的本来形式。

`execute` 方法使用 IN 参数并返回包含所有 `out` 参数的 `Map` ，其中参数名称为影射的键，如存储过程中指定的那样。这种情况下，它们是 `out_first_name`，`out_last_name`，和 `out_birth_date`。

`execute` 方法的最后一部分创建一个 `Actor` 实例，使用数据检索返回的数据。再一次地，使用 `out` 参数在存储过程中声明的名称是很重要的。同样，结果映射中存储的 `out` 参数名称的大小写与数据库中`out`参数名称的大小写匹配，这在不同数据库中可能会有所不同。为了使你的代码具有更好的可移植性，你应该使用大小写敏感的查找策略，或者指示 Spring 使用 `LinkedCaseInsensitiveMap` 。为了实现后者，你可以创建自己的 `JdbcTemplate` 并设定其 `setResultsMapCaseInsensitive` 属性为 `true` 。然后你可以将这个自定义的 `JdbcTemplate` 实例传入你的 `SimpleJdbcCall` 的构造器中。下面的例子展示了该配置：

```java
public class JdbcActorDao implements ActorDao {

    private SimpleJdbcCall procReadActor;

    public void setDataSource(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
        jdbcTemplate.setResultsMapCaseInsensitive(true);
        this.procReadActor = new SimpleJdbcCall(jdbcTemplate)
                .withProcedureName("read_actor");
    }

    // ... additional methods
}
```

通过执行此操作，可以避免在用于返回的 `out` 参数名称的情况下发生冲突。

### 3.6.6 显式声明用于 `SimpleJdbcCall` 的参数

前文中，我们描述了如何从元数据推导出参数，但是如果需要，可以显式声明它们。您可以通过使用 `declareParameters` 方法创建和配置 `SimpleJdbcCall` 来实现，该方法采用可变数量的 `SqlParameter` 对象作为输入。请参阅 [下一节](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-params) 了解有关如何定义 `SqlParameter` 。

> 如果您使用的数据库不是 Spring 支持的数据库，则必须进行显式声明。当前，Spring 支持针对以下数据库的存储过程调用的元数据查找：Apache Derby，DB2，MySQL，Microsoft SQL Server，Oracle 和 Sybase。我们还支持MySQL，Microsoft SQL Server 和 Oracle 存储函数的元数据查找。

您可以选择显式声明一个，一些或所有参数。在未显式声明参数的地方，仍使用参数元数据。要绕过对潜在参数的元数据查找的所有处理，并且仅使用声明的参数，可以在声明中调用方法 `withoutProcedureColumnMetaDataAccess`。假设您为数据库函数声明了两个或多个不同的调用签名。在这种情况下，您调用 `useInParameterNames` 来指定要包含在给定签名中的 IN 参数名称列表。

下面的例子展示了完整的声明的存储过程调用，并使用了前面例子中的信息：

```java
public class JdbcActorDao implements ActorDao {

    private SimpleJdbcCall procReadActor;

    public void setDataSource(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
        jdbcTemplate.setResultsMapCaseInsensitive(true);
        this.procReadActor = new SimpleJdbcCall(jdbcTemplate)
                .withProcedureName("read_actor")
                .withoutProcedureColumnMetaDataAccess()
                .useInParameterNames("in_id")
                .declareParameters(
                        new SqlParameter("in_id", Types.NUMERIC),
                        new SqlOutParameter("out_first_name", Types.VARCHAR),
                        new SqlOutParameter("out_last_name", Types.VARCHAR),
                        new SqlOutParameter("out_birth_date", Types.DATE)
                );
    }

    // ... additional methods
}
```

两个例子执行的结果是一样的。第二个例子显式指定了所有细节，而没有依赖元数据。

