## 3.5 JDBC 批量操作

大多数 JDBC 驱动提供更高的性能，如果你将多个调用合并为批量准备语句。通过将多个更新语句编组进入批量操作，你减少了通向数据库的往返路程。

### 3.5.1  `JdbcTemplate` 基本批量操作

你通过实现特定接口的两个方法来实现 `JdbcTemplate` 批量处理，`BatchPreparedStatementSetter`，同时将该实现作为你的 `batchUpdate` 方法调用的第二个参数。你可以使用 `getBatchSize` 方法来提供当前批量的尺寸。你可以使用 `setValues` 方法来设定准备语句的参数值。该方法被调用的次数就是你在 `getBatchSize` 调用中指定的值。下面的例子基于一个列表中的实体来更新 `actor` 表，实体列表用于批量操作：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public int[] batchUpdate(final List<Actor> actors) {
        return this.jdbcTemplate.batchUpdate(
                "update t_actor set first_name = ?, last_name = ? where id = ?",
                new BatchPreparedStatementSetter() {
                    public void setValues(PreparedStatement ps, int i) throws SQLException {
                        ps.setString(1, actors.get(i).getFirstName());
                        ps.setString(2, actors.get(i).getLastName());
                        ps.setLong(3, actors.get(i).getId().longValue());
                    }
                    public int getBatchSize() {
                        return actors.size();
                    }
                });
    }

    // ... additional methods
}
```

如果你处理一个更新或者读取文件的流，你可能有偏好的批量处理尺寸，不过最后一次的批量操作可能没有足够数量的实体。这种情况下，你可以使用 `InterruptibleBatchPreparedStatementSetter` 接口，它允许你打断批量处理，一旦输入数据耗尽。`isBatchExhausted` 方法允许你标记批量操作的结束。

