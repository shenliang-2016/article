### 使用存储过程

存储过程是一组形成逻辑单元并执行特定任务的SQL语句，它们用于封装一组要在数据库服务器上执行的操作或查询。例如，员工数据库上的操作（雇用，激活，升级，查找）可以编码为由应用程序代码执行的存储过程。存储过程可以使用不同的参数和结果进行编译和执行，并且它们可以具有输入，输出和输入/输出参数的任意组合。

请注意，大多数DBMS都支持存储过程，但语法和功能存在相当大的差异。因此，本教程包含两个类，`StoredProcedureJavaDBSample`和`StoredProcedureMySQLSample`，分别演示如何在Java DB和MySQL中创建存储过程。

本章节涵盖以下主题：

- [存储过程示例概述](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#overview_stored_procedures_examples)
- [参数模式](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#parameter_modes)
- 在 Java DB 中创建存储过程
  - [使用 SQL 脚本或者 JDBC API 在 Java DB 中创建存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#creating_javadb_sql_jdbc)
  - [在 Java DB 中创建存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#creating_stored_procedures_java_db)
  - [打包 Java 类到 JAR 文件中](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#package_java_class_in_jar_file)
- 在 MySQL 中创建存储过程
  - [使用 SQL 脚本或者 JDBC API 在 MySQL 中创建存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#create_jdbc_mysql)
- [在 MySQL 和 Java DB 中调用存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#calling_javadb_mysql)

**存储过程示例概述**

示例`StoredProcedureJavaDBSample.java`和`StoredProcedureMySQLSample.java`创建并调用以下存储过程：

- `SHOW_SUPPLIERS`：打印一个结果集，其中包含咖啡供应商的名称和他们提供给 The Coffee Break 的咖啡。此存储过程不需要任何参数。当示例调用此存储过程时，该示例生成类似于以下内容的输出：

  ```
  Acme, Inc.: Colombian_Decaf
  Acme, Inc.: Colombian
  Superior Coffee: French_Roast_Decaf
  Superior Coffee: French_Roast
  The High Ground: Espresso
  ```

- `GET_SUPPLIER_OF_COFFEE`： 打印咖啡`coffeeName`的供应商的名称`supplierName`。它需要以下参数：

  - `IN coffeeName varchar(32)`: 咖啡的名称
  - `OUT supplierName varchar(40)`: 咖啡供应商的名称

  当示例使用`Colombian`作为`coffeeName`的值调用此存储过程时，该示例将生成类似于以下内容的输出：

  ```
  Supplier of the coffee Colombian: Acme, Inc.
  ```

- `RAISE_PRICE`: 将名为`coffeeName`的咖啡价格提高到`newPrice`的价格。如果价格上涨大于`maximumPercentage`百分比，那么价格会按该百分比上调。如果价格`newPrice`低于咖啡的原始价格，此程序将不会更改价格。它需要以下参数：

  - `IN coffeeName varchar(32)`: 咖啡的名称
  - `IN maximumPercentage float`: 咖啡涨价最大百分比
  - `INOUT newPrice numeric(10,2)`: 咖啡的新价格。调用`RAISE_PRICE`存储过程后，此参数将包含名为`coffeeName`的咖啡的当前价格。

  当示例使用`Colombian`作为`coffeeName`的值，将`0.10`作为`maximumPercentage`的值，将`19.99`作为`newPrice`的值调用此存储过程时，该示例将生成类似于以下内容的输出：

  ```
  Contents of COFFEES table before calling RAISE_PRICE:
  Colombian, 101, 7.99, 0, 0
  Colombian_Decaf, 101, 8.99, 0, 0
  Espresso, 150, 9.99, 0, 0
  French_Roast, 49, 8.99, 0, 0
  French_Roast_Decaf, 49, 9.99, 0, 0

  Calling the procedure RAISE_PRICE

  Value of newPrice after calling RAISE_PRICE: 8.79

  Contents of COFFEES table after calling RAISE_PRICE:
  Colombian, 101, 8.79, 0, 0
  Colombian_Decaf, 101, 8.99, 0, 0
  Espresso, 150, 9.99, 0, 0
  French_Roast, 49, 8.99, 0, 0
  French_Roast_Decaf, 49, 9.99, 0, 0
  ```

**参数模式**

参数属性`IN`（默认值），`OUT`和`INOUT`是参数模式。它们定义了形式参数的作用。下表总结了有关参数模式的信息。

| Characteristic of Parameter Mode         | IN                                       | OUT                                      | INOUT                                    |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| Must it be specified in the stored procedure definition? | No; if omitted, then the parameter mode of the formal parameter is `IN`. | Must be specified.                       | Must be specified.                       |
| Does the parameter pass a value to the stored procedure or return a value? | Passes values to a stored procedure.     | Returns values to the caller.            | Both; passes initial values to a stored procedure; returns updated values to the caller. |
| Does the formal parameter act as a constant or a variable in the stored procedure? | Formal parameter acts like a constant.   | Formal parameter acts like an uninitialized variable. | Formal parameter acts like an initialized variable. |
| Can the formal parameter be assigned a value in the stored procedure? | Formal parameter cannot be assigned a value. | Formal parameter cannot be used in an expression; must be assigned a value. | Formal parameter must be assigned a value. |
| What kinds of actual parameters (arguments) can be passed to the stored procedure? | Actual parameter can be a constant, initialized variable, literal, or expression. | Actual parameter must be a variable.     | Actual parameter must be a variable.     |

**在 Java DB 中创建存储过程**

**注意：**有关在Java DB中创建存储过程的更多信息，请参阅 [*Java DB Reference Manual*](http://docs.oracle.com/javadb/index_jdk8.html) 中的“CREATE PROCEDURE语句”一节。

在Java DB中创建和使用存储过程涉及以下步骤：

1. [在Java类中创建公共静态Java方法](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#creating_public_static_java_method)：此方法执行存储过程所需的任务。
2. [创建存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#creating_javadb_sql_jdbc)：此存储过程调用您创建的Java方法。
3. [将Java类（包含您之前创建的公共静态Java方法）打包到JAR文件中](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#package_java_class_in_jar_file) 。
4. 使用`CALL` SQL语句调用存储过程。请参阅 [Calling Stored Procedures in Java DB and MySQL](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#calling_javadb_mysql) 。

**创建 Public Static Java 方法**

以下方法`StoredProcedureJavaDBSample.showSuppliers`包含存储过程`SHOW_SUPPLIERS`调用的SQL语句：

```java
public static void showSuppliers(ResultSet[] rs)
    throws SQLException {

    Connection con = DriverManager.getConnection("jdbc:default:connection");
    Statement stmt = null;

    String query =
        "select SUPPLIERS.SUP_NAME, " +
        "COFFEES.COF_NAME " +
        "from SUPPLIERS, COFFEES " +
        "where SUPPLIERS.SUP_ID = " +
        "COFFEES.SUP_ID " +
        "order by SUP_NAME";

    stmt = con.createStatement();
    rs[0] = stmt.executeQuery(query);
}
```

`SHOW_SUPPLIERS`存储过程不带参数。您可以通过在公共静态Java方法的方法签名中定义参数来指定存储过程中的参数。请注意，方法`showSuppliers`包含`ResultSet[]`类型的参数。如果存储过程返回任意数量的`ResultSet`对象，请在Java方法中指定一个`ResultSet[]`类型的参数。此外，请确保此Java方法是公共的和静态的。

从URL `jdbc:default:connection`中检索`Connection`对象。这是Java DB中的一种约定，用于指示存储过程将使用当前存在的`Connection`对象。

请注意，此方法中未关闭`Statement`对象。不要在存储过程的Java方法中关闭任何`Statement`对象; 如果这样做，则在调用存储过程时发出`CALL`语句时，`ResultSet`对象将不存在。

为了使存储过程返回生成的结果集，必须将结果集分配给`ResultSet[]`参数的数组组件。在此示例中，生成的结果集被分配给数组组件`rs[0]`。

以下方法是`StoredProcedureJavaDBSample.showSuppliers`：

```java
public static void getSupplierOfCoffee(String coffeeName, String[] supplierName)
    throws SQLException {

    Connection con = DriverManager.getConnection("jdbc:default:connection");
    PreparedStatement pstmt = null;
    ResultSet rs = null;

    String query =
        "select SUPPLIERS.SUP_NAME " +
        "from SUPPLIERS, COFFEES " +
        "where " +
        "SUPPLIERS.SUP_ID = COFFEES.SUP_ID " +
        "and ? = COFFEES.COF_NAME";

    pstmt = con.prepareStatement(query);
    pstmt.setString(1, coffeeName);
    rs = pstmt.executeQuery();

    if (rs.next()) {
        supplierName[0] = rs.getString(1);
    } else {
        supplierName[0] = null;
    }
}
```

形式参数`coffeeName`具有参数模式`IN`。此形式参数与Java方法中的任何其他参数一样使用。因为形式参数`supplierName`具有参数模式`OUT`，所以它必须使用一维数组数据类型。由于此方法不生成结果集，因此方法定义不包含`ResultSet[]`类型的参数。要从`OUT`形式参数检索值，必须将要检索的值分配给`OUT`形参的数组组件。在此示例中，将检索到的咖啡供应商名称分配给数组组件`supplierName[0]`。

以下是`StoredProcedureJavaDBSample.raisePrice`方法的方法签名：

```java
public static void raisePrice(
   String coffeeName, double maximumPercentage,
   BigDecimal[] newPrice) throws SQLException
```

因为形式参数`newPrice`具有参数模式`INOUT`，所以它必须使用一维数组数据类型。Java DB分别将`FLOAT`和`NUMERIC` SQL数据类型映射到`double`和`java.math.BigDecimal` Java数据类型。

**使用 SQL 脚本或者 JDBC API 在 Java DB 中创建存储过程**

Java DB将Java编程语言用于其存储过程。因此，在定义存储过程时，可以指定要调用的Java类以及Java DB可以在何处找到该Java类。

以下来自`StoredProcedureJavaDBSample.createProcedures`的摘录创建了一个名为`SHOW_SUPPLIERS`的存储过程：

```java
public void createProcedures(Connection con)
    throws SQLException {

    Statement stmtCreateShowSuppliers = null;

    // ...

    String queryShowSuppliers =
        "CREATE PROCEDURE SHOW_SUPPLIERS() " +
        "PARAMETER STYLE JAVA " +
        "LANGUAGE JAVA " +
        "DYNAMIC RESULT SETS 1 " +
        "EXTERNAL NAME " +
        "'com.oracle.tutorial.jdbc." +
        "StoredProcedureJavaDBSample." +
        "showSuppliers'";

    // ...

    try {
        System.out.println("Calling CREATE PROCEDURE");
        stmtCreateShowSuppliers = con.createStatement();

        // ...

    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmtCreateShowSuppliers != null) {
            stmtCreateShowSuppliers.close();
        }
        // ...
    }
}
```

以下列表描述了您可以在`CREATE PROCEDURE`语句中指定的过程元素：

- `PARAMETER STYLE`: 标识用于将参数传递给存储过程的约定。以下选项有效
  - `JAVA`: 指定存储过程使用符合Java语言和SQL例程规范的参数传递约定。
  - `DERBY`: 指定存储过程支持可变参数作为参数列表中的最后一个参数。
- `LANGUAGE JAVA`: 指定存储过程的编程语言（目前，JAVA是唯一的选项）。
- `DYNAMIC RESULT SETS 1`: 指定检索的最大结果集数; 在这种情况下，它是`1`。
- `EXTERNAL NAME 'com.oracle.tutorial.jdbc.StoredProcedureJavaDBSample.showSuppliers'`: 指定此存储过程调用的完全限定的Java方法。**注意：**Java DB必须能够在类路径或直接添加到数据库的JAR文件中找到此处指定的方法。请参阅以下步骤， [Package Java Class in JAR File](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#package_java_class_in_jar_file) 。

以下语句（在`StoredProcedureJavaDBSample.createProcedures`中找到）创建名为`GET_SUPPLIERS_OF_COFFEE`的存储过程（为清楚起见，已添加换行符）：

```sql
CREATE PROCEDURE GET_SUPPLIER_OF_COFFEE(
    IN coffeeName varchar(32),
    OUT supplierName
    varchar(40))
    PARAMETER STYLE JAVA
    LANGUAGE JAVA
    DYNAMIC RESULT SETS 0
    EXTERNAL NAME 'com.oracle.tutorial.jdbc.
        StoredProcedureJavaDBSample.
        getSupplierOfCoffee'
```

此存储过程有两个形式参数，`coffeeName`和`supplierName`。参数说明符`IN`和`OUT`称为参数模式。它们定义了形式参数的作用。有关更多信息，请参阅 [参数模式](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#parameter_modes) 。此存储过程不检索结果集，因此过程元素`DYNAMIC RESULT SETS`为`0`。

以下语句创建名为`RAISE_PRICE`的存储过程（为清晰起见，已添加换行符）：

```sql
CREATE PROCEDURE RAISE_PRICE(
    IN coffeeName varchar(32),
    IN maximumPercentage float,
    INOUT newPrice float)
    PARAMETER STYLE JAVA
    LANGUAGE JAVA
    DYNAMIC RESULT SETS 0
    EXTERNAL NAME 'com.oracle.tutorial.jdbc.
        StoredProcedureJavaDBSample.raisePrice'
```

您可以使用SQL脚本在Java DB中创建存储过程。 请参阅`build.xml` Ant构建脚本中的脚本`javadb/create-procedures.sql`和Ant目标`javadb-create-procedure`。

**打包 Java 类到 JAR 文件中**

Ant构建脚本`build.xml`包含用于在JAR文件中编译和打包本教程文件的目标。在命令提示符下，将当前目录更改为`<JDBC tutorial directory> `。从此目录中，运行以下命令以在JAR文件中编译和打包教程：

`ant jar`

JAR文件的名称是`<JDBC tutorial directory>/lib/JDBCTutorial.jar`。

Ant构建脚本将文件`JDBCTutorial.jar`添加到类路径中。您还可以在`CLASSPATH`环境变量中指定JAR文件的位置。这使Java DB能够找到存储过程调用的Java方法。

**直接将JAR文件添加到数据库**

Java DB首先在类路径中查找任何所需的类，然后在数据库中查找。本节介绍如何将JAR文件直接添加到数据库。

使用以下系统过程将`JDBCTutorial.jar JAR`文件添加到数据库（为清晰起见，已添加换行符）：

```sql
CALL sqlj.install_jar(
  '<JDBC tutorial directory>/
  lib/JDBCTutorial.jar',
  'APP.JDBCTutorial', 0)
CALL sqlj.replace_jar(
  '<JDBC tutorial directory>/
  lib/JDBCTutorial.jar',
  'APP.JDBCTutorial')";
CALL syscs_util.syscs_set_database_property(
  'derby.database.classpath',
  'APP.JDBCTutorial')";
```

**注意：**方法`StoredProcedureJavaDBSample.registerJarFile`演示了如何调用这些系统过程。如果调用此方法，请确保已修改`javadb-sample-properties.xml`，以便将属性`jar_file`的值设置为`JDBCTutorial.jar`的完整路径名。

SQL模式中的`install_jar`过程将JAR文件添加到数据库。此过程的第一个参数是运行此过程的计算机上的JAR文件的完整路径名。第二个参数是Java DB用于引用JAR文件的标识符。（标识符`APP`是Java DB默认模式。）`replace_jar`过程替换数据库中已有的JAR文件。

系统过程`SYSCS_UTIL.SYSCS_SET_DATABASE_PROPERTY`设置或删除当前连接上数据库的属性值。此方法将属性`derby.database.classpath`设置为`install_jar`文件中指定的标识符。 Java DB首先查找你的Java类路径，然后查看`derby.database.classpath`。

**在 MySQL 中创建存储过程**

在Java DB中创建和使用存储过程涉及以下步骤：

1. [使用SQL脚本或JDBC API创建存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#create_jdbc_mysql)
2. 使用`CALL` SQL语句调用存储过程。请参阅 [Java DB和MySQL中的调用存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#calling_javadb_mysql) 一节

**使用 SQL 脚本或者 JDBC API 在 MySQL 中创建存储过程**

MySQL对其存储过程使用基于SQL的语法。以下摘自SQL脚本`mysql/create-procedures.sql`创建了一个名为`SHOW_SUPPLIERS`的存储过程：

```
SELECT 'Dropping procedure SHOW_SUPPLIERS' AS ' '|
drop procedure if exists SHOW_SUPPLIERS|

# ...

SELECT 'Creating procedure SHOW_SUPPLIERS' AS ' '|
create procedure SHOW_SUPPLIERS()
    begin
        select SUPPLIERS.SUP_NAME,
        COFFEES.COF_NAME
        from SUPPLIERS, COFFEES
        where SUPPLIERS.SUP_ID = COFFEES.SUP_ID
        order by SUP_NAME;
    end|
```

`DROP PROCEDURE`语句删除该过程`SHOW_SUPPLIERS`（如果存在）。在MySQL中，存储过程中的语句由分号分隔。但是，需要使用不同的分隔符来结束`create procedure`语句。此示例使用管道（|）字符; 你可以使用另一个字符（或多个字符）。分隔语句的这个字符在调用此脚本的Ant目标的`delimiter`属性中定义。此摘录来自Ant构建文件`build.xml`（为了清楚起见，已插入换行符）：

```sql
<target name="mysql-create-procedure">

  <sql driver="${DB.DRIVER}"
       url="${DB.URL}" userid="${DB.USER}"
       password="${DB.PASSWORD}"
       classpathref="CLASSPATH"
       print="true"
       delimiter="|"
       autocommit="false"
       onerror="abort">
       <transaction
         src="./sql/${DB.VENDOR}/
           create-procedures.sql">
       </transaction>
  </sql>

</target>
```

或者，您可以使用`DELIMITER` SQL语句指定不同的分隔符。

`CREATE PROCEDURE`语句由过程的名称，括号中的逗号分隔的参数列表以及`BEGIN`和`END`关键字中的SQL语句组成。

您可以使用JDBC API创建存储过程。以下方法`StoredProcedureMySQLSample.createProcedureShowSuppliers`执行与上一个脚本相同的任务：

```java
public void
    createProcedureShowSuppliers()
    throws SQLException {
    String createProcedure = null;

    String queryDrop =
        "DROP PROCEDURE IF EXISTS SHOW_SUPPLIERS";

    createProcedure =
        "create procedure SHOW_SUPPLIERS() " +
        "begin " +
            "select SUPPLIERS.SUP_NAME, " +
            "COFFEES.COF_NAME " +
            "from SUPPLIERS, COFFEES " +
            "where SUPPLIERS.SUP_ID = " +
            "COFFEES.SUP_ID " +
            "order by SUP_NAME; " +
        "end";
    Statement stmt = null;
    Statement stmtDrop = null;

    try {
        System.out.println("Calling DROP PROCEDURE");
        stmtDrop = con.createStatement();
        stmtDrop.execute(queryDrop);
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmtDrop != null)
        {
            stmtDrop.close();
        }
    }

    try {
        stmt = con.createStatement();
        stmt.executeUpdate(createProcedure);
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

请注意，此方法中未更改分隔符。

存储过程`SHOW_SUPPLIERS`生成结果集，即使`createProcedureShowSuppliers`方法的返回类型为`void`且该方法不包含任何参数。使用`CallableStatement.executeQuery`方法调用存储过程`SHOW_SUPPLIERS`时，将返回结果集：

```java
CallableStatement cs = null;
cs = this.con.prepareCall("{call SHOW_SUPPLIERS}");
ResultSet rs = cs.executeQuery();
```

以下摘自方法`StoredProcedureMySQLSample.createProcedureGetSupplierOfCoffee`包含用于创建名为`GET_SUPPLIER_OF_COFFEE`的存储过程的SQL查询：

```java
public void createProcedureGetSupplierOfCoffee()
    throws SQLException {

    String createProcedure = null;

    // ...

    createProcedure =
        "create procedure GET_SUPPLIER_OF_COFFEE(" +
        "IN coffeeName varchar(32), " +
        "OUT supplierName varchar(40)) " +
        "begin " +
            "select SUPPLIERS.SUP_NAME into " +
            "supplierName " +
            "from SUPPLIERS, COFFEES " +
            "where SUPPLIERS.SUP_ID = " +
            "COFFEES.SUP_ID " +
            "and coffeeName = COFFEES.COF_NAME; " +
            "select supplierName; " +
        "end";
    // ...
}
```

此存储过程有两个形式参数，`coffeeName`和`supplierName`。参数说明符`IN`和`OUT`称为参数模式。它们定义了形式参数的作用。有关更多信息，请参阅 [参数模式](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html#parameter_modes) 。形式参数在SQL查询中定义，而不是在`createProcedureGetSupplierOfCoffee`方法中定义。要为`OUT`参数`supplierName`分配值，此存储过程使用`SELECT`语句。

以下摘自方法`StoredProcedureMySQLSample.createProcedureRaisePrice`包含创建名为`RAISE_PRICE`的存储过程的SQL查询：

```java
public void createProcedureRaisePrice()
    throws SQLException {

    String createProcedure = null;

    // ...

    createProcedure =
        "create procedure RAISE_PRICE(" +
        "IN coffeeName varchar(32), " +
        "IN maximumPercentage float, " +
        "INOUT newPrice numeric(10,2)) " +
        "begin " +
        "main: BEGIN " +
            "declare maximumNewPrice " +
                "numeric(10,2); " +
            "declare oldPrice numeric(10,2); " +
            "select COFFEES.PRICE into oldPrice " +
                "from COFFEES " +
                "where COFFEES.COF_NAME " +
                "= coffeeName; " +
            "set maximumNewPrice = " +
                "oldPrice * (1 + " +
                "maximumPercentage); " +
            "if (newPrice > maximumNewPrice) " +
                "then set newPrice = " +
                "maximumNewPrice; " +
            "end if; " +
            "if (newPrice <= oldPrice) " +
                "then set newPrice = oldPrice; " +
                "leave main; " +
            "end if; " +
            "update COFFEES " +
                "set COFFEES.PRICE = newPrice " +
                "where COFFEES.COF_NAME " +
                "= coffeeName; " +
            "select newPrice; " +
        "END main; " +
        "end";

    // ...
}
```

存储过程使用`SET`和`SELECT`语句为`INOUT`参数`newPrice`赋值。要退出存储过程，存储过程首先将语句括在标记为`main`的`BEGIN ... END`块中。要退出该过程，该方法使用语句`leave main`。

**在 MySQL 和 Java DB 中调用存储过程**

以下摘自方法`runStoredProcedures`，调用存储过程`SHOW_SUPPLIERS`并打印生成的结果集：

```java
cs = this.con.prepareCall("{call SHOW_SUPPLIERS()}");
ResultSet rs = cs.executeQuery();

while (rs.next()) {
    String supplier = rs.getString("SUP_NAME");
    String coffee = rs.getString("COF_NAME");
    System.out.println(supplier + ": " + coffee);
}
```

**注意：**与`Statement`对象一样，要调用存储过程，可以调用`execute`，`executeQuery`或`executeUpdate`，具体取决于过程返回的`ResultSet`对象的数量。但是，如果您不确定该过程返回了多少`ResultSet`对象，请调用`execute`。

调用存储过程`SHOW_SUPPLIERS`在`MySQL`中使用JDBC API创建存储过程一节中进行了演示。

以下摘自方法`runStoredProcedures`，调用存储过程`GET_SUPPLIER_OF_COFFEE`：

```java
cs = this.con.prepareCall("{call GET_SUPPLIER_OF_COFFEE(?, ?)}");
cs.setString(1, coffeeNameArg);
cs.registerOutParameter(2, Types.VARCHAR);
cs.executeQuery();

String supplierName = cs.getString(2);
```

`CallableStatement`接口扩展了`PreparedStatement`。它用于调用存储过程。通过调用相应的`setter`方法，就像使用`PreparedStatement`对象一样，指定`IN`参数的值（例如本例中的`coffeeName`）。但是，如果存储过程包含`OUT`参数，则必须使用`registerOutParameter`方法注册它。

以下摘自方法`runStoredProcedures`，调用存储过程`RAISE_PRICE`：

```java
cs = this.con.prepareCall("{call RAISE_PRICE(?,?,?)}");
cs.setString(1, coffeeNameArg);
cs.setFloat(2, maximumPercentageArg);
cs.registerOutParameter(3, Types.NUMERIC);
cs.setFloat(3, newPriceArg);

cs.execute();
```

因为参数`newPrice`（过程`RAISE_PRICE`中的第三个参数）具有参数模式`INOUT`，所以必须通过调用适当的`setter`方法指定其值并使用`registerOutParameter`方法注册它。