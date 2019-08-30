### 使用 JoinRowSet 对象

`JoinRowSet`实现允许您在`RowSet`对象未连接到数据源时创建SQL`JOIN`。这很重要，因为它节省了必须创建一个或多个连接的开销。

本节涵盖以下主题：

- [创建 JoinRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/joinrowset.html#creating-joinrowset-object)
- [添加 RowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/joinrowset.html#adding-rowset-objects)
- [管理匹配列](https://docs.oracle.com/javase/tutorial/jdbc/basics/joinrowset.html#managing-match-columns)

`JoinRowSet`接口是`CachedRowSet`接口的子接口，从而继承了`CachedRowSet`对象的功能。这意味着`JoinRowSet`对象是一个断开连接的`RowSet`对象，可以在不总是连接到数据源的情况下运行。

**创建 JoinRowSet 对象**

`JoinRowSet`对象充当SQL`JOIN`的持有者。以下代码行显示创建`JoinRowSet`对象：

```java
JoinRowSet jrs = new JoinRowSetImpl();
```

变量`jrs`在添加`RowSet`对象之前不会保留任何内容。

**注意**：或者，您可以使用 JDBC 驱动程序的`JoinRowSet`实现中的构造函数。但是，`RowSet`接口的实现将与参考实现不同。这些实现将具有不同的名称和构造函数。例如，Oracle JDBC 驱动程序的`JoinRowSet`接口的实现名为`oracle.jdbc.rowset.OracleJoinRowSet`。

**添加 RowSet 对象**

任何`RowSet`对象都可以添加到`JoinRowSet`对象，只要它可以是SQL`JOIN`的一部分。可以添加一个始终连接到其数据源的`JdbcRowSet`对象，但通常它通过直接操作数据源而成为`JOIN`的一部分，而不是通过添加到`JoinRowSet`对象成为`JOIN`的一部分。提供`JoinRowSet`实现的目的是使断开连接的`RowSet`对象成为`JOIN`关系的一部分成为可能。

Coffee Break 连锁咖啡馆的老板想要获得他从 Acme, Inc. 购买的咖啡清单。为了做到这一点，店主必须从两个表`COFFEES`和`SUPPLIERS`获取信息。在`RowSet`技术之前的数据库世界中，程序员会将以下查询发送到数据库：

```java
String query =
    "SELECT COFFEES.COF_NAME " +
    "FROM COFFEES, SUPPLIERS " +
    "WHERE SUPPLIERS.SUP_NAME = Acme.Inc. " +
    "and " +
    "SUPPLIERS.SUP_ID = COFFEES.SUP_ID";
```

在`RowSet`技术的世界中，您可以得到相同的结果，而无需向数据源发送查询。您可以将包含两个表中数据的`RowSet`对象添加到`JoinRowSet`对象。然后，因为所有相关数据都在`JoinRowSet`对象中，所以您可以对其执行查询以获取所需数据。

来自 [`JoinSample.testJoinRowSet`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 的以下代码片段创建了两个`CachedRowSet`对象，`coffees`由来自表`COFFEES`的数据填充，`suppliers` 由表`SUPPLIERS`中的数据填充。`coffees`和`suppliers`对象必须与数据库建立连接以执行它们的命令并填充数据，但在此之后，它们不必再次重新连接以形成`JOIN`。

```java
coffees = new CachedRowSetImpl();
coffees.setCommand("SELECT * FROM COFFEES");
coffees.setUsername(settings.userName);
coffees.setPassword(settings.password);
coffees.setUrl(settings.urlString);
coffees.execute();

suppliers = new CachedRowSetImpl();
suppliers.setCommand("SELECT * FROM SUPPLIERS");
suppliers.setUsername(settings.userName);
suppliers.setPassword(settings.password);
suppliers.setUrl(settings.urlString);
suppliers.execute(); 
```

**管理匹配列**

查看`SUPPLIERS`表，您可以看到 Acme, Inc. 的识别号码是101。表`COFFEES`中供应商识别号为101的咖啡是 Colombian 和 Colombian_Decaf。两个表中的信息连接是可能的，因为这两个表具有共同的`SUP_ID`列。在JDBC`RowSet`技术中，`SUP_ID`，`JOIN`所基于的列，被称为*匹配列*。

添加到`JoinRowSet`对象的每个`RowSet`对象必须有一个匹配列，即`JOIN`所基于的列。有两种方法可以为`RowSet`对象设置匹配列。第一种方法是将匹配列传递给`JoinRowSet`方法`addRowSet`，如下面的代码行所示：

```java
jrs.addRowSet(coffees, 2);
```

这行代码将`coffees` `CachedRowSet`添加到`jrs`对象，并将`coffees`（`SUP_ID`）的第二列设置为匹配列。代码行也可以使用列名而不是列号。

```java
jrs.addRowSet(coffees, "SUP_ID");
```

在这一点上，`jrs`中只有 `coffees` 。添加到`jrs`的下一个`RowSet`对象必须能够与`coffees`形成`JOIN`，这对于 `suppliers` 是正确的，因为两个表都有列`SUP_ID`。以下代码行将`suppliers`添加到`jrs`并将列`SUP_ID`设置为匹配列。

```java
jrs.addRowSet(suppliers, 1);
```

现在`jrs`在`coffees`和`suppliers`之间包含`JOIN`，老板可以从中获取 Acme, Inc. 提供的咖啡的名称。因为代码没有设置`JOIN`的类型，`jrs` 保持`inner JOIN`，这是默认值。换句话说，`jrs`中的一行合并了`coffees`中的一行和`suppliers`中的一行。它保存了`coffees`中的列加上`供应商`中的列，其中`COFFEES.SUP_ID`列中的值与`SUPPLIERS.SUP_ID`中的值匹配。下面的代码打印出 Acme, Inc. 提供的咖啡的名称，其中`String` `supplierName`等于`Acme,Inc.`。注意这是可能的，因为来自`suppliers` 的`SUP_NAME`列和来自`coffees`的`COF_NAME`列现在都包含在`JoinRowSet`对象`jrs`中。

```java
System.out.println("Coffees bought from " + supplierName + ": ");

while (jrs.next()) {
    if (jrs.getString("SUP_NAME").equals(supplierName)) {
        String coffeeName = jrs.getString(1);
        System.out.println("     " + coffeeName);
    }
}
```

这将产生类似于以下的输出：

```
Coffees bought from Acme, Inc.:
     Colombian
     Colombian_Decaf
```

`JoinRowSet`接口提供了用于设置将要形成的`JOIN`类型的常量，但是目前唯一实现的类型是`JoinRowSet.INNER_JOIN`。

