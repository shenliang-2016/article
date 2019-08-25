# Java™教程

[主页](https://docs.oracle.com/javase/tutorial/index.html)

## Java教程学习路径

> Java教程是为JDK 8编写的。本页描述的示例和实践没有利用后续版本中引入的改进。

## 入门

- [入门](https://docs.oracle.com/javase/tutorial/getStarted/index.html) - 介绍Java技术和安装Java开发软件并使用它来创建简单程序的课程。
- [学习Java语言](https://docs.oracle.com/javase/tutorial/java/index.html) - 描述基本概念（如类，对象，继承，数据类型，泛型和包）的课程。
- [基本Java类](https://docs.oracle.com/javase/tutorial/essential/index.html) - 有关异常，基本输入/输出，并发，正则表达式和平台环境的课程。

## 基础

- [集合](https://docs.oracle.com/javase/tutorial/collections/index.html) - 使用和扩展Java集合框架的经验教训。
- [Lambda表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)：了解如何以及为何在应用程序中使用Lambda表达式。
- [聚合操作](https://docs.oracle.com/javase/tutorial/collections/streams/index.html)：探索聚合操作，流和Lambda表达式如何协同工作以提供强大的过滤功能。
- [JAR文件中的打包程序](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html) - 有关创建和签署JAR文件的课程。
- [国际化](https://docs.oracle.com/javase/tutorial/i18n/index.html) - 设计软件的介绍，以便可以轻松地适应（本地化）各种语言和区域。
- [反射](https://docs.oracle.com/javase/tutorial/reflect/index.html) - 表示（“反映”）当前Java虚拟机中的类，接口和对象的API。
- [安全性](https://docs.oracle.com/javase/tutorial/security/index.html) - Java平台功能，有助于保护应用程序免受恶意软
- [JavaBeans](https://docs.oracle.com/javase/tutorial/javabeans/index.html) - Java平台的组件技术。
- [扩展机制](https://docs.oracle.com/javase/tutorial/ext/index.html) - 如何使Java平台上运行的所有应用程序都可以使用自定义API。
- [泛型](https://docs.oracle.com/javase/tutorial/extra/generics/index.html) - 对类型系统的增强，支持对各种类型的对象的操作，同时提供编译时类型安全性。

## 客户端开发

- [JavaFX入门](http://www.oracle.com/pls/topic/lookup?ctx=javase80&id=JFXST804) - 一组示例应用程序，旨在帮助您开始使用常见的JavaFX任务
- [Scene Builder入门](http://www.oracle.com/pls/topic/lookup?ctx=javase80&id=JSBGS101) - 逐步向您展示如何使用JavaFX Scene Builder工具创建简单的问题跟踪应用程序。
- [使用Swing创建GUI](https://docs.oracle.com/javase/tutorial/uiswing/index.html) - 全面介绍Java平台上的GUI创建。
- [部署](https://docs.oracle.com/javase/tutorial/deployment/index.html) - 如何使用JAR文件打包应用程序和applet，并使用Java Web Start和Java Plug-in进行部署。
- [2D图形](https://docs.oracle.com/javase/tutorial/2d/index.html) - 如何在应用程序中显示和打印2D图形。
- [全屏独占模式API](https://docs.oracle.com/javase/tutorial/extra/fullscreen/index.html) - 如何编写更充分利用用户图形硬件的应用程序。

## 服务端开发

- [JDBC数据库访问](https://docs.oracle.com/javase/tutorial/jdbc/index.html) - 介绍用于Java应用程序与各种数据库和数据源之间的连接的API。
- [JMX](https://docs.oracle.com/javase/tutorial/jmx/index.html) - Java Management Extensions提供了一种管理应用程序，设备和服务等资源的标准方法。
- [JNDI](https://docs.oracle.com/javase/tutorial/jndi/index.html) - Java命名和目录接口支持访问DNS和LDAP等命名和目录服务。
- [JAXP](https://docs.oracle.com/javase/tutorial/jaxp/index.html) - 介绍用于XML处理的Java API（JAXP）1.4技术。
- [RMI](https://docs.oracle.com/javase/tutorial/rmi/index.html) - 远程方法调用API允许对象调用在另一个Java虚拟机上运行的对象的方法。
- [并发](https://docs.oracle.com/javase/tutorial/essential/concurrency/index.html) - Java平台具有API，可帮助您开发多线程程序。

# JDBC™ 数据库访问

JDBC™ API 的设计目标是保持简单。这意味着 JDBC 使得所有的数据库任务变得简单。本课程带领你通过使用 JDBC 的实例来执行普通的 SQL 语句，以及执行数据库应用的常见任务。

本课程分为以下部分：

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**JDBC 介绍**](https://docs.oracle.com/javase/tutorial/jdbc/overview/index.html) 列出 JDBC 特性，描述 JDBC 体系结构，SQL 命令和关系数据库概念综述。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**JDBC 基础**](https://docs.oracle.com/javase/tutorial/jdbc/basics/index.html) 涵盖 JDBC API，包含在 Java™ SE 6 版本中。

完成第一部分学习后，你将知道如何使用基本的 JDBC API 来创建表，向表中插入数据，查询表，检索查询结果，以及更新表等。在此过程中，你将学习如何使用简单语句和预编译语句，同时你将看到一个存储过程的例子。你也将学到如何执行事务以及如何捕获异常和警告。

## JDBC 介绍

JDBC API 是可以访问任何类型的表格式的数据的 Java API，特别是存储在 [关系数据库](https://docs.oracle.com/javase/tutorial/jdbc/overview/index.html#relational) 中的数据。

JDBC 帮助你编写 Java 程序来管理以下三类程序活动：

* 连接数据源，比如数据库
* 发送查询和更新语句到数据库
* 检索并处理来自数据库的作为你的查询的响应的查询结果

下面的简单代码片段展示了这三个步骤的例子：

```java
public void connectToAndQueryDatabase(String username, String password) {

    Connection con = DriverManager.getConnection(
                         "jdbc:myDriver:myDatabase",
                         username,
                         password);

    Statement stmt = con.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT a, b, c FROM Table1");

    while (rs.next()) {
        int x = rs.getInt("a");
        String s = rs.getString("b");
        float f = rs.getFloat("c");
    }
}
```

此代码片段实例化一个 `DriverManager` 对象来连接到一个数据库驱动并登录到数据库中，实例化一个 `Statement` 对象运输你的 SQL 查询到数据库，实例化一个 `ResultSet` 对象来获取你的查询结果，并执行一个简单的 `while` 循环，获取并显示那些结果。

**JDBC 产品组件**

JDBC 包含四个组件：

1. **JDBC API** — JDBC™ API 提供了编程方式通过 Java™ 编程语言访问关系数据的能力。使用 JDBC API，程序能够执行 SQL 语句，检索结果，并反向传播更改到数据源。JDBC API 可以在异质的分布式环境中同时与多个数据源交互。

   JDBC API 是 Java 平台的一部分，该平台包含 *Java™ Standard Edition* (Java™ SE ) 和 *Java™ Enterprise Edition* (Java™ EE)。JDBC 4.0 API 被分为两个包： `java.sql` 和 `javax.sql` 。两个包都包含在 Java SE 和 Java EE 平台中。

2. **JDBC Driver Manager** —  JDBC `DriverManager` 类定义了能够将 Java 程序连接到 JDBC 驱动的类。`DriverManager` 从来就是 JDBC 架构的核心。它非常精简。

   标准扩展包 `javax.naming` 和 `javax.sql` 使得你可以使用在 *Java Naming and Directory Interface*™ (JNDI) 命名服务中注册的 `DataSource` 对象来建立与数据源的连接。您可以使用任一连接机制，但建议尽可能使用DataSource对象。

3. **JDBC Test Suite** —  JDBC driver 测试套件帮助你确定 JDBC 驱动将运行你的程序。这些测试并不全面或详尽，但它们确实运用了 JDBC API 中的许多重要功能。

4. **JDBC-ODBC Bridge** —  Java Software bridge 通过 ODBC 驱动程序提供 JDBC 访问。请注意，您需要将 ODBC 二进制代码加载到使用此驱动程序的每台客户端计算机上。因此，ODBC 驱动程序最适用于客户端安装不是主要问题的公司网络，或者适用于以三层体系结构用 Java 编写的应用程序服务器代码。

此课程使用这四个 JDBC 组件中的前两个连接到数据库，然后构建一个使用 SQL 命令与测试关系数据库通信的Java程序。最后两个组件用于特定环境以测试 web 应用程序，或与 ODBC 敏感的 DBMS 进行通信。

### JDBC 体系结构

JDBC API 同时支持两层或者三层数据库访问过程模型。

![The DBMS-proprietary protocol provides two-way communication between the client machine and the database server](https://docs.oracle.com/javase/tutorial/jdbc/overview/intro.anc2.gif)

Figure 1: 数据访问的两层体系结构

在两层模型中，Java 程序直接与数据源交互。这就需要 JDBC 驱动能够与被访问的特定数据源进行通信。一个用户的命令被交付给该数据库或者其他数据源，同时那些语句的结果被回送给用户。数据源可以位于别的机器上，用户通过网络进行连接。这被称为客户端/服务器配置，用户的机器作为客户端，数据源所在的机器作为服务器。网络可以是内联网，例如，连接公司内的员工，也可以是因特网。

在三层模型中，命令被发送到服务的“中间层”，然后将命令发送到数据源。数据源处理命令并将结果发送回中间层，然后中间层将它们发送给用户。MIS 主管发现三层模型非常具有吸引力，因为中间层可以保持对访问的控制以及可以对公司数据进行的更新。另一个优点是它简化了应用程序的部署。最后，在许多情况下，三层架构可以提供性能优势。

![The DBMS-proprietary protocol provides two-way communication between the database server and the server machine. HTTP, RMI, CORBA or other calls provide two way communication between the server machine and the client machine](https://docs.oracle.com/javase/tutorial/jdbc/overview/intro.anc1.gif)

Figure 2: 数据访问的三层体系结构

直到最近，中间层通常用 C 或 C++ 等语言编写，这些语言提供了足够高的性能。然而，随着优化编译器的引入，将 Java 字节码转换为高效的机器特定代码和诸如 Enterprise JavaBeans™ 的技术，Java 平台正迅速成为中间层开发的标准平台。这是一个很大的优势，可以利用 Java 的健壮性，多线程和安全功能。

随着企业越来越多地使用 Java 编程语言编写服务器代码，JDBC API 在三层体系结构的中间层中越来越多地被使用。使 JDBC 成为服务器技术的一些功能是它支持连接池，分布式事务和断开连接的行集。JDBC API也允许从 Java 中间层访问数据源。

### 关系数据库概览

数据库是一种以可以从中检索信息的方式存储信息的方法。简单来说，关系数据库是在包含行和列的表中显示信息的数据库。表在某种意义上被称为关系，它是相同类型（行）的对象的集合。表中的数据可以根据公共键或概念进行关联，并且从表中检索相关数据的能力是关系数据库术语的基础。数据库管理系统（DBMS）处理数据的存储，维护和检索方式。对于关系数据库，关系数据库管理系统（RDBMS）执行这些任务。本书中使用的DBMS是包含RDBMS的通用术语。

**完整性规则**

关系表遵循某些完整性规则，以确保它们包含的数据保持准确并始终可访问。首先，关系表中的行应该都是不同的。如果存在重复行，则可能存在解决两个可能选择中哪一个是正确选择的问题。对于大多数DBMS，用户可以指定不允许重复行，如果这样做，DBMS将阻止添加任何重复现有行的行。

传统关系模型的第二个完整性规则是列值不能是重复的组或数组。数据完整性的第三个方面涉及空值的概念。数据库通过使用空值来指示缺少值，从而处理数据可能不可用的情况。它不等于空白或零。空白被认为等于另一个空白，零等于另一个零，但两个空值不被认为是相等的。

当表中的每一行不同时，可以使用一列或多列来标识特定行。此唯一列或列组称为主键。作为主键一部分的任何列都不能为空；如果为空，则包含它的主键将不再是完整的标识符。此规则称为实体完整性规则。

`Employees` 表展示了一些关系数据库概念。它包含 5 列和 6 行，每行数据表示一个不同的雇员。

| `Employee_Number` | `First_name` | `Last_Name` | `Date_of_Birth` | `Car_Number` |
| ----------------- | ------------ | ----------- | --------------- | ------------ |
| 10001             | John         | Washington  | 28-Aug-43       | 5            |
| 10083             | Arvid        | Sharma      | 24-Nov-54       | null         |
| 10120             | Jonas        | Ginsberg    | 01-Jan-69       | null         |
| 10005             | Florence     | Wojokowski  | 04-Jul-71       | 12           |
| 10099             | Sean         | Washington  | 21-Sep-66       | null         |
| 10035             | Elizabeth    | Yamaguchi   | 24-Dec-59       | null         |

该表的主键通常是员工编号，因为每个人都保证不同。（如果进行比较，数字也比字符串更有效。）也可以使用 `First_Name` 和 `Last_Name` ，因为两者的组合也能识别我们的示例数据库中的一行。单独使用姓氏是行不通的，因为有两名员工的姓氏为“华盛顿”。在这种特殊情况下，名字都是不同的，因此可以设想使用该列作为主键，但最好避免使用可能发生重复的列。如果 Elizabeth Jones 在这家公司工作并且主键是 `First_Name` ，则RDBMS将不允许添加她的名字（如果已经指定不允许重复）。因为表中已经有一个 Elizabeth，所以添加第二个会使主键无法用作识别一行的方法。请注意，尽管使用 `First_Name` 和 `Last_Name` 是此示例的唯一复合键，但在较大的数据库中它可能不是唯一的。另请注意，`Employees` 表假定每个员工只能有一辆车。

**`SELECT` 语句**

SQL是一种旨在与关系数据库一起使用的语言。有一组基本的SQL命令被认为是标准的，并且被所有RDBMS使用。例如，所有RDBMS都使用 `SELECT` 语句。

`SELECT` 语句，也称为查询，用于从表中获取信息。它指定一个或多个列标题，一个或多个要从中选择数据的表，以及一些选择标准。RDBMS返回满足所述要求的列条件的行。如下所示的 `SELECT` 语句将获取拥有公司汽车的员工的名字和姓氏：

```sql
SELECT First_Name, Last_Name
FROM Employees
WHERE Car_Number IS NOT NULL
```

结果集（满足 `Car_Number` 列中不具有 `null` 的要求的行集）如下。为满足要求的每一行打印名字和姓氏，因为 `SELECT` 语句（第一行）指定列 `First_Name` 和 `Last_Name` 。`FROM` 子句（第二行）给出了将从中选择列的表。

| `FIRST_NAME` | `LAST_NAME` |
| ------------ | ----------- |
| John         | Washington  |
| Florence     | Wojokowski  |

下面的代码生成一个包含整个表内容的结果集，因为它要求 `Employees` 表中没有限制的所有列（没有 `WHERE` 子句）。请注意，`SELECT *` 表示 `SELECT` 所有列。

```sql
SELECT *
FROM Employees
```

**`WHERE` 子句**

`SELECT` 语句中的 `WHERE` 子句提供选择值的约束条件。比如，在下面的语句中，只有列 `Last_Name` 以字符串 `Washington` 开头的行中的值才会被选择。

```sql
SELECT First_Name, Last_Name
FROM Employees
WHERE Last_Name LIKE 'Washington%'
```

关键字 `LIKE` 用来比较字符床，同时提供了可以使用包含通配符的模式的功能特性。比如，上面的语句中，`Washington` 的末尾跟着一个百分号 `%`，表示任何包含 `Washington` 加上零个或者多个附加字符的值都符合选择约束条件。另一个用于 `LIKE` 子句的通配符是下划线 `_` ，表示任何单个字符。比如：

```sql
WHERE Last_Name LIKE 'Ba_man'
```

将匹配 'Barman', 'Badman', 'Balman', 'Bagman', 'Bamman', 等等。

下面的语句包含一个 `WHERE` 子句，使用等号 `=` 来比较数字。它选择分配了车号 12 的员工的姓名。

```sql
SELECT First_Name, Last_Name
FROM Employees
WHERE Car_Number = 12
```

下面的语句选择员工号大于 10005 的员工的姓名：

```sql
SELECT First_Name, Last_Name
FROM Employees
WHERE Employee_Number > 10005
```

`WHERE`子句可以包含多个条件而变得非常缜密，在某些DBMS中，还可以包含嵌套条件。这个概述不会涵盖复杂的`WHERE`子句，但是下面的代码片段有一个带有两个条件的`WHERE`子句。此查询选择员工编号小于 10100 且没有公司汽车的员工的名字和姓氏。

```sql
SELECT First_Name, Last_Name
FROM Employees
WHERE Employee_Number < 10100 and Car_Number IS NULL
```

一种特殊类型的 `WHERE` 子句涉及 `join` ，在下一章节中解释。

**Joins**

关系数据库的一个显着特征是可以从所谓的连接中的多个表中获取数据。假设在检索拥有公司汽车的员工的姓名后，人们想知道谁拥有哪辆汽车，包括车牌号码，里程数和汽车年份。此信息存储在另一个表 `Cars` 中：

| `Car_Number` | `License_Plate` | `Mileage` | `Year` |
| ------------ | --------------- | --------- | ------ |
| 5            | ABC123          | 5000      | 1996   |
| 12           | DEF123          | 7500      | 1999   |

两个表中必须有相同的一列才能将它们相互关联。此列必须是一个表中的主键，在另一个表中称为外键。在这种情况下，出现在两个表中的列是`Car_Number`，它是表`Cars`的主键和表`Employees`中的外键。如果车牌号为 ABC123 的 1996 年汽车被破坏并从`Cars`表中删除，则还必须从`Employees`表中删除`Car_Number` 5以维持所谓的参照完整性。否则，`Employees`表中的外键列（`Car_Number`）将包含一个未引用`Cars`表中任何内容的条目。外键必须为`null`或等于其引用的表的现有主键值。这与主键不同，主键不能为空。表`Employees`中的`Car_Number`列中有几个空值，因为员工可能没有公司汽车。

以下代码查询拥有公司汽车的员工的名字和姓氏，以及这些车辆的车牌号码，里程数和年份。请注意，`FROM`子句列出了`Employees`和`Cars`表，因为请求的数据包含在两个表中。在列名称前使用表名和点（`.`）表示哪个表包含该列。

```sql
SELECT Employees.First_Name, Employees.Last_Name,
    Cars.License_Plate, Cars.Mileage, Cars.Year
FROM Employees, Cars
WHERE Employees.Car_Number = Cars.Car_Number
```

返回的结果集如下：

| `FIRST_NAME` | `LAST_NAME` | `LICENSE_PLATE` | `MILEAGE` | `YEAR` |
| ------------ | ----------- | --------------- | --------- | ------ |
| John         | Washington  | ABC123          | 5000      | 1996   |
| Florence     | Wojokowski  | DEF123          | 7500      | 1999   |

**通用 SQL 命令**

SQL 命令分为几个类别，主要的两个种类是数据维护语言（DML）命令和数据定义语言（DDL）命令。DML 命令处理数据，检索或者更新数据以保持实时。DDL 命令创建或者修改表以及其他数据库对象，比如视图和索引。

更多的通用 DML 命令如下：

* `SELECT` - 用于从数据库查询数据并展示。此语句指定查询结果集包含哪些列。应用中用到的 SQL 命令绝大部分都是 `SELECT` 语句。
* `INSERT` - 添加新行到表中。`INSERT` 通常被用来向新建的表中添加数据或者向已经存在的表中添加新行。
* `DELETE` - 从表中删除特定行或者行集。
* `UPDATE` - 修改表中已经存在的列值或者列组的值。

通用 DDL 命令如下：

* `CREATE TABLE` - 使用用户提供的列名创建表。用户还需要指定每个列的数据类型。不同的 RDBMS 中的数据类型有所不同，因此用户可能需要使用元数据来建立特定数据库使用的数据类型。`CREATE TABLE` 通常不像 DML 命令那样经常使用，因为每个表都只会创建一次，而新增、删除和修改单个列值当然会更频繁发生。
* `DROP TABLE` - 删除所有行并从数据库中删除表定义。JDBC API 实现必须支持由 SQL92, Transitional Level 规范指定的 `DROP TABLE` 命令。不过 `DROP TABLE` 的 `CASCADE` 和 `RESTRICT` 选项是可选的。另外，当被删除的表有视图或者完整性约束定义引用时，此指令的行为是由具体实现定义的。
* `ALTER TABLE` - 添加或者删除表中的列。还可以添加或者删除表约束或者修改列属性。

**结果集和游标**

满足查询约束条件的行被称为结果集。结果集中返回的行数可以是0，1，或者更多。用户可以访问结果集中的数据，每次一行，同时提供了一个游标来实现这种操作。游标可以被认为是包含结果集数据行的文件中的指针，该指针有能力跟踪当前正在访问的行数据。游标允许用户从上到下处理结果集中的每行数据从而可以用于迭代过程。大多数 DBMS 在结果集产生时自动创建游标。

早期的 JDBC API 版本已经添加了结果集游标能力，允许游标向前或者向后移动，还允许游标移动到特定行，或者移动到相对于另一行的一个位置的行。

参考 [Retrieving and Modifying Values from Result Sets](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) 获取更多信息。

**事务**

当用户访问数据库中的数据时，另外的用户可能同时也在访问相同的数据。如果，比如，第一个用户正在更新表中的某些列，与此同时第二个用户正在从同一张表中选择这些列，此时第二个用户就有可能得到部分老数据和部分新数据。因此，DBMS 使用事务来保持数据一致状态（数据一致性），同时允许多个用户同时访问数据库（数据并发）。

事务是一条或者多条 SQL 语句的集合，这些语句构成了一个工作逻辑单元。一个事务结束于提交或者回滚，取决于数据一致性和数据并发是否有问题。提交语句使得事务中的 SQL 语句导致的变化持久化，而回滚语句撤销事务中所有 SQL 语句导致的数据变化。

锁是禁止同时维护相同的数据的两个事务的机制。比如，表锁在表上存在尚未提交的事务时将会阻止该表被删除。在一些 DBMS 中，表锁还会锁住表中的所有行。行锁阻止同时修改同一行的两个事务，或者阻止一个事务查询一行的同时，另一个事务正在修改这一行。

参考 [Using Transactions](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html) 获取更多信息。

**存储过程**

存储过程是可以通过名称调用的一组 SQL 语句。换句话说，它是可执行代码，一个微型程序，执行一个特定任务，可以像方法或者函数一样被调用。传统上，存储过程使用 DBMS 特定的编程语言编写。最新一代的数据库产品允许使用 Java 语言和 JDBC API 编写存储过程。使用 Java 语言编写的存储过程在不同 DBMS 之间是字节可移植的。一旦存储过程被编写完成，它就可以被使用并复用，因为支持存储过程的 DBMS 将会，顾名思义，存储该存储过程到数据库中。参考 [Using Stored Procedures](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html) 获取编写存储过程的更多信息。

**元数据**

数据库存储用户数据，它们还存储有关数据库本身的信息。大多数 DBMS 都有一组系统表，它们列出数据库中的表，每个表中的列名，主键，外键，存储过程等。每个 DBMS 都有自己的函数来获取有关表格布局和数据库功能的信息。JDBC 提供了接口 `DatabaseMetaData`，驱动程序编写者必须实现该接口，以便其方法返回有关驱动程序和/或为其编写驱动程序的 DBMS 的信息。例如，大量方法返回驱动程序是否支持特定功能。此接口为用户和工具提供了获取元数据的标准方法。通常，编写工具和驱动程序的开发人员最有可能关注元数据。

## JDBC 基础

本章节中你将学到 JDBC API 基础。

- [起步](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 建立一个基本的数据库开发环境并展示如何编译运行 JDBC 示例程序。
- [使用 JDBC 处理 SQL 语句](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html) 概述了处理任何 SQL 语句所需的步骤。以下页面更详细地描述了这些步骤：
  - [建立连接](https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html) 连接到数据库。
  - [使用数据源对象连接](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html) 展示如何使用 `Datasource` 对象连接你的数据库，这是获取数据源连接的首选方法。
  - [处理 SQL 异常](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlexception.html) 展示如何处理数据库错误导致的异常。
  - [建立表](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html) 描述所有例子中用到的数据库表，展示如何使用 JDBC API 和 SQL 脚本创建它们。
  - [检索和修改来自结果集的值](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) 配置数据库，发送查询，从数据库检索数据等过程的开发。
  - [使用预编译语句](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 描述创建数据库查询的一种更灵活的方法。
  - [使用事务](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html) 展示如何控制一个数据库查询实际的执行时机。
- [使用  RowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/rowset.html) 介绍 `RowSet` 对象；这些对象持有表格式的数据，持有方式使得相对于结果集更加便于访问。下面的页面描述了各种可用的 `RowSet` 对象：
  - [使用 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html)
  - [使用 CachedRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/cachedrowset.html)
  - [使用 JoinRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/joinrowset.html)
  - [使用 FilteredRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html)
  - [使用 WebRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html)
- [使用高级数据类型](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqltypes.html) 介绍另外的数据类型。下面的页面更详细地介绍了这些数据类型：
  - [使用大对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html)
  - [使用 SQLXML 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html)
  - [使用 Array 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/array.html)
  - [使用 DISTINCT 数据类型](https://docs.oracle.com/javase/tutorial/jdbc/basics/distinct.html)
  - [使用 Structured 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlstructured.html)
  - [使用自定义类型映射](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlcustommapping.html)
  - [使用 Datalink 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatalink.html)
  - [使用 RowId 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlrowid.html)
- [使用存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html) 向您展示如何创建和使用存储过程，存储过程是一组可以像具有可变输入和输出参数的 Java 方法一样调用的 SQL 语句。
- [使用 JDBC 和 GUI API](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcswing.html) 展示如何集成 JDBC 和 Swing API。

### 起步

本课程中的示例代码创建一个数据库供一家名为 The Coffee Break 的小咖啡馆使用，该咖啡馆按照磅来购买咖啡豆，咖啡按照杯出售。

下面的步骤配置一个 JDBC 开发环境，你可以在其中编译和运行本课程中的示例代码：

1. [安装最新版本的 Java SE SDK 到你的电脑上](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step1)
2. [按需安装你的数据库管理系统 DBMS](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step2)
3. [安装来自数据库供应商的 JDBC 驱动](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step3)
4. [安装 Apache Ant](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step4)
5. [安装 Apache Xalan](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step5)
6. [下载示例代码](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step6)
7. [修改 `build.xml` 文件](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step7)
8. [修改示例属性文件](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step8)
9. [编译和打包示例](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step9)
10. [创建数据库、表、并填充表](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step10)
11. [运行示例](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html#step11)

**安装最新版本的 Java SE SDK 在你的电脑上**

确保 Java SE SDK 的 `bin` 目录的完整路径包含在你的 `PATH` 环境变量中，以使得你可以在任何目录下直接运行 Java 编译器和 Java 程序启动器。

**按需安装你的数据库管理系统 DBMS**

你可以使用 Java DB，随着最新版本的 Java SE SDK 提供。本课程中的示例已经通过了下列 DBMS 测试：

- [Java DB](http://www.oracle.com/technetwork/java/javadb/overview/index.html)
- [MySQL](http://www.mysql.com/)

注意，如果你使用的是别的 DBMS，就可能需要修改示例代码。

**安装来自数据库提供商的 JDBC 驱动**

如果你正在使用 Java DB，那么它已经携带了 JDBC 驱动。如果你真在使用 MySQL,，安装最新版本的 [Connector/J](http://www.mysql.com/products/connector/) 。

联系你的数据库产品提供商来获取相应的 JDBC 驱动。

JDBC 驱动存在很多种可能实现。这些实现分类如下：

- **Type 1**: 驱动程序将JDBC API实现为另一个数据访问 API 的映射，例如ODBC（开放式数据库连接）。此类驱动程序通常依赖于本地库，这限制了它们的可移植性。JDBC-ODBC Bridge是Type 1驱动程序的例子。

  **Note**: JDBC-ODBC Bridge应被视为过渡解决方案。Oracle不支持它。仅当您的 DBMS 不提供 Java-only 的 JDBC 驱动程序时才应该考虑使用此选项。

- **Type 2**: 部分使用Java编程语言编写，部分使用本地代码编写的驱动程序。这些驱动程序使用特定于它们所连接的数据源的本地客户端库。同样，由于本机代码，它们的可移植性是有限的。Oracle的OCI（Oracle调用接口）客户端驱动程序是Type 2驱动程序的一个例子。

- **Type 3**: 使用纯Java客户端并使用独立于数据库的协议与中间件服务器通信的驱动程序。然后，中间件服务器将客户端的请求传递给数据源。

- **Type 4**: 纯Java的驱动程序，并为特定数据源实现网络协议。客户端直接连接到数据源。

检查 DBMS 附带的驱动程序类型。Java DB 附带两个 Type 4 驱动程序，一个嵌入式驱动程序和一个网络客户端驱动程序。MySQL Connector/J 是 Type 4 驱动程序。

安装 JDBC 驱动程序通常包括将驱动程序复制到计算机，然后将其位置添加到类路径中。此外，除 Type 4 驱动程序之外的许多 JDBC 驱动程序都要求您安装客户端 API。通常不需要其他特殊配置。

**安装 Apache Ant**

这些步骤使用 Apache Ant（一种基于Java的工具）来构建，编译和运行 JDBC 教程示例。转到以下链接下载 Apache Ant：

```
http://ant.apache.org/
```

确保 Apache Ant 可执行文件位于您的`PATH`环境变量中，以便您可以从任何目录运行它。

**安装 Apache Xalan**

在 [使用SQLXML对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html) 中描述的示例`RSSFeedsTable.java`如果您的 DBMS 是 Java DB，则需要 Apache Xalan。该示例使用 Apache Xalan-Java。转到以下链接下载它：

```
http://xml.apache.org/xalan-j/
```

**下载示例代码**

 `JDBCTutorial.zip` ，包含以下文件：

- ```
  properties
  ```

  - `javadb-build-properties.xml`
  - `javadb-sample-properties.xml`
  - `mysql-build-properties.xml`
  - `mysql-sample-properties.xml`

- ```
  sql
  ```

  - ```
    javadb
    ```

    - `create-procedures.sql`
    - `create-tables.sql`
    - `drop-tables.sql`
    - `populate-tables.sql`

  - ```
    mysql
    ```

    - `create-procedures.sql`
    - `create-tables.sql`
    - `drop-tables.sql`
    - `populate-tables.sql`

- ```
  src/com/oracle/tutorial/jdbc
  ```

  - `CachedRowSetSample.java`
  - `CityFilter.java`
  - `ClobSample.java`
  - `CoffeesFrame.java`
  - `CoffeesTable.java`
  - `CoffeesTableModel.java`
  - `DatalinkSample.java`
  - `ExampleRowSetListener.java`
  - `FilteredRowSetSample.java`
  - `JdbcRowSetSample.java`
  - `JDBCTutorialUtilities.java`
  - `JoinSample.java`
  - `ProductInformationTable.java`
  - `RSSFeedsTable.java`
  - `StateFilter.java`
  - `StoredProcedureJavaDBSample.java`
  - `StoredProcedureMySQLSample.java`
  - `SuppliersTable.java`
  - `WebRowSetSample.java`

- ```
  txt
  ```

  - `colombian-description.txt`

- ```
  xml
  ```

  - `rss-coffee-industry-news.xml`
  - `rss-the-coffee-break-blog.xml`

- `build.xml`

创建一个目录以包含该示例的所有文件。下面步骤中将此目录称为`*<JDBC tutorial directory>*`。将`JDBCTutorial.zip`的内容解压缩到`* <JDBC tutorial directory> *`中。

**修改 build.xml 文件**

`build.xml`文件是Apache Ant用于编译和执行JDBC示例的构建文件。文件`properties/javadb-build-properties.xml`和`properties/mysql-build-properties.xml`分别包含Java DB和MySQL所需的其他Apache Ant属性。文件`properties/javadb-sample-properties.xml`和`properties/mysql-sample-properties.xml`包含示例所需的属性。

修改这些XML文件，如下所示：

**修改 build.xml**

在`build.xml`文件中，修改属性`ANTPROPERTIES`以引用`properties/javadb-build-properties.xml`或`properties/mysql-build-properties.xml`，具体取决于您的DBMS。例如，如果您使用的是Java DB，那么`build.xml`文件将包含以下内容：

```xml
<property
  name="ANTPROPERTIES"
  value="properties/javadb-build-properties.xml"/>

  <import file="${ANTPROPERTIES}"/>
```

同样，如果您使用的是MySQL，那么`build.xml`文件将包含以下内容：

```xml
<property
  name="ANTPROPERTIES"
  value="properties/mysql-build-properties.xml"/>

  <import file="${ANTPROPERTIES}"/>
```

**修改特定于数据库的属性文件**

在`properties/javadb-build-properties.xml`或`properties/mysql-build-properties.xml`文件中（取决于您的DBMS），修改以下属性，如下表所述：

| Property             | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| `JAVAC`              | The full path name of your Java compiler, `javac`            |
| `JAVA`               | The full path name of your Java runtime executable, `java`   |
| `PROPERTIESFILE`     | The name of the properties file, either `properties/javadb-sample-properties.xml` or `properties/mysql-sample-properties.xml` |
| `MYSQLDRIVER`        | The full path name of your MySQL driver. For Connector/J, this is typically `*<Connector/J installation directory>*/mysql-connector-java-*version-number*.jar`. |
| `JAVADBDRIVER`       | The full path name of your Java DB driver. This is typically `*<Java DB installation directory>*/lib/derby.jar`. |
| `XALANDIRECTORY`     | The full path name of the directory that contains Apache Xalan. |
| `CLASSPATH`          | The class path that the JDBC tutorial uses. *You do not need to change this value.* |
| `XALAN`              | The full path name of the file `xalan.jar`.                  |
| `DB.VENDOR`          | A value of either `derby` or `mysql` depending on whether you are using Java DB or MySQL, respectively. The tutorial uses this value to construct the URL required to connect to the DBMS and identify DBMS-specific code and SQL statements. |
| `DB.DRIVER`          | The fully qualified class name of the JDBC driver. For Java DB, this is `org.apache.derby.jdbc.EmbeddedDriver`. For MySQL, this is `com.mysql.jdbc.Driver`. |
| `DB.HOST`            | The host name of the computer hosting your DBMS.             |
| `DB.PORT`            | The port number of the computer hosting your DBMS.           |
| `DB.SID`             | The name of the database the tutorial creates and uses.      |
| `DB.URL.NEWDATABASE` | The connection URL used to connect to your DBMS when creating a new database. *You do not need to change this value.* |
| `DB.URL`             | The connection URL used to connect to your DBMS. *You do not need to change this value.* |
| `DB.USER`            | The name of the user that has access to create databases in the DBMS. |
| `DB.PASSWORD`        | The password of the user specified in `DB.USER`.             |
| `DB.DELIMITER`       | The character used to separate SQL statements. *Do not change this value.* It should be the semicolon character (`;`). |

**修改教程属性文件**

教程示例使用`properties/javadb-sample-properties.xml`文件或`properties/mysql-sample-properties.xml`文件（取决于您的DBMS）中的值来连接到DBMS并初始化数据库和表 ，如下表所述：

| Property        | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| `dbms`          | A value of either `derby` or `mysql` depending on whether you are using Java DB or MySQL, respectively. The tutorial uses this value to construct the URL required to connect to the DBMS and identify DBMS-specific code and SQL statements. |
| `jar_file`      | The full path name of the JAR file that contains all the class files of this tutorial. |
| `driver`        | The fully qualified class name of the JDBC driver. For Java DB, this is `org.apache.derby.jdbc.EmbeddedDriver`. For MySQL, this is `com.mysql.jdbc.Driver`. |
| `database_name` | The name of the database the tutorial creates and uses.      |
| `user_name`     | The name of the user that has access to create databases in the DBMS. |
| `password`      | The password of the user specified in `user_name`.           |
| `server_name`   | The host name of the computer hosting your DBMS.             |
| `port_number`   | The port number of the computer hosting your DBMS.           |

**注意**：为了简单地演示JDBC API，JDBC教程示例代码不执行已部署系统通常使用的密码管理技术。在生产环境中，您可以遵循Oracle数据库密码管理准则并禁用任何示例帐户。请参阅  [*Oracle Database Security Guide*](http://docs.oracle.com/cd/B28359_01/network.111/b28531/toc.htm)  中的  [Managing Security for Application Developers](http://docs.oracle.com/cd/B28359_01/network.111/b28531/app_devs.htm) 中的 [Securing Passwords in Application Design](http://docs.oracle.com/cd/B28359_01/network.111/b28531/app_devs.htm#CJADABGG) 用于密码管理指南和其他安全建议。

**编译并打包示例程序**

在命令提示符下，将当前目录切换到`*<JDBC tutorial directory>*`。从此目录中，运行以下命令以编译示例并将其打包在jar文件中：

```
ant jar
```

**创建数据库，表，并填充表**

如果您使用的是MySQL，请运行以下命令来创建数据库：

```
ant create-mysql-database
```

**注意**：为buildDB创建数据库的`build.xml`文件中没有相应的Ant目标。用于建立数据库连接的Java DB的数据库URL包括创建数据库的选项（如果它尚不存在）。有关详细信息，请参阅 [Establishing a Connection](https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html) 。

如果您使用的是Java DB或MySQL，则从同一目录运行以下命令以删除现有的示例数据库表，重新创建表并填充它们。对于Java DB，此命令还会创建数据库（如果该数据库尚不存在）：

```
ant setup
```

**注意**：每次运行示例中的一个Java类之前，都应该运行命令`ant setup`。其中许多样本都希望样本数据库表的内容中包含特定数据。

**运行示例**

`build.xml`文件中的每个目标对应于JDBC示例中的Java类或SQL脚本。下表列出了`build.xml`文件中的目标，每个目标执行的类或脚本，以及每个目标所需的其他类或文件：

| Ant Target                | Class or SQL Script                                          | Other Required Classes or Files                              |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `javadb-create-procedure` | `javadb/create-procedures.sql`; see the `build.xml`file to view other SQL statements that are run | No other required files                                      |
| `mysql-create-procedure`  | `mysql/create-procedures.sql`.                               | No other required files                                      |
| `run`                     | `JDBCTutorialUtilities`                                      | No other required classes                                    |
| `runct`                   | `CoffeesTable`                                               | `JDBCTutorialUtilities`                                      |
| `runst`                   | `SuppliersTable`                                             | `JDBCTutorialUtilities`                                      |
| `runjrs`                  | `JdbcRowSetSample`                                           | `JDBCTutorialUtilities`                                      |
| `runcrs`                  | `CachedRowSetSample`, `ExampleRowSetListener`                | `JDBCTutorialUtilities`                                      |
| `runjoin`                 | `JoinSample`                                                 | `JDBCTutorialUtilities`                                      |
| `runfrs`                  | `FilteredRowSetSample`                                       | `JDBCTutorialUtilities`, `CityFilter`, `StateFilter`         |
| `runwrs`                  | `WebRowSetSample`                                            | `JDBCTutorialUtilities`                                      |
| `runclob`                 | `ClobSample`                                                 | `JDBCTutorialUtilities`, `txt/colombian-description.txt`     |
| `runrss`                  | `RSSFeedsTable`                                              | `JDBCTutorialUtilities`, the XML files contained in the `xml` directory |
| `rundl`                   | `DatalinkSample`                                             | `JDBCTutorialUtilities`                                      |
| `runspjavadb`             | `StoredProcedureJavaDBSample`                                | `JDBCTutorialUtilities`, `SuppliersTable`, `CoffeesTable`    |
| `runspmysql`              | `StoredProcedureMySQLSample`                                 | `JDBCTutorialUtilities`, `SuppliersTable`, `CoffeesTable`    |
| `runframe`                | `CoffeesFrame`                                               | `JDBCTutorialUtilities`, `CoffeesTableModel`                 |

例如，要运行类`CoffeesTable`，请将当前目录切换到`* <JDBC tutorial directory> *`，然后从该目录运行以下命令：

```
ant runct
```

### 使用 JDBC 处理 SQL 语句

通常，为了使用 JDBC 处理任何 SQL 语句，你必须遵循以下步骤：

1. [建立连接](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html#establishing_connections)
2. [创建语句](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html#creating_statements)
3. [执行查询](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html#executing_queries)
4. [处理 `ResultSet` 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html#processing_resultset_objects)
5. [关闭连接](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html#closing_connections)

此页面使用教程示例中的以下方法`CoffeesTables.viewTable`来演示这些步骤。此方法输出表`COFFEES`的内容。本教程后面将详细讨论此方法：

```java
public static void viewTable(Connection con, String dbName)
    throws SQLException {

    Statement stmt = null;
    String query = "select COF_NAME, SUP_ID, PRICE, " +
                   "SALES, TOTAL " +
                   "from " + dbName + ".COFFEES";
    try {
        stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery(query);
        while (rs.next()) {
            String coffeeName = rs.getString("COF_NAME");
            int supplierID = rs.getInt("SUP_ID");
            float price = rs.getFloat("PRICE");
            int sales = rs.getInt("SALES");
            int total = rs.getInt("TOTAL");
            System.out.println(coffeeName + "\t" + supplierID +
                               "\t" + price + "\t" + sales +
                               "\t" + total);
        }
    } catch (SQLException e ) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

**建立连接**

首先，与要使用的数据源建立连接。数据源可以是DBMS，遗留文件系统或具有相应JDBC驱动程序的某些其他数据源。此连接由`Connection`对象表示。有关详细信息，请参阅 [建立连接](https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html) 。

**创建语句**

`Statement`是表示SQL语句的接口。执行`Statement`对象，它们生成`ResultSet`对象，这是一个表示数据库结果集的数据表。你需要一个`Connection`对象来创建一个`Statement`对象。

例如，`CoffeesTables.viewTable`使用以下代码创建一个`Statement`对象：

```java
stmt = con.createStatement();
```

有三种不同的语句：

 - `Statement`：用于实现没有参数的简单SQL语句。
 - `PreparedStatement` ：(扩展`Statement`。）用于预编译可能包含输入参数的SQL语句。有关详细信息，请参阅[使用预编译语句](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 。
 - `CallableStatement：`（扩展`PreparedStatement`。）用于执行可能包含输入和输出参数的存储过程。有关详细信息，请参阅[存储过程](https://docs.oracle.com/javase/tutorial/jdbc/basics/storedprocedures.html) 。

**执行查询**

要执行查询，请从`Statement`调用`execute`方法，如下所示：

 - `execute`：如果查询返回的第一个对象是`ResultSet`对象，则返回`true`。如果查询可以返回一个或多个`ResultSet`对象，请使用此方法。通过重复调用`Statement.getResultSet`来检索从查询返回的`ResultSet`对象。
 - `executeQuery`：返回一个`ResultSet`对象。
 - `executeUpdate`：返回一个整数，表示受SQL语句影响的行数。如果您使用`INSERT`，`DELETE`或`UPDATE` SQL语句，请使用此方法。

例如，`CoffeesTables.viewTable`使用以下代码执行`Statement`对象：

```java
ResultSet rs = stmt.executeQuery（query）;
```

有关详细信息，请参阅[从结果集中检索和修改值](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) 。

**处理结果集对象**

您可以通过游标访问`ResultSet`对象中的数据。请注意，此游标不是数据库游标。该游标是一个指向`ResultSet`对象中一行数据的指针。最初，光标位于第一行之前。您可以调用`ResultSet`对象中定义的各种方法来移动光标。

例如，`CoffeesTables.viewTable`重复调用方法`ResultSet.next`将光标向前移动一行。每次调用`next`时，该方法都会输出光标当前所在行的数据：

```java
try {
    stmt = con.createStatement();
    ResultSet rs = stmt.executeQuery(query);
    while (rs.next()) {
        String coffeeName = rs.getString("COF_NAME");
        int supplierID = rs.getInt("SUP_ID");
        float price = rs.getFloat("PRICE");
        int sales = rs.getInt("SALES");
        int total = rs.getInt("TOTAL");
        System.out.println(coffeeName + "\t" + supplierID +
                           "\t" + price + "\t" + sales +
                           "\t" + total);
    }
}
// ...
```

参考 [Retrieving and Modifying Values from Result Sets](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) 获取更多信息。

**关闭连接**

当你完成使用`Statement`时，调用方法`Statement.close`立即释放它正在使用的资源。当您调用此方法时，其`ResultSet`对象将被关闭。

例如，方法`CoffeesTables.viewTable`通过将它包装在`finally`块中，确保在方法结束时关闭`Statement`对象，而不管抛出任何`SQLException`对象：

```java
} finally {
    if (stmt != null) { stmt.close(); }
}
```

JDBC在与数据源交互期间遇到错误时会抛出`SQLException`。有关详细信息，请参阅[处理SQL异常](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlexception.html) 。

在Java SE 7及更高版本中可用的JDBC 4.1中，您可以使用`try-with-resources`语句自动关闭`Connection`，`Statement`和`ResultSet`对象，无论是否已经抛出`SQLException ` 。自动资源语句由`try`语句和一个或多个声明的资源组成。例如，您可以修改`CoffeesTables.viewTable`，使其`Statement`对象自动关闭，如下所示：

```java
public static void viewTable(Connection con) throws SQLException {

    String query = "select COF_NAME, SUP_ID, PRICE, " +
                   "SALES, TOTAL " +
                   "from COFFEES";

    try (Statement stmt = con.createStatement()) {

        ResultSet rs = stmt.executeQuery(query);

        while (rs.next()) {
            String coffeeName = rs.getString("COF_NAME");
            int supplierID = rs.getInt("SUP_ID");
            float price = rs.getFloat("PRICE");
            int sales = rs.getInt("SALES");
            int total = rs.getInt("TOTAL");
            System.out.println(coffeeName + ", " + supplierID +
                               ", " + price + ", " + sales +
                               ", " + total);
        }
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    }
}
```

以下语句是一个`try-with-resources`语句，它声明了一个资源`stmt`，它将在`try`块终止时自动关闭：

```java
try (Statement stmt = con.createStatement()) {
    // ...
}
```

参考 [Essential Classes](https://docs.oracle.com/javase/tutorial/essential/index.html) 中的 [The `try`-with-resources Statement](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html) 部分获取更多信息。

### 建立连接

首先，您需要与要使用的数据源建立连接。数据源可以是DBMS，遗留文件系统或具有相应JDBC驱动程序的某些其他数据源。通常，JDBC应用程序使用以下两个类之一连接到目标数据源：

 - `DriverManager`：这个完全实现的类将应用程序连接到数据源，数据源由数据库URL指定。当此类首次尝试建立连接时，它会自动加载在类路径中找到的任何JDBC 4.0驱动程序。请注意，在JDBC 4.0版本之前您的应用程序必须手动加载驱动程序。
 - `DataSource`：这个接口比`DriverManager`更受欢迎，因为它允许底层数据源的细节对你的应用程序是透明的。设置`DataSource`对象的属性，使其表示特定的数据源。有关详细信息，请参阅[与DataSource对象连接](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html) 。有关使用`DataSource`类开发应用程序的更多信息，请参阅最新的*Java EE 教程*。

**注意**：本教程中的示例使用`DriverManager`类而不是`DataSource`类，因为它更易于使用，并且示例不需要`DataSource`类的功能。

此页面包含以下主题：

 -  [使用DriverManager类](https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html#drivermanager)
 -  [指定数据库连接URL](https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html#db_connection_url)

**使用 DriverManager 类**

使用`DriverManager`类连接到DBMS涉及调用方法`DriverManager.getConnection`。以下方法`JDBCTutorialUtilities.getConnection`建立数据库连接：

```java
public Connection getConnection() throws SQLException {

    Connection conn = null;
    Properties connectionProps = new Properties();
    connectionProps.put("user", this.userName);
    connectionProps.put("password", this.password);

    if (this.dbms.equals("mysql")) {
        conn = DriverManager.getConnection(
                   "jdbc:" + this.dbms + "://" +
                   this.serverName +
                   ":" + this.portNumber + "/",
                   connectionProps);
    } else if (this.dbms.equals("derby")) {
        conn = DriverManager.getConnection(
                   "jdbc:" + this.dbms + ":" +
                   this.dbName +
                   ";create=true",
                   connectionProps);
    }
    System.out.println("Connected to database");
    return conn;
}
```

方法`DriverManager.getConnection`建立数据库连接。此方法需要数据库URL，具体取决于您的DBMS。以下是数据库URL的一些示例：

1. MySQL：`jdbc:mysql://localhost:3306/`，其中`localhost`是托管数据库的服务器的名称，`3306`是端口号

2. Java DB：`jdbc:derby:*testdb*;create=true`，其中`testdb`是要连接的数据库的名称，`create=true`指示DBMS创建数据库。

    **注意**：此URL与Java DB嵌入式驱动程序建立数据库连接。 Java DB还包括一个网络客户端驱动程序，它使用不同的URL。

此方法使用`Properties`对象指定访问DBMS所需的用户名和密码。

**注意**：

 - 通常，在数据库URL中，还指定要连接的现有数据库的名称。例如，URL `jdbc:mysql://localhost:3306/mysql` 表示名为`mysql`的MySQL数据库的数据库URL。本教程中的示例使用未指定特定数据库的URL，因为示例创建了一个新数据库。

 - 在以前的JDBC版本中，要获得连接，首先必须通过调用方法`Class.forName`来初始化JDBC驱动程序。此方法需要一个类型为`java.sql.Driver`的对象。每个JDBC驱动程序都包含一个或多个实现接口`java.sql.Driver`的类。 Java DB的驱动程序是`org.apache.derby.jdbc.EmbeddedDriver`和`org.apache.derby.jdbc.ClientDriver`，而MySQL Connector/J的驱动程序是`com.mysql.jdbc.Driver`。请参阅DBMS驱动程序的文档以获取实现接口`java.sql.Driver`的类的名称。

   在类路径中找到的任何JDBC 4.0驱动程序都会自动加载。 （但是，您必须使用方法`Class.forName`手动加载JDBC 4.0之前的任何驱动程序。）

该方法返回一个`Connection`对象，该对象表示与DBMS或特定数据库的连接。通过此对象查询数据库。

**指定数据库连接 URL**

数据库连接URL是DBMS JDBC驱动程序用于连接数据库的字符串。它可以包含诸如搜索数据库的位置，要连接的数据库的名称以及配置属性等信息。数据库连接URL的确切语法由DBMS指定。

**Java DB 数据库连接 URLs**

以下是Java DB的数据库连接URL语法：

```
jdbc:derby:[subsubprotocol:][databaseName]
    [;attribute=value]*
```

 - `subsubprotocol`指定Java DB应在目录，内存，类路径或JAR文件中搜索数据库的位置。通常省略它。
 - `databaseName`是要连接的数据库的名称。
 - `attribute = value`表示可选的，以分号分隔的属性列表。这些属性使您可以指示Java DB执行各种任务，包括以下内容：
    - 创建连接URL中指定的数据库。
    - 加密连接URL中指定的数据库。
    - 指定存储日志记录和跟踪信息的目录。
    - 指定用于连接数据库的用户名和密码。

有关详细信息，请参阅 [Java DB Technical Documentation](http://docs.oracle.com/javadb/index_jdk8.html) 中的*Java DB开发人员指南*和*Java DB参考手册*。

**MySQL Connector/J 数据库 URL**

以下是MySQL Connector/J的数据库连接URL语法：

```
jdbc:mysql://[host][,failoverhost...]
    [:port]/[database]
    [?propertyName1][=propertyValue1]
    [&propertyName2][=propertyValue2]...
```

 - `host:port`是托管数据库的计算机的主机名和端口号。如果未指定，则`host`和`port`的默认值分别为`127.0.0.1`和`3306`。
 - `database`是要连接的数据库的名称。如果未指定，则建立连接而不使用默认数据库。
 - `failover`是备用数据库的名称（MySQL Connector/J支持故障转移）。
 - `propertyName=propertyValue`表示一个可选的，与`＆`符号分隔的属性列表。这些属性使您可以指示MySQL Connector/J执行各种任务。

有关详细信息，请参阅 [*MySQL Reference Manual*](http://dev.mysql.com/doc/) 。

### 连接 DataSource 对象

本节介绍`DataSource`对象，它是获取数据源连接的首选方法。除了将在后面解释的其他优点之外，`DataSource`对象还可以提供连接池和分布式事务。此功能对于企业数据库计算至关重要。特别是，它是 Enterprise JavaBeans (EJB) 技术不可或缺的一部分。

本节介绍如何使用`DataSource`接口获取连接以及如何使用分布式事务和连接池。这两者都涉及JDBC应用程序中很少的代码更改。

部署使这些操作成为可能的类，系统管理员通常使用工具（例如Apache Tomcat或Oracle WebLogic Server）执行，所执行的工作因所部署的`DataSource`对象的类型而异。因此，本节的大部分内容专门用于说明系统管理员如何设置环境，以便程序员可以使用`DataSource`对象来获取连接。

本章节涵盖以下主题：

- [使用 DataSource 对象获取连接](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html#datasource_connection)
- [部署基本的 DataSource 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html#deploy_datasource)
- [部署其他 DataSource 实现](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html#datasource_implementation)
- [获取并使用连接池](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html#pooled_connection)
- [部署分布式事务](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html#deployment_distributed_transactions)
- [使用分布式事务的连接](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html#using_connections_distributed_transactions)

**使用 DataSource 对象获取连接**

在 [Establishing a Connection](https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html) 中，您学习了如何使用`DriverManager`类获取连接。本节介绍如何使用`DataSource`对象获取与数据源的连接，这是首选方法。

由实现`DataSource`的类实例化的对象表示特定的DBMS或某些其他数据源，例如文件。`DataSource`对象表示特定的DBMS或某些其他数据源，例如文件。如果公司使用多个数据源，它将为每个数据源部署一个单独的`DataSource`对象。`DataSource`接口由驱动程序供应商实现。它可以通过三种不同的方式实现：

- 基本的`DataSource`实现，生成标准的`Connection`对象，这些连接对象没有你池化，这些对象不是在分布式事务中使用的。
- 支持连接池的`DataSource`实现，产生参与连接池的`Connection`对象，即可以回收的连接。
- 支持分布式事务的`DataSource`实现，产生可以在分布式事务中使用的`Connection`对象，即访问两个或多个DBMS服务器的事务。

JDBC驱动程序至少应包含一个基本的`DataSource`实现。例如，Java DB JDBC驱动程序包括实现`org.apache.derby.jdbc.ClientDataSource`和用于MySQL的，`com.mysql.jdbc.jdbc2.optional.MysqlDataSource`。如果您的客户端在Java 8 compact profile 2上运行，那么Java DB JDBC驱动程序是`org.apache.derby.jdbc.BasicClientDataSource40`。本教程的示例需要  compact profile 3 或更高版本。

支持分布式事务的`DataSource`类通常还实现对连接池的支持。例如，EJB供应商提供的`DataSource`类几乎总是支持连接池和分布式事务。

假设之前的例子中，兴旺的咖啡店连锁店的所有者决定通过互联网进一步扩大销售咖啡。由于预计会有大量的在线业务，所有者肯定需要连接池。打开和关闭连接涉及大量开销，并且所有者预计该在线订购系统将需要大量的查询和更新。通过连接池，可以反复使用连接池，从而避免为每个数据库访问创建新连接的费用。此外，所有者现在拥有第二个DBMS，其中包含最近收购的咖啡烘焙公司的数据。这意味着所有者希望能够编写使用旧DBMS服务器和新DBMS服务器的分布式事务。

连锁店主已重新配置计算机系统，以服务于更大的新客户群。所有者购买了最新的JDBC驱动程序和与其一起使用的EJB应用程序服务器，以便能够使用分布式事务并获得连接池带来的更高性能。许多JDBC驱动程序与最近购买的EJB服务器兼容。所有者现在具有三层体系结构，中间层有一个新的EJB应用服务器和JDBC驱动程序，第二层有两个DBMS服务器。发出请求的客户端计算机是第一层。

**部署基本的 DataSource 对象**

系统管理员需要部署`DataSource`对象，以便Coffee Break的编程团队可以开始使用它们。部署`DataSource`对象包含三个任务：

1. 创建`DataSource`类的实例
2. 设置其属性
3. 将其注册到使用Java命名和目录接口（JNDI）API的命名服务

首先，考虑最基本的情况，即使用`DataSource`接口的基本实现，即不支持连接池或分布式事务的接口。在这种情况下，只需要部署一个`DataSource`对象。`DataSource`的基本实现产生了与`DriverManager`类产生的相同类型的连接。

**创建 DataSource 类实例并设置其属性**

假设一个只想要基本实现`DataSource`的公司从JDBC供应商 DB Access, Inc 购买了一个驱动程序。该驱动程序包含实现`DataSource`接口的`com.dbaccess.BasicDataSource`类。以下代码片段创建类`BasicDataSource`的实例并设置其属性。在部署了`BasicDataSource`实例之后，程序员可以调用方法`DataSource.getConnection`来获得与公司数据库`CUSTOMER_ACCOUNTS`的连接。首先，系统管理员使用默认构造函数创建`BasicDataSource`对象`ds`。然后系统管理员设置三个属性。请注意，以下代码通常由部署工具执行：

```java
com.dbaccess.BasicDataSource ds = new com.dbaccess.BasicDataSource();
ds.setServerName("grinder");
ds.setDatabaseName("CUSTOMER_ACCOUNTS");
ds.setDescription("Customer accounts database for billing");
```

变量`ds`现在表示服务器上安装的数据库`CUSTOMER_ACCOUNTS`。由`BasicDataSource`对象`ds`生成的任何连接都将是与数据库`CUSTOMER_ACCOUNTS`的连接。

**使用 JNDI API 注册 DataSource 对象到名称服务**

通过设置属性，系统管理员可以使用JNDI（Java命名和目录接口）命名服务注册`BasicDataSource`对象。使用的特定命名服务通常由系统属性确定，此处未显示。以下代码片段注册了`BasicDataSource`对象并将其与逻辑名称`jdbc/billingDB`绑定：

```java
Context ctx = new InitialContext();
ctx.bind("jdbc/billingDB", ds);
```

此代码使用JNDI API。第一行创建一个`InitialContext`对象，它作为名称的起始点，类似于文件系统中的根目录。第二行将`BasicDataSource`对象`ds`关联或绑定到逻辑名`jdbc/billingDB`。在下一个代码片段中，您将为命名服务提供此逻辑名称，并返回`BasicDataSource`对象。逻辑名称可以是任何字符串。在这种情况下，公司决定使用名称`billingDB`作为`CUSTOMER_ACCOUNTS`数据库的逻辑名。

在前面的示例中，`jdbc`是初始上下文下的子上下文，就像根目录下的目录是子目录一样。名称`jdbc/billingDB`类似于路径名，其中路径中的最后一项与文件名类似。在这种情况下，`billingDB`是给`BasicDataSource`对象`ds`的逻辑名。子上下文`jdbc`保留用于绑定到`DataSource`对象的逻辑名，因此`jdbc`将始终是数据源的逻辑名的第一部分。

**使用部署的 DataSource 对象**

在系统管理员部署了基本的`DataSource`实现之后，程序员就可以使用它了。这意味着程序员可以提供绑定到`DataSource`类实例的逻辑数据源名称，JNDI命名服务将返回该`DataSource`类的实例。然后可以在`DataSource`对象上调用方法`getConnection`以获得与它所代表的数据源的连接。例如，程序员可能会编写以下两行代码来获取一个`DataSource`对象，该对象生成与数据库`CUSTOMER_ACCOUNTS`的连接。

```java
Context ctx = new InitialContext();
DataSource ds = (DataSource)ctx.lookup("jdbc/billingDB");
```

第一行代码获取初始上下文作为检索`DataSource`对象的起点。当您向方法`lookup`提供逻辑名称`jdbc/billingDB`时，该方法返回系统管理员在部署时绑定到`jdbc/billingDB`的`DataSource`对象。因为`lookup`方法的返回值是Java `Object`，所以我们必须将它转换为更具体的`DataSource`类型，然后再将它赋给变量`ds`。

变量`ds`是实现`DataSource`接口的`com.dbaccess.BasicDataSource`类的实例。调用方法`ds.getConnection`会产生与`CUSTOMER_ACCOUNTS`数据库的连接。

```java
Connection con = ds.getConnection("fernanda","brewed");
```

`getConnection`方法只需要用户名和密码，因为变量`ds`具有在其属性中与`CUSTOMER_ACCOUNTS`数据库建立连接所需的其余信息，例如数据库名称和位置。

**DataSource 对象的优点**

由于它的属性，`DataSource`对象比获取连接的`DriverManager`类更好。程序员不再需要在其应用程序中对驱动程序名称或JDBC URL进行硬编码，这使得它们更具可移植性。此外，`DataSource`属性使维护代码更加简单。如果有更改，系统管理员可以更新数据源属性，而不用担心更改连接到数据源的每个应用程序。例如，如果数据源被移动到不同的服务器，则系统管理员所要做的就是将`serverName`属性设置为新的服务器名称。

除了可移植性和易维护性之外，使用`DataSource`对象获取连接还可以提供其他优势。当实现`DataSource`接口以使用`ConnectionPoolDataSource`实现时，该`DataSource`类的实例产生的所有连接将自动成为池化连接。类似地，当实现`DataSource`实现以使用`XADataSource`类时，它产生的所有连接将自动成为可以在分布式事务中使用的连接。下一节将介绍如何部署这些类型的`DataSource`实现。

**部署其他 DataSource 实现**

系统管理员或以该角色工作的其他人可以部署`DataSource`对象，以便它产生的连接是池化连接。为此，他首先部署一个`ConnectionPoolDataSource`对象，然后部署一个`DataSource`对象来实现它。设置`ConnectionPoolDataSource`对象的属性，使其表示将生成连接的数据源。在使用JNDI命名服务注册`ConnectionPoolDataSource` 对象之后，部署`DataSource`对象。通常只需要为`DataSource`对象设置两个属性：`description`和`dataSourceName`。赋给`dataSourceName` 属性的值是标识先前部署的`ConnectionPoolDataSource`对象的逻辑名，该对象包含进行连接所需的属性。

部署了`ConnectionPoolDataSource`和`DataSource`对象后，可以在`DataSource`对象上调用`DataSource.getConnection`方法并获得池连接。此连接将是`ConnectionPoolDataSource`对象属性中指定的数据源。

以下示例描述了The Coffee Break的系统管理员如何部署实现为提供池连接的`DataSource`对象。系统管理员通常使用部署工具，因此本节中显示的代码片段是部署工具将执行的代码。

为了获得更好的性能，The Coffee Break公司从 DB Access, Inc 购买了一个JDBC驱动程序，其中包含`com.dbaccess.ConnectionPoolDS`类，它实现了`ConnectionPoolDataSource`接口。系统管理员创建创建此类的实例，设置其属性，并将其注册到JNDI命名服务。Coffee Break从其EJB服务器供应商Application Logic, Inc 购买了它的`DataSource`类`com.applogic.PooledDataSource` 。`com.applogic.PooledDataSource`类通过使用由`ConnectionPoolDataSource`类和`com.dbaccess.ConnectionPoolDS`提供的底层支持来实现连接池。

必须首先部署`ConnectionPoolDataSource`对象。以下代码创建`com.dbaccess.ConnectionPoolDS`的实例并设置其属性：

```java
com.dbaccess.ConnectionPoolDS cpds = new com.dbaccess.ConnectionPoolDS();
cpds.setServerName("creamer");
cpds.setDatabaseName("COFFEEBREAK");
cpds.setPortNumber(9040);
cpds.setDescription("Connection pooling for " + "COFFEEBREAK DBMS");
```

在部署`ConnectionPoolDataSource`对象之后，系统管理员部署`DataSource`对象。以下代码使用JNDI命名服务注册`com.dbaccess.ConnectionPoolDS`对象`cpds`。请注意，与`cpds`变量关联的逻辑名称在子上下文`jdbc`下添加了子上下文`pool`，这类似于将子目录添加到分层文件系统中的另一个子目录。类`com.dbaccess.ConnectionPoolDS`的任何实例的逻辑名将始终以`jdbc/pool`开头。Oracle建议将所有`ConnectionPoolDataSource`对象放在子上下文`jdbc/pool`下：

```java
Context ctx = new InitialContext();
ctx.bind("jdbc/pool/fastCoffeeDB", cpds);
```

接下来，部署实现与`cpds`变量和`com.dbaccess.ConnectionPoolDS`类的其他实例交互的`DataSource`类。以下代码创建此类的实例并设置其属性。请注意，只为此`com.applogic.PooledDataSource`实例设置了两个属性。设置`description`属性是因为它始终是必需的。设置的另一个属性`dataSourceName`为`cpds`提供了逻辑JNDI名称，它是`com.dbaccess.ConnectionPoolDS`类的一个实例。换句话说，`cpds `表示将实现`DataSource`对象的连接池的`ConnectionPoolDataSource`对象。

以下代码可能由部署工具执行，它创建一个`PooledDataSource`对象，设置其属性，并将其绑定到逻辑名称`jdbc/fastCoffeeDB`：

```java
com.applogic.PooledDataSource ds = new com.applogic.PooledDataSource();
ds.setDescription("produces pooled connections to COFFEEBREAK");
ds.setDataSourceName("jdbc/pool/fastCoffeeDB");
Context ctx = new InitialContext();
ctx.bind("jdbc/fastCoffeeDB", ds);
```

此时，部署了一个`DataSource`对象，应用程序可以从该对象获得与数据库`COFFEEBREAK`的池化连接。

**获取并使用连接池**

A *connection pool* is a cache of database connection objects. The objects represent physical database connections that can be used by an application to connect to a database. At run time, the application requests a connection from the pool. If the pool contains a connection that can satisfy the request, it returns the connection to the application. If no connections are found, a new connection is created and returned to the application. The application uses the connection to perform some work on the database and then returns the object back to the pool. The connection is then available for the next connection request.

Connection pools promote the reuse of connection objects and reduce the number of times that connection objects are created. Connection pools significantly improve performance for database-intensive applications because creating connection objects is costly both in terms of time and resources.

Now that these `DataSource` and `ConnectionPoolDataSource` objects are deployed, a programmer can use the `DataSource` object to get a pooled connection. The code for getting a pooled connection is just like the code for getting a nonpooled connection, as shown in the following two lines:

```
ctx = new InitialContext();
ds = (DataSource)ctx.lookup("jdbc/fastCoffeeDB");
```

The variable `*ds*` represents a `DataSource` object that produces pooled connections to the database `COFFEEBREAK`. You need to retrieve this `DataSource` object only once because you can use it to produce as many pooled connections as needed. Calling the method `getConnection` on the `*ds*` variable automatically produces a pooled connection because the `DataSource` object that the `*ds*` variable represents was configured to produce pooled connections.

Connection pooling is generally transparent to the programmer. There are only two things you need to do when you are using pooled connections:

1. Use a `DataSource` object rather than the `DriverManager` class to get a connection. In the following line of code, `*ds*`is a `DataSource` object implemented and deployed so that it will create pooled connections and `username` and `password` are variables that represent the credentials of the user that has access to the database:

   ```
   Connection con = ds.getConnection(username, password);
   ```

2. Use a `finally` statement to close a pooled connection. The following `finally` block would appear after the `try/catch` block that applies to the code in which the pooled connection was used:

   ```
   try {
       Connection con = ds.getConnection(username, password);
       // ... code to use the pooled
       // connection con
   } catch (Exception ex {
       // ... code to handle exceptions
   } finally {
       if (con != null) con.close();
   }
   ```

Otherwise, an application using a pooled connection is identical to an application using a regular connection. The only other thing an application programmer might notice when connection pooling is being done is that performance is better.

The following sample code gets a `DataSource` object that produces connections to the database `COFFEEBREAK` and uses it to update a price in the table `COFFEES`:

```
import java.sql.*;
import javax.sql.*;
import javax.ejb.*;
import javax.naming.*;

public class ConnectionPoolingBean implements SessionBean {

    // ...

    public void ejbCreate() throws CreateException {
        ctx = new InitialContext();
        ds = (DataSource)ctx.lookup("jdbc/fastCoffeeDB");
    }

    public void updatePrice(float price, String cofName,
                            String username, String password)
        throws SQLException{

        Connection con;
        PreparedStatement pstmt;
        try {
            con = ds.getConnection(username, password);
            con.setAutoCommit(false);
            pstmt = con.prepareStatement("UPDATE COFFEES " +
                        "SET PRICE = ? " +
                        "WHERE COF_NAME = ?");
            pstmt.setFloat(1, price);
            pstmt.setString(2, cofName);
            pstmt.executeUpdate();

            con.commit();
            pstmt.close();

        } finally {
            if (con != null) con.close();
        }
    }

    private DataSource ds = null;
    private Context ctx = null;
}
```

The connection in this code sample participates in connection pooling because the following are true:

- An instance of a class implementing `ConnectionPoolDataSource` has been deployed.
- An instance of a class implementing `DataSource` has been deployed, and the value set for its `dataSourceName`property is the logical name that was bound to the previously deployed `ConnectionPoolDataSource` object.

Note that although this code is very similar to code you have seen before, it is different in the following ways:

- It imports the `javax.sql`, `javax.ejb`, and `javax.naming` packages in addition to `java.sql`.

  The `DataSource` and `ConnectionPoolDataSource` interfaces are in the `javax.sql` package, and the JNDI constructor `InitialContext` and method `Context.lookup` are part of the `javax.naming` package. This particular example code is in the form of an EJB component that uses API from the `javax.ejb` package. The purpose of this example is to show that you use a pooled connection the same way you use a nonpooled connection, so you need not worry about understanding the EJB API.

- It uses a `DataSource` object to get a connection instead of using the `DriverManager` facility.

- It uses a `finally` block to ensure that the connection is closed.

Getting and using a pooled connection is similar to getting and using a regular connection. When someone acting as a system administrator has deployed a `ConnectionPoolDataSource` object and a `DataSource` object properly, an application uses that `DataSource` object to get a pooled connection. An application should, however, use a `finally` block to close the pooled connection. For simplicity, the preceding example used a `finally` block but no `catch` block. If an exception is thrown by a method in the `try` block, it will be thrown by default, and the `finally` clause will be executed in any case.

**部署分布式事务**

`DataSource` objects can be deployed to get connections that can be used in distributed transactions. As with connection pooling, two different class instances must be deployed: an `XADataSource` object and a `DataSource` object that is implemented to work with it.

Suppose that the EJB server that The Coffee Break entrepreneur bought includes the `DataSource` class `com.applogic.TransactionalDS`, which works with an `XADataSource` class such as `com.dbaccess.XATransactionalDS`. The fact that it works with any `XADataSource` class makes the EJB server portable across JDBC drivers. When the `DataSource` and `XADataSource` objects are deployed, the connections produced will be able to participate in distributed transactions. In this case, the class `com.applogic.TransactionalDS` is implemented so that the connections produced are also pooled connections, which will usually be the case for `DataSource`classes provided as part of an EJB server implementation.

The `XADataSource` object must be deployed first. The following code creates an instance of `com.dbaccess.XATransactionalDS` and sets its properties:

```
com.dbaccess.XATransactionalDS xads = new com.dbaccess.XATransactionalDS();
xads.setServerName("creamer");
xads.setDatabaseName("COFFEEBREAK");
xads.setPortNumber(9040);
xads.setDescription("Distributed transactions for COFFEEBREAK DBMS");
```

The following code registers the `com.dbaccess.XATransactionalDS` object `*xads*` with a JNDI naming service. Note that the logical name being associated with `*xads*` has the subcontext `xa` added under `jdbc`. Oracle recommends that the logical name of any instance of the class `com.dbaccess.XATransactionalDS` always begin with `jdbc/xa`.

```
Context ctx = new InitialContext();
ctx.bind("jdbc/xa/distCoffeeDB", xads);
```

Next, the `DataSource` object that is implemented to interact with `*xads*` and other `XADataSource` objects is deployed. Note that the `DataSource` class, `com.applogic.TransactionalDS`, can work with an `XADataSource` class from any JDBC driver vendor. Deploying the `DataSource` object involves creating an instance of the `com.applogic.TransactionalDS`class and setting its properties. The `dataSourceName` property is set to `jdbc/xa/distCoffeeDB`, the logical name associated with `com.dbaccess.XATransactionalDS`. This is the `XADataSource` class that implements the distributed transaction capability for the `DataSource` class. The following code deploys an instance of the `DataSource` class:

```
com.applogic.TransactionalDS ds = new com.applogic.TransactionalDS();
ds.setDescription("Produces distributed transaction " +
                  "connections to COFFEEBREAK");
ds.setDataSourceName("jdbc/xa/distCoffeeDB");
Context ctx = new InitialContext();
ctx.bind("jdbc/distCoffeeDB", ds);
```

Now that instances of the classes `com.applogic.TransactionalDS` and `com.dbaccess.XATransactionalDS` have been deployed, an application can call the method `getConnection` on instances of the `TransactionalDS` class to get a connection to the `COFFEEBREAK` database that can be used in distributed transactions.

**使用分布式事务的连接**

To get a connection that can be used for distributed transactions, must use a `DataSource` object that has been properly implemented and deployed, as shown in the section [Deploying Distributed Transactions](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html#deployment_distributed_transactions). With such a `DataSource` object, call the method `getConnection` on it. After you have the connection, use it just as you would use any other connection. Because `jdbc/distCoffeesDB` has been associated with an `XADataSource` object in a JNDI naming service, the following code produces a `Connection` object that can be used in distributed transactions:

```
Context ctx = new InitialContext();
DataSource ds = (DataSource)ctx.lookup("jdbc/distCoffeesDB");
Connection con = ds.getConnection();
```

There are some minor but important restrictions on how this connection is used while it is part of a distributed transaction. A transaction manager controls when a distributed transaction begins and when it is committed or rolled back; therefore, application code should never call the methods `Connection.commit` or `Connection.rollback`. An application should likewise never call `Connection.setAutoCommit(true)`, which enables the auto-commit mode, because that would also interfere with the transaction manager's control of the transaction boundaries. This explains why a new connection that is created in the scope of a distributed transaction has its auto-commit mode disabled by default. Note that these restrictions apply only when a connection is participating in a distributed transaction; there are no restrictions while the connection is not part of a distributed transaction.

For the following example, suppose that an order of coffee has been shipped, which triggers updates to two tables that reside on different DBMS servers. The first table is a new `INVENTORY` table, and the second is the `COFFEES` table. Because these tables are on different DBMS servers, a transaction that involves both of them will be a distributed transaction. The code in the following example, which obtains a connection, updates the `COFFEES` table, and closes the connection, is the second part of a distributed transaction.

Note that the code does not explicitly commit or roll back the updates because the scope of the distributed transaction is being controlled by the middle tier server's underlying system infrastructure. Also, assuming that the connection used for the distributed transaction is a pooled connection, the application uses a `finally` block to close the connection. This guarantees that a valid connection will be closed even if an exception is thrown, thereby ensuring that the connection is returned to the connection pool to be recycled.

The following code sample illustrates an enterprise Bean, which is a class that implements the methods that can be called by a client computer. The purpose of this example is to demonstrate that application code for a distributed transaction is no different from other code except that it does not call the `Connection` methods `commit`, `rollback`, or `setAutoCommit(true)`. Therefore, you do not need to worry about understanding the EJB API that is used.

```
import java.sql.*;
import javax.sql.*;
import javax.ejb.*;
import javax.naming.*;

public class DistributedTransactionBean implements SessionBean {

    // ...

    public void ejbCreate() throws CreateException {

        ctx = new InitialContext();
        ds = (DataSource)ctx.lookup("jdbc/distCoffeesDB");
    }

    public void updateTotal(int incr, String cofName, String username,
                            String password)
        throws SQLException {

        Connection con;
        PreparedStatement pstmt;

        try {
            con = ds.getConnection(username, password);
            pstmt = con.prepareStatement("UPDATE COFFEES " +
                        "SET TOTAL = TOTAL + ? " +
                        "WHERE COF_NAME = ?");
            pstmt.setInt(1, incr);
            pstmt.setString(2, cofName);
            pstmt.executeUpdate();
            stmt.close();
        } finally {
            if (con != null) con.close();
        }
    }

    private DataSource ds = null;
    private Context ctx = null;
}
```