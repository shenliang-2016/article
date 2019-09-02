### 使用 Array 对象

**注意：**MySQL 和 Java DB 目前不支持 `ARRAY` SQL 数据类型。因此，没有可用的 JDBC 例子可以展示 `Array` JDBC 数据类型的使用。

本章节涵盖以下主题：

- [创建 Array 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/array.html#creating_array)
- [检索和访问 ResultSet 中的 Array 值](https://docs.oracle.com/javase/tutorial/jdbc/basics/array.html#retrieving_array)
- [存储和更新 Array 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/array.html#storing_array)
- [释放 Array 资源](https://docs.oracle.com/javase/tutorial/jdbc/basics/array.html#releasing_array)

**创建 Array 对象**

使用 `Connection.createArrayOf` 方法来创建 `Array` 对象。

比如，假设你的数据库包含一张名为 `REGIONS` 的表，已经使用下面的 SQL 语句创建并填充。注意，这些语句的语法可能会因为你的数据库而有所不同：

```sql
create table REGIONS
    (REGION_NAME varchar(32) NOT NULL,
    ZIPS varchar32 ARRAY[10] NOT NULL,
    PRIMARY KEY (REGION_NAME));

insert into REGIONS values(
    'Northwest',
    '{"93101", "97201", "99210"}');
insert into REGIONS values(
    'Southwest',
    '{"94105", "90049", "92027"}');
```

```java
Connection con = DriverManager.getConnection(url, props);
String [] northEastRegion = { "10022", "02110", "07399" };
Array aArray = con.createArrayOf("VARCHAR", northEastRegionnewYork);
```

Oracle Database JDBC 驱动以 `oracle.sql.ARRAY` 类实现 `java.sql.Array` 接口。

**检索和访问 ResultSet 中的 Array 值**

使用 JDBC 4.0 大对象接口（`Blob`，`Clob`，`NClob`），你可以不需要将所有数据从数据库服务器上获取到你的客户端机器上就能操作表中的 `Array` 对象。`Array`对象将它表示的SQL `ARRAY`实现为结果集或 Java 数组。

以下摘录检索`ZIPS`列中的SQL `ARRAY`值，并将其分配给`java.sql.Array`对象`z`对象。摘录检索`z`的内容并将其存储在`zips`中，这是一个包含`String`类型对象的 Java 数组。摘录遍历`zips`数组并检查每个邮政（`zip`）代码是否有效。此代码假定先前已使用方法`isValid`定义`ZipCode`类，如果给定的邮政编码与有效邮政编码的主列表中的某个邮政编码匹配，则返回`true`：

```java
ResultSet rs = stmt.executeQuery(
    "SELECT region_name, zips FROM REGIONS");

while (rs.next()) {
    Array z = rs.getArray("ZIPS");
    String[] zips = (String[])z.getArray();
    for (int i = 0; i < zips.length; i++) {
        if (!ZipCode.isValid(zips[i])) {
            // ...
            // Code to display warning
        }
    }
}
```

下面的语句中，`ResultSet` 方法 `getArray` 返回作为 `java.sql.Array` 对象 `z` 的当前行中的 `ZIPS` 列中存储的值：

```java
Array z = rs.getArray("ZIPS");
```

变量*z*包含一个定位符，它是服务器上SQL `ARRAY`的逻辑指针；它不包含`ARRAY`本身的元素。作为逻辑指针，*z*可用于操作服务器上的数组。

在以下行中，`getArray`是`Array.getArray`方法，而不是上一行中使用的`ResultSet.getArray`方法。因为`Array.getArray`方法返回 Java 编程语言中的`Object`，并且因为每个邮政编码都是`String`对象，所以在分配给变量`zips`之前，结果将转换为`String`对象数组。

```java
String[] zips = (String[])z.getArray();
```

`Array.getArray`方法将客户端上的SQL `ARRAY`元素实现为`String`对象的数组。因为实际上变量*zips*包含数组的元素，所以可以在`for`循环中遍历`zip`，查找无效的邮政编码。

**存储和更新 Array 对象**

使用`PreparedStatement.setArray`和`PreparedStatement.setObject`方法将`Array`值作为输入参数传递给`PreparedStatement`对象。

以下示例将`Array`对象`northEastRegion`（在前面的示例中创建）设置为`PreparedStatement pstmt`的第二个参数：

```java
PreparedStatement pstmt = con.prepareStatement(
    "insert into REGIONS (region_name, zips) " + "VALUES (?, ?)");
pstmt.setString(1, "NorthEast");
pstmt.setArray(2, northEastRegion);
pstmt.executeUpdate();
```

类似地，使用 `PreparedStatement.updateArray` 和 `PreparedStatement.updateObject` 来更新表中的 `Array` 值。

**释放 Array 资源**

`Array` 对象至少在创建它们的事务持续时间内保持有效。这可能导致应用程序在长时间运行的事务期间耗尽资源。应用程序可以通过调用其`free`方法来释放`Array`资源。

在下面的摘录中，调用方法`Array.free`以释放为先前创建的`Array`对象保留的资源。

```java
Array aArray = con.createArrayOf("VARCHAR", northEastRegionnewYork);
// ...
aArray.free();
```

