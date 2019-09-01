### 使用高级数据类型

本节中介绍的高级数据类型为关系数据库提供了更多的灵活性，可以用作表列的值。例如，列可用于存储`BLOB`（二进制大对象）值，这些值可以将非常大量的数据存储为原始字节。列也可以是`CLOB`类型（字符大对象），它能够以字符格式存储非常大量的数据。

最新版本的 ANSI/ISO SQL 标准通常称为 SQL:2003。本标准规定了以下数据类型：

- SQL92 内建类型，包括大家熟悉的 SQL 列类型诸如 `CHAR`， `FLOAT`，和 `DATE`

- SQL99 内建类型，包括 SQL99 添加的类型：

  - `BOOLEAN`：布尔值 (`true` or `false`)
  - `BLOB`：二进制大对象
  - `CLOB`：字符大对象

- SQL:2003 添加的新的内建类型：

  - `XML`：XML 对象

- 用户定义类型：

  - 结构化类型：用户定义类型；比如：

    ```sql
    CREATE TYPE PLANE_POINT
    AS (X FLOAT, Y FLOAT) NOT FINAL
    ```

  - `DISTINCT` 类型：基于内建类型的用户定义类型；比如：

    ```sql
    CREATE TYPE MONEY
    AS NUMERIC(10,2) FINAL
    ```

- 结构化类型：基于给定基类型的新类型：

  - `REF(*structured-type*)`：持久表示驻留在数据库中的结构化类型的实例的指针
  - `*base-type* ARRAY[*n*]`：*n*个基类型元素的数组

- 定位器：作为驻留在数据库服务器上的数据的逻辑指针的实体。定位器存在于客户端计算机中，是指向服务器上数据的瞬态逻辑指针。定位器通常指的是太大而无法在客户端上实现的数据，例如图像或音频。 （*物化视图*是作为模式对象预先存储或“物化”的查询结果。）在SQL级别定义了运算符，以检索由定位符表示的随机访问的数据片段：

  - `LOCATOR(*structured-type*)`：服务器上一个结构化实例的定位器
  - `LOCATOR(*array*)`：服务器上一个数组的定位器
  - `LOCATOR(*blob*)`：服务器上一个二进制大对象的定位器
  - `LOCATOR(*clob*)`：服务器上一个字符大对象的定位器

- `Datalink`：用于管理数据源外部数据的类型。`Datalink`值是 SQL MED（外部数据管理）的一部分，是 SQL ANSI/ISO 标准规范的一部分。

**映射高级数据类型**

JDBC API 为 SQL:2003 标准指定的高级数据类型提供默认映射。以下列表给出了数据类型以及它们映射到的接口或类：

 - `BLOB`：`Blob`接口
 - `CLOB`：`Clob`接口
 - `NCLOB`：`NClob`接口
 - `ARRAY`：`Array`接口
 - `XML`：`SQLXML`接口
 - 结构化类型：`Struct`接口
 - `REF（结构化类型）`：`Ref`接口
 - `ROWID`：`RowId`接口
 - `DISTINCT`：基类型映射到的类型。 例如，基于SQL`NUMERIC`类型的`DISTINCT`值映射到`java.math.BigDecimal`类型，因为`NUMERIC`映射到Java编程语言中的`BigDecimal`。
 - `DATALINK`：`java.net.URL`对象

**使用高级数据类型**

您可以像处理其他数据类型一样检索，存储和更新高级数据类型。您可以使用`ResultSet.getDataType`或`CallableStatement.getDataType`方法来检索它们，使用`PreparedStatement.setDataType`方法来存储它们，使用`ResultSet.updateDataType`方法来更新它们。（变量`DataType`是映射到高级数据类型的Java接口或类的名称。）可能在高级数据类型上执行的操作的 90％ 涉及使用`getDataType`，`setDataType`和`updateDataType`方法。下表显示了要使用的方法：

| **Advanced Data Type** | **getDataType Method** | **setDataType method** | **updateDataType Method** |
| ---------------------- | ---------------------- | ---------------------- | ------------------------- |
| `BLOB`                 | `getBlob`              | `setBlob`              | `updateBlob`              |
| `CLOB`                 | `getClob`              | `setClob`              | `updateClob`              |
| `NCLOB`                | `getNClob`             | `setNClob`             | `updateNClob`             |
| `ARRAY`                | `getArray`             | `setArray`             | `updateArray`             |
| `XML`                  | `getSQLXML`            | `setSQLXML`            | `updateSQLXML`            |
| `Structured type`      | `getObject`            | `setObject`            | `updateObject`            |
| `REF(structured type)` | `getRef`               | `setRef`               | `updateRef`               |
| `ROWID`                | `getRowId`             | `setRowId`             | `updateRowId`             |
| `DISTINCT`             | `getBigDecimal`        | `setBigDecimal`        | `updateBigDecimal`        |
| `DATALINK`             | `getURL`               | `setURL`               | `updateURL`               |

**注意**：`DISTINCT`数据类型与其他高级SQL数据类型的行为不同。作为基于已存在的内置类型的用户定义类型，它没有接口作为Java编程语言中的映射。因此，您使用与`DISTINCT`数据类型所基于的Java类型对应的方法。有关详细信息，请参阅  [Using DISTINCT Data Type](https://docs.oracle.com/javase/tutorial/jdbc/basics/distinct.html) 。

例如，以下代码片段检索SQL`ARRAY`值。对于此示例，假设表`STUDENTS`中的`SCORES`列包含`ARRAY`类型的值。变量`stmt`是一个`Statement`对象。

```java
ResultSet rs = stmt.executeQuery(
    "SELECT SCORES FROM STUDENTS " +
    "WHERE ID = 002238");
rs.next();
Array scores = rs.getArray("SCORES");
```

变量`scores`是存储在表`STUDENTS`中的学生`002238`行中的SQL`ARRAY`对象的逻辑指针。

如果要在数据库中存储值，可以使用适当的`set`方法。例如，下面的代码片段，其中`rs`是`ResultSet`对象，存储一个`Clob`对象：

```java
Clob notes = rs.getClob("NOTES");
PreparedStatement pstmt =
    con.prepareStatement(
        "UPDATE MARKETS SET COMMENTS = ? " +
        "WHERE SALES < 1000000");
pstmt.setClob(1, notes);
pstmt.executeUpdate();
```

此代码将`notes`设置为发送到数据库的`update`语句中的第一个参数。由`notes`指定的`Clob`值将存储在表`MARKETS`中的每一行中的`COMMENTS`列中，其中`SALES`列中的值小于一百万。

