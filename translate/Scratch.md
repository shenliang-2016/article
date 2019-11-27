## 3.7 将 JDBC 操作建模为 Java 对象

`org.springframework.jdbc.object` 包中包含允许你以更加面向对象的方式访问数据库的类。作为一个例子，你可以执行查询并获取包含业务对象的列表形式的结果，通过将列数据映射到业务对象的属性。你也可以运行存储过程或者运行更新、删除以及插入语句。

> 许多 Spring 开发者相信下面描述的各种 RDBMS 操作类 ( [`StoredProcedure`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-StoredProcedure) 类例外) 都可以被直接的 `JdbcTemplate` 调用替代。通常情况下，编写直接调用 `JdbcTemplate` 上的方法的 DAO 方法相比于将查询封装成完整的类要更加简单。
>
> 不过，如果你正通过 RDBMS 操作类获取可测量的值，你应该继续使用这些类。

### 3.7.1 理解 `SqlQuery`

`SqlQuery` 是一个可重用的，线程安全的类，封装了一个 SQL 查询。子类必须实现 `newRowMapper(..)` 方法以提供一个 `RowMapper` 实例，它能够为从在查询执行过程中创建的 `ResultSet` 上的迭代器获取的每行数据创建一个新的对象。`SqlQuery` 类很少会被直接用到，因为 `MappingSqlQuery` 子类提供了一个更加方法的实现来将数据行映射到 Java 类。其他扩展了 `SqlQuery` 的实现有 `MappingSqlQueryWithParameters` 和 `UpdatableSqlQuery` 。

### 3.7.2 使用 `MappingSqlQuery`

`MappingSqlQuery` 是一个可重用查询，每个子类必须实现抽象的 `mapRow(..)` 方法，来将给定的 `ResultSet` 中的每行数据转化为特定类型的对象。下面的例子展示了一个自定义查询，将来自 `t_actor` 表的数据转化为 `Actor` 类实例：

```java
public class ActorMappingQuery extends MappingSqlQuery<Actor> {

    public ActorMappingQuery(DataSource ds) {
        super(ds, "select id, first_name, last_name from t_actor where id = ?");
        declareParameter(new SqlParameter("id", Types.INTEGER));
        compile();
    }

    @Override
    protected Actor mapRow(ResultSet rs, int rowNumber) throws SQLException {
        Actor actor = new Actor();
        actor.setId(rs.getLong("id"));
        actor.setFirstName(rs.getString("first_name"));
        actor.setLastName(rs.getString("last_name"));
        return actor;
    }

}
```

扩展了 `MappingSqlQuery` 的类使用 `Actor` 类型进行参数化。该自定义查询的构造方法使用唯一的 `DataSource` 类型参数。在该构造方法中，你可以使用 `DataSource` 调用超类的构造方法，以及应该执行的 SQL 以为该查询检索数据行。其中的 SQL 被用来创建一个 `PrepareStatement` ，因此，它可以包含任何可以在执行期间出入的参数的占位符。你必须通过使用 `declareParameter` 方法传入一个 `SqlParameter` 声明每个参数。该 `SqlParameter` 携带一个名称，以及一个定义在 `java.sql.Types` 中的 JDBC 类型。定义了所有参数之后，你可以调用 `compile()` 方法，该语句会被预处理并稍后运行。被编译之后这个类就是线程安全的，因此，一旦这些实例在 DAO 初始化时被创建，它们就可以被作为实例变量而重用。下面的例子展示了如何定义这样的类：

```java
private ActorMappingQuery actorMappingQuery;

@Autowired
public void setDataSource(DataSource dataSource) {
    this.actorMappingQuery = new ActorMappingQuery(dataSource);
}

public Customer getCustomer(Long id) {
    return actorMappingQuery.findObject(id);
}
```

上面例子中的方法根据传入的 `id` 查询顾客。由于我们希望只返回一个对象，我们以 `id` 作为参数调用 `findObject` 方便方法。如果我们需要将查询替换为携带更多参数并返回对象数组的查询，就应该使用多个 `execute` 方法之一。如下面例子所示：

```java
public List<Actor> searchForActors(int age, String namePattern) {
    List<Actor> actors = actorSearchMappingQuery.execute(age, namePattern);
    return actors;
}
```

