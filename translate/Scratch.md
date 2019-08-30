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

更新`JdbcRowSet`对象和更新`CachedRowSet`对象之间存在重大差异。由于`JdbcRowSet`对象连接到其数据源，因此`updateRow`，`insertRow`和`deleteRow`方法可以更新`JdbcRowSet`对象和数据源。但是，在断开连接的`RowSet`对象的情况下，这些方法会更新存储在`CachedRowSet`对象内存中的数据，但不会影响数据源。断开连接的`RowSet`对象必须调用方法`acceptChanges`，以便将其更改保存到数据源。在示例库存场景中，返回总部，应用程序将调用方法`acceptChanges`以使用列`QUAN`的新值更新数据库。

```java
crs.acceptChanges();
```

**Writer 的功能**

与方法`execute`一样，方法`acceptChanges`暗中完成其工作。方法`execute`将其工作委托给`RowSet`对象的`reader`，方法`acceptChanges`将其任务委托给`RowSet`对象的`writer`。在后台，`writer`打开与数据库的连接，使用对`RowSet`对象所做的更改来更新数据库，然后关闭连接。

**使用默认实现**

困难在于可能产生冲突。冲突是指另一方更新了数据库中与`RowSet`对象中更新的值相对应的值的情况。哪个值应该在数据库中保留？`writer`在发生冲突时所做的工作取决于具体实现，并且有很多可能性。另一方面，`writer`甚至不检查冲突，只是将所有更改写入数据库。这是`RIXMLProvider`实现的情况，它由`WebRowSet`对象使用。另一方面，`writer`通过设置阻止其他人进行更改的数据库锁来确保不存在冲突。

`crs`对象的`writer`是默认的`SyncProvider`实现`RIOptimisticProvider`提供的`writer`。`RIOPtimisticProvider`实现的名称源于它使用乐观并发模型的事实。此模型假定冲突很少（如果有），因此不设置数据库锁。`writer`检查是否存在任何冲突，如果没有冲突，则会将对`crs`对象所做的更改写入数据库，并且这些更改将成为持久性更改。如果存在任何冲突，则默认情况下不将新的`RowSetvalues`写入数据库。

在该场景中，默认行为非常有效。因为总部的任何人都不可能更改`COF_INVENTORY`的`QUAN`列中的值，所以不会发生冲突。结果，输入仓库中的`crs`对象的值将被写入数据库，因此将是持久的，这是期望的结果。

**使用 SyncResolver 对象**

但是，在其他情况下，冲突可能存在。为了适应这些情况，`RIOPtimisticProvider`实现提供了一个选项，使您可以查看冲突中的值并确定哪些值应该是持久的。此选项是使用`SyncResolver`对象。

当`writer`完成查找冲突并找到一个或多个冲突时，它会创建一个`SyncResolver`对象，其中包含导致冲突的数据库值。接下来，方法`acceptChanges`抛出一个`SyncProviderException`对象，应用程序可以捕获该对象并使用它来检索`SyncResolver`对象。以下代码行检索`SyncResolver`对象解析器：

```java
try {
    crs.acceptChanges();
} catch (SyncProviderException spe) {
    SyncResolver resolver = spe.getSyncResolver();
}
```

对象`resolver`是一个`RowSet`对象，它复制`crs`对象，但它只包含导致冲突的数据库中的值。所有其他列值均为`null`。

使用`resolver`对象，您可以遍历其行以查找非空值，那些就是导致冲突的值。然后，您可以在`crs`对象中的相同位置找到该值并进行比较。以下代码片段检索`resolver`并使用`SyncResolver`方法`nextConflict`迭代具有冲突值的行。对象`resolver`获取每个冲突值的状态，如果它是`UPDATE_ROW_CONFLICT`，意味着`crs`在发生冲突时正在尝试更新，则`resolver`对象将获取该值的行号，然后代码将`crs`对象的光标移动到同一行。接下来，代码在`resolver`对象的该行中查找包含冲突值的列，该值将是非空值。从`resolver`和`crs`对象中检索该列中的值后，您可以比较两者并确定要保持哪一个。最后，代码使用方法`setResolvedValue`在`crs`对象和数据库中设置该值，如以下代码所示：

```java
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

**通知监听器**

作为 JavaBeans 组件意味着`RowSet`对象可以在发生某些事情时通知其他组件。例如，如果`RowSet`对象中的数据发生更改，则`RowSet`对象可以通知感兴趣的各方该更改。这种通知机制的好处在于，作为应用程序员，您所要做的就是添加或删除监听通知的组件。

本章节涵盖以下主题：

- [创建监听器](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#setting-up-listeners)
- [通知如何工作](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html#how-notification-works)

**创建监听器**

`RowSet`对象的监听器是从`RowSetListener`接口实现以下方法的组件：

 -  `cursorMoved`：定义当`RowSet`对象中的游标移动时侦听器将执行的操作（如果有）。
 -  `rowChanged`：定义监听器将执行的操作（如果有），行中的一个或多个列值发生更改，插入行或删除行时。
 -  `rowSetChanged`：定义在使用新数据填充`RowSet`对象时监听器将执行的操作（如果有）。

可能希望成为监听器的组件示例是`BarGraph`对象，该对象用于绘制`RowSet`对象中的数据。随着数据的变化，`BarGraph`对象可以自行更新以反映新数据。

作为应用程序程序员，利用通知机制必须做的唯一事情是添加或删除监听器。以下代码行表示每次`crs`对象的游标移动时，`crs`中的值都会更改，或者`crs`作为一个整体获取新数据，`BarGraph`对象`bar`将被通知：

```java
crs.addRowSetListener(bar);
```

您还可以通过删除监听器来停止通知，如以下代码行中所示：

```java
crs.removeRowSetListener(bar);
```

Coffee Break 场景中，假设总部定期检查数据库，以获取其在线销售的咖啡的最新价目表。在这种情况下，监听器是 Coffee Break 网站上的`PriceList`对象`priceList`，它必须实现`RowSetListener`方法`cursorMoved`，`rowChanged`和`rowSetChanged`。`cursorMoved`方法的实现可能是什么都不做，因为游标的位置不会影响`priceList`对象。另一方面，`rowChanged`和`rowSetChanged`方法的实现必须确定已进行了哪些更改并相应地更新`priceList`。

**通知如何工作**

在参考实现中，导致任何`RowSet`事件的方法会自动通知所有已注册的监听器。例如，任何移动游标的方法也会在每个监听器上调用方法`cursorMoved`。类似地，方法`execute`在所有监听器上调用方法`rowSetChanged`，而`acceptChanges`在所有监听器上调用`rowChanged`。

**发送大量数据**

示例代码 [`CachedRowSetSample.testCachedRowSet`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 展示了如何将大量数据分片发送。

