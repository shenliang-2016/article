### 3.3.6 更新数据库

下面的例子根据某个主键更新某一字段值：

```java
import javax.sql.DataSource;
import org.springframework.jdbc.core.JdbcTemplate;

public class ExecuteAnUpdate {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public void setName(int id, String name) {
        this.jdbcTemplate.update("update mytable set name = ? where id = ?", name, id);
    }
}
```

在上面的例子中，SQL 语句中的占位符作为行参数。你可以传递变量或者对象数组作为该参数的值。因此，你应该将基本数据类型显式包装为相应的包装类，或者使用自动装箱。

### 3.3.7 检索自增键

一个 `update()` 便捷方法支持由数据库产生的主键的检索。这种支持是 JDBC 3.0 标准的一部分。参考规范文档 13.6 章节了解更多细节。该方法将 `PreparedStatementCreator` 作为它的第一个参数，这也是插入语句所需的特定方式。另外的参数是一个 `KeyHolder` ，包含从更新操作正确返回的产生的主键。创建合适的 `PreparedStatement` 没有标准的唯一方式 (解释为什么该方法签名会是这个样子) 。下面的例子在 Oracle 平台上运行，其他平台不一定可行。

```java
final String INSERT_SQL = "insert into my_test (name) values(?)";
final String name = "Rob";

KeyHolder keyHolder = new GeneratedKeyHolder();
jdbcTemplate.update(
    new PreparedStatementCreator() {
        public PreparedStatement createPreparedStatement(Connection connection) throws SQLException {
            PreparedStatement ps = connection.prepareStatement(INSERT_SQL, new String[] {"id"});
            ps.setString(1, name);
            return ps;
        }
    },
    keyHolder);

// keyHolder.getKey() now contains the generated key
```