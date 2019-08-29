### 使用 JdbcRowSet 对象

`JdbcRowSet`对象是一个增强的`ResultSet`对象。它保持与其数据源的连接，就像`ResultSet`对象一样。最大的区别在于它具有一组属性和一个监听器通知机制，使其成为 JavaBeans 组件。

`JdbcRowSet`对象的主要用途之一是使`ResultSet`对象在没有这些功能的情况下可滚动和可更新。

本节包括以下主题：

- [创建 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#creating-jdbcrowset-object)
- [默认 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#default-jdbcrowset-objects)
- [设定属性](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#setting-properties)
- [使用 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#using-jdbcrowset-object)
- [代码示例](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#code-sample)

**创建 JdbcRowSet 对象**

您可以通过各种方式创建`JdbcRowSet`对象：

 - 使用带有`ResultSet`对象的参考实现构造函数
 - 使用带有`Connection`对象的参考实现构造函数
 - 使用参考实现默认构造函数
 - 使用`RowSetFactory`的实例，它是从类`RowSetProvider`创建的

**注意**：或者，您可以使用 JDBC 驱动程序的`JdbcRowSet`实现中的构造函数。但是，`RowSet`接口的实现将与参考实现不同。这些实现将具有不同的名称和构造函数。例如，Oracle JDBC 驱动程序的`JdbcRowSet`接口的实现名为`oracle.jdbc.rowset.OracleJDBCRowSet`。

**传递 ResultSet 对象**

创建`JdbcRowSet`对象的最简单方法是生成一个`ResultSet`对象并将其传递给`JdbcRowSetImpl`构造器。这样做不仅会创建一个`JdbcRowSet`对象，还会使用`ResultSet`对象中的数据填充它。

**注意**：传递给`JdbcRowSetImpl`构造函数的`ResultSet`对象必须是可滚动的。

例如，下面的代码片段使用`Connection`对象`con`来创建`Statement`对象`stmt`，然后执行查询。该查询生成`ResultSet`对象`rs`，它被传递给构造函数以创建一个用`rs`中的数据初始化的新`JdbcRowSet`对象：

```java
stmt = con.createStatement(
           ResultSet.TYPE_SCROLL_SENSITIVE,
           ResultSet.CONCUR_UPDATABLE);
rs = stmt.executeQuery("select * from COFFEES");
jdbcRs = new JdbcRowSetImpl(rs);
```

使用`ResultSet`对象创建的`JdbcRowSet`对象充当`ResultSet`对象的包装器。因为`RowSet`对象`rs`是可滚动和可更新的，所以`jdbcRs`也是可滚动和可更新的。如果你运行没有任何参数的`createStatement`方法，`rs`将不可滚动或可更新，并且`jdbcRs`也不会。

**传递 Connection 对象**

以下代码摘录自 [`JdbcRowSetSample`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 中的第一个语句创建了一个`JdbcRowSet`对象，该对象连接到数据库 `Connection`对象`con`：

```java
jdbcRs = new JdbcRowSetImpl(con);
jdbcRs.setCommand("select * from COFFEES");
jdbcRs.execute();
```

在您使用方法`setCommand`指定 SQL 语句之前，对象`jdbcRs`不包含任何数据，然后运行方法`execute`。

对象`jdbcRs`是可滚动和可更新的；默认情况下，`JdbcRowSet`和所有其他`RowSet`对象是可滚动和可更新的，除非另有说明。有关您可以指定的`JdbcRowSet`属性的更多信息，请参见  [Default JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#default-jdbcrowset-objects) 。

**使用默认构造器**

以下代码片段中的第一个语句创建一个空的`JdbcRowSet`对象。

```java
public void createJdbcRowSet(String username, String password) {

    jdbcRs = new JdbcRowSetImpl();
    jdbcRs.setCommand("select * from COFFEES");
    jdbcRs.setUrl("jdbc:myDriver:myAttribute");
    jdbcRs.setUsername(username);
    jdbcRs.setPassword(password);
    jdbcRs.execute();
    // ...
}
```

在您使用方法`setCommand`指定SQL语句之前，对象`jdbcRs`不包含任何数据，指定`JdbcResultSet`对象如何连接数据库，然后运行方法`execute`。

所有参考实现构造函数都为 [Default JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#default-jdbcrowset-objects) 部分中列出的属性分配默认值。

**使用 RowSetFactory 接口**

使用RowSet 1.1，它是Java SE 7及更高版本的一部分，您可以使用`RowSetFactory`的实例来创建`JdbcRowSet`对象。例如，以下代码摘录使用`RowSetFactory`接口的实例来创建`JdbcRowSet`对象，`jdbcRs`：

```java
public void createJdbcRowSetWithRowSetFactory(
    String username, String password)
    throws SQLException {

    RowSetFactory myRowSetFactory = null;
    JdbcRowSet jdbcRs = null;
    ResultSet rs = null;
    Statement stmt = null;

    try {
        myRowSetFactory = RowSetProvider.newFactory();
        jdbcRs = myRowSetFactory.createJdbcRowSet();

        jdbcRs.setUrl("jdbc:myDriver:myAttribute");
        jdbcRs.setUsername(username);
        jdbcRs.setPassword(password);

        jdbcRs.setCommand("select * from COFFEES");
        jdbcRs.execute();

        // ...
    }
}
```

下面的语句使用默认的`RowSetFactory`实现，`com.sun.rowset.RowSetFactoryImpl`创建`RowSetProvider`对象`myRowSetFactory`：

```java
myRowSetFactory = RowSetProvider.newFactory();
```

或者，如果您的 JDBC 驱动程序有自己的`RowSetFactory`实现，您可以将其指定为`newFactory`方法的参数。

以下语句创建`JdbcRowSet`对象`jdbcRs`并配置其数据库连接属性：

```java
jdbcRs = myRowSetFactory.createJdbcRowSet();
jdbcRs.setUrl("jdbc:myDriver:myAttribute");
jdbcRs.setUsername(username);
jdbcRs.setPassword(password);
```

`RowSetFactory`接口包含创建 RowSet 1.1 及更高版本中可用的不同类型的`RowSet`实现的方法：

- `createCachedRowSet`
- `createFilteredRowSet`
- `createJdbcRowSet`
- `createJoinRowSet`
- `createWebRowSet`

**默认 JdbcRowSet 对象**

使用默认构造函数创建`JdbcRowSet`对象时，新的`JdbcRowSet`对象将具有以下属性：

 - `type`：`ResultSet.TYPE_SCROLL_INSENSITIVE`（有一个可滚动的游标）
 - `concurrency`：`ResultSet.CONCUR_UPDATABLE`（可以更新）
 - `escapeProcessing`：`true`（驱动程序将执行转义处理；启用转义处理时，驱动程序将扫描任何转义语法并将其转换为特定数据库理解的代码）
 - `maxRows`：`0`（行数没有限制）
 - `maxFieldSize`：`0`（对列值的字节数没有限制;仅适用于存储`BINARY`，`VARBINARY`，`LONGVARBINARY`，`CHAR`，`VARCHAR`和`LONGVARCHAR`值）
 - `queryTimeout`：`0`（没有时间限制执行查询所需的时间）
 - `showDeleted`：`false`（删除的行不可见）
 - `transactionIsolation`：`Connection.TRANSACTION_READ_COMMITTED`（只读取已提交的数据）
 - `typeMap`：`null`（与`RowSet`对象使用的`Connection`对象关联的类型映射是`null`）

从这个列表中你必须记住的主要事情是`JdbcRowSet`和所有其他`RowSet`对象是可滚动和可更新的，除非你为这些属性设置不同的值。

**设定属性**

 [Default JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#default-jdbcrowset-objects) 一节列出了新的`JdbcRowSet`被创建时默认设置的属性。如果使用默认构造函数，则必须先设置一些其他属性，然后才能使用数据填充新的`JdbcRowSet`对象。

为了获取其数据，`JdbcRowSet`对象首先需要连接到数据库。以下四个属性包含用于获取与数据库的连接的信息。

 - `username`：用户提供给数据库的名称，作为获取访问权限的一部分
 - `password`：用户的数据库密码
 - `url`：用户想要连接的数据库的 JDBC URL
 - `datasourceName`：用于检索已向 JNDI 命名服务注册的`DataSource`对象的名称

这些属性中的哪一个需要设置取决于您要如何建立连接。首选方法是使用`DataSource`对象，但是使用 JNDI 命名服务注册`DataSource`对象可能不实际，这通常由系统管理员完成。因此，代码示例都使用`DriverManager`机制来获取连接，您使用`url`属性而不是`datasourceName`属性。

您必须设置的另一个属性是`command`属性。此属性是确定`JdbcRowSet`对象将包含哪些数据的查询。例如，以下代码行将`command`属性设置为一个查询，该查询生成一个`ResultSet`对象，该对象包含表`COFFEES`中的所有数据：

```java
jdbcRs.setCommand("select * from COFFEES");
```

在设置`command`属性和建立连接所需的属性之后，您可以通过调用`execute`方法填充`jdbcRs`对象和数据。

```java
jdbcRs.execute();
```

`execute`方法在后台为你做了很多事情：

 - 它使用您分配给`url`，`username`和`password`properties的值建立与数据库的连接。
 - 它执行您在`command`属性中设置的查询。
 - 它将生成的`ResultSet`对象中的数据读入`jdbcRs`对象。

**使用 JdbcRowSet 对象**

您更新，插入和删除`JdbcRowSet`对象中的行的方式与更新，插入和删除可更新的`ResultSet`对象中的行的方式相同。类似地，您导航`JdbcRowSet`对象的方式与导航可滚动的`ResultSet`对象的方式相同。

Coffee Break 的连锁店获得了另一家咖啡馆连锁店，现在拥有一个不支持滚动或更新结果集的遗留数据库。换句话说，此遗留数据库生成的任何`ResultSet`对象都没有可滚动的游标，并且其中的数据无法修改。但是，通过创建一个用`ResultSet`对象填充数据的`JdbcRowSet`对象，实际上可以使`ResultSet`对象可滚动和可更新。

如前所述，`JdbcRowSet`对象默认是可滚动和可更新的。因为它的内容与`ResultSet`对象中的内容相同，所以对`JdbcRowSet`对象进行操作相当于对`ResultSet`对象本身进行操作。并且因为`JdbcRowSet`对象与数据库有持续的连接，所以对其中的数据的修改也会对其连接的数据库中的数据进行更改。

本节涵盖以下主题：

- [导航 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#navigating-jdbcrowset-object)
- [更新列值](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#updating-column-value)
- [插入行](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#inserting-row)
- [删除行](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#deleting-row)

**导航 JdbcRowSet 对象**

不可滚动的`ResultSet`对象只能使用`next`方法向前移动光标，它只能将光标从第一行向前移动到最后一行。 但是，默认的`JdbcRowSet`对象可以使用`ResultSet`接口中定义的所有游标移动方法。

`JdbcRowSet`对象可以调用方法`next`，它也可以调用任何其他`ResultSet`光标移动方法。 例如，以下代码行将光标移动到`jdbcRs`对象中的第四行，然后返回第三行：

```java
jdbcRs.absolute(4);
jdbcRs.previous();
```

方法`previous`类似于`next`方法，因为它可以在`while`循环中用于按顺序遍历所有行。不同之处在于您必须将光标移动到最后一行之后的位置，并且`previous`将光标移向开头。

**更新列值**

您更新`JdbcRowSet`对象中的数据的方式与更新`ResultSet`对象中的数据的方式相同。

假设 Coffee Break 所有者想要提高一磅 Espresso 咖啡的价格。如果所有者知道 Espresso 位于`jdbcRs`对象的第三行，则执行此操作的代码可能如下所示：

```java
jdbcRs.absolute(3);
jdbcRs.updateFloat("PRICE", 10.99f);
jdbcRs.updateRow();
```

代码将光标移动到第三行，并将`PRICE`列的值更改为10.99，然后使用新价格更新数据库。

调用方法`updateRow`会更新数据库，因为`jdbcRs`已经保持与数据库的连接。对于断开连接的`RowSet`对象，情况是不同的。

**插入行**

如果 Coffee Break 连锁店的所有者想要为他提供的东西添加一种或多种咖啡，那么所有者将需要为每种新咖啡在`COFFEES`表中添加一行，如下面的代码片段`JdbcRowSetSample`所示。请注意，因为`jdbcRs`对象始终连接到数据库，所以将一行插入`JdbcRowSet`对象与将一行插入`ResultSet`对象相同：您将光标移动到插入行，使用适当的 updater 方法为每列设置一个值，并调用方法`insertRow`：

```java
jdbcRs.moveToInsertRow();
jdbcRs.updateString("COF_NAME", "HouseBlend");
jdbcRs.updateInt("SUP_ID", 49);
jdbcRs.updateFloat("PRICE", 7.99f);
jdbcRs.updateInt("SALES", 0);
jdbcRs.updateInt("TOTAL", 0);
jdbcRs.insertRow();

jdbcRs.moveToInsertRow();
jdbcRs.updateString("COF_NAME", "HouseDecaf");
jdbcRs.updateInt("SUP_ID", 49);
jdbcRs.updateFloat("PRICE", 8.99f);
jdbcRs.updateInt("SALES", 0);
jdbcRs.updateInt("TOTAL", 0);
jdbcRs.insertRow();
```

当您调用方法`insertRow`时，新行将插入到`jdbcRs`对象中，并且也会插入到数据库中。前面的代码片段经历了两次这个过程，因此在`jdbcRs`对象和数据库中插入了两个新行。

**删除行**

与更新数据和插入新行一样，删除行对于`JdbcRowSet`对象和对于`ResultSet`对象来说是相同的。店主想停止销售法国烤无咖啡因咖啡，这是`jdbcRs`对象的最后一行。在下面的代码行中，第一行将光标移动到最后一行，第二行删除`jdbcRs`对象和数据库中的最后一行：

```java
jdbcRs.last();
jdbcRs.deleteRow();
```

**代码示例**

示例 `JdbcRowSetSample` 执行以下操作：

 - 创建一个新的`JdbcRowSet`对象，该对象使用`ResultSet`对象初始化，该对象是由执行查询生成的，该查询检索`COFFEES`表中的所有行
 - 将光标移动到`COFFEES`表的第三行，并更新该行中的`PRICE`列
 - 插入两个新行，一个用于`HouseBlend`，另一个用于`HouseDecaf`
 - 将光标移动到最后一行并删除它

