### 3.3.4 运行语句

运行一条 SQL 语句只需要很少的代码。你需要一个 `DataSource` 和一个 `JdbcTemplate` ，包括连同后者一起提供的方便方法。下面的例子展示了创建一张新表的最小需求但是功能完备的类：

```java
import javax.sql.DataSource;
import org.springframework.jdbc.core.JdbcTemplate;

public class ExecuteAStatement {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public void doExecute() {
        this.jdbcTemplate.execute("create table mytable (id integer, name varchar(100))");
    }
}
```

### 3.3.5 运行查询

一些查询方法返回单独的一个值。为了从一行中检索特定值的数量，使用 `queryForObject(..)`。该方法将返回的 JDBC `Type` 转化为作为参数传入的 Java 类。如果类型转换不可用，则抛出 `InvalidDataAccessApiUsageException` 。下面的例子包含两个查询方法，一个用来查询一个 `int` ，另一个查询一个 `String` ：

```java
import javax.sql.DataSource;
import org.springframework.jdbc.core.JdbcTemplate;

public class RunAQuery {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public int getCount() {
        return this.jdbcTemplate.queryForObject("select count(*) from mytable", Integer.class);
    }

    public String getName() {
        return this.jdbcTemplate.queryForObject("select name from mytable", String.class);
    }
}
```

除了单个结果的查询方法，若干方法返回一个列表，其中每个实体都是查询返回的一行数据。最通用的方法是 `queryForList(..)` ，它返回一个 `List` ，其中每个元素都是包含每个表列的数据实体的 `Map` ，使用表列名作为键。如果你为上面例子添加一个查询所有行的列表的方法，可能如下所示：

```java
private JdbcTemplate jdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.jdbcTemplate = new JdbcTemplate(dataSource);
}

public List<Map<String, Object>> getList() {
    return this.jdbcTemplate.queryForList("select * from mytable");
}
```

返回的列表将被构造如下：

```
[{name=Bob, id=1}, {name=Mary, id=2}]
```

