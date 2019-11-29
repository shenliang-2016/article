### 3.8.3 为 IN 子句传入值列表

SQL 标准允许基于包含变量值列表的表达式选择行。一个典型的例子是  `select * from T_ACTOR where id in (1, 2, 3)`。JDBC 标准不直接为准备好的语句支持此变量列表。您不能声明可变数量的占位符。您需要准备好所需数量的占位符的多种变体，或者一旦知道需要多少个占位符，就需要动态生成 SQL 字符串。在 `NamedParameterJdbcTemplate` 和 `JdbcTemplate` 中提供的命名参数支持采用后一种方法。您可以将值作为原始对象的 `java.util.List` 传入。此列表用于插入所需的占位符，并在语句执行期间传递值。

> 传递许多值时要小心。JDBC 标准不保证您可以为 `in` 表达式列表使用100个以上的值。各种数据库都超过了这个数目，但是它们通常对允许多少个值有硬性限制。例如，Oracle 的限制为1000。

除了在值列表中放入基本数据类型值，你可以创建对象数组的 `java.util.List` 。该列表能够支持为 `in` 子句定义的多个表达式，比如 `select * from T_ACTOR where ( id, last_name ) in ((1, 'Johnson'), (2, 'Harrop'\)) ` 。当然，这也要求你的数据库支持这种语法。

### 3.8.4 为存储过程调用处理复杂类型

当你调用存储过程时，你有时候可以使用特定于数据的复杂类型。为了容纳这些类型，Spring 提供了两个类， `SqlReturnType` 用来在它们被存储过程调用返回时处理它们，`SqlTypeValue` 用来当它们被作为参数传递给存储过程时处理它们。

`SqlReturnType` 接口只有一个方法 (名为 `getTypeValue`) 必须被实现。该接口被用作 `SqlOutParameter` 声明的一部分。下面的例子展示了返回用户声明的类型 `ITEM_TYPE` 的 Oracle `STRUCT` 对象的值：

```java
public class TestItemStoredProcedure extends StoredProcedure {

    public TestItemStoredProcedure(DataSource dataSource) {
        ...
        declareParameter(new SqlOutParameter("item", OracleTypes.STRUCT, "ITEM_TYPE",
            new SqlReturnType() {
                public Object getTypeValue(CallableStatement cs, int colIndx, int sqlType, String typeName) throws SQLException {
                    STRUCT struct = (STRUCT) cs.getObject(colIndx);
                    Object[] attr = struct.getAttributes();
                    TestItem item = new TestItem();
                    item.setId(((Number) attr[0]).longValue());
                    item.setDescription((String) attr[1]);
                    item.setExpirationDate((java.util.Date) attr[2]);
                    return item;
                }
            }));
        ...
    }
```

你可以使用 `SqlTypeValue` 来传递 Java 对象（比如 `TestItem`）的值给存储过程。`SqlTypeValue` 接口只有一个方法 (名为 `createTypeValue` ) 必须被实现。活动连接被传入，你可以使用它来创建特定于数据库的对象，比如 `StructDescriptor` 实例或者 `ArrayDescriptor` 实例。下面的例子创建一个 `StructDescriptor` 实例：

```java
final TestItem testItem = new TestItem(123L, "A test item",
        new SimpleDateFormat("yyyy-M-d").parse("2010-12-31"));

SqlTypeValue value = new AbstractSqlTypeValue() {
    protected Object createTypeValue(Connection conn, int sqlType, String typeName) throws SQLException {
        StructDescriptor itemDescriptor = new StructDescriptor(typeName, conn);
        Struct item = new STRUCT(itemDescriptor, conn,
        new Object[] {
            testItem.getId(),
            testItem.getDescription(),
            new java.sql.Date(testItem.getExpirationDate().getTime())
        });
        return item;
    }
};
```

现在你可以添加该 `SqlTypeValue` 到包含对存储过程的 `execute` 调用的参数的 `Map` 中。

`SqlTypeValue` 的另一个用法是传入一个值数组然后传递给 Oracle 存储过程。Oracle 拥有自己的内部 `Array` 类，这种情况下必须使用该类，你可以使用 `SqlTypeValue` 来创建 Oracle `Array` 实例并用来自 Java `Array` 的值填充它。如下面例子所示：

```java
final Long[] ids = new Long[] {1L, 2L};

SqlTypeValue value = new AbstractSqlTypeValue() {
    protected Object createTypeValue(Connection conn, int sqlType, String typeName) throws SQLException {
        ArrayDescriptor arrayDescriptor = new ArrayDescriptor(typeName, conn);
        ARRAY idArray = new ARRAY(arrayDescriptor, conn, ids);
        return idArray;
    }
};
```

