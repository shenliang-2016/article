### 使用 RowSet 对象

JDBC `RowSet`对象以一种比结果集更灵活，更易于使用的方式保存表格数据。

Oracle为`RowSet`的一些更流行的用途定义了五个`RowSet`接口，并且这些`RowSet`接口可以使用标准引用。在本教程中，您将学习如何使用这些参考实现。

这些版本的`RowSet`接口及其实现是为了方便程序员而提供的。程序员可以自由编写自己的`javax.sql.RowSet`接口版本，扩展五个`RowSet`接口的实现，或编写自己的实现。但是，许多程序员可能会发现标准参考实现已经满足他们的需求并将按原样使用它们。

本节向您介绍`RowSet`接口以及扩展此接口的以下接口：

- `JdbcRowSet`
- `CachedRowSet`
- `WebRowSet`
- `JoinRowSet`
- `FilteredRowSet`

涵盖以下主题：

- [RowSet 对象能干什么？](https://docs.oracle.com/javase/tutorial/jdbc/basics/rowset.html#what_can_rowset_objects_do)
- [RowSet 对象种类](https://docs.oracle.com/javase/tutorial/jdbc/basics/rowset.html#kinds_of_rowset_objects)

**RowSet 对象能干什么？**

所有的 `RowSet` 对象都派生自 `ResultSet` 接口，因而共享它的所有能力。使得 JDBC `RowSet` 具有特殊性的是添加了以下新能力：

- [作为 JavaBeans 组件](https://docs.oracle.com/javase/tutorial/jdbc/basics/rowset.html#javabeans)
- [添加可滚动性和可更新性](https://docs.oracle.com/javase/tutorial/jdbc/basics/rowset.html#scrollability)

**作为 JavaBeans Component**

所有的 `RowSet` 对象都是 JavaBeans 组件。这意味着它们拥有：

- 属性
- JavaBeans 通知机制

**属性**

所有 `RowSet` 对象都拥有属性。一个属性是一个拥有相应 getter 和 setter 方法的字段。属性被暴露给构建工具（诸如那些随 IDEs JDeveloper 和 Eclipse 提供的）以允许你可视化维护 beans 。跟多信息请参考 [JavaBeans](https://docs.oracle.com/javase/tutorial/javabeans/) 课程中的 [Properties](https://docs.oracle.com/javase/tutorial/javabeans/writing/properties.html) 部分。

**JavaBeans 通知机制** 

`RowSet` 对象使用 JavaBeans 事件模型，注册于其中的组件当特定事件发生时会被通知。对所有的 `RowSet` 对象，三类事件会触发通知：

- 游标移动
- 更新、插入、或者删除一行
- 整个 `RowSet` 内容的改变

事件通知会到达所有的*监听器*，这些所谓的监听器组件实现了 `RowSetListener` 接口，并将自身添加到 `RowSet` 对象的三类事件发生时的通知列表中。

监听器可以是 GUI 组件，例如柱状图。如果柱状图正在跟踪`RowSet`对象中的数据，则只要数据发生更改，监听器就会想知道新的数据值。因此，监听器将实现`RowSetListener`方法，以定义在特定事件发生时它将执行的操作。然后，还必须将监听器添加到`RowSet`对象的监听器列表中。以下代码行使用`RowSet`对象`rs`注册柱状图组件`bg`。

```java
rs.addListener(bg);
```

现在每次光标移动，更改行或者所有`rs`都获得新数据时，都会通知`bg`。

**添加可滚动性或者可更新性**

一些 DBMS 不支持可滚动的结果集，另外一些不支持可更新的结果集。如果驱动程序没有为这些 DBMS 添加可滚动和可更新结果集能力，你就可以使用`RowSet` 对象来实现。`RowSet` 对象默认是可滚动和可更新的，因此通过使用结果集的内容产生一个 `RowSet` 对象，你就可以有效地将结果集变成可滚动和可更新的。

**RowSet 对象种类**

`RowSet`对象被视为已连接的或已断开连接的。*连接的*`RowSet`对象使用 JDBC 驱动程序建立与关系数据库的连接，并在整个生命周期内维护该连接。*断开连接的*`RowSet`对象仅与数据源建立连接，以从`ResultSet`对象读取数据或将数据写回数据源。从数据源读取数据或向其数据源写入数据后，`RowSet`对象与其断开连接，从而变为“断开连接”。在其生命周期的大部分时间内，断开连接的`RowSet`对象与其数据源没有连接并且独立运行。接下来的两个部分将告诉您连接或断开连接意味着`RowSet`对象可以执行的操作。

**已连接的 RowSet 对象**

只有一个标准`RowSet`实现是连接的`RowSet`对象：`JdbcRowSet`。始终连接到数据库时，`JdbcRowSet`对象与`ResultSet`对象最相似，并且通常用作包装器，以使其他不可滚动且只读的`ResultSet`对象可滚动和可更新。

作为 JavaBeans 组件，可以使用`JdbcRowSet`对象，例如，在 GUI 工具中选择 JDBC 驱动程序。可以通过这种方式使用`JdbcRowSet`对象，因为它实际上是获取其与数据库的连接的驱动程序的包装器。

**断开连接的 RowSet 对象**

其他四个实现是断开连接的`RowSet`实现。断开连接的`RowSet`对象具有连接的`RowSet`对象的所有功能，并且它们具有仅对断开连接的`RowSet`对象可用的附加功能。例如，不必维护与数据源的连接，使得断开连接的`RowSet`对象比`JdbcRowSet`对象或`ResultSet`对象轻得多。断开连接的`RowSet`对象也是可序列化的，并且可序列化和轻量级的组合使它们成为通过网络发送数据的理想选择。它们甚至可以用于向瘦客户端（如 PDA 和移动电话）发送数据。

`CachedRowSet`接口定义了所有未连接的`RowSet`对象可用的基本功能。其他三个是`CachedRowSet`接口的扩展，它提供了更多的专用功能。以下信息显示了它们的相关性：

`CachedRowSet`对象具有`JdbcRowSet`对象的所有功能，并且还可以执行以下操作：

 - 获取与数据源的连接并执行查询
 - 从生成的`ResultSet`对象中读取数据，并使用该数据填充自身
 - 在断开连接时处理数据并对数据进行更改
 - 重新连接到数据源以将更改写回其中
 - 检查与数据源的冲突并解决这些冲突

`WebRowSet`对象具有`CachedRowSet`对象的所有功能，并且还可以执行以下操作：

 - 将自己写为 XML 文档
 - 读取描述 `WebRowSet` 对象的 XML 文档

`JoinRowSet`对象具有`WebRowSet`对象的所有功能（因此也具有`CachedRowSet`对象的功能），还可以执行以下操作：

 - 形成等效的`SQL JOIN`而无需连接到数据源

`FilteredRowSet`对象同样具有`WebRowSet`对象的所有功能（因此也是`CachedRowSet`对象），并且还可以执行以下操作：

 - 应用过滤条件，以便只显示选定的数据。这相当于在`RowSet`对象上执行查询，而不必使用查询语言或连接到数据源。

