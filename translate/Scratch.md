### 使用 CachedRowSet 对象

`CachedRowSet`对象的特殊之处在于它可以在不连接到其数据源的情况下运行，也就是说，它是一个断开连接的`RowSet`对象。它的名称来源于它将数据存储（缓存）在内存中，以便它可以在自己的数据上运行，而不是在数据库中存储的数据上运行。

`CachedRowSet`接口是所有已断开连接的`RowSet`对象的超接口，因此此处演示的所有内容也适用于`WebRowSet`，`JoinRowSet`和`FilteredRowSet`对象。

请注意，虽然`CachedRowSet`对象的数据源（以及从中派生的`RowSet`对象）几乎总是关系数据库，但`CachedRowSet`对象能够从以表格格式存储其数据的任何数据源获取数据。例如，平面文件（无结构文件）或电子表格可能是数据的来源。当实现断开连接的`RowSet`对象的`RowSetReader`对象以从此类数据源读取数据时，就会出现这种情况。`CachedRowSet`接口的引用实现具有一个`RowSetReader`对象，该对象从关系数据库中读取数据，因此在本教程中，数据源始终是一个数据库。

本节涵盖以下主题：

- [创建 CachedRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#setting-up-cachedrowset-object)
- [填充 CachedRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#populating-cachedrowset-object)
- [Reader 的功能](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#reader)
- [更新 CachedRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#updating-cachedrowset-object)
- [更新数据源](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#updating-data-source)
- [Writer 的功能](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#writer)
- [通知监听器](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#notifying-listeners)
- [发送大量数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#sending-large-amounts-of-data)

**创建 CachedRowSet 对象**

创建 `CachedRowSet` 对象涉及以下步骤：

- [创建 CachedRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#creating-cachedrowset-object)
- [设定 CachedRowSet 属性](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#setting-cachedrowset-properties)
- [设定主键列](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#setting-key-columns)

**创建 CachedRowSet 对象**

你可以通过不同方式创建新的 `CachedRowSet` 对象：

- [使用默认构造器](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#using-default-constructor)
- 使用 `RowSetFactory` 实例，创建自类 `RowSetProvider` ：参考 [Using JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html) 中的 [Using the RowSetFactory Interface](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#rowsetfactory) 获取更多信息。

**注意：**另外，你还可以使用来自你的 JDBC 驱动的 `CachedRowSet` 实现的构造器。不过，`RowSet` 接口的实现将不同于参考实现。这些实现将具有不同的名称和构造器。比如，Oracle JDBC 驱动的 `CachedRowSet` 接口实现名为 `oracle.jdbc.rowset.OracleCachedRowSet` 。

**使用默认构造器**

创建 `CachedRowSet` 对象的一种方式是调用参考实现中定义的默认构造器，如下面这行代码所示：

```java
CachedRowSet crs = new CachedRowSetImpl();
```

在它首次被创建后，对象 `crs` 拥有与 `JdbcRowSet` 对象相同的属性默认值，另外，它被分配一个默认 `SyncProvider` 实现实例，`RIOptimisticProvider` 。

`SyncProvider` 对象提供一个 `RowSetReader` 对象（一个*reader*）和一个 `RowSetWriter` 对象（一个*writer*），断开连接的 `RowSet` 对象需要它以便从它的数据源读取数据并将数据写回它的数据源。读取器和写入器的功能稍后介绍。需要注意的是，读取器和写入器都是完全工作在后台的，因此关于它们工作原理的解释只是帮助你理解 `CachedRowSet` 接口中定义的一些方法在后台执行的操作。

**设定 CachedRowSet 属性**

通常，属性的默认值都可以正常使用，不过你可以通过调用相应的 setter 方法修改属性值。一些属性值没有默认值，你必须手动设定它们。

为了获取数据，断开连接的 `RowSet` 对象必须能够连接到数据源并具有一些选择要保存的数据的方法。以下属性包含获取与数据库的连接所需的必要信息。

* `username` ：用户提供给数据库的名称，作为获取访问权限的一部分。
* `password` ：用户的数据库密码。
* `url` ：用户想要连接的数据库的 JDBC URL。
* `datasourceName` ：用于检索已向 JNDI 命名服务注册的`DataSource`对象的名称。

这些属性中你需要设定的部分取决于你将要以何种方式建立连接。首选的方式是使用 `DateSource` 对象，但是使用 JNDI 命名服务注册 `DataSource` 对象可能不现实，因为这通常是系统管理员的工作。因此，示例代码都使用了`DriverManager` 机制来获取连接，其中你使用 `url` 属性而不是 `datasourceName` 属性。

下面的代码设置 `username` ，`password` ，以及 `url` 属性，因而可以通过 `DriverManager` 类获取连接。（您将在 JDBC 驱动程序的文档中找到要设置为`url`属性值的 JDBC URL。）

```java
public void setConnectionProperties(
    String username, String password) {
    crs.setUsername(username);
    crs.setPassword(password);
    crs.setUrl("jdbc:mySubprotocol:mySubname");
    // ...
```

另一个你必须设置的属性是 `command` 属性。在参考实现中，数据从 `ResultSet` 对象读入 `RowSet` 对象中。产生该 `ResultSet` 对象的查询就是 `command` 属性的值。比如，下面的代码设定 `command` 属性值为产生包含 `MERCH_INVENTORY` 表全部数据的 `ResultSet ` 对象的查询：

```java
crs.setCommand("select * from MERCH_INVENTORY");
```

**设定主键列**

如果你希望对 `crs` 对象进行任何修改，并且希望这些修改被保存到数据库中，你必须设定更多信息：主键列。主键列基本上就是主键，因为它们表示一列或者多列可以唯一标识一行数据。两者的区别是主键设置在数据库表上，而主键列设置在特定 `RowSet` 对象上。下面的代码为 `crs` 设定主键列为第一列：

```java
int [] keys = {1};
crs.setKeyColumns(keys);
```

表 `MERCH_INVENTORY` 的第一列是 `ITEM_ID` ，它可以作为主键列，因为每个商品的 ID 都是不同的，因而可以唯一标识表中的一行。另外，这一列在表 `MERCH_INVENTORY` 的定义中被指定为主键。方法 `setKeyColumns` 携带一个数组参数，因为事实上，可能需要两列或者多列才能唯一标识一行数据。

作为一个兴趣点，方法`setKeyColumns`不设置属性的值。在这种情况下，它设置字段`keyCols`的值。主键列在内部使用，因此在设置它们之后，您不再对它们执行任何操作。您将在 [Using SyncResolver Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#syncresolver) 一节中看到如何以及何时使用主键列。

**填充 CachedRowSet 对象**

填充断开连接的`RowSet`对象涉及比填充连接的`RowSet`对象更多的工作。幸运的是，额外的工作是在后台完成的。完成初步工作以设置`CachedRowSet`对象`crs`后，以下代码行填充`crs`：

```java
crs.execute();
```

`crs` 中的数据就是 `ResultSet` 对象中的数据，也即是执行 `command` 属性值表示的查询得到的数据。

不同的是，`execute`方法的`CachedRowSet`实现比`JdbcRowSet`实现做得更多。或者更确切地说，方法`execute` 委托其任务的`CachedRowSet`对象的读取器做了很多其它工作。

每个断开连接的`RowSet`对象都有一个分配给它的`SyncProvider`对象，而这个`SyncProvider`对象提供了`RowSet`对象的读取器（`RowSetReader`对象）。创建`crs`对象时，它被用作默认的`CachedRowSetImpl`构造函数，除了设置属性的默认值之外，还将`RIOptimisticProvider`实现的实例指定为默认的`SyncProvider`对象。

**Reader 的功能**

当应用程序调用方法`execute`时，断开连接的`RowSet`对象的读取器将在后台工作，以使用数据填充`RowSet`对象。新创建的`CachedRowSet`对象未连接到数据源，因此必须获取与该数据源的连接才能从中获取数据。默认`SyncProvider`对象（`RIOptimisticProvider`）的参考实现提供了一个读取器，它通过使用为用户名，密码以及 JDBC URL 或数据源名称（最新设置的那个）设置的值来获取连接。然后，读取器执行该`command` 的查询集。它读取查询生成的`ResultSet`对象中的数据，并使用该数据填充`CachedRowSet`对象。最后，读取器关闭连接。

**更新 CachedRowSet 对象**

在Coffee Break场景中，老板希望简化操作。业主决定让仓库中的员工直接将库存输入PDA（个人数字助理），从而避免让第二个人进行数据输入的容易出错的过程。在这种情况下，`CachedRowSet`对象是理想的，因为它是轻量级的，可序列化的，并且可以在不连接数据源的情况下进行更新。

老板将让应用程序开发团队为 PDA 创建 GUI 工具，仓库员工将使用该工具输入库存数据。总部将创建一个`CachedRowSet`对象，该对象填充有显示当前库存的表，并使用 Internet 将其发送到 PDA。当仓库员工使用 GUI 工具输入数据时，该工具会将每个条目添加到数组中，`CachedRowSet`对象将使用该数组在后台执行更新。完成清单后，PDA 将新数据发送回总部，数据将上传到主服务器。

本章节涵盖以下主题：

- [更新列值](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#updating-column-value)
- [插入和删除行](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#inserting-and-deleting-rows)

**更新列值**

更新`CachedRowSet`对象中的数据与更新`JdbcRowSet`对象中的数据相同。例如，`CachedRowSetSample.java`中的以下代码片段将`QUEM`列中的值增加1，其中`ITEM_ID`列的数据项标识符为`12345`：

```java
while (crs.next()) {
    System.out.println(
        "Found item " + crs.getInt("ITEM_ID") +
        ": " + crs.getString("ITEM_NAME"));
    if (crs.getInt("ITEM_ID") == 1235) {
        int currentQuantity = crs.getInt("QUAN") + 1;
        System.out.println("Updating quantity to " +
          currentQuantity);
        crs.updateInt("QUAN", currentQuantity + 1);
        crs.updateRow();
        // Synchronizing the row
        // back to the DB
        crs.acceptChanges(con);
    }
```

**插入和删除行**

与更新列值一样，在`CachedRowSet`对象中插入和删除行的代码与`JdbcRowSet`对象的代码相同。

以下摘自`CachedRowSetSample.java`将新行插入到`CachedRowSet`对象`crs`中：

```java
crs.moveToInsertRow();
crs.updateInt("ITEM_ID", newItemId);
crs.updateString("ITEM_NAME", "TableCloth");
crs.updateInt("SUP_ID", 927);
crs.updateInt("QUAN", 14);
Calendar timeStamp;
timeStamp = new GregorianCalendar();
timeStamp.set(2006, 4, 1);
crs.updateTimestamp(
    "DATE_VAL",
    new Timestamp(timeStamp.getTimeInMillis()));
crs.insertRow();
crs.moveToCurrentRow();
```

如果总部决定停止库存特定物品，那么它可能会删除该咖啡本身的行。但是，在该方案中，使用PDA的仓库员工也具有删除它的能力。以下代码片段查找`ITEM_ID`列中的值为`12345`的行，并从`CachedRowSet crs`中删除它：

```java
while (crs.next()) {
    if (crs.getInt("ITEM_ID") == 12345) {
        crs.deleteRow();
        break;
    }
}
```

**更新数据源**

There is a major difference between making changes to a `JdbcRowSet` object and making changes to a `CachedRowSet` object. Because a `JdbcRowSet` object is connected to its data source, the methods `updateRow`, `insertRow`, and `deleteRow` can update both the `JdbcRowSet` object and the data source. In the case of a disconnected `RowSet` object, however, these methods update the data stored in the `CachedRowSet` object's memory but cannot affect the data source. A disconnected `RowSet` object must call the method `acceptChanges` in order to save its changes to the data source. In the inventory scenario, back at headquarters, an application will call the method `acceptChanges` to update the database with the new values for the column `QUAN`.

```
crs.acceptChanges();

```

## [What Writer Does]()

Like the method `execute`, the method `acceptChanges` does its work invisibly. Whereas the method `execute` delegates its work to the `RowSet` object's reader, the method `acceptChanges` delegates its tasks to the `RowSet` object's writer. In the background, the writer opens a connection to the database, updates the database with the changes made to the `RowSet` object, and then closes the connection.

### Using Default Implementation

The difficulty is that a *conflict* can arise. A conflict is a situation in which another party has updated a value in the database that corresponds to a value that was updated in a `RowSet` object. Which value should persist in the database? What the writer does when there is a conflict depends on how it is implemented, and there are many possibilities. At one end of the spectrum, the writer does not even check for conflicts and just writes all changes to the database. This is the case with the `RIXMLProvider` implementation, which is used by a `WebRowSet` object. At the other end, the writer ensures that there are no conflicts by setting database locks that prevent others from making changes.

The writer for the `crs` object is the one provided by the default `SyncProvider` implementation, `RIOptimisticProvider`. The `RIOPtimisticProvider` implementation gets its name from the fact that it uses an optimistic concurrency model. This model assumes that there will be few, if any, conflicts and therefore sets no database locks. The writer checks to see if there are any conflicts, and if there is none, it writes the changes made to the `crs` object to the database, and those changes become persistent. If there are any conflicts, the default is not to write the new `RowSet`values to the database.

In the scenario, the default behavior works very well. Because no one at headquarters is likely to change the value in the `QUAN` column of `COF_INVENTORY`, there will be no conflicts. As a result, the values entered into the `crs` object at the warehouse will be written to the database and thus will be persistent, which is the desired outcome.

## [Using SyncResolver Objects]()

In other situations, however, it is possible for conflicts to exist. To accommodate these situations, the `RIOPtimisticProvider` implementation provides an option that lets you look at the values in conflict and decide which ones should be persistent. This option is the use of a `SyncResolver` object.

When the writer has finished looking for conflicts and has found one or more, it creates a `SyncResolver` object containing the database values that caused the conflicts. Next, the method `acceptChanges` throws a `SyncProviderException` object, which an application may catch and use to retrieve the `SyncResolver` object. The following lines of code retrieve the `SyncResolver` object `resolver`:

```
try {
    crs.acceptChanges();
} catch (SyncProviderException spe) {
    SyncResolver resolver = spe.getSyncResolver();
}

```

The object `resolver` is a `RowSet` object that replicates the `crs` object except that it contains only the values in the database that caused a conflict. All other column values are null.

With the `resolver` object, you can iterate through its rows to locate the values that are not null and are therefore values that caused a conflict. Then you can locate the value at the same position in the `crs` object and compare them. The following code fragment retrieves `resolver` and uses the `SyncResolver` method `nextConflict` to iterate through the rows that have conflicting values. The object `resolver` gets the status of each conflicting value, and if it is `UPDATE_ROW_CONFLICT`, meaning that the `crs` was attempting an update when the conflict occurred, the `resolver` object gets the row number of that value. Then the code moves the cursor for the `crs` object to the same row. Next, the code finds the column in that row of the `resolver` object that contains a conflicting value, which will be a value that is not null. After retrieving the value in that column from both the `resolver` and `crs` objects, you can compare the two and decide which one you want to become persistent. Finally, the code sets that value in both the `crs` object and the database using the method `setResolvedValue`, as shown in the following code:

```
try {
    crs.acceptChanges();
} catch (SyncProviderException spe) {
    SyncResolver resolver = spe.getSyncResolver();
  
    // value in crs
    Object crsValue;
  
    // value in the SyncResolver object
    Object resolverValue; 
  
    // value to be persistent
    Object resolvedValue; 

    while (resolver.nextConflict()) {
        if (resolver.getStatus() ==
            SyncResolver.UPDATE_ROW_CONFLICT) {
            int row = resolver.getRow();
            crs.absolute(row);
            int colCount =
                crs.getMetaData().getColumnCount();
            for (int j = 1; j <= colCount; j++) {
                if (resolver.getConflictValue(j)
                    != null) {
                    crsValue = crs.getObject(j);
                    resolverValue = 
                        resolver.getConflictValue(j);

                    // ...
                    // compare crsValue and
                    // resolverValue to
                    // determine the value to be
                    // persistent

                    resolvedValue = crsValue;
                    resolver.setResolvedValue(
                        j, resolvedValue);
                }
            }
        }
    }
}

```

## [Notifying Listeners]()

Being a JavaBeans component means that a `RowSet` object can notify other components when certain things happen to it. For example, if data in a `RowSet` object changes, the `RowSet` object can notify interested parties of that change. The nice thing about this notification mechanism is that, as an application programmer, all you have to do is add or remove the components that will be notified.

This section covers the following topics:

- [Setting Up Listeners](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#setting-up-listeners)
- [How Notification Works](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#how-notification-works)

### [Setting Up Listeners]()

A *listener* for a `RowSet` object is a component that implements the following methods from the `RowSetListener` interface:

- `cursorMoved`: Defines what the listener will do, if anything, when the cursor in the `RowSet` object moves.
- `rowChanged`: Defines what the listener will do, if anything, when one or more column values in a row have changed, a row has been inserted, or a row has been deleted.
- `rowSetChanged`: Defines what the listener will do, if anything, when the `RowSet` object has been populated with new data.

An example of a component that might want to be a listener is a `BarGraph` object that graphs the data in a `RowSet` object. As the data changes, the `BarGraph` object can update itself to reflect the new data.

As an application programmer, the only thing you must do to take advantage of the notification mechanism is to add or remove listeners. The following line of code means that every time the cursor for the `crs` objects moves, values in `crs` are changed, or `crs` as a whole gets new data, the `BarGraph` object `bar` will be notified:

```
crs.addRowSetListener(bar);

```

You can also stop notifications by removing a listener, as is done in the following line of code:

```
crs.removeRowSetListener(bar);

```

Using the Coffee Break scenario, assume that headquarters checks with the database periodically to get the latest price list for the coffees it sells online. In this case, the listener is the `PriceList` object `priceList` at the Coffee Break web site, which must implement the `RowSetListener`methods `cursorMoved`, `rowChanged`, and `rowSetChanged`. The implementation of the `cursorMoved` method could be to do nothing because the position of the cursor does not affect the `priceList` object. The implementations for the `rowChanged` and `rowSetChanged` methods, on the other hand, must ascertain what changes have been made and update `priceList` accordingly.

### [How Notification Works]()

In the reference implementation, methods that cause any of the `RowSet` events automatically notify all registered listeners. For example, any method that moves the cursor also calls the method `cursorMoved` on each of the listeners. Similarly, the method `execute` calls the method `rowSetChanged` on all listeners, and `acceptChanges` calls `rowChanged` on all listeners.

## [Sending Large Amounts of Data]()

The sample code [`CachedRowSetSample.testCachedRowSet`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) demonstrates how data can be sent in smaller pieces.