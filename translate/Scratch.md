### 使用预编译语句

本页面涵盖如下主题：

- [预编译语句概述](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html#overview_ps)
- [创建 PreparedStatement 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html#create_ps)
- [为 PreparedStatement 参数提供值](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html#supply_values_ps)

**预编译语句概述**

有时候使用 `PreparedStatement` 对象将 SQL 语句发送到数据库更方便。这种特别的语句产生自更通用的类，`Statement`，如前面章节所述。

如果你想要多次执行 `Statement` 对象，那么通常使用 `PreparedStatement` 对象可以缩短执行时间。

`PrepareStatement` 对象的主要特性如下：不像 `Statement` 对象，预编译语句对象被创建时将被给定 SQL 语句。大多数情况下，这种做法的优点是，该 SQL 语句会立即被发送给 DBMS，在那里该语句会被编译。结果就是，`PreparedStatement` 对象不仅包含 SQL 语句，还包含已经预编译完成的 SQL 语句。这就意味着，当 `PreparedStatement` 被执行时，DBMS 能够直接执行 `PreparedStatement` SQL 语句，而不需要首先编译它。

虽然`PreparedStatement`对象可用于没有参数的SQL语句，但您最常使用它们来获取带参数的SQL语句。使用带参数的SQL语句的优点是，您可以使用相同的语句，并在每次执行时为其提供不同的值。这方面的例子在以下部分中。

以下方法，`CoffeesTable.updateCoffeeSales`，将当前销售的咖啡磅数存储在每种类型咖啡的`SALES`列中，并为每种咖啡更新`TOTAL`列中销售的咖啡总磅数：

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

**创建 PreparedStatement 对象**

下面创建一个携带两个输入参数的 `PreparedStatement` 对象：

```java
String updateString =
    "update " + dbName + ".COFFEES " +
    "set SALES = ? where COF_NAME = ?";
updateSales = con.prepareStatement(updateString);
```

**为 PreparedStatement 参数提供值**

在执行`PreparedStatement`对象之前，必须提供值来代替问号占位符（如果有的话）。通过调用`PreparedStatement`类中定义的 setter 方法之一来完成此操作。以下语句在名为`updateSales`的`PreparedStatement`中提供了两个问号占位符：

```java
updateSales.setInt(1, e.getValue().intValue());
updateSales.setString(2, e.getKey());
```

每个 setter 方法的第一个参数指定问号占位符。在这个例子中，`setInt`指定第一个占位符，`setString`指定第二个占位符。

使用值设置参数后，它会保留该值，直到将其重置为另一个值，或者调用方法`clearParameters`。使用`PreparedStatement`对象`updateSales`，下面的代码片段说明了在重置其中一个参数的值并使另一个参数保持原值之后重用该预编译语句：

```java
// changes SALES column of French Roast
//row to 100

updateSales.setInt(1, 100);
updateSales.setString(2, "French_Roast");
updateSales.executeUpdate();

// changes SALES column of Espresso row to 100
// (the first parameter stayed 100, and the second
// parameter was reset to "Espresso")

updateSales.setString(2, "Espresso");
updateSales.executeUpdate();
```

**循环设定值**

通过使用`for`循环或`while`循环来设置输入参数的值，通常可以使编码更容易。

`CoffeesTable.updateCoffeeSales`方法使用 for-each 循环重复设置`PreparedStatement`对象`updateSales`和`updateTotal`中的值：

```java
for (Map.Entry<String, Integer> e : salesForWeek.entrySet()) {

    updateSales.setInt(1, e.getValue().intValue());
    updateSales.setString(2, e.getKey());

    // ...
}
```

方法`CoffeesTable.updateCoffeeSales`接受一个参数，`HashMap`。 `HashMap`参数中的每个元素都包含一种咖啡的名称以及当周销售的那种咖啡的磅数。for-each循环遍历`HashMap`参数的每个元素，并在`updateSales`和`updateTotal`中设置相应的问号占位符。

**执行 PreparedStatement 对象**

与`Statement`对象一样，要执行`PreparedStatement`对象，如果查询只返回一个`ResultSet`（例如`SELECT` SQL语句），则调用执行语句：`executeQuery` 。如果查询执行不返回`ResultSet`（例如`UPDATE` SQL语句），执行`executeUpdate`。如果查询可能返回多个`ResultSet`对象，则则执行`execute`。 `CoffeesTable.updateCoffeeSales`中的`PreparedStatement`对象都包含`UPDATE` SQL语句，因此两者都是通过调用`executeUpdate`来执行的：

```java
updateSales.setInt(1, e.getValue().intValue());
updateSales.setString(2, e.getKey());
updateSales.executeUpdate();

updateTotal.setInt(1, e.getValue().intValue());
updateTotal.setString(2, e.getKey());
updateTotal.executeUpdate();
con.commit();
```

当`executeUpdate`用于执行`updateSales`和`updateTotals`时，它们没有提供参数；两个`PreparedStatement`对象都已包含要执行的SQL语句。

**注意**：在`CoffeesTable.updateCoffeeSales`的开头，自动提交模式设置为`false`：

```java
con.setAutoCommit(false);
```

因此，在调用方法`commit`之前，不会提交任何SQL语句。有关自动提交模式的更多信息，请参阅 [Transactions](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html) 。

**executeUpdate 方法的返回值**

`executeQuery`返回一个`ResultSet`对象，其中包含发送给 DBMS 的查询结果，`executeUpdate`的返回值是一个`int`值，表示一个表的更新行数。例如，以下代码显示了`executeUpdate`的返回值被赋值给变量`n`：

```java
updateSales.setInt(1, 50);
updateSales.setString(2, "Espresso");
int n = updateSales.executeUpdate();
// n = 1 because one row had a change in it
```

表`COFFEES`已更新；值50替换`Espresso`行中`SALES`列中的值。该更新会影响表中的一行，因此`n`等于1。

当方法`executeUpdate`用于执行DDL（数据定义语言）语句时，例如在创建表时，它返回`int`值为0。因此，在下面的代码片段中，执行使用的DDL语句创建表`COFFEES`，`n`被赋值为0：

```java
// n = 0
int n = executeUpdate(createTableCoffees); 
```

请注意，当`executeUpdate`的返回值为0时，它可能意味着以下两种情况之一：

 - 执行的语句是一个影响零行的更新语句。
 - 执行的语句是DDL语句。