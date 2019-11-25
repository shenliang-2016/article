### 3.5.2 对象列表的批量操作

`JdbcTemplate` 和 `NamedParameterJdbcTemplate` 都提供了不同的方法用来进行批量更新。不同于实现特定的批量接口，你在方法调用中使用一个列表提供所有的参数值。该框架遍历这些值并使用一个内部的准备语句设定器方法。不同的 API，取决于你是否使用命名参数。为了命名参数，你提供一个 `SqlParameterSource` 数组，数组中的实体就是批量处理的成员。你可以使用方便方法 `SqlParameterSourceUtils.createBatch` 创建这样的数组，将其作为 bean 形式的对象（携带对应于参数的 getter 方法），或者键为 `String` 的 `Map` 实例（包含对应的参数作为的值）的数组进行传递，或者两者混合使用。

下面的例子展示了使用命名参数的批量更新：

```java
public class JdbcActorDao implements ActorDao {

    private NamedParameterTemplate namedParameterJdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
    }

    public int[] batchUpdate(List<Actor> actors) {
        return this.namedParameterJdbcTemplate.batchUpdate(
                "update t_actor set first_name = :firstName, last_name = :lastName where id = :id",
                SqlParameterSourceUtils.createBatch(actors));
    }

    // ... additional methods
}
```

对于使用经典的 `?` 占位符的 SQL 语句，你传入一个包含携带更新值的对象数组。该对象数组必须为 SQL 语句中每个占位符提供一个数据实体，而且它们必须遵循它们在 SQL 语句中定义的顺序。

下面的例子与之前的例子相同，处理它使用了经典的 JDBC `?` 占位符：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public int[] batchUpdate(final List<Actor> actors) {
        List<Object[]> batch = new ArrayList<Object[]>();
        for (Actor actor : actors) {
            Object[] values = new Object[] {
                    actor.getFirstName(), actor.getLastName(), actor.getId()};
            batch.add(values);
        }
        return this.jdbcTemplate.batchUpdate(
                "update t_actor set first_name = ?, last_name = ? where id = ?",
                batch);
    }

    // ... additional methods
}
```

我们前面介绍的所有批处理更新方法都返回一个 `int` 数组，其中包含每个批处理条目的受影响行数。此计数由 JDBC 驱动程序报告。如果该计数不可用，则 JDBC 驱动程序将返回值 `-2`。

> 在这种情况下，通过基础 `PreparedStatement` 上的自动设定，需要从给定的 Java 类型派生每个值的对应 JDBC 类型。尽管这通常效果很好，但是存在潜在的问题（例如，`Map` 包含的 `null` 值）。在这种情况下，Spring 默认情况下会调用 `ParameterMetaData.getParameterType`，这对于您的 JDBC 驱动程序可能会相当费用高昂。如果遇到以下情况，则应使用最新的驱动程序版本，并考虑将 `spring.jdbc.getParameterType.ignore` 属性设置为 `true`（作为 JVM 系统属性或在类路径根目录中的 `spring.properties` 文件中）。性能问题-例如，关于Oracle 12c（SPR-16139）的报告。
>
> 或者，您可以考虑通过 `BatchPreparedStatementSetter`（如前所示），通过为基于 `List<Object[]>` 的调用提供的显式类型数组，通过在服务器上的 `registerSqlType` 调用来显式指定相应的 JDBC 类型。自定义 `MapSqlParameterSource` 实例，或者通过 `BeanPropertySqlParameterSource` 实例从 Java 声明的属性类型中获取 SQL 类型，即使对于 `null` 值也是如此。

### 3.5.3 多个批量的批量操作

前面的批处理更新示例处理的批处理过大，您想将它们分解成几个较小的批处理。您可以通过多次调用 `batchUpdate` 方法来使用前面提到的方法来执行此操作，但是现在有了一个更方便的方法。除了 SQL 语句外，此方法还包含对象的 `Collection` ，其中包含参数，每个批处理要进行的更新次数以及 `ParameterizedPreparedStatementSetter` 来设置准备语句的参数值。框架遍历提供的值，并将更新调用分成指定大小的批处理。

下面的例子展示了使用批量尺寸为 100  的批量更新：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public int[][] batchUpdate(final Collection<Actor> actors) {
        int[][] updateCounts = jdbcTemplate.batchUpdate(
                "update t_actor set first_name = ?, last_name = ? where id = ?",
                actors,
                100,
                new ParameterizedPreparedStatementSetter<Actor>() {
                    public void setValues(PreparedStatement ps, Actor argument) throws SQLException {
                        ps.setString(1, argument.getFirstName());
                        ps.setString(2, argument.getLastName());
                        ps.setLong(3, argument.getId().longValue());
                    }
                });
        return updateCounts;
    }

    // ... additional methods
}
```

这里调用的批处理更新方法返回一个 `int` 数组，其中包含每个批处理的数组条目以及每次更新受影响的行数的数组。顶层数组的长度指示已执行的批处理数量，第二层数组的长度指示该批处理中的更新数量。每个批次中的更新数量应该是为所有批次提供的批次大小（最后一个可能更少），这取决于所提供的更新对象的总数。每个更新语句的更新计数是 JDBC 驱动程序报告的计数。如果该计数不可用，则 JDBC 驱动程序将返回值 `-2`。

