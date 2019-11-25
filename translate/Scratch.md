## 3.6 使用 `SimpleJdbc` 类简化 JDBC 操作

得益于可以通过 JDBC 检索得到的数据库元数据的优点， `SimpleJdbcInsert` 和 `SimpleJdbcCall` 类提供了简化的配置。这就意味着你需要的配置更好。不过，你当然可以关闭这种元数据处理，如果你希望在你的代码中配置所有细节。

### 3.6.1 使用 `SimpleJdbcInsert` 插入数据

首先，我们查看具有最少配置选项的 `SimpleJdbcInsert` 类。你应该在数据访问层的实例化方法中实例化 `SimpleJdbcInsert` 。对本示例而言，初始化方法就是 `setDataSource` 。你不需要子类化 `SimpleJdbcInsert` 类，相反，你可以创建一个新的实例并使用 `withTableName` 方法设定表名。这个类的配置方法遵循 `fluid` 风格，返回 `SimpleJdbcInsert` 实例，它允许你串联起所有的配置方法。下面的例子只使用一个配置方法，稍后我们将展示使用多个方法的例子。

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcInsert insertActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.insertActor = new SimpleJdbcInsert(dataSource).withTableName("t_actor");
    }

    public void add(Actor actor) {
        Map<String, Object> parameters = new HashMap<String, Object>(3);
        parameters.put("id", actor.getId());
        parameters.put("first_name", actor.getFirstName());
        parameters.put("last_name", actor.getLastName());
        insertActor.execute(parameters);
    }

    // ... additional methods
}
```

这里使用的 `execute` 方法采用普通的 `java.util.Map` 作为它唯一的参数。这里需要注意的重要的事情是，使用的 `Map` 的键必须匹配定义在数据库中的表的列名。这是因为我们读取元数据来构造实际的插入语句。

### 3.6.2 使用 `SimpleJdbcInsert` 检索自动生成的键

下一个例子使用相同的插入语句，不同的是，不是传入 `id` ，它检索自动生成的主键并将它设置到新的 `Actor` 对象上。当它创建 `SimpleJdbcInsert` 时，除了指定表名，它还通过 `usingGeneratedKeyColumns` 方法指定产生主键列名。下面的例子展示了如何做：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcInsert insertActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.insertActor = new SimpleJdbcInsert(dataSource)
                .withTableName("t_actor")
                .usingGeneratedKeyColumns("id");
    }

    public void add(Actor actor) {
        Map<String, Object> parameters = new HashMap<String, Object>(2);
        parameters.put("first_name", actor.getFirstName());
        parameters.put("last_name", actor.getLastName());
        Number newId = insertActor.executeAndReturnKey(parameters);
        actor.setId(newId.longValue());
    }

    // ... additional methods
}
```

使用第二种方法运行插入的主要区别在于，您没有将 `id` 添加到 `Map` 中，而是调用了 `executeAndReturnKey` 方法。这将返回一个 `java.lang.Number` 对象，您可以使用该对象创建域类中使用的数字类型的实例。您不能依赖所有数据库在这里返回特定的 Java 类。`java.lang.Number` 是您可以依赖的基类。如果您有多个自动生成的列或生成的值是非数字的，则可以使用从 `executeAndReturnKeyHolder` 方法返回的 `KeyHolder`。

