### 3.7.3 使用 `SqlUpdate`

`SqlUpdate` 类封装了一个 SQL 更新。与查询一样，更新对象是可重用的，并且与所有 `RdbmsOperation` 类一样，更新可以具有参数并在 SQL 中定义。此类提供了许多类似于查询对象的 `execute(..)` 方法的 `update(..)` 方法。`SQLUpdate` 类是具体的。可以将其子类化-例如，添加自定义更新方法。但是，不必继承 `SqlUpdate` 类，因为可以通过设置 SQL 和声明参数来轻松地对其进行参数化。以下示例创建一个名为 `execute` 的自定义更新方法：

```java
import java.sql.Types;
import javax.sql.DataSource;
import org.springframework.jdbc.core.SqlParameter;
import org.springframework.jdbc.object.SqlUpdate;

public class UpdateCreditRating extends SqlUpdate {

    public UpdateCreditRating(DataSource ds) {
        setDataSource(ds);
        setSql("update customer set credit_rating = ? where id = ?");
        declareParameter(new SqlParameter("creditRating", Types.NUMERIC));
        declareParameter(new SqlParameter("id", Types.NUMERIC));
        compile();
    }

    /**
     * @param id for the Customer to be updated
     * @param rating the new value for credit rating
     * @return number of rows updated
     */
    public int execute(int id, int rating) {
        return update(rating, id);
    }
}
```