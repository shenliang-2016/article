### 使用 DISTINCT 数据类型

**注意：**MySQL 和 Java DB 当前不支持`DISTINCT` SQL数据类型。因此，没有 JDBC 教程示例可用于演示本节中描述的功能。

`DISTINCT`数据类型的行为与其他高级SQL数据类型不同。作为基于已存在的内置类型之一的用户定义类型，它没有接口作为 Java 编程语言中的映射。相反，`DISTINCT`数据类型的标准映射是其基础SQL数据类型映射到的Java类型。

为了说明以上问题，创建一个`DISTINCT`数据类型，然后查看如何检索，设置或更新它。假设您始终对状态使用双字母缩写，并希望创建用于这些缩写的`DISTINCT`数据类型。您可以使用以下SQL语句定义新的`DISTINCT`数据类型：

```sql
CREATE TYPE STATE AS CHAR(2);
```

某些数据库使用不同的语法来创建`DISTINCT`数据类型，如以下代码行所示：

```sql
CREATE DISTINCT TYPE STATE AS CHAR(2);
```

如果一种语法不起作用，您可以尝试另一种语法。或者，您可以查看驱动程序的文档以查看其预期的确切语法。

这些语句创建一个新的数据类型`STATE`，它可以用作列值或SQL结构类型的属性值。因为`STATE`类型的值实际上是两个`CHAR`类型的值，所以使用检索`CHAR`值相同的方法来检索它，即`getString`。例如，假设`ResultSet rs`的第四列存储类型为`STATE`的值，则以下代码行检索其值：

```sql
String state = rs.getString(4);
```

类似地，您将使用方法`setString`在数据库中存储`STATE`值，并使用方法`updateString`来修改其值。

### 使用 Structured 对象

**注意：** MySQL和Java DB目前不支持用户定义的类型。 因此，没有JDBC教程示例可用于演示本节中描述的功能。

本章节涵盖以下主题：

- [结构化类型概述](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlstructured.html#overview_structured)
- [在结构化类型中使用 DISTINCT 类型](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlstructured.html#using_distinct_in_structured)
- [使用结构化类型的引用](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlstructured.html#references_structured)
- [创建 SQL REF 对象示例代码](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlstructured.html#code_ref)
- [使用用户自定义类型作为列值](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlstructured.html#udt_column_values)
- [将用户自定义类型数据插入表](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlstructured.html#insert_udt)

**结构化类型概述**

SQL结构化类型和`DISTINCT`类型是用户可以在SQL中定义的两种数据类型。它们通常被称为UDT（用户定义的类型），您可以使用SQL `CREATE TYPE`语句创建它们。

回到 The Coffee Break 的例子，假设店主已经超出了所有人的预期，并且一直在扩展新的分支机构。店主已决定将`STORES`表添加到包含有关每个企业的信息的数据库中。`STORES`将有四列：

- `STORE_NO` 每个咖啡店的 ID 号
- `LOCATION` 咖啡店地址
- `COF_TYPES` 咖啡店销售的咖啡for the coffees it sells
- `MGR` 店长的名字

所有者将列`LOCATION`设置为SQL结构化类型，列`COF_TYPES`为SQL` ARRAY`，列`MGR`为`REF(MANAGER)`，其中`MANAGER`为SQL结构化类型。

店主必须首先为地址和经理定义新的结构化类型。SQL结构化类型类似于Java编程语言中的结构化类型，因为它具有可为任何数据类型的成员，称为属性。店主编写以下SQL语句以创建新数据类型`ADDRESS`：

```sql
CREATE TYPE ADDRESS
(
    NUM INTEGER,
    STREET VARCHAR(40),
    CITY VARCHAR(40),
    STATE CHAR(2),
    ZIP CHAR(5)
);
```

在此语句中，新类型`ADDRESS`具有五个属性，类似于Java类中的字段。属性`NUM`是`INTEGER`，属性`STREET`是`VARCHAR(40)`，属性`CITY`是`VARCHAR(40)`，属性`STATE`是`CHAR(2)`，属性`ZIP`是`CHAR(5)`。

以下摘录（其中`con`是有效的`Connection`对象）将`ADDRESS`的定义发送到数据库：

```java
String createAddress =
    "CREATE TYPE ADDRESS " +
    "(NUM INTEGER, STREET VARCHAR(40), " +
    "CITY VARCHAR(40), STATE CHAR(2), ZIP CHAR(5))";
Statement stmt = con.createStatement();
stmt.executeUpdate(createAddress);
```

现在，`ADDRESS`结构化类型作为数据类型在数据库中注册，并且店主可以将其用作表列的数据类型或其它结构化类型的属性。

**在结构化类型中使用 DISTINCT 类型**

The Coffee Break 的店主计划在新的结构化类型`MANAGER`中包含的属性之一是经理的电话号码。因为店主将始终将电话号码列为10位数字（以确保它包含区号）并且永远不会将其作为数字进行操作，所以店主决定定义一个名为`PHONE_NO`的新类型，该类型由10个字符组成。此数据类型的SQL定义（可以被视为仅具有一个属性的结构化类型）如下所示：

```sql
CREATE TYPE PHONE_NO AS CHAR(10);
```

或者，如前所述，对于某些驱动程序，定义可能如下所示：

```sql
CREATE DISTINCT TYPE PHONE_NO AS CHAR(10);
```

`DISTINCT`类型始终基于另一种数据类型，该类型必须是预定义类型。换句话说，`DISTINCT`类型不能基于用户定义的类型（UDT）。要检索或设置`DISTINCT`类型的值，请对基础类型（它所基于的类型）使用适当的方法。例如，要检索基于`CHAR`类型的`PHONE_NO`实例，您将使用方法`getString`，因为这是检索`CHAR`的方法。

假设`PHONE_NO`类型的值位于`ResultSet`对象*rs*的当前行的第四列中，则以下代码行检索它：

```java
String phoneNumber = rs.getString(4);
```

类似地，以下代码行设置一个输入参数，该参数的类型为`PHONE_NO`，用于发送到数据库的预编译语句：

```java
pstmt.setString(1, phoneNumber);
```

添加到前面的代码片段，`PHONE_NO`的定义将使用以下代码行发送到数据库：

```java
stmt.executeUpdate(
    "CREATE TYPE PHONE_NO AS CHAR(10)");
```

在数据库中注册`PHONE_NO`类型后，店主可以将其用作表中的列类型或结构化类型中属性的数据类型。以下SQL语句中的`MANAGER`定义使用`PHONE_NO`作为属性`PHONE`的数据类型：

```sql
CREATE TYPE MANAGER
(
    MGR_ID INTEGER,
    LAST_NAME VARCHAR(40),
    FIRST_NAME VARCHAR(40),
    PHONE PHONE_NO
);
```

重用前面定义的`stmt`，以下代码片段将结构化类型`MANAGER`的定义发送到数据库：

```java
  String createManager =
    "CREATE TYPE MANAGER " +
    "(MGR_ID INTEGER, LAST_NAME " +
    "VARCHAR(40), " +
    "FIRST_NAME VARCHAR(40), " +
    "PHONE PHONE_NO)";
  stmt.executeUpdate(createManager);
```

**使用结构化类型的引用**

The Coffee Break 的店主创建了三种新数据类型，用作数据库中的列类型或属性类型：结构化类型`LOCATION`和`MANAGER`，以及`DISTINCT`类型`PHONE_NO`。店主使用`PHONE_NO`作为新类型`MANAGER`中属性`PHONE`的类型，并使用`ADDRESS`作为表`STORES`中`LOCATION`列的数据类型。`MANAGER`类型可以用作`MGR`列的类型，但店主更喜欢使用`REF(MANAGER)`类型，因为店主通常有一个人管理两个或三个商店。使用`REF(MANAGER)`作为列类型可避免在一个人管理多个商店时重复`MANAGER`的所有数据。

使用已创建的结构化类型`MANAGER`，店主现在可以创建一个包含可以引用的`MANAGER`实例的表。对`MANAGER`实例的引用将具有`REF(MANAGER)`类型。SQL `REF`只不过是指向结构化类型的逻辑指针，因此`REF(MANAGER)`的实例充当指向`MANAGER`实例的逻辑指针。

因为SQL `REF`值需要与它引用的结构化类型的实例永久关联，所以它与其关联的实例一起存储在特殊表中。程序员不直接创建`REF`类型，而是创建将存储可引用的特定结构化类型的实例的表。每个要引用的结构化类型都有自己的表。将结构化类型的实例插入表中时，数据库会自动创建`REF`实例。例如，要包含可以引用的`MANAGER`实例，所有者使用SQL创建以下特殊表：

```sql
  CREATE TABLE MANAGERS OF MANAGER
  (OID REF(MANAGER)
  VALUES ARE SYSTEM GENERATED);
```

此语句创建一个具有特殊列`OID`的表，该列存储`REF(MANAGER)`类型的值。每次将`MANAGER`实例插入表中时，数据库将生成`REF(MANAGER)`实例并将其存储在列`OID`中。隐含地，附加列还存储已插入表中的`MANAGER`的每个属性。例如，以下代码片段显示了店主如何创建三个`MANAGER`结构化类型的实例来表示三个店长：

```sql
  INSERT INTO MANAGERS (
    MGR_ID, LAST_NAME,
    FIRST_NAME, PHONE) VALUES
  (
    000001,
    'MONTOYA',
    'ALFREDO',
    '8317225600'
  );

  INSERT INTO MANAGERS (
    MGR_ID, LAST_NAME,
    FIRST_NAME, PHONE) VALUES
  (
    000002,
    'HASKINS',
    'MARGARET',
    '4084355600'
  );

  INSERT INTO MANAGERS (
    MGR_ID, LAST_NAME,
    FIRST_NAME, PHONE) VALUES
  (
    000003,
    'CHEN',
    'HELEN',
    '4153785600'
   );
```

表`MANAGERS`现在将有三行，到目前为止插入的每个店长都有一行。列`OID`将包含三个类型为`REF(MANAGER)`的唯一对象标识符，每个对象用于`MANAGER`的每个实例。这些对象标识符由数据库自动生成，并将永久存储在表`MANAGERS`中。隐式地，附加列存储`MANAGER`的每个属性。例如，在表`MANAGERS`中，一行包含引用`Alfredo Montoya`的`REF(MANAGER)`，另一行包含引用`Margaret Haskins`的`REF(MANAGER)`，第三行包含引用`Helen Chen`的`REF(MANAGER)`。

要访问`REF(MANAGER)`实例，请从其表中选择它。例如，店主检索了对`Alfredo Montoya`的引用，其ID号为 000001，使用以下代码片段：

```java
  String selectMgr =
    "SELECT OID FROM MANAGERS " +
    "WHERE MGR_ID = 000001";
  ResultSet rs = stmt.executeQuery(selectMgr);
  rs.next();
  Ref manager = rs.getRef("OID");
```

现在变量`manager`可以用作引用`Alfredo Montoya`的列值。

**创建 SQL REF 对象示例代码**

下面的代码示例创建表`MANAGERS`，一个可以引用的结构化类型`MANAGER`的实例表，并将三个`MANAGER`实例插入到表中。此表中的列`OID`将存储`REF(MANAGER)`的实例。执行此代码后，`MANAGERS`表将为插入的三个`MANAGER`对象中的每一个都有一行，`OID`列中的值将是`REF(MANAGER)`类型，用于标识存储在该行中的`MANAGER`实例。

```java
package com.oracle.tutorial.jdbc;

import java.sql.*;

public class CreateRef {

    public static void main(String args[]) {

        JDBCTutorialUtilities myJDBCTutorialUtilities;
        Connection myConnection = null;

        if (args[0] == null) {
            System.err.println("Properties file not specified " +
                               "at command line");
            return;
        } else {
            try {
                myJDBCTutorialUtilities = new JDBCTutorialUtilities(args[0]);
            } catch (Exception e) {
                System.err.println("Problem reading properties " +
                                   "file " + args[0]);
                e.printStackTrace();
                return;
            }
        }

        Connection con = null;
        Statement stmt = null;

        try {
            String createManagers =
                "CREATE TABLE " +
                "MANAGERS OF MANAGER " +
                "(OID REF(MANAGER) " +
                "VALUES ARE SYSTEM " +
                "GENERATED)";

            String insertManager1 =
                "INSERT INTO MANAGERS " +
                "(MGR_ID, LAST_NAME, " +
                "FIRST_NAME, PHONE) " +
                "VALUES " +
                "(000001, 'MONTOYA', " +
                "'ALFREDO', " +
                "'8317225600')";

            String insertManager2 =
                "INSERT INTO MANAGERS " +
                "(MGR_ID, LAST_NAME, " +
                "FIRST_NAME, PHONE) " +
                "VALUES " +
                "(000002, 'HASKINS', " +
                "'MARGARET', " +
                "'4084355600')";

            String insertManager3 =
                "INSERT INTO MANAGERS " +
                "(MGR_ID, LAST_NAME, " +
                "FIRST_NAME, PHONE) " +
                "VALUES " +
                "(000003, 'CHEN', 'HELEN', " +
                "'4153785600')";
  
            con = myJDBCTutorialUtilities.getConnection();
            con.setAutoCommit(false);

            stmt = con.createStatement();
            stmt.executeUpdate(createManagers);

            stmt.addBatch(insertManager1);
            stmt.addBatch(insertManager2);
            stmt.addBatch(insertManager3);
            int [] updateCounts = stmt.executeBatch();

            con.commit();

            System.out.println("Update count for:  ");
            for (int i = 0; i < updateCounts.length; i++) {
                System.out.print("    command " + (i + 1) + " = ");
                System.out.println(updateCounts[i]);
            }
        } catch(BatchUpdateException b) {
            System.err.println("-----BatchUpdateException-----");
            System.err.println("Message:  " + b.getMessage());
            System.err.println("SQLState:  " + b.getSQLState());
            System.err.println("Vendor:  " + b.getErrorCode());
            System.err.print("Update counts for " + "successful commands:  ");
            int [] rowsUpdated = b.getUpdateCounts();
            for (int i = 0; i < rowsUpdated.length; i++) {
                System.err.print(rowsUpdated[i] + "   ");
            }
            System.err.println("");
        } catch(SQLException ex) {
            System.err.println("------SQLException------");
            System.err.println("Error message:  " + ex.getMessage());
            System.err.println("SQLState:  " + ex.getSQLState());
            System.err.println("Vendor:  " + ex.getErrorCode());
        } finally {
            if (stmt != null) { stmt.close(); }
              JDBCTutorialUtilities.closeConnection(con);
        }
    }
}
```

**使用用户自定义类型作为列值**

店主现在拥有创建表`STORES`所需的UDT。结构化类型`ADDRESS`是列`LOCATION`的类型，类型`REF(MANAGER)`是列`MGR`的类型。

UDT `COF_TYPES`基于SQL数据类型`ARRAY`，是`COF_TYPES`列的类型。以下代码行将`COF_ARRAY`类型创建为具有10个元素的`ARRAY`值。`COF_ARRAY`的基本类型是`VARCHAR(40)`。

```sql
  CREATE TYPE COF_ARRAY AS ARRAY(10) OF VARCHAR(40);
```

定义了新的数据类型后，以下SQL语句将创建表`STORES`：

```sql
  CREATE TABLE STORES
  (
    STORE_NO INTEGER,
    LOCATION ADDRESS,
    COF_TYPES COF_ARRAY,
    MGR REF(MANAGER)
  );
```

**将用户自定义类型数据插入表**

以下代码片段在`STORES`表中插入一行，按以下顺序提供`STORE_NO`，`LOCATION`，`COF_TYPES`和`MGR`列的值：

```sql
  INSERT INTO STORES VALUES
  (
    100001,
    ADDRESS(888, 'Main_Street',
      'Rancho_Alegre',
      'CA', '94049'),
    COF_ARRAY('Colombian', 'French_Roast',
      'Espresso', 'Colombian_Decaf',
      'French_Roast_Decaf'),
    SELECT OID FROM MANAGERS
      WHERE MGR_ID = 000001
  );
```

以下内容遍历每列并插入其中的值。

```
  STORE_NO: 100001
```

此列的类型为`INTEGER`，数字`100001`是`INTEGER`类型，类似于之前在表`COFFEES`和`SUPPLIERS`中创建的条目。

```
  LOCATION: ADDRESS(888, 'Main_Street',
    'Rancho_Alegre', 'CA', '94049')
```

此列的类型是结构化类型`ADDRESS`，此值是`ADDRESS`实例的构造函数。当我们发送`ADDRESS`的定义到数据库时，它所做的一件事就是为新类型创建一个构造函数。括号中的逗号分隔值是`ADDRESS`类型属性的初始化值，它们必须按照`ADDRESS`类型定义中列出属性的顺序出现。`888`是属性`NUM`的值，它是`INTEGER`值。`"Main_Street"`是`STREET`的值，`"Rancho_Alegre"`是`CITY`的值，两个属性都是`VARCHAR(40)`类型。属性`STATE`的值是`"CA"`，其类型为`CHAR(2)`，属性`ZIP`的值是`"94049"`，其类型为`CHAR(5)`。

```
  COF_TYPES: COF_ARRAY(
    'Colombian',
    'French_Roast',
    'Espresso',
    'Colombian_Decaf',
    'French_Roast_Decaf'),
```

`COF_TYPES`列的类型为`COF_ARRAY`，基类型为`VARCHAR(40)`，括号内的逗号分隔值是作为数组元素的`String`对象。店主将类型`COF_ARRAY`定义为最多包含10个元素。这个数组有5个元素，因为店主只为它提供了5个`String`对象。

```
  MGR: SELECT OID FROM MANAGERS
    WHERE MGR_ID = 000001
```

列`MGR`是`REF(MANAGER)`类型，这意味着此列中的值必须是对结构化类型`MANAGER`的引用。`MANAGER`的所有实例都存储在表`MANAGERS`中。`REF(MANAGER)`的所有实例也存储在该表的`OID`列中。此表格行中描述的商店经理是`Alfredo Montoya`，他的信息存储在`MANAGER`实例中，该实例具有`100001`属性`MGR_ID`。要获取与`Alfredo Montoya`的`MANAGER`对象关联的`REF(MANAGER)`实例，请在表`MANAGERS`中选择`MGR_ID`为`100001`的行中的列`OID`。将存储在`STORES`表的`MGR`列中的值（`REF(MANAGER)`值）是DBMS生成的值，用于唯一标识`MANAGER`结构类型的此实例。

使用以下代码片段将前面的SQL语句发送到数据库：

```java
  String insertMgr =
    "INSERT INTO STORES VALUES " +
    "(100001, " +
    "ADDRESS(888, 'Main_Street', " +
      "'Rancho_Alegre', 'CA', " +
      "'94049'), " +
    "COF_ARRAY('Colombian', " +
      "'French_Roast', 'Espresso', " +
      "'Colombian_Decaf', " +
      "'French_Roast_Decaf'}, " +
    "SELECT OID FROM MANAGERS " +
    "WHERE MGR_ID = 000001)";

  stmt.executeUpdate(insertMgr);
```

但是，因为您要发送几个`INSERT INTO`语句，所以将它们作为批量更新一起发送将更有效，如下面的代码示例所示：

```java
package com.oracle.tutorial.jdbc;

import java.sql.*;

public class InsertStores {
    public static void main(String args[]) {

        JDBCTutorialUtilities myJDBCTutorialUtilities;
        Connection myConnection = null;

        if (args[0] == null) {
            System.err.println(
                "Properties file " +
                "not specified " +
                "at command line");
            return;
        } else {
            try {
                myJDBCTutorialUtilities = new
                    JDBCTutorialUtilities(args[0]);
            } catch (Exception e) {
                System.err.println(
                    "Problem reading " +
                    "properties file " +
                    args[0]);
                e.printStackTrace();
                return;
            }
        }

        Connection con = null;
        Statement stmt = null;

        try {
            con = myJDBCTutorialUtilities.getConnection();
            con.setAutoCommit(false);

            stmt = con.createStatement();

            String insertStore1 =
                "INSERT INTO STORES VALUES (" +
                "100001, " +
                "ADDRESS(888, 'Main_Street', " +
                    "'Rancho_Alegre', 'CA', " +
                    "'94049'), " +
                "COF_ARRAY('Colombian', " +
                    "'French_Roast', " +
                    "'Espresso', " +
                    "'Colombian_Decaf', " +
                    "'French_Roast_Decaf'), " +
                "(SELECT OID FROM MANAGERS " +
                "WHERE MGR_ID = 000001))";

            stmt.addBatch(insertStore1);

            String insertStore2 =
                "INSERT INTO STORES VALUES (" +
                "100002, " +
                "ADDRESS(1560, 'Alder', " +
                    "'Ochos_Pinos', " +
                    "'CA', '94049'), " +
                "COF_ARRAY('Colombian', " +
                    "'French_Roast', " +
                    "'Espresso', " +
                    "'Colombian_Decaf', " +
                    "'French_Roast_Decaf', " +
                    "'Kona', 'Kona_Decaf'), " +
                "(SELECT OID FROM MANAGERS " +
                "WHERE MGR_ID = 000001))";

            stmt.addBatch(insertStore2);

            String insertStore3 =
                "INSERT INTO STORES VALUES (" +
                "100003, " +
                "ADDRESS(4344, " +
                    "'First_Street', " +
                    "'Verona', " +
                    "'CA', '94545'), " +
                "COF_ARRAY('Colombian', " +
                    "'French_Roast', " +
                    "'Espresso', " +
                    "'Colombian_Decaf', " +
                    "'French_Roast_Decaf', " +
                    "'Kona', 'Kona_Decaf'), " +
                "(SELECT OID FROM MANAGERS " +
                "WHERE MGR_ID = 000002))";

            stmt.addBatch(insertStore3);

            String insertStore4 =
                "INSERT INTO STORES VALUES (" +
                "100004, " +
                "ADDRESS(321, 'Sandy_Way', " +
                    "'La_Playa', " +
                    "'CA', '94544'), " +
                "COF_ARRAY('Colombian', " +
                    "'French_Roast', " +
                    "'Espresso', " +
                    "'Colombian_Decaf', " +
                    "'French_Roast_Decaf', " +
                    "'Kona', 'Kona_Decaf'), " +
                "(SELECT OID FROM MANAGERS " +
                "WHERE MGR_ID = 000002))";

            stmt.addBatch(insertStore4);

            String insertStore5 =
                "INSERT INTO STORES VALUES (" +
                "100005, " +
                "ADDRESS(1000, 'Clover_Road', " +
                    "'Happyville', " +
                    "'CA', '90566'), " +
                "COF_ARRAY('Colombian', " +
                    "'French_Roast', " +
                    "'Espresso', " + 
                    "'Colombian_Decaf', " +
                    "'French_Roast_Decaf'), " +
                "(SELECT OID FROM MANAGERS " +
                "WHERE MGR_ID = 000003))";

            stmt.addBatch(insertStore5);

            int [] updateCounts = stmt.executeBatch();

            ResultSet rs = stmt.executeQuery(
                "SELECT * FROM STORES");
            System.out.println("Table STORES after insertion:");
            System.out.println("STORE_NO   " + "LOCATION   " +
                "COF_TYPE   " + "MGR");

            while (rs.next()) {
                int storeNo = rs.getInt("STORE_NO");
                Struct location = (Struct)rs.getObject("LOCATION");
                Object[] locAttrs = location.getAttributes();
                Array coffeeTypes = rs.getArray("COF_TYPE");
                String[] cofTypes = (String[])coffeeTypes.getArray();

                Ref managerRef = rs.getRef("MGR");
                PreparedStatement pstmt = con.prepareStatement(
                    "SELECT MANAGER " +
                    "FROM MANAGERS " +
                    "WHERE OID = ?");
  
                pstmt.setRef(1, managerRef);
                ResultSet rs2 = pstmt.executeQuery();
                rs2.next();
                Struct manager = (Struct)rs2.getObject("MANAGER");
                Object[] manAttrs = manager.getAttributes();
      
                System.out.print(storeNo + "   ");
                System.out.print(
                    locAttrs[0] + " " +
                    locAttrs[1] + " " +
                    locAttrs[2] + ", " +
                    locAttrs[3] + " " +
                    locAttrs[4] + " ");

                for (int i = 0; i < cofTypes.length; i++)
                    System.out.print( cofTypes[i] + " ");
          
                System.out.println(
                    manAttrs[1] + ", " +
                    manAttrs[2]);
        
                rs2.close();
                pstmt.close();
            }

            rs.close();

        } catch(BatchUpdateException b) {
            System.err.println("-----BatchUpdateException-----");
            System.err.println("SQLState:  " + b.getSQLState());
            System.err.println("Message:  " + b.getMessage());
            System.err.println("Vendor:  " + b.getErrorCode());
            System.err.print("Update counts:  ");
            int [] updateCounts = b.getUpdateCounts();

            for (int i = 0; i < updateCounts.length; i++) {
                System.err.print(updateCounts[i] + "   ");
            }
            System.err.println("");

        } catch(SQLException ex) {
            System.err.println("SQLException: " + ex.getMessage());
            System.err.println("SQLState:  " + ex.getSQLState());
            System.err.println("Message:  " + ex.getMessage());
            System.err.println("Vendor:  " + ex.getErrorCode());
        } finally {
            if (stmt != null) { stmt.close(); }
                JDBCTutorialUtilities.closeConnection(con);
            }
        }
    }
}
```