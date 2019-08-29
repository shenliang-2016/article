### 使用事务

有时候你可能会希望一个语句在另外一个语句执行完成之后才生效。比如，The Coffee Break 的老板要更新每周的咖啡销量，同时还要更新目前为止的销售总量。但是，每周销量和销售总量应该同时更新，否则数据将会不一致。确保这两个操作要么全部成功，要么全部不成功，就需要使用事务。事务时一个或者多个语句的集合，作为一个单元执行，要么所有语句都执行成功，要么全部不执行。

本页面涵盖以下主题：

- [关闭自动提交模式](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#disable_auto_commit)
- [提交事务](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#commit_transactions)
- [使用事务保持数据完整性](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#transactions_data_integrity)
- [设定和滚回保存点](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#set_roll_back_savepoints)
- [释放保存点](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#release_savepoints)
- [何时调用 rollback 方法](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#call_rollback)

**关闭自动提交模式**

当一个连接被创建后，它处于自动提交模式。这意味着每条 SQL 语句都被作为单独的事务，执行完成之后马上就会自动提交。（更准确地说，默认是语句执行完成后被提交，而不是执行时。语句执行完成，指的是它的所有结果集和更新计数都被得到。大多数情况下，其实就是一个语句完成了，然后就会被提交，就在它刚刚执行之后。）

允许两个或者多个语句编组进入一个事务的方法时关闭自动提交模式。下面的例子展示了这种用法，其中`con` 时一个活动连接：

```java
con.setAutoCommit(false);
```

**提交事务**

自动提交模式关闭之后，除非你显式调用 `commit` ，没有任何 SQL 语句会被提交。前一次 `commit` 方法调用之后的所有执行语句都被包含到当前事务中，作为一个单元提交。下面的方法 `CoffeeTable.updateCoffeeSales` ，其中 `con` 是一个活动连接，展示了一个事务：

```java
public void updateCoffeeSales(HashMap<String, Integer> salesForWeek)
    throws SQLException {

    PreparedStatement updateSales = null;
    PreparedStatement updateTotal = null;

    String updateString =
        "update " + dbName + ".COFFEES " +
        "set SALES = ? where COF_NAME = ?";

    String updateStatement =
        "update " + dbName + ".COFFEES " +
        "set TOTAL = TOTAL + ? " +
        "where COF_NAME = ?";

    try {
        con.setAutoCommit(false);
        updateSales = con.prepareStatement(updateString);
        updateTotal = con.prepareStatement(updateStatement);

        for (Map.Entry<String, Integer> e : salesForWeek.entrySet()) {
            updateSales.setInt(1, e.getValue().intValue());
            updateSales.setString(2, e.getKey());
            updateSales.executeUpdate();
            updateTotal.setInt(1, e.getValue().intValue());
            updateTotal.setString(2, e.getKey());
            updateTotal.executeUpdate();
            con.commit();
        }
    } catch (SQLException e ) {
        JDBCTutorialUtilities.printSQLException(e);
        if (con != null) {
            try {
                System.err.print("Transaction is being rolled back");
                con.rollback();
            } catch(SQLException excep) {
                JDBCTutorialUtilities.printSQLException(excep);
            }
        }
    } finally {
        if (updateSales != null) {
            updateSales.close();
        }
        if (updateTotal != null) {
            updateTotal.close();
        }
        con.setAutoCommit(true);
    }
}
```

该方法中，连接 `con` 的自动提交模式被关闭，意味着当 `commit` 方法被调用时，两个预编译语句 `updateSales` 和 `updateTotal` 会被一起提交。无论何时 `commit ` 方法被调用（自动提交模式打开时自动被调用，或者自动提交模式关闭时被显式调用），所有当前事务中的语句造成的变化就会被持久化。例子的情况下，意味着 Colombian 咖啡的 `SALES` 和 `TOTAL` 列已经被修改为 `50` （如果之前 `TOTAL` 是 `0`），并将保持此值直到被其它的更新语句修改。

语句 `con.setAutoCommit(true);` 启动自动提交模式，意味着每条语句一旦执行完成就会被提交。这样，你就回到了不需要显式调用 `commit ` 方法的默认状态。建议仅在事务模式期间禁用自动提交模式。这样，您可以避免为多个语句保留数据库锁，这会增加与其他用户冲突的可能性。

**使用事务保持数据完整性**

除了将语句编组为一个执行单元，事务还有助于保持表中数据的完整性。比如，假设一个咖啡店的员工想要在 `COFFEES` 表中输入新的咖啡价格，但是拖延了几天才做。与此同时，咖啡价格上涨了，今天老板正在输入更高的价格。而该员工也正在输入已经过时的价格。插入过时的价格之后，该员工意识到这些价格已经没用了，然后调用 `Connection` 方法 `rollback` 来撤销修改。（方法 `rollback` 取消一个事务并重置那些被修改的值为更改之前）同时，老板正在执行 `SELECT` 语句并打印新的价格。在这种情况下，老板可能会打印已回滚到其先前值的价格，从而使打印价格不正确。

通过使用事务可以避免这种情况，事务为当两个用户同时访问相同数据时产生冲突的情况提供了一定程度的保护。

为了避免事务期间的冲突，DBMS 使用锁机制来阻止来自其它人对正在被当前事务访问的数据的访问。（注意，在自动提交模式中，每条语句都是一个事务，为每条语句锁定并保持。）当设置锁之后，它会强制保持直到事务被提交或者回滚。比如，DBMS 可以所供一张表的一行直到更新它的事务被提交。此锁定的作用就是防止其它用户的脏读，也就是说，读取到更改被持久化之前的值。（访问一个被更新而尚未被提交的值被称为*脏读*，因为该值随时有可能被回滚回到它之前的值。如果你读取了一个稍后被回滚的值，你将获得一个无效的值。）

锁定设置方法取决于事务隔离级别，事务隔离级别的范围从完全不支持事务直到支持强制非常严格的访问规则的事务。

事务隔离级别的一个例子时 `TRANSACTION_READ_COMMITTED` ，它不允许在一个值被提交之前被访问。换句话说，如果事务隔离级别被设置为 `TRANSACTION_READ_COMMITTED` ，DBMS 不允许脏读的发生。`Connection` 接口包含5个值表示你可以在 JDBC 中使用的事务隔离级别：

| Isolation Level                | Transactions  | Dirty Reads      | Non-Repeatable Reads | Phantom Reads    |
| ------------------------------ | ------------- | ---------------- | -------------------- | ---------------- |
| `TRANSACTION_NONE`             | Not supported | *Not applicable* | *Not applicable*     | *Not applicable* |
| `TRANSACTION_READ_COMMITTED`   | Supported     | Prevented        | Allowed              | Allowed          |
| `TRANSACTION_READ_UNCOMMITTED` | Supported     | Allowed          | Allowed              | Allowed          |
| `TRANSACTION_REPEATABLE_READ`  | Supported     | Prevented        | Prevented            | Allowed          |
| `TRANSACTION_SERIALIZABLE`     | Supported     | Prevented        | Prevented            | Prevented        |

*不可重复读*发生的情形大概是这样，事务 A 查询一行，事务 B 随后更新这一行，然后事务 A 稍后再次获取同一行。事务 A 获取同一行两次但是得到了不同的数据。

*幻读*发生的情形，事务 A 查询满足特定条件的行集，事务 B 接下来插入或者更新一行到满足事务 A 中查询条件的行集中，稍后事务 A 再次执行相同条件的查询。此时事务 A 可以看到新增的行。该行数据指向表中的幻影数据。

通常，你不需要任何有关事务隔离级别的工作：你可以仅仅使用 DBMS 的默认值。默认事务隔离级别取决于你的 DBMS。比如，Java DB 的默认事务隔离级别是 `TRANSACTION_READ_COMMITTED` ，JDBC 允许你查看你的 DBMS 设置的事务隔离级别（使用 `Connection` 方法 `getTransactionIsolation` ）并允许你将其设置为别的值（使用 `Connection` 方法 `setTransactionIsolation`）。

**注意：**JDBC 驱动可能不支持所有的事务隔离级别。如果驱动程序不支持调用 `setTransactionIsolation` 方法指定的事务隔离级别，则会选择一个更好级别的、限制更严格的事务隔离级别。如果驱动无法选择一个更高的事务隔离级别，它将抛出 `SQLException` 。使用 `DatabaseMetaData.supportsTransactionIsolationLevel` 确定驱动程序是否支持给定的事务隔离级别。

**设定和滚回保存点**

方法 `Connction.setSavepoint` 方法，在当前事务中设置一个 `Savepoint` 对象。`Connection.rollback` 方法被重载以携带一个 `Savepoint` 参数。

下面的方法，`CoffeeTable.modifyPricesByPercentage` ，按照百分比提升特定咖啡的价格，`priceModifier` 。然而，如果新价格超过特定价格，`maximumPrice` ，则价格会被恢复称为初始价格：

```java
public void modifyPricesByPercentage(
    String coffeeName,
    float priceModifier,
    float maximumPrice)
    throws SQLException {
    
    con.setAutoCommit(false);

    Statement getPrice = null;
    Statement updatePrice = null;
    ResultSet rs = null;
    String query =
        "SELECT COF_NAME, PRICE FROM COFFEES " +
        "WHERE COF_NAME = '" + coffeeName + "'";

    try {
        Savepoint save1 = con.setSavepoint();
        getPrice = con.createStatement(
                       ResultSet.TYPE_SCROLL_INSENSITIVE,
                       ResultSet.CONCUR_READ_ONLY);
        updatePrice = con.createStatement();

        if (!getPrice.execute(query)) {
            System.out.println(
                "Could not find entry " +
                "for coffee named " +
                coffeeName);
        } else {
            rs = getPrice.getResultSet();
            rs.first();
            float oldPrice = rs.getFloat("PRICE");
            float newPrice = oldPrice + (oldPrice * priceModifier);
            System.out.println(
                "Old price of " + coffeeName +
                " is " + oldPrice);

            System.out.println(
                "New price of " + coffeeName +
                " is " + newPrice);

            System.out.println(
                "Performing update...");

            updatePrice.executeUpdate(
                "UPDATE COFFEES SET PRICE = " +
                newPrice +
                " WHERE COF_NAME = '" +
                coffeeName + "'");

            System.out.println(
                "\nCOFFEES table after " +
                "update:");

            CoffeesTable.viewTable(con);

            if (newPrice > maximumPrice) {
                System.out.println(
                    "\nThe new price, " +
                    newPrice +
                    ", is greater than the " +
                    "maximum price, " +
                    maximumPrice +
                    ". Rolling back the " +
                    "transaction...");

                con.rollback(save1);

                System.out.println(
                    "\nCOFFEES table " +
                    "after rollback:");

                CoffeesTable.viewTable(con);
            }
            con.commit();
        }
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (getPrice != null) { getPrice.close(); }
        if (updatePrice != null) {
            updatePrice.close();
        }
        con.setAutoCommit(true);
    }
}
```

以下语句指定在调用`commit`方法时，将关闭从`getPrice`查询生成的`ResultSet`对象的游标。请注意，如果您的 DBMS 不支持`ResultSet.CLOSE_CURSORS_AT_COMMIT`，则忽略此常量：

```java
getPrice = con.prepareStatement(query, ResultSet.CLOSE_CURSORS_AT_COMMIT);
```

该方法首先使用以下语句创建`Savepoint`：

```java
Savepoint save1 = con.setSavepoint();
```

该方法检查新价格是否大于`maximumPrice`值。如果是，则该方法使用以下语句回滚事务：

```java
con.rollback(save1);
```

因此，当方法通过调用`Connection.commit`方法提交事务时，它不会提交任何已关联的`Savepoint`已回滚的行；它将提交所有其他更新的行。

**释放保存点**

`Connection.releaseSavepoint`方法将`Savepoint`对象作为参数，并将其从当前事务中删除。

释放保存点后，尝试在回滚操作中引用它会导致抛出`SQLException`。在事务提交时或回滚整个事务时，事务中创建的任何保存点都将自动释放并变为无效。将事务滚动回保存点会自动释放该保存点，并使在相关保存点之后创建的任何其他保存点无效。

**何时调用 rollback 方法**

如前所述，调用方法`rollback`会终止事务并将已修改的任何值恢复为其先前值。如果您尝试在事务中执行一个或多个语句而获得了`SQLException`，请调用方法`rollback`以结束事务并重新开始事务。这是了解已提交内容和未提交内容的唯一方法。捕获`SQLException`会告诉您出现了问题，但它并未告诉您已提交或未提交的内容。因为你不能指望没有提交任何东西，所以调用方法`rollback`是确定的唯一方法。

方法`CoffeesTable.updateCoffeeSales`演示了一个事务，并包含一个调用方法`rollback`的`catch`块。如果应用程序继续并使用事务的结果，则对`catch`块中的`rollback`方法的此调用将阻止使用可能不正确的数据。

