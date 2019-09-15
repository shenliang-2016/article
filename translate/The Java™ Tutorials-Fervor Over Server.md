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

| Property             | Description                              |
| -------------------- | ---------------------------------------- |
| `JAVAC`              | The full path name of your Java compiler, `javac` |
| `JAVA`               | The full path name of your Java runtime executable, `java` |
| `PROPERTIESFILE`     | The name of the properties file, either `properties/javadb-sample-properties.xml` or `properties/mysql-sample-properties.xml` |
| `MYSQLDRIVER`        | The full path name of your MySQL driver. For Connector/J, this is typically `*<Connector/J installation directory>*/mysql-connector-java-*version-number*.jar`. |
| `JAVADBDRIVER`       | The full path name of your Java DB driver. This is typically `*<Java DB installation directory>*/lib/derby.jar`. |
| `XALANDIRECTORY`     | The full path name of the directory that contains Apache Xalan. |
| `CLASSPATH`          | The class path that the JDBC tutorial uses. *You do not need to change this value.* |
| `XALAN`              | The full path name of the file `xalan.jar`. |
| `DB.VENDOR`          | A value of either `derby` or `mysql` depending on whether you are using Java DB or MySQL, respectively. The tutorial uses this value to construct the URL required to connect to the DBMS and identify DBMS-specific code and SQL statements. |
| `DB.DRIVER`          | The fully qualified class name of the JDBC driver. For Java DB, this is `org.apache.derby.jdbc.EmbeddedDriver`. For MySQL, this is `com.mysql.jdbc.Driver`. |
| `DB.HOST`            | The host name of the computer hosting your DBMS. |
| `DB.PORT`            | The port number of the computer hosting your DBMS. |
| `DB.SID`             | The name of the database the tutorial creates and uses. |
| `DB.URL.NEWDATABASE` | The connection URL used to connect to your DBMS when creating a new database. *You do not need to change this value.* |
| `DB.URL`             | The connection URL used to connect to your DBMS. *You do not need to change this value.* |
| `DB.USER`            | The name of the user that has access to create databases in the DBMS. |
| `DB.PASSWORD`        | The password of the user specified in `DB.USER`. |
| `DB.DELIMITER`       | The character used to separate SQL statements. *Do not change this value.* It should be the semicolon character (`;`). |

**修改教程属性文件**

教程示例使用`properties/javadb-sample-properties.xml`文件或`properties/mysql-sample-properties.xml`文件（取决于您的DBMS）中的值来连接到DBMS并初始化数据库和表 ，如下表所述：

| Property        | Description                              |
| --------------- | ---------------------------------------- |
| `dbms`          | A value of either `derby` or `mysql` depending on whether you are using Java DB or MySQL, respectively. The tutorial uses this value to construct the URL required to connect to the DBMS and identify DBMS-specific code and SQL statements. |
| `jar_file`      | The full path name of the JAR file that contains all the class files of this tutorial. |
| `driver`        | The fully qualified class name of the JDBC driver. For Java DB, this is `org.apache.derby.jdbc.EmbeddedDriver`. For MySQL, this is `com.mysql.jdbc.Driver`. |
| `database_name` | The name of the database the tutorial creates and uses. |
| `user_name`     | The name of the user that has access to create databases in the DBMS. |
| `password`      | The password of the user specified in `user_name`. |
| `server_name`   | The host name of the computer hosting your DBMS. |
| `port_number`   | The port number of the computer hosting your DBMS. |

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

| Ant Target                | Class or SQL Script                      | Other Required Classes or Files          |
| ------------------------- | ---------------------------------------- | ---------------------------------------- |
| `javadb-create-procedure` | `javadb/create-procedures.sql`; see the `build.xml`file to view other SQL statements that are run | No other required files                  |
| `mysql-create-procedure`  | `mysql/create-procedures.sql`.           | No other required files                  |
| `run`                     | `JDBCTutorialUtilities`                  | No other required classes                |
| `runct`                   | `CoffeesTable`                           | `JDBCTutorialUtilities`                  |
| `runst`                   | `SuppliersTable`                         | `JDBCTutorialUtilities`                  |
| `runjrs`                  | `JdbcRowSetSample`                       | `JDBCTutorialUtilities`                  |
| `runcrs`                  | `CachedRowSetSample`, `ExampleRowSetListener` | `JDBCTutorialUtilities`                  |
| `runjoin`                 | `JoinSample`                             | `JDBCTutorialUtilities`                  |
| `runfrs`                  | `FilteredRowSetSample`                   | `JDBCTutorialUtilities`, `CityFilter`, `StateFilter` |
| `runwrs`                  | `WebRowSetSample`                        | `JDBCTutorialUtilities`                  |
| `runclob`                 | `ClobSample`                             | `JDBCTutorialUtilities`, `txt/colombian-description.txt` |
| `runrss`                  | `RSSFeedsTable`                          | `JDBCTutorialUtilities`, the XML files contained in the `xml` directory |
| `rundl`                   | `DatalinkSample`                         | `JDBCTutorialUtilities`                  |
| `runspjavadb`             | `StoredProcedureJavaDBSample`            | `JDBCTutorialUtilities`, `SuppliersTable`, `CoffeesTable` |
| `runspmysql`              | `StoredProcedureMySQLSample`             | `JDBCTutorialUtilities`, `SuppliersTable`, `CoffeesTable` |
| `runframe`                | `CoffeesFrame`                           | `JDBCTutorialUtilities`, `CoffeesTableModel` |

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

*连接池*是数据库连接对象的缓存。连接对象表示应用程序可用于连接到数据库的物理数据库连接。在运行时，应用程序从连接池请求连接。如果池包含可以满足请求的连接，则它将返回与应用程序的连接。如果未找到任何连接，则会创建新连接并将其返回给应用程序。应用程序使用连接对数据库执行某些操作，然后将连接对象返回连接池。然后，该连接可用于下一个连接请求。

连接池可以促进连接对象的重用，并减少创建连接对象的次数。连接池显着提高了数据库密集型应用程序的性能，因为创建连接对象在时间和资源方面都很昂贵。

现在已经部署了这些`DataSource`和`ConnectionPoolDataSource`对象，程序员可以使用`DataSource`对象来获得池化连接。获取池连接的代码就像获取非池化连接的代码一样，如以下两行所示：

```java
ctx = new InitialContext();
ds = (DataSource)ctx.lookup("jdbc/fastCoffeeDB");
```

变量`ds`表示一个`DataSource`对象，它产生与数据库`COFFEEBREAK`的池连接。您只需要检索一次这个`DataSource`对象，因为您可以根据需要使用它来生成尽可能多的池连接。在`ds`变量上调用`getConnection`方法会自动产生一个池化连接，因为`ds`变量所代表的`DataSource`对象被配置为产生池化连接。

连接池通常对程序员是透明的。使用池化连接时，只需要执行两项操作：

1. 使用`DataSource`对象而不是`DriverManager`类来获取连接。在下面的代码行中，`ds`是一个实现和部署的`DataSource`对象，它将创建池连接，`username`和`password`是代表有权访问数据库的用户凭据的变量：

   ```java
   Connection con = ds.getConnection(username, password);
   ```

2. 使用`finally`语句关闭池化连接。以下`finally`块将出现在`try/catch`块之后，该块适用于使用池化连接的代码：

   ```java
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

除此之外，使用池化连接的应用程序与使用常规连接的应用程序相同。应用程序员在完成连接池时可能会注意到的另一件事是性能更好。

以下示例代码获取一个`DataSource`对象，该对象生成与数据库`COFFEEBREAK`的连接，并使用它来更新表`COFFEES`中的价格：

```java
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

此代码示例中的连接参与连接池，因为以下情况属实：

 - 已部署实现`ConnectionPoolDataSource`的类的实例。
 - 已经部署了实现`DataSource`的类的实例，并且为其`dataSourceName`属性设置的值是绑定到先前部署的`ConnectionPoolDataSource`对象的逻辑名。

请注意，尽管此代码与您之前看到的代码非常相似，但它在以下方面有所不同：

 - 除了`java.sql`之外，它还导入`javax.sql`，`javax.ejb`和`javax.naming`包。

   `DataSource`和`ConnectionPoolDataSource`接口在`javax.sql`包中，JNDI构造函数`InitialContext`和方法`Context.lookup`是`javax.naming`包的一部分。此特定示例代码采用EJB组件的形式，该组件使用来自`javax.ejb`包的API。此示例的目的是显示您使用池化连接的方式与使用非池化连接的方式相同，因此您无需担心理解EJB API。

 - 它使用`DataSource`对象来获取连接，而不是使用`DriverManager`工具。

 - 它使用`finally`块来确保连接被关闭。

获取和使用池化连接类似于获取和使用常规连接。当充当系统管理员的人正确部署了`ConnectionPoolDataSource`对象和`DataSource`对象时，应用程序使用该`DataSource`对象来获得池化连接。但是，应用程序应使用`finally`块来关闭池连接。为简单起见，前面的示例使用了`finally`块但没有使用`catch`块。如果`try`块中的方法抛出异常，则默认情况下将抛出该异常，并且在任何情况下都将执行`finally`子句。

**部署分布式事务**

可以部署`DataSource`对象以获取可在分布式事务中使用的连接。与连接池一样，必须部署两个不同的类实例：一个`XADataSource`对象和一个与之一起使用的`DataSource`实现对象。

假设The Coffee Break企业家购买的EJB服务器包含`DataSource`类`com.applogic.TransactionalDS`，它与`XADataSource`类（如`com.dbaccess.XATransactionalDS`）一起使用。它适用于任何`XADataSource`类这一事实使EJB服务器可以跨JDBC驱动程序移植。当部署`DataSource`和`XADataSource`对象时，生成的连接将能够参与分布式事务。在这种情况下，实现了类`com.applogic.TransactionalDS`，以便生成的连接也是池化连接，这通常是作为EJB服务器实现的一部分提供的`DataSource`类的情况。

必须首先部署`XADataSource`对象。以下代码创建`com.dbaccess.XATransactionalDS`的实例并设置其属性：

```java
com.dbaccess.XATransactionalDS xads = new com.dbaccess.XATransactionalDS();
xads.setServerName("creamer");
xads.setDatabaseName("COFFEEBREAK");
xads.setPortNumber(9040);
xads.setDescription("Distributed transactions for COFFEEBREAK DBMS");
```

以下代码使用JNDI命名服务注册`com.dbaccess.XATransactionalDS`对象`xads`。 请注意，与`xads`相关联的逻辑名称在`jdbc`下添加了子上下文`xa`。Oracle建议`com.dbaccess.XATransactionalDS`类的任何实例的逻辑名始终以`jdbc/xa`开头。

```java
Context ctx = new InitialContext();
ctx.bind("jdbc/xa/distCoffeeDB", xads);
```

接下来，部署了实现与`xads`和其他`XADataSource`对象交互的`DataSource`对象。请注意，`DataSource`类，`com.applogic.TransactionalDS`，可以与任何JDBC驱动程序供应商的`XADataSource`类一起使用。部署`DataSource`对象涉及创建`com.applogic.TransactionalDS`类的实例并设置其属性。`dataSourceName`属性设置为`jdbc/xa/distCoffeeDB`，这是与`com.dbaccess.XATransactionalDS`相关联的逻辑名。这是`XADataSource`类，它实现了`DataSource`类的分布式事务功能。以下代码部署了`DataSource`类的实例：

```java
com.applogic.TransactionalDS ds = new com.applogic.TransactionalDS();
ds.setDescription("Produces distributed transaction " +
                  "connections to COFFEEBREAK");
ds.setDataSourceName("jdbc/xa/distCoffeeDB");
Context ctx = new InitialContext();
ctx.bind("jdbc/distCoffeeDB", ds);
```

现在已经部署了类`com.applogic.TransactionalDS`和`com.dbaccess.XATransactionalDS`的实例，应用程序可以在`TransactionalDS`类的实例上调用方法`getConnection`以获得与`COFFEEBREAK的连接 `可以在分布式事务中使用的数据库。

**使用分布式事务的连接**

要获得可用于分布式事务的连接，必须使用已正确实现和部署的`DataSource`对象，如 [Deploying Distributed Transactions](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html#deployment_distributed_transactions) 中所述。使用这样的`DataSource`对象，在其上调用方法`getConnection`。连接后，使用它就像使用任何其他连接一样。因为`jdbc/distCoffeesDB`已经与JNDI命名服务中的`XADataSource`对象相关联，所以下面的代码生成一个可以在分布式事务中使用的`Connection`对象：

```java
Context ctx = new InitialContext();
DataSource ds = (DataSource)ctx.lookup("jdbc/distCoffeesDB");
Connection con = ds.getConnection();
```

当它是分布式事务的一部分时，对如何使用此连接存在一些次要但重要的限制。事务管理器控制分布式事务何时开始以及何时提交或回滚。因此，应用程序代码永远不应该调用方法`Connection.commit`或`Connection.rollback`。应用程序同样应该永远不会调用`Connection.setAutoCommit（true）`，它启用自动提交模式，因为这也会干扰事务管理器对事务边界的控制。这解释了为什么在分布式事务范围内创建的新连接默认情况下禁用其自动提交模式。请注意，这些限制仅适用于连接参与分布式事务的情况。连接不是分布式事务的一部分时没有限制。

对于以下示例，假设已发送咖啡订单，这会触发对位于不同DBMS服务器上的两个表的更新。第一个表是一个新的`INVENTORY`表，第二个表是`COFFEES`表。由于这些表位于不同的DBMS服务器上，因此涉及它们的事务将是分布式事务。以下示例中的代码获取连接，更新`COFFEES`表，并关闭连接，是分布式事务的第二部分。

请注意，代码未显式提交或回滚更新，因为分布式事务的范围由中间层服务器的底层系统基础结构控制。此外，假设用于分布式事务的连接是池连接，应用程序使用`finally`块来关闭连接。这可以保证即使抛出异常也会关闭有效连接，从而确保连接返回到连接池以进行回收。

以下代码示例演示了一个企业Bean，它是一个实现客户端计算机可以调用的方法的类。此示例的目的是演示分布式事务的应用程序代码与其他代码没有区别，除了它不调用`Connection`方法`commit`，`rollback`或`setAutoCommit（true）`。因此，您无需担心了解所使用的EJB API。

```java
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

### 处理 SQL 异常

本页面涵盖以下主题：

- [SQLException 概述](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlexception.html#overview_sqlexception)
- [获取 Exceptions](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlexception.html#retrieving_exceptions)
- [获取 Warnings](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlexception.html#retrieving_warnings)
- [SQLExceptions 分类](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlexception.html#categorized_sqlexceptions)
- [SQLException 的其它子类型](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlexception.html#subclasses_sqlexception)

**SQLException 概述**

当JDBC在与数据源交互期间遇到错误时，它会抛出`SQLException`实例而不是`Exception`。（此上下文中的数据源表示`Connection`对象所连接的数据库。）`SQLException`实例包含以下信息，可帮助您确定错误原因：

 - 错误的描述。通过调用方法`SQLException.getMessage`检索包含此描述的`String`对象。
 - SQLState 代码。这些代码及其各自的含义已经由 ISO/ANSI 和 Open Group (X/Open) 标准化，尽管已经为数据库供应商保留了一些代码来自行定义。此`String`对象由五个字母数字字符组成。通过调用方法`SQLException.getSQLState`来检索此代码。
 - 错误代码。这是一个整数值，用于标识导致抛出`SQLException`实例的错误。它的值和含义是特定于实现的，可能是底层数据源返回的实际错误代码。通过调用方法`SQLException.getErrorCode`来检索错误。
- 原因。`SQLException`实例可能具有因果关系，该关系由一个或多个`Throwable`对象组成，这些对象导致抛出`SQLException`实例。要导航此原因链，请递归调用方法`SQLException.getCause`，直到返回`null`值。
 - 对任何链式异常的引用。如果发生多个错误，则通过此链引用异常。通过对抛出的异常调用方法`SQLException.getNextException`来检索这些异常。

**获取异常**

下面的方法， `JDBCTutorialUtilities.printSQLException` 输出包含在 `SQLException` 以及任何与之形成异常链的异常中的 SQLState，错误码，错误描述，以及原因（如果存在）：

```java
public static void printSQLException(SQLException ex) {

    for (Throwable e : ex) {
        if (e instanceof SQLException) {
            if (ignoreSQLException(
                ((SQLException)e).
                getSQLState()) == false) {

                e.printStackTrace(System.err);
                System.err.println("SQLState: " +
                    ((SQLException)e).getSQLState());

                System.err.println("Error Code: " +
                    ((SQLException)e).getErrorCode());

                System.err.println("Message: " + e.getMessage());

                Throwable t = ex.getCause();
                while(t != null) {
                    System.out.println("Cause: " + t);
                    t = t.getCause();
                }
            }
        }
    }
}
```

比如，如果你调用方法 `CoffeesTable.dropTable` 并使用 Java DB 作为你的 DBMS，表 `COFFEES` 不存在，同时你删除了对 `JDBCTutorialUtilities.ignoreSQLException` 的调用，将得到类似下面的输出：

```
SQLState: 42Y55
Error Code: 30000
Message: 'DROP TABLE' cannot be performed on
'TESTDB.COFFEES' because it does not exist.
```

您可以改为首先检索 `SQLState`，然后相应地处理`SQLException`，而不是输出`SQLException`信息。例如，如果`SQLState`等于代码`42Y55`（并且您使用Java DB作为DBMS），则`JDBCTutorialUtilities.ignoreSQLException`方法返回`true`，这会导致`JDBCTutorialUtilities.printSQLException`忽略`SQLException`：

```java
public static boolean ignoreSQLException(String sqlState) {

    if (sqlState == null) {
        System.out.println("The SQL state is not defined!");
        return false;
    }

    // X0Y32: Jar file already exists in schema
    if (sqlState.equalsIgnoreCase("X0Y32"))
        return true;

    // 42Y55: Table already exists in schema
    if (sqlState.equalsIgnoreCase("42Y55"))
        return true;

    return false;
}
```

**获取警告**

`SQLWarning`对象是`SQLException`的子类，用于处理数据库访问警告。警告不会像异常那样停止执行应用程序，它们只是提醒用户某些事情没有按计划发生。例如，警告可能会让您知道您尝试撤销的权限未被撤销。或者警告可能会告诉您在请求的断开连接期间发生了错误。

可以在`Connection`对象，`Statement`对象（包括`PreparedStatement`和`CallableStatement`对象）或`ResultSet`对象上报告警告。这些类中的每一个都有一个`getWarnings`方法，您必须调用该方法才能看到在调用对象上报告的第一个警告。如果`getWarnings`返回警告，则可以在其上调用`SQLWarning`方法`getNextWarning`以获取任何其他警告。执行语句会自动清除先前语句中的警告，因此警告不会积聚。但是，这意味着如果要检索语句上报告的警告，则必须在执行另一个语句之前执行。

`JDBCTutorialUtilities`中的以下方法说明了如何获取有关`Statement`或`ResultSet`对象上报告的任何警告的完整信息：

```java
public static void getWarningsFromResultSet(ResultSet rs)
    throws SQLException {
    JDBCTutorialUtilities.printWarnings(rs.getWarnings());
}

public static void getWarningsFromStatement(Statement stmt)
    throws SQLException {
    JDBCTutorialUtilities.printWarnings(stmt.getWarnings());
}

public static void printWarnings(SQLWarning warning)
    throws SQLException {

    if (warning != null) {
        System.out.println("\n---Warning---\n");

    while (warning != null) {
        System.out.println("Message: " + warning.getMessage());
        System.out.println("SQLState: " + warning.getSQLState());
        System.out.print("Vendor error code: ");
        System.out.println(warning.getErrorCode());
        System.out.println("");
        warning = warning.getNextWarning();
    }
}
```

最常见的警告是`DataTruncation`警告，它是`SQLWarning`的子类。所有`DataTruncation`对象的`SQLState`都为`01004`，表示读取或写入数据时出现问题。通过`DataTruncation`方法，您可以找出截断的列或参数数据，截断是在读取还是写入操作，应该传输了多少字节，以及实际传输了多少字节。

**SQLExceptions 分类**

您的JDBC驱动程序可能抛出`SQLException`的子类，该子类对应于公共`SQLState`或与特定`SQLState`类值无关的常见错误状态。这使您可以编写更多可移植的错误处理代码。这些异常是以下类之一的子类：

 -  `SQLNonTransientException`
 -  `SQLTransientException`
 -  `SQLRecoverableException`

有关这些子类的更多信息，请参阅`java.sql`包的最新Javadoc或JDBC驱动程序的文档。

**SQLException 的其它子类型**

还可以抛出以下`SQLException`子类：

 - 批处理更新操作期间发生错误时抛出`BatchUpdateException`。除了`SQLException`提供的信息之外，`BatchUpdateException`还提供在错误发生之前执行的所有语句的更新计数。
 - 无法在`Connection`上设置一个或多个客户端信息属性时抛出`SQLClientInfoException`。除了`SQLException`提供的信息之外，`SQLClientInfoException`还提供了未设置的客户端信息属性列表。

### 建表

本页描述教程中使用的所有表，并介绍如何创建它们：

- [COFFEES Table](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html#coffees)
- [SUPPLIERS Table](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html#suppliers)
- [COF_INVENTORY Table](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html#cof_inventory)
- [MERCH_INVENTORY Table](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html#merch_inventory)
- [COFFEE_HOUSES Table](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html#coffee_houses)
- [DATA_REPOSITORY Table](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html#data_repository)
- [创建表](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html#create)
- [填充表](https://docs.oracle.com/javase/tutorial/jdbc/basics/tables.html#populate)

**COFFEES Table**

`COFFEES`表存储 The Coffee Break 可销售的咖啡的信息：

| `COF_NAME`         | `SUP_ID` | `PRICE` | `SALES` | `TOTAL` |
| ------------------ | -------- | ------- | ------- | ------- |
| Colombian          | 101      | 7.99    | 0       | 0       |
| French_Roast       | 49       | 8.99    | 0       | 0       |
| Espresso           | 150      | 9.99    | 0       | 0       |
| Colombian_Decaf    | 101      | 8.99    | 0       | 0       |
| French_Roast_Decaf | 49       | 9.99    | 0       | 0       |

下面介绍 `COFFEES` 表中的每个列：

- `COF_NAME`: 存储咖啡名称。使用SQL类型`VARCHAR`保存值，最大长度为32个字符。因为每种类型的咖啡的名称都不同，所以该名称唯一地标识特定的咖啡并且用作主键。
- `SUP_ID`: 存储识别咖啡供应商的编号。保存SQL类型为`INTEGER`的值。它被定义为引用`SUPPLIERS`表中的`SUP_ID`列的外键。因此，DBMS将强制执行此列中的每个值与`SUPPLIERS`表中相应列中的某个值匹配。
- `PRICE`: 存储每磅咖啡的成本。使用SQL类型`FLOAT`保存值，因为它需要保存带小数点的值。（请注意，货币值通常存储在SQL类型`DECIMAL`或`NUMERIC`中，但由于DBMS之间存在差异并且为了避免与早期版本的JDBC不兼容，本教程使用更标准的`FLOAT`类型。）
- `SALES`: 存储本周销售的咖啡磅数。保存SQL类型为`INTEGER`的值。
- `TOTAL`: 存储迄今为止销售的咖啡磅数。保存SQL类型为`INTEGER`的值。

**SUPPLIERS Table**

`SUPPLIERS` 存储有关供应商的信息：

| `SUP_ID` | `SUP_NAME`      | `STREET`         | `CITY`       | `STATE` | `ZIP` |
| -------- | --------------- | ---------------- | ------------ | ------- | ----- |
| 101      | Acme, Inc.      | 99 Market Street | Groundsville | CA      | 95199 |
| 49       | Superior Coffee | 1 Party Place    | Mendocino    | CA      | 95460 |
| 150      | The High Ground | 100 Coffee Lane  | Meadows      | CA      | 93966 |

以下描述了`SUPPLIERS`表中的每个列：

 -  `SUP_ID`：存储标识咖啡供应商的编号。保存SQL类型为`INTEGER`的值。它是此表中的主键。
 -  `SUP_NAME`：存储咖啡供应商的名称。
 -  `STREET`，`CITY`，`STATE`和`ZIP`：这些列存储咖啡供应商的地址。

**COF_INVENTORY Table**

表`COF_INVENTORY`存储有关每个仓库中存储的咖啡量的信息：

| `WAREHOUSE_ID` | `COF_NAME`        | `SUP_ID` | `QUAN` | `DATE_VAL` |
| -------------- | ----------------- | -------- | ------ | ---------- |
| 1234           | House_Blend       | 49       | 0      | 2006_04_01 |
| 1234           | House_Blend_Decaf | 49       | 0      | 2006_04_01 |
| 1234           | Colombian         | 101      | 0      | 2006_04_01 |
| 1234           | French_Roast      | 49       | 0      | 2006_04_01 |
| 1234           | Espresso          | 150      | 0      | 2006_04_01 |
| 1234           | Colombian_Decaf   | 101      | 0      | 2006_04_01 |

以下描述了`COF_INVENTORY`表中的每个列：

 -  `WAREHOUSE_ID`：存储标识仓库的编号。
 -  `COF_NAME`：存储特定类型咖啡的名称。
 -  `SUP_ID`：存储标识供应商的编号。
 -  `QUAN`：存储一个表示可用商品数量的数字。
 -  `DATE`：存储时间戳值，指示上次更新行的时间。

**MERCH_INVENTORY Table**

表`MERCH_INVENTORY`存储有关库存中非咖啡商品数量的信息：

| `ITEM_ID` | `ITEM_NAME` | `SUP_ID` | `QUAN` | `DATE`     |
| --------- | ----------- | -------- | ------ | ---------- |
| 00001234  | Cup_Large   | 00456    | 28     | 2006_04_01 |
| 00001235  | Cup_Small   | 00456    | 36     | 2006_04_01 |
| 00001236  | Saucer      | 00456    | 64     | 2006_04_01 |
| 00001287  | Carafe      | 00456    | 12     | 2006_04_01 |
| 00006931  | Carafe      | 00927    | 3      | 2006_04_01 |
| 00006935  | PotHolder   | 00927    | 88     | 2006_04_01 |
| 00006977  | Napkin      | 00927    | 108    | 2006_04_01 |
| 00006979  | Towel       | 00927    | 24     | 2006_04_01 |
| 00004488  | CofMaker    | 08732    | 5      | 2006_04_01 |
| 00004490  | CofGrinder  | 08732    | 9      | 2006_04_01 |
| 00004495  | EspMaker    | 08732    | 4      | 2006_04_01 |
| 00006914  | Cookbook    | 00927    | 12     | 2006_04_01 |

以下内容描述了`MERCH_INVENTORY`表中的每个列：

 -  `ITEM_ID`：存储标识项目的编号。
 -  `ITEM_NAME`：存储商品的名称。
 -  `SUP_ID`：存储标识供应商的编号。
 -  `QUAN`：存储一个数字，表示该项目的可用数量。
 -  `DATE`：存储时间戳值，指示上次更新行的时间。

**COFFEE_HOUSES Table**

`COFFEE_HOUSES`表存放咖啡馆的位置：

| `STORE_ID` | `CITY`     | `COFFEE` | `MERCH` | `TOTAL` |
| ---------- | ---------- | -------- | ------- | ------- |
| 10023      | Mendocino  | 3450     | 2005    | 5455    |
| 33002      | Seattle    | 4699     | 3109    | 7808    |
| 10040      | SF         | 5386     | 2841    | 8227    |
| 32001      | Portland   | 3147     | 3579    | 6726    |
| 10042      | SF         | 2863     | 1874    | 4710    |
| 10024      | Sacramento | 1987     | 2341    | 4328    |
| 10039      | Carmel     | 2691     | 1121    | 3812    |
| 10041      | LA         | 1533     | 1007    | 2540    |
| 33005      | Olympia    | 2733     | 1550    | 4283    |
| 33010      | Seattle    | 3210     | 2177    | 5387    |
| 10035      | SF         | 1922     | 1056    | 2978    |
| 10037      | LA         | 2143     | 1876    | 4019    |
| 10034      | San_Jose   | 1234     | 1032    | 2266    |
| 32004      | Eugene     | 1356     | 1112    | 2468    |

以下描述了`COFFEE_HOUSES`表中的每个列：

 -  `STORE_ID`：存储识别咖啡馆的号码。除其他外，它表示咖啡馆所处的状态。例如，以10开头的值表示该州是加利福尼亚州。以32开头的`STORE_ID`值表示俄勒冈州，以33开头的`STORE_ID`值表示华盛顿州。
 -  `CITY`：存储咖啡馆所在城市的名称。
 -  `COFFEE`：存储一个表示销售咖啡量的数字。
 -  `MERCH`：存储一个表示销售商品数量的数字。
 -  `TOTAL`：存储一个数字，表示销售的咖啡和商品的总量。

**DATA_REPOSITORY Table**

表`DATA_REPOSITORY`存储引用The Coffee Break感兴趣的文档和其他数据的URL。脚本`populate_tables.sql`不会向此表添加任何数据。以下描述了此表中的每个列：

 -  `DOCUMENT_NAME`：存储标识URL的字符串。
 -  `URL`：存储URL。

**创建表**

你可以使用 Apache Ant 或者 JDBC API 创建表。

**使用 Apache Ant 创建表**

要创建与教程示例代码一起使用的表，请在目录`<JDBC tutorial directory>`中运行以下命令：

```
ant setup
```

此命令运行多个Ant目标，包括以下构建表（来自`build.xml`文件）：

```xml
<target name="build-tables"
  description="Create database tables">
  <sql
    driver="${DB.DRIVER}"
    url="${DB.URL}"
    userid="${DB.USER}"
    password="${DB.PASSWORD}"
    classpathref="CLASSPATH"
    delimiter="${DB.DELIMITER}"
    autocommit="false" onerror="abort">
    <transaction src=
  "./sql/${DB.VENDOR}/create-tables.sql"/>
  </sql>
</target>
```

该示例指定以下 `sql` Ant任务参数的值：

| Parameter      | Description                              |
| -------------- | ---------------------------------------- |
| `driver`       | Fully qualified class name of your JDBC driver. This sample uses `org.apache.derby.jdbc.EmbeddedDriver` for Java DB and `com.mysql.jdbc.Driver` for MySQL Connector/J. |
| `url`          | Database connection URL that your DBMS JDBC driver uses to connect to a database. |
| `userid`       | Name of a valid user in your DBMS.       |
| `password`     | Password of the user specified in `userid` |
| `classpathref` | Full path name of the JAR file that contains the class specified in `driver` |
| `delimiter`    | String or character that separates SQL statements. This sample uses the semicolon (`;`). |
| `autocommit`   | Boolean value; if set to `false`, all SQL statements are executed as one transaction. |
| `onerror`      | Action to perform when a statement fails; possible values are `continue`, `stop`, and `abort`. The value `abort` specifies that if an error occurs, the transaction is aborted. |

该示例将这些参数的值存储在单独的文件中。构建文件`build.xml`使用`import`任务检索这些值：

```xml
<import file="${ANTPROPERTIES}"/>
```

`transaction`元素指定包含要执行的SQL语句的文件。`create-tables.sql`文件包含创建此页面上描述的所有表的SQL语句。例如，以下片段自此文件创建表`SUPPLIERS`和`COFFEES`：

```sql
create table SUPPLIERS
    (SUP_ID integer NOT NULL,
    SUP_NAME varchar(40) NOT NULL,
    STREET varchar(40) NOT NULL,
    CITY varchar(20) NOT NULL,
    STATE char(2) NOT NULL,
    ZIP char(5),
    PRIMARY KEY (SUP_ID));

create table COFFEES
    (COF_NAME varchar(32) NOT NULL,
    SUP_ID int NOT NULL,
    PRICE numeric(10,2) NOT NULL,
    SALES integer NOT NULL,
    TOTAL integer NOT NULL,
    PRIMARY KEY (COF_NAME),
    FOREIGN KEY (SUP_ID)
        REFERENCES SUPPLIERS (SUP_ID));
```

**注意：**文件`build.xml`包含另一个名为`drop-tables`的目标，用于删除教程使用的表。`setup`目标在运行`build-tables`目标之前运行`drop-tables`。

**使用 JDBC API 创建表**

下面的方法，`SuppliersTable.createTable`，创建 `SUPPLIERS` 表：

```java
public void createTable() throws SQLException {
    String createString =
        "create table " + dbName +
        ".SUPPLIERS " +
        "(SUP_ID integer NOT NULL, " +
        "SUP_NAME varchar(40) NOT NULL, " +
        "STREET varchar(40) NOT NULL, " +
        "CITY varchar(20) NOT NULL, " +
        "STATE char(2) NOT NULL, " +
        "ZIP char(5), " +
        "PRIMARY KEY (SUP_ID))";

    Statement stmt = null;
    try {
        stmt = con.createStatement();
        stmt.executeUpdate(createString);
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

下面的方法，`CoffeesTable.createTable`，创建 `COFFEES` 表：

```java
  public void createTable() throws SQLException {
    String createString =
        "create table " + dbName +
        ".COFFEES " +
        "(COF_NAME varchar(32) NOT NULL, " +
        "SUP_ID int NOT NULL, " +
        "PRICE float NOT NULL, " +
        "SALES integer NOT NULL, " +
        "TOTAL integer NOT NULL, " +
        "PRIMARY KEY (COF_NAME), " +
        "FOREIGN KEY (SUP_ID) REFERENCES " +
        dbName + ".SUPPLIERS (SUP_ID))";

    Statement stmt = null;
    try {
        stmt = con.createStatement();
        stmt.executeUpdate(createString);
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

在这两种方法中，`con`是`Connection`对象，`dbName`是要在其中创建表的数据库的名称。

要执行SQL查询（例如`String createString`指定的查询），请使用`Statement`对象。要创建`Statement`对象，请从现有`Connection`对象调用`Connection.createStatement`方法。要执行SQL查询，请调用`Statement.executeUpdate`方法。

关闭创建它们的连接时，将关闭所有`Statement`对象。但是，完成它们后立即显式关闭`Statement`对象是一种很好的编码实践。这允许立即释放语句正在使用的任何外部资源。通过调用`Statement.close`方法关闭语句。将此语句放在`finally`中以确保即使正常程序流因为抛出异常（例如`SQLException`）而中断也会关闭。

**注意：**您必须在`COFFEES`之前创建`SUPPLIERS`表，因为`COFFEES`包含引用`SUPPLIERS`的外键`SUP_ID`。

**填充表**

同样，您可以使用 Apache Ant 或 JDBC API 将数据插入表中。

**使用 Apache Ant 填充表**

除了创建本教程使用的表之外，命令`ant setup`还会填充这些表。此命令运行 Ant 目标`populate-tables`，它运行 SQL 脚本`populate-tables.sql`。

以下是`populate-tables.sql`的摘录，用于填充表`SUPPLIERS`和`COFFEES`：

```sql
insert into SUPPLIERS values(
    49, 'Superior Coffee', '1 Party Place',
    'Mendocino', 'CA', '95460');
insert into SUPPLIERS values(
    101, 'Acme, Inc.', '99 Market Street',
    'Groundsville', 'CA', '95199');
insert into SUPPLIERS values(
    150, 'The High Ground',
    '100 Coffee Lane', 'Meadows', 'CA', '93966');
insert into COFFEES values(
    'Colombian', 00101, 7.99, 0, 0);
insert into COFFEES values(
    'French_Roast', 00049, 8.99, 0, 0);
insert into COFFEES values(
    'Espresso', 00150, 9.99, 0, 0);
insert into COFFEES values(
    'Colombian_Decaf', 00101, 8.99, 0, 0);
insert into COFFEES values(
    'French_Roast_Decaf', 00049, 9.99, 0, 0);
```

**使用 JDBC API 填充表**

下面的方法，`SuppliersTable.populateTable`，向表中插入数据：

```java
public void populateTable() throws SQLException {

    Statement stmt = null;
    try {
        stmt = con.createStatement();
        stmt.executeUpdate(
            "insert into " + dbName +
            ".SUPPLIERS " +
            "values(49, 'Superior Coffee', " +
            "'1 Party Place', " +
            "'Mendocino', 'CA', '95460')");

        stmt.executeUpdate(
            "insert into " + dbName +
            ".SUPPLIERS " +
            "values(101, 'Acme, Inc.', " +
            "'99 Market Street', " +
            "'Groundsville', 'CA', '95199')");

        stmt.executeUpdate(
            "insert into " + dbName +
            ".SUPPLIERS " +
            "values(150, " +
            "'The High Ground', " +
            "'100 Coffee Lane', " +
            "'Meadows', 'CA', '93966')");
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

下面的方法，`CoffeesTable.populateTable`，将数据插入表：

```java
public void populateTable() throws SQLException {

    Statement stmt = null;
    try {
        stmt = con.createStatement();
        stmt.executeUpdate(
            "insert into " + dbName +
            ".COFFEES " +
            "values('Colombian', 00101, " +
            "7.99, 0, 0)");

        stmt.executeUpdate(
            "insert into " + dbName +
            ".COFFEES " +
            "values('French_Roast', " +
            "00049, 8.99, 0, 0)");

        stmt.executeUpdate(
            "insert into " + dbName +
            ".COFFEES " +
            "values('Espresso', 00150, 9.99, 0, 0)");

        stmt.executeUpdate(
            "insert into " + dbName +
            ".COFFEES " +
            "values('Colombian_Decaf', " +
            "00101, 8.99, 0, 0)");

        stmt.executeUpdate(
            "insert into " + dbName +
            ".COFFEES " +
            "values('French_Roast_Decaf', " +
            "00049, 9.99, 0, 0)");
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmt != null) {
          stmt.close();
        }
    }
}
```

### 检索并修改来自结果集的值

下面的方法，`CoffeesTable.viewTable` 输出 `COFFEES` 表的内容，同时展示 `ResultSet` 对象和游标的使用方法：

```java
public static void viewTable(Connection con, String dbName)
    throws SQLException {

    Statement stmt = null;
    String query =
        "select COF_NAME, SUP_ID, PRICE, " +
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

`ResultSet`对象是表示数据库结果集的数据表，通常通过执行查询数据库的语句生成。例如，`CoffeeTables.viewTable`方法在通过`Statement`对象，`stmt`执行查询时创建`ResultSet rs`。请注意，可以通过实现`Statement`接口的任何对象创建`ResultSet`对象，包括`PreparedStatement`，`CallableStatement`和`RowSet`。

您可以通过游标访问`ResultSet`对象中的数据。请注意，此游标不是数据库游标。此游标是指向`ResultSet`中一行数据的指针。最初，游标位于第一行之前。`ResultSet.next`方法将光标移动到下一行。如果光标位于最后一行之后，则此方法返回`false`。此方法使用`while`循环重复调用`ResultSet.next`方法以迭代`ResultSet`中的所有数据。

本页面包含下列主题：

- [ResultSet 接口](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html#rs_interface)
- [从 Rows 获取 Column 值](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html#retrieve_rs)
- [游标](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html#cursors)
- [更新 ResultSet 对象中的 Rows](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html#rs_update)
- [使用 Statement 对象进行批量更新](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html#batch_updates)
- [在 ResultSet 对象插入 Rows](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html#rs_insert)

**ResultSet 接口**

`ResultSet`接口提供了检索和操作已执行查询结果的方法，`ResultSet`对象可以具有不同的功能和特征。这些特性是类型，并发性和游标可保持性。

**结果集类型**

`ResultSet`对象的类型在两个维度确定其功能级别：可以操作游标的方式，以及`ResultSet`对象如何反映对基础数据源的并发更改。

`ResultSet`对象的敏感性由三种不同的`ResultSet`类型之一确定：

 -  `TYPE_FORWARD_ONLY`：无法滚动结果集；它的游标仅向前移动，从第一行之前到最后一行之后。结果集中包含的行取决于底层数据库如何生成结果。也就是说，它包含在执行查询时或检索行时满足查询的行。
 -  `TYPE_SCROLL_INSENSITIVE`：结果集可以滚动；它的游标可以相对于当前位置向前和向后移动，并且它可以移动到绝对位置。结果集打开时对基础数据源所做的更改不敏感。它包含在执行查询时或检索行时满足查询的行。
 -  `TYPE_SCROLL_SENSITIVE`：结果可以滚动；它的游标可以相对于当前位置向前和向后移动，并且它可以移动到绝对位置。结果集反映了在结果集保持打开状态时对基础数据源所做的更改。

默认的`ResultSet`类型是`TYPE_FORWARD_ONLY`。

**注意：**并非所有数据库和JDBC驱动程序都支持所有`ResultSet`类型。如果支持指定的`ResultSet`类型，则`DatabaseMetaData.supportsResultSetType`方法返回`true`，否则返回`false`。

**结果集并发性**

`ResultSet`对象的并发性确定支持的更新功能级别。

有两个并发级别：

 -  `CONCUR_READ_ONLY`：无法使用`ResultSet`接口更新`ResultSet`对象。
 -  `CONCUR_UPDATABLE`：可以使用`ResultSet`接口更新`ResultSet`对象。

默认的`ResultSet`并发性是`CONCUR_READ_ONLY`。

**注意：**并非所有JDBC驱动程序和数据库都支持并发。如果驱动程序支持指定的并发级别，则`DatabaseMetaData.supportsResultSetConcurrency`方法返回`true`，否则返回`false`。

方法`CoffeesTable.modifyPrices`演示了如何使用并发级别为`CONCUR_UPDATABLE`的`ResultSet`对象。

**游标可保持性**

调用 `Connection.commit` 方法能够关闭当前事务中已经创建的 `ResultSet` 对象。某些情况下，这并不一定是我们想要的行为。`ResultSet` 属性可保持性使得应用可以控制当`commit`被调用时`ResultSet` 对象（游标）是否会被关闭。

下面的 `ResultSet` 常量可以被提供给 `Connection` 方法 `createStatement`，`prepareStatement`，以及`prepareCall` ：

- `HOLD_CURSORS_OVER_COMMIT`: `ResultSet` 游标不会被关闭，它们是*可保持的*：当 `commit` 方法被调用之后，它们将保持开放状态。可保持的游标是理想的，特别是你的应用大部分使用的都是只读的 `ResultSet` 对象时。
- `CLOSE_CURSORS_AT_COMMIT`: `ResultSet` 对象（游标）当 `commit` 方法被调用时会被关闭。对某些应用来说，调用 `commit` 方法时关闭游标可能会得到更好的性能。

默认的游标可保持性取决于你的 DBMS。

**注意：**并不是所有的 JDBC 驱动和数据库都支持可保持的游标和不可保持游标。下面的方法，`JDBCTutotialUtilities.cursorHoldabilitySupport`，输出 `ResultSet` 对象的默认刻薄爱吃行，以及 `HOLD_CURSORS_OVER_COMMIT` 和 `CLOSE_CURSORS_AT_COMMIT` 是否被支持：

```java
public static void cursorHoldabilitySupport(Connection conn)
    throws SQLException {

    DatabaseMetaData dbMetaData = conn.getMetaData();
    System.out.println("ResultSet.HOLD_CURSORS_OVER_COMMIT = " +
        ResultSet.HOLD_CURSORS_OVER_COMMIT);

    System.out.println("ResultSet.CLOSE_CURSORS_AT_COMMIT = " +
        ResultSet.CLOSE_CURSORS_AT_COMMIT);

    System.out.println("Default cursor holdability: " +
        dbMetaData.getResultSetHoldability());

    System.out.println("Supports HOLD_CURSORS_OVER_COMMIT? " +
        dbMetaData.supportsResultSetHoldability(
            ResultSet.HOLD_CURSORS_OVER_COMMIT));

    System.out.println("Supports CLOSE_CURSORS_AT_COMMIT? " +
        dbMetaData.supportsResultSetHoldability(
            ResultSet.CLOSE_CURSORS_AT_COMMIT));
}
```

**从 Rows 获取 Column 值**

`ResultSet`接口声明`getter`方法（例如，`getBoolean`和`getLong`），用于从当前行检索列值。您可以使用列的索引号或列的别名或名称来检索值。列索引通常更有效。列从1开始编号。为了获得最大的可移植性，每行中的结果集列应按从左到右的顺序读取，每列应只读一次。

例如，以下方法`CoffeesTable.alternateViewTable`按编号检索列值：

```java
public static void alternateViewTable(Connection con)
    throws SQLException {

    Statement stmt = null;
    String query =
        "select COF_NAME, SUP_ID, PRICE, " +
        "SALES, TOTAL from COFFEES";

    try {
        stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery(query);
        while (rs.next()) {
            String coffeeName = rs.getString(1);
            int supplierID = rs.getInt(2);
            float price = rs.getFloat(3);
            int sales = rs.getInt(4);
            int total = rs.getInt(5);
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

用作`getter`方法输入的字符串不区分大小写。当使用字符串调用`getter`方法并且多个列具有与字符串相同的别名或名称时，将返回第一个匹配列的值。使用字符串而不是整数的选项设计用于在生成结果集的 SQL 查询中使用列别名和名称时使用。对于未在查询中明确命名的列（例如，`select * from COFFEES`），最好使用列号。如果使用列名，开发人员应保证使用列别名唯一引用预期的列。列别名有效地重命名结果集的列。要指定列别名，请在`SELECT`语句中使用`AS`子句。

适当类型的`getter`方法检索每列中的值。例如，在方法`CoffeeTables.viewTable`中，`ResultSet rs`的每一行中的第一列是`COF_NAME`，它存储SQL类型`VARCHAR`的值。检索SQL类型`VARCHAR`的值的方法是`getString`。每行中的第二列存储SQL类型`INTEGER`的值，并且用于检索该类型的值的方法是`getInt`。

请注意，尽管建议使用`getString`方法来检索SQL类型`CHAR`和`VARCHAR`，但可以使用它检索任何基本SQL类型。使用`getString`获取所有值可能非常有用，但它也有其局限性。例如，如果它用于检索数字类型，则`getString`将数值转换为Java `String`对象，并且必须先将值转换回数字类型，然后才能将其作为数字进行操作。如果将值视为字符串，则没有任何缺点。此外，如果希望应用程序检索除 SQL3 类型之外的任何标准SQL类型的值，请使用`getString`方法。

**游标**

如前所述，你通过游标访问 `ResultSet` 中的数据，游标指向 `ResultSet` 中的一行数据。不过，当一个 `ResultSet` 对象刚被创建出来时，游标指向第一行数据之前。方法 `CoffeeTables.viewTable` 通过调用 `ResultSet.next` 方法移动游标。还有一些方法可以移动游标：

- `next`: 游标前进一行。如果移动之后游标指向一行数据则返回 `true` ，如果游标指向最后一行数据之后，则返回 `false` 。
- `previous`: 游标后退一行。如果移动之后游标指向一行数据则返回 `true` ，如果游标指向第一行数据之前，则返回 `false` 。
- `first`: 将游标移动到 `ResultSet` 对象中第一行。如果移动之后游标指向第一行数据则返回 `true` ，如果 `ResultSet` 对象不包含任何行数据则返回 `false` 。
- `last:`: Moves the cursor to the last row in the `ResultSet` object. Returns `true` if the cursor is now positioned on the last row and `false` if the `ResultSet` object does not contain any rows.将游标移动到 `ResultSet` 对象中最后一行。如果移动之后游标指向最后一行数据则返回 `true` ，如果 `ResultSet` 对象不包含任何行数据则返回 `false` 。
- `beforeFirst`: 将游标定位到 `ResultSet` 对象的开头，第一行数据之前。如果 `ResultSet` 对象不包含任何行，则此方法没有影响。
- `afterLast`: 将游标定位到 `ResultSet` 对象的末尾，最后一行数据之后。如果 `ResultSet` 对象不包含任何行，则此方法没有影响。
- `relative(int rows)`: 相对于当前位置移动游标。
- `absolute(int row)`: 将光标定位在参数`row`指定的行上。

请注意，`ResultSet`的默认灵敏度为`TYPE_FORWARD_ONLY`，这意味着它无法滚动。如果无法滚动`ResultSet`，则无法调用任何移动光标的方法（`next`除外）。下一节中描述的方法`CoffeesTable.modifyPrices`演示了如何移动`ResultSet`的光标。

**更新 ResultSet 对象中的 Rows**

你不能更新默认的 `ResultSet` 对象，只能向前移动它的游标。不过，你可以创建可滚动的 `ResultSet` 对象(游标可以向前和向后移动到绝对位置)，可以更新该对象。

下面的方法，`CoffeeTable.modifyPrices`，将每行的`PRICE`列乘以参数`percentage`：

```java
public void modifyPrices(float percentage) throws SQLException {

    Statement stmt = null;
    try {
        stmt = con.createStatement();
        stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE,
                   ResultSet.CONCUR_UPDATABLE);
        ResultSet uprs = stmt.executeQuery(
            "SELECT * FROM " + dbName + ".COFFEES");

        while (uprs.next()) {
            float f = uprs.getFloat("PRICE");
            uprs.updateFloat( "PRICE", f * percentage);
            uprs.updateRow();
        }

    } catch (SQLException e ) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

字段`ResultSet.TYPE_SCROLL_SENSITIVE`创建一个`ResultSet`对象，其游标可以相对于当前位置向前和向后移动到绝对位置。字段`ResultSet.CONCUR_UPDATABLE`创建一个可以更新的`ResultSet`对象。有关修改`ResultSet`对象行为的其他字段，请参阅`ResultSet` 文档。

方法`ResultSet.updateFloat`更新指定的列（在本例中，在游标所在的行中具有指定的`float`值的`PRICE`。`ResultSet`包含各种更新方法，使您可以更新列值。但是，这些更新方法都不会修改数据库。必须调用方法`ResultSet.updateRow`来更新数据库。

**使用 Statement 对象进行批量更新**

`Statement`，`PreparedStatement`和`CallableStatement`对象有一个与它们相关的命令列表。该列表可能包含更新，插入或删除行的语句；它还可能包含DDL语句，例如`CREATE TABLE`和`DROP TABLE`。但是，它不能包含一个产生`ResultSet`对象的语句，例如`SELECT`语句。换句话说，该列表只能包含能够产生更新计数的语句。

该列表在创建时与`Statement`对象相关联，最初为空。您可以使用方法`addBatch`将SQL命令添加到此列表中，并使用`clearBatch`方法将其清空。完成向列表添加语句后，调用方法`executeBatch`将它们全部发送到数据库，作为一个单元或批处理执行。

例如，以下方法`CoffeesTable.batchUpdate`通过批量更新向`COFFEES`表添加四行：

```java
public void batchUpdate() throws SQLException {

    Statement stmt = null;
    try {
        this.con.setAutoCommit(false);
        stmt = this.con.createStatement();

        stmt.addBatch(
            "INSERT INTO COFFEES " +
            "VALUES('Amaretto', 49, 9.99, 0, 0)");

        stmt.addBatch(
            "INSERT INTO COFFEES " +
            "VALUES('Hazelnut', 49, 9.99, 0, 0)");

        stmt.addBatch(
            "INSERT INTO COFFEES " +
            "VALUES('Amaretto_decaf', 49, " +
            "10.99, 0, 0)");

        stmt.addBatch(
            "INSERT INTO COFFEES " +
            "VALUES('Hazelnut_decaf', 49, " +
            "10.99, 0, 0)");

        int [] updateCounts = stmt.executeBatch();
        this.con.commit();

    } catch(BatchUpdateException b) {
        JDBCTutorialUtilities.printBatchUpdateException(b);
    } catch(SQLException ex) {
        JDBCTutorialUtilities.printSQLException(ex);
    } finally {
        if (stmt != null) { stmt.close(); }
        this.con.setAutoCommit(true);
    }
}
```

以下行禁用`Connection`对象`con`的自动提交模式，以便在调用方法`executeBatch`时不会自动提交或回滚事务。

```java
this.con.setAutoCommit(false);
```

要允许正确的错误处理，应始终在开始批量更新之前禁用自动提交模式。

方法`Statement.addBatch`将命令添加到与`Statement`对象`stmt`相关联的命令列表中。在这个例子中，这些命令都是`INSERT INTO`语句，每个语句都添加一个由五列值组成的行。`COF_NAME`和`PRICE`列的值分别是咖啡的名称及其价格。每行中的第二个值为`49`，因为这是供应商`Superior Coffee`的标识号。最后两个值，列`SALES`和`TOTAL`的条目都是零，因为还没有销售。（`SALES`是本周销售的这一排咖啡的磅数；`TOTAL`是这种咖啡累计销售的总和。）

以下行将添加到其命令列表中的四个SQL命令发送到要作为批处理执行的数据库：

```java
int [] updateCounts = stmt.executeBatch();
```

请注意，`stmt`使用`executeBatch`方法发送一批插入，而不是方法`executeUpdate`，它只发送一个命令并返回一个更新计数。DBMS按照将命令添加到命令列表的顺序执行命令，因此它首先添加`Amaretto`的值所在的行，然后添加`Hazelnut`，然后是`Amaretto decaf`，最后是`Hazelnut decaf`。如果所有四个命令都成功执行，则DBMS将按照执行顺序为每个命令返回更新计数。更新计数表示每个命令影响的行数存储在数组`updateCounts`中。

如果批处理中的所有四个命令都成功执行，`updateCounts`将包含四个值，所有这些值都是1，因为插入会影响一行。与`stmt`相关联的命令列表现在将为空，因为当`stmt`调用方法`executeBatch`时，先前添加的四个命令被发送到数据库。您可以随时使用`clearBatch`方法显式清空此命令列表。

`Connection.commit`方法使`COFFEES`表的批量更新永久化。需要显式调用此方法，因为此连接的自动提交模式先前已禁用。

以下行为当前的`Connection`对象启用自动提交模式。

```java
this.con.setAutoCommit(true);
```

现在，示例中的每个语句在执行后都会自动提交，并且不再需要调用方法`commit`。

**执行参数化批量更新**

也可以进行参数化批量更新，如下面的代码片段所示，其中`con`是一个`Connection`对象：

```java
con.setAutoCommit(false);
PreparedStatement pstmt = con.prepareStatement(
                              "INSERT INTO COFFEES VALUES( " +
                              "?, ?, ?, ?, ?)");
pstmt.setString(1, "Amaretto");
pstmt.setInt(2, 49);
pstmt.setFloat(3, 9.99);
pstmt.setInt(4, 0);
pstmt.setInt(5, 0);
pstmt.addBatch();

pstmt.setString(1, "Hazelnut");
pstmt.setInt(2, 49);
pstmt.setFloat(3, 9.99);
pstmt.setInt(4, 0);
pstmt.setInt(5, 0);
pstmt.addBatch();

// ... and so on for each new
// type of coffee

int [] updateCounts = pstmt.executeBatch();
con.commit();
con.setAutoCommit(true);
```

**处理批量更新异常**

如果(1)您添加到批处理中的一个SQL语句生成结果集（通常是查询）或(2)批处理中的一个SQL语句由于某些其他原因未成功执行，则在调用方法`executeBatch`时将得到`BatchUpdateException`。

您不应该向一批SQL命令添加查询（一个`SELECT`语句），因为返回更新计数数组的`executeBatch`方法需要每个成功执行的SQL语句的更新计数。这意味着只有返回更新计数的命令（诸如`INSERT INTO`，`UPDATE`，`DELETE`之类的命令）或返回0的命令（例如``CREATE TABLE`，`DROP TABLE`，`ALTER TABLE`）才能使用`executeBatch`方法成功执行批处理。

`BatchUpdateException`包含一个更新计数数组，类似于`executeBatch`方法返回的数组。在这两种情况下，更新计数的顺序与生成它们的命令的顺序相同。这告诉您批处理中有多少命令成功执行以及它们是哪些命令。例如，如果成功执行了五个命令，则该数组将包含五个数字：第一个是第一个命令的更新计数，第二个是第二个命令的更新计数，依此类推。

`BatchUpdateException`派生自`SQLException`。这意味着您可以使用`SQLException`对象可用的所有方法。以下方法`JDBCTutorialUtilities.printBatchUpdateException`打印所有`SQLException`信息以及`BatchUpdateException`对象中包含的更新计数。因为`BatchUpdateException.getUpdateCounts`返回一个`int`数组，所以代码使用`for`循环来打印每个更新计数：

```java
public static void printBatchUpdateException(BatchUpdateException b) {

    System.err.println("----BatchUpdateException----");
    System.err.println("SQLState:  " + b.getSQLState());
    System.err.println("Message:  " + b.getMessage());
    System.err.println("Vendor:  " + b.getErrorCode());
    System.err.print("Update counts:  ");
    int [] updateCounts = b.getUpdateCounts();

    for (int i = 0; i < updateCounts.length; i++) {
        System.err.print(updateCounts[i] + "   ");
    }
}
```

**在 ResultSet 对象中插入 Rows**

**注意**：并非所有JDBC驱动程序都支持使用`ResultSet`接口插入新行。如果尝试插入新行并且JDBC驱动程序数据库不支持此功能，则会引发`SQLFeatureNotSupportedException`异常。

下面的方法`CoffeesTable.insertRow`通过`ResultSet`对象在`COFFEES`中插入一行：

```java
public void insertRow(String coffeeName, int supplierID,
                      float price, int sales, int total)
    throws SQLException {

    Statement stmt = null;
    try {
        stmt = con.createStatement(
            ResultSet.TYPE_SCROLL_SENSITIVE
            ResultSet.CONCUR_UPDATABLE);

        ResultSet uprs = stmt.executeQuery(
            "SELECT * FROM " + dbName +
            ".COFFEES");

        uprs.moveToInsertRow();
        uprs.updateString("COF_NAME", coffeeName);
        uprs.updateInt("SUP_ID", supplierID);
        uprs.updateFloat("PRICE", price);
        uprs.updateInt("SALES", sales);
        uprs.updateInt("TOTAL", total);

        uprs.insertRow();
        uprs.beforeFirst();
    } catch (SQLException e ) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

此示例使用两个参数`ResultSet.TYPE_SCROLL_SENSITIVE`和`ResultSet.CONCUR_UPDATABLE`调用`Connection.createStatement`方法。第一个值使`ResultSet`对象的游标可以向前和向后移动。如果要将行插入到`ResultSet`对象中，则需要第二个值`ResultSet.CONCUR_UPDATABLE`：它指定该`ResultSet`是可以更新的。

在`getter`方法中使用字符串的相同规定也适用于`updater`方法。

方法`ResultSet.moveToInsertRow`将游标移动到插入行。插入行是与可更新结果集关联的特殊行。它本质上是一个缓冲区，可以通过在将行插入结果集之前调用`updater`方法来构造新行。例如，此方法调用方法`ResultSet.updateString`将插入行的`COF_NAME`列更新为`Kona`。

方法`ResultSet.insertRow`将插入行的内容插入到`ResultSet`对象中并插入到数据库中。

**注意**：使用`ResultSet.insertRow`插入行后，应将游标移动到插入行以外的行。例如，此示例使用方法`ResultSet.beforeFirst`将其移动到结果集中的第一行之前。因为如果应用程序的另一部分使用相同的结果集并且游标仍指向插入行，则可能会出现意外结果。

### 使用预编译语句

本页面涵盖如下主题：

-[预编译语句概述](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html#overview_ps)
-[创建 PreparedStatement 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html#create_ps)
-[为 PreparedStatement 参数提供值](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html#supply_values_ps)

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

### 使用事务

有时候你可能会希望一个语句在另外一个语句执行完成之后才生效。比如，The Coffee Break 的老板要更新每周的咖啡销量，同时还要更新目前为止的销售总量。但是，每周销量和销售总量应该同时更新，否则数据将会不一致。确保这两个操作要么全部成功，要么全部不成功，就需要使用事务。事务时一个或者多个语句的集合，作为一个单元执行，要么所有语句都执行成功，要么全部不执行。

本页面涵盖以下主题：

- [关闭自动提交模式](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#disable_auto_commit)
- [提交事务](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#commit_transactions)
- [使用事务保持数据完整性](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#transactions_data_integrity)
- [设定和滚回保存点](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#set_roll_back_savepoints)
- [释放保存点](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#release_savepoints)
- [何时调用 rollback 方法](https://docs.oracle.com/javase/tutorial/jdbc/basics/transactions.html#call_rollback)

**关闭自动提交模式**

当一个连接被创建后，它处于自动提交模式。这意味着每条 SQL 语句都被作为单独的事务，执行完成之后马上就会自动提交。（更准确地说，默认是语句执行完成后被提交，而不是执行时。语句执行完成，指的是它的所有结果集和更新计数都被得到。大多数情况下，其实就是一个语句完成了，然后就会被提交，就在它刚刚执行之后。）

允许两个或者多个语句编组进入一个事务的方法时关闭自动提交模式。下面的例子展示了这种用法，其中`con` 时一个活动连接：

```java
con.setAutoCommit(false);
```

**提交事务**

自动提交模式关闭之后，除非你显式调用 `commit` ，没有任何 SQL 语句会被提交。前一次 `commit` 方法调用之后的所有执行语句都被包含到当前事务中，作为一个单元提交。下面的方法 `CoffeeTable.updateCoffeeSales` ，其中 `con` 是一个活动连接，展示了一个事务：

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

该方法中，连接 `con` 的自动提交模式被关闭，意味着当 `commit` 方法被调用时，两个预编译语句 `updateSales` 和 `updateTotal` 会被一起提交。无论何时 `commit ` 方法被调用（自动提交模式打开时自动被调用，或者自动提交模式关闭时被显式调用），所有当前事务中的语句造成的变化就会被持久化。例子的情况下，意味着 Colombian 咖啡的 `SALES` 和 `TOTAL` 列已经被修改为 `50` （如果之前 `TOTAL` 是 `0`），并将保持此值直到被其它的更新语句修改。

语句 `con.setAutoCommit(true);` 启动自动提交模式，意味着每条语句一旦执行完成就会被提交。这样，你就回到了不需要显式调用 `commit ` 方法的默认状态。建议仅在事务模式期间禁用自动提交模式。这样，您可以避免为多个语句保留数据库锁，这会增加与其他用户冲突的可能性。

**使用事务保持数据完整性**

除了将语句编组为一个执行单元，事务还有助于保持表中数据的完整性。比如，假设一个咖啡店的员工想要在 `COFFEES` 表中输入新的咖啡价格，但是拖延了几天才做。与此同时，咖啡价格上涨了，今天老板正在输入更高的价格。而该员工也正在输入已经过时的价格。插入过时的价格之后，该员工意识到这些价格已经没用了，然后调用 `Connection` 方法 `rollback` 来撤销修改。（方法 `rollback` 取消一个事务并重置那些被修改的值为更改之前）同时，老板正在执行 `SELECT` 语句并打印新的价格。在这种情况下，老板可能会打印已回滚到其先前值的价格，从而使打印价格不正确。

通过使用事务可以避免这种情况，事务为当两个用户同时访问相同数据时产生冲突的情况提供了一定程度的保护。

为了避免事务期间的冲突，DBMS 使用锁机制来阻止来自其它人对正在被当前事务访问的数据的访问。（注意，在自动提交模式中，每条语句都是一个事务，为每条语句锁定并保持。）当设置锁之后，它会强制保持直到事务被提交或者回滚。比如，DBMS 可以所供一张表的一行直到更新它的事务被提交。此锁定的作用就是防止其它用户的脏读，也就是说，读取到更改被持久化之前的值。（访问一个被更新而尚未被提交的值被称为*脏读*，因为该值随时有可能被回滚回到它之前的值。如果你读取了一个稍后被回滚的值，你将获得一个无效的值。）

锁定设置方法取决于事务隔离级别，事务隔离级别的范围从完全不支持事务直到支持强制非常严格的访问规则的事务。

事务隔离级别的一个例子时 `TRANSACTION_READ_COMMITTED` ，它不允许在一个值被提交之前被访问。换句话说，如果事务隔离级别被设置为 `TRANSACTION_READ_COMMITTED` ，DBMS 不允许脏读的发生。`Connection` 接口包含5个值表示你可以在 JDBC 中使用的事务隔离级别：

| Isolation Level                | Transactions  | Dirty Reads      | Non-Repeatable Reads | Phantom Reads    |
| ------------------------------ | ------------- | ---------------- | -------------------- | ---------------- |
| `TRANSACTION_NONE`             | Not supported | *Not applicable* | *Not applicable*     | *Not applicable* |
| `TRANSACTION_READ_COMMITTED`   | Supported     | Prevented        | Allowed              | Allowed          |
| `TRANSACTION_READ_UNCOMMITTED` | Supported     | Allowed          | Allowed              | Allowed          |
| `TRANSACTION_REPEATABLE_READ`  | Supported     | Prevented        | Prevented            | Allowed          |
| `TRANSACTION_SERIALIZABLE`     | Supported     | Prevented        | Prevented            | Prevented        |

*不可重复读*发生的情形大概是这样，事务 A 查询一行，事务 B 随后更新这一行，然后事务 A 稍后再次获取同一行。事务 A 获取同一行两次但是得到了不同的数据。

*幻读*发生的情形，事务 A 查询满足特定条件的行集，事务 B 接下来插入或者更新一行到满足事务 A 中查询条件的行集中，稍后事务 A 再次执行相同条件的查询。此时事务 A 可以看到新增的行。该行数据指向表中的幻影数据。

通常，你不需要任何有关事务隔离级别的工作：你可以仅仅使用 DBMS 的默认值。默认事务隔离级别取决于你的 DBMS。比如，Java DB 的默认事务隔离级别是 `TRANSACTION_READ_COMMITTED` ，JDBC 允许你查看你的 DBMS 设置的事务隔离级别（使用 `Connection` 方法 `getTransactionIsolation` ）并允许你将其设置为别的值（使用 `Connection` 方法 `setTransactionIsolation`）。

**注意：**JDBC 驱动可能不支持所有的事务隔离级别。如果驱动程序不支持调用 `setTransactionIsolation` 方法指定的事务隔离级别，则会选择一个更好级别的、限制更严格的事务隔离级别。如果驱动无法选择一个更高的事务隔离级别，它将抛出 `SQLException` 。使用 `DatabaseMetaData.supportsTransactionIsolationLevel` 确定驱动程序是否支持给定的事务隔离级别。

**设定和滚回保存点**

方法 `Connction.setSavepoint` 方法，在当前事务中设置一个 `Savepoint` 对象。`Connection.rollback` 方法被重载以携带一个 `Savepoint` 参数。

下面的方法，`CoffeeTable.modifyPricesByPercentage` ，按照百分比提升特定咖啡的价格，`priceModifier` 。然而，如果新价格超过特定价格，`maximumPrice` ，则价格会被恢复称为初始价格：

```java
public void modifyPricesByPercentage(
    String coffeeName,
    float priceModifier,
    float maximumPrice)
    throws SQLException {
    
    con.setAutoCommit(false);

    Statement getPrice = null;
    Statement updatePrice = null;
    ResultSet rs = null;
    String query =
        "SELECT COF_NAME, PRICE FROM COFFEES " +
        "WHERE COF_NAME = '" + coffeeName + "'";

    try {
        Savepoint save1 = con.setSavepoint();
        getPrice = con.createStatement(
                       ResultSet.TYPE_SCROLL_INSENSITIVE,
                       ResultSet.CONCUR_READ_ONLY);
        updatePrice = con.createStatement();

        if (!getPrice.execute(query)) {
            System.out.println(
                "Could not find entry " +
                "for coffee named " +
                coffeeName);
        } else {
            rs = getPrice.getResultSet();
            rs.first();
            float oldPrice = rs.getFloat("PRICE");
            float newPrice = oldPrice + (oldPrice * priceModifier);
            System.out.println(
                "Old price of " + coffeeName +
                " is " + oldPrice);

            System.out.println(
                "New price of " + coffeeName +
                " is " + newPrice);

            System.out.println(
                "Performing update...");

            updatePrice.executeUpdate(
                "UPDATE COFFEES SET PRICE = " +
                newPrice +
                " WHERE COF_NAME = '" +
                coffeeName + "'");

            System.out.println(
                "\nCOFFEES table after " +
                "update:");

            CoffeesTable.viewTable(con);

            if (newPrice > maximumPrice) {
                System.out.println(
                    "\nThe new price, " +
                    newPrice +
                    ", is greater than the " +
                    "maximum price, " +
                    maximumPrice +
                    ". Rolling back the " +
                    "transaction...");

                con.rollback(save1);

                System.out.println(
                    "\nCOFFEES table " +
                    "after rollback:");

                CoffeesTable.viewTable(con);
            }
            con.commit();
        }
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } finally {
        if (getPrice != null) { getPrice.close(); }
        if (updatePrice != null) {
            updatePrice.close();
        }
        con.setAutoCommit(true);
    }
}
```

以下语句指定在调用`commit`方法时，将关闭从`getPrice`查询生成的`ResultSet`对象的游标。请注意，如果您的 DBMS 不支持`ResultSet.CLOSE_CURSORS_AT_COMMIT`，则忽略此常量：

```java
getPrice = con.prepareStatement(query, ResultSet.CLOSE_CURSORS_AT_COMMIT);
```

该方法首先使用以下语句创建`Savepoint`：

```java
Savepoint save1 = con.setSavepoint();
```

该方法检查新价格是否大于`maximumPrice`值。如果是，则该方法使用以下语句回滚事务：

```java
con.rollback(save1);
```

因此，当方法通过调用`Connection.commit`方法提交事务时，它不会提交任何已关联的`Savepoint`已回滚的行；它将提交所有其他更新的行。

**释放保存点**

`Connection.releaseSavepoint`方法将`Savepoint`对象作为参数，并将其从当前事务中删除。

释放保存点后，尝试在回滚操作中引用它会导致抛出`SQLException`。在事务提交时或回滚整个事务时，事务中创建的任何保存点都将自动释放并变为无效。将事务滚动回保存点会自动释放该保存点，并使在相关保存点之后创建的任何其他保存点无效。

**何时调用 rollback 方法**

如前所述，调用方法`rollback`会终止事务并将已修改的任何值恢复为其先前值。如果您尝试在事务中执行一个或多个语句而获得了`SQLException`，请调用方法`rollback`以结束事务并重新开始事务。这是了解已提交内容和未提交内容的唯一方法。捕获`SQLException`会告诉您出现了问题，但它并未告诉您已提交或未提交的内容。因为你不能指望没有提交任何东西，所以调用方法`rollback`是确定的唯一方法。

方法`CoffeesTable.updateCoffeeSales`演示了一个事务，并包含一个调用方法`rollback`的`catch`块。如果应用程序继续并使用事务的结果，则对`catch`块中的`rollback`方法的此调用将阻止使用可能不正确的数据。

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

### 使用 JdbcRowSet 对象

`JdbcRowSet`对象是一个增强的`ResultSet`对象。它保持与其数据源的连接，就像`ResultSet`对象一样。最大的区别在于它具有一组属性和一个监听器通知机制，使其成为 JavaBeans 组件。

`JdbcRowSet`对象的主要用途之一是使`ResultSet`对象在没有这些功能的情况下可滚动和可更新。

本节包括以下主题：

- [创建 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#creating-jdbcrowset-object)
- [默认 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#default-jdbcrowset-objects)
- [设定属性](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#setting-properties)
- [使用 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#using-jdbcrowset-object)
- [代码示例](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#code-sample)

**创建 JdbcRowSet 对象**

您可以通过各种方式创建`JdbcRowSet`对象：

- 使用带有`ResultSet`对象的参考实现构造函数
- 使用带有`Connection`对象的参考实现构造函数
- 使用参考实现默认构造函数
- 使用`RowSetFactory`的实例，它是从类`RowSetProvider`创建的

**注意**：或者，您可以使用 JDBC 驱动程序的`JdbcRowSet`实现中的构造函数。但是，`RowSet`接口的实现将与参考实现不同。这些实现将具有不同的名称和构造函数。例如，Oracle JDBC 驱动程序的`JdbcRowSet`接口的实现名为`oracle.jdbc.rowset.OracleJDBCRowSet`。

**传递 ResultSet 对象**

创建`JdbcRowSet`对象的最简单方法是生成一个`ResultSet`对象并将其传递给`JdbcRowSetImpl`构造器。这样做不仅会创建一个`JdbcRowSet`对象，还会使用`ResultSet`对象中的数据填充它。

**注意**：传递给`JdbcRowSetImpl`构造函数的`ResultSet`对象必须是可滚动的。

例如，下面的代码片段使用`Connection`对象`con`来创建`Statement`对象`stmt`，然后执行查询。该查询生成`ResultSet`对象`rs`，它被传递给构造函数以创建一个用`rs`中的数据初始化的新`JdbcRowSet`对象：

```java
stmt = con.createStatement(
           ResultSet.TYPE_SCROLL_SENSITIVE,
           ResultSet.CONCUR_UPDATABLE);
rs = stmt.executeQuery("select * from COFFEES");
jdbcRs = new JdbcRowSetImpl(rs);
```

使用`ResultSet`对象创建的`JdbcRowSet`对象充当`ResultSet`对象的包装器。因为`RowSet`对象`rs`是可滚动和可更新的，所以`jdbcRs`也是可滚动和可更新的。如果你运行没有任何参数的`createStatement`方法，`rs`将不可滚动或可更新，并且`jdbcRs`也不会。

**传递 Connection 对象**

以下代码摘录自 [`JdbcRowSetSample`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 中的第一个语句创建了一个`JdbcRowSet`对象，该对象连接到数据库 `Connection`对象`con`：

```java
jdbcRs = new JdbcRowSetImpl(con);
jdbcRs.setCommand("select * from COFFEES");
jdbcRs.execute();
```

在您使用方法`setCommand`指定 SQL 语句之前，对象`jdbcRs`不包含任何数据，然后运行方法`execute`。

对象`jdbcRs`是可滚动和可更新的；默认情况下，`JdbcRowSet`和所有其他`RowSet`对象是可滚动和可更新的，除非另有说明。有关您可以指定的`JdbcRowSet`属性的更多信息，请参见  [Default JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#default-jdbcrowset-objects) 。

**使用默认构造器**

以下代码片段中的第一个语句创建一个空的`JdbcRowSet`对象。

```java
public void createJdbcRowSet(String username, String password) {

    jdbcRs = new JdbcRowSetImpl();
    jdbcRs.setCommand("select * from COFFEES");
    jdbcRs.setUrl("jdbc:myDriver:myAttribute");
    jdbcRs.setUsername(username);
    jdbcRs.setPassword(password);
    jdbcRs.execute();
    // ...
}
```

在您使用方法`setCommand`指定SQL语句之前，对象`jdbcRs`不包含任何数据，指定`JdbcResultSet`对象如何连接数据库，然后运行方法`execute`。

所有参考实现构造函数都为 [Default JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#default-jdbcrowset-objects) 部分中列出的属性分配默认值。

**使用 RowSetFactory 接口**

使用RowSet 1.1，它是Java SE 7及更高版本的一部分，您可以使用`RowSetFactory`的实例来创建`JdbcRowSet`对象。例如，以下代码摘录使用`RowSetFactory`接口的实例来创建`JdbcRowSet`对象，`jdbcRs`：

```java
public void createJdbcRowSetWithRowSetFactory(
    String username, String password)
    throws SQLException {

    RowSetFactory myRowSetFactory = null;
    JdbcRowSet jdbcRs = null;
    ResultSet rs = null;
    Statement stmt = null;

    try {
        myRowSetFactory = RowSetProvider.newFactory();
        jdbcRs = myRowSetFactory.createJdbcRowSet();

        jdbcRs.setUrl("jdbc:myDriver:myAttribute");
        jdbcRs.setUsername(username);
        jdbcRs.setPassword(password);

        jdbcRs.setCommand("select * from COFFEES");
        jdbcRs.execute();

        // ...
    }
}
```

下面的语句使用默认的`RowSetFactory`实现，`com.sun.rowset.RowSetFactoryImpl`创建`RowSetProvider`对象`myRowSetFactory`：

```java
myRowSetFactory = RowSetProvider.newFactory();
```

或者，如果您的 JDBC 驱动程序有自己的`RowSetFactory`实现，您可以将其指定为`newFactory`方法的参数。

以下语句创建`JdbcRowSet`对象`jdbcRs`并配置其数据库连接属性：

```java
jdbcRs = myRowSetFactory.createJdbcRowSet();
jdbcRs.setUrl("jdbc:myDriver:myAttribute");
jdbcRs.setUsername(username);
jdbcRs.setPassword(password);
```

`RowSetFactory`接口包含创建 RowSet 1.1 及更高版本中可用的不同类型的`RowSet`实现的方法：

- `createCachedRowSet`
- `createFilteredRowSet`
- `createJdbcRowSet`
- `createJoinRowSet`
- `createWebRowSet`

**默认 JdbcRowSet 对象**

使用默认构造函数创建`JdbcRowSet`对象时，新的`JdbcRowSet`对象将具有以下属性：

- `type`：`ResultSet.TYPE_SCROLL_INSENSITIVE`（有一个可滚动的游标）
- `concurrency`：`ResultSet.CONCUR_UPDATABLE`（可以更新）
- `escapeProcessing`：`true`（驱动程序将执行转义处理；启用转义处理时，驱动程序将扫描任何转义语法并将其转换为特定数据库理解的代码）
- `maxRows`：`0`（行数没有限制）
- `maxFieldSize`：`0`（对列值的字节数没有限制;仅适用于存储`BINARY`，`VARBINARY`，`LONGVARBINARY`，`CHAR`，`VARCHAR`和`LONGVARCHAR`值）
- `queryTimeout`：`0`（没有时间限制执行查询所需的时间）
- `showDeleted`：`false`（删除的行不可见）
- `transactionIsolation`：`Connection.TRANSACTION_READ_COMMITTED`（只读取已提交的数据）
- `typeMap`：`null`（与`RowSet`对象使用的`Connection`对象关联的类型映射是`null`）

从这个列表中你必须记住的主要事情是`JdbcRowSet`和所有其他`RowSet`对象是可滚动和可更新的，除非你为这些属性设置不同的值。

**设定属性**

 [Default JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#default-jdbcrowset-objects) 一节列出了新的`JdbcRowSet`被创建时默认设置的属性。如果使用默认构造函数，则必须先设置一些其他属性，然后才能使用数据填充新的`JdbcRowSet`对象。

为了获取其数据，`JdbcRowSet`对象首先需要连接到数据库。以下四个属性包含用于获取与数据库的连接的信息。

- `username`：用户提供给数据库的名称，作为获取访问权限的一部分
- `password`：用户的数据库密码
- `url`：用户想要连接的数据库的 JDBC URL
- `datasourceName`：用于检索已向 JNDI 命名服务注册的`DataSource`对象的名称

这些属性中的哪一个需要设置取决于您要如何建立连接。首选方法是使用`DataSource`对象，但是使用 JNDI 命名服务注册`DataSource`对象可能不实际，这通常由系统管理员完成。因此，代码示例都使用`DriverManager`机制来获取连接，您使用`url`属性而不是`datasourceName`属性。

您必须设置的另一个属性是`command`属性。此属性是确定`JdbcRowSet`对象将包含哪些数据的查询。例如，以下代码行将`command`属性设置为一个查询，该查询生成一个`ResultSet`对象，该对象包含表`COFFEES`中的所有数据：

```java
jdbcRs.setCommand("select * from COFFEES");
```

在设置`command`属性和建立连接所需的属性之后，您可以通过调用`execute`方法填充`jdbcRs`对象和数据。

```java
jdbcRs.execute();
```

`execute`方法在后台为你做了很多事情：

- 它使用您分配给`url`，`username`和`password`properties的值建立与数据库的连接。
- 它执行您在`command`属性中设置的查询。
- 它将生成的`ResultSet`对象中的数据读入`jdbcRs`对象。

**使用 JdbcRowSet 对象**

您更新，插入和删除`JdbcRowSet`对象中的行的方式与更新，插入和删除可更新的`ResultSet`对象中的行的方式相同。类似地，您导航`JdbcRowSet`对象的方式与导航可滚动的`ResultSet`对象的方式相同。

Coffee Break 的连锁店获得了另一家咖啡馆连锁店，现在拥有一个不支持滚动或更新结果集的遗留数据库。换句话说，此遗留数据库生成的任何`ResultSet`对象都没有可滚动的游标，并且其中的数据无法修改。但是，通过创建一个用`ResultSet`对象填充数据的`JdbcRowSet`对象，实际上可以使`ResultSet`对象可滚动和可更新。

如前所述，`JdbcRowSet`对象默认是可滚动和可更新的。因为它的内容与`ResultSet`对象中的内容相同，所以对`JdbcRowSet`对象进行操作相当于对`ResultSet`对象本身进行操作。并且因为`JdbcRowSet`对象与数据库有持续的连接，所以对其中的数据的修改也会对其连接的数据库中的数据进行更改。

本节涵盖以下主题：

- [导航 JdbcRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#navigating-jdbcrowset-object)
- [更新列值](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#updating-column-value)
- [插入行](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#inserting-row)
- [删除行](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#deleting-row)

**导航 JdbcRowSet 对象**

不可滚动的`ResultSet`对象只能使用`next`方法向前移动光标，它只能将光标从第一行向前移动到最后一行。 但是，默认的`JdbcRowSet`对象可以使用`ResultSet`接口中定义的所有游标移动方法。

`JdbcRowSet`对象可以调用方法`next`，它也可以调用任何其他`ResultSet`光标移动方法。 例如，以下代码行将光标移动到`jdbcRs`对象中的第四行，然后返回第三行：

```java
jdbcRs.absolute(4);
jdbcRs.previous();
```

方法`previous`类似于`next`方法，因为它可以在`while`循环中用于按顺序遍历所有行。不同之处在于您必须将光标移动到最后一行之后的位置，并且`previous`将光标移向开头。

**更新列值**

您更新`JdbcRowSet`对象中的数据的方式与更新`ResultSet`对象中的数据的方式相同。

假设 Coffee Break 所有者想要提高一磅 Espresso 咖啡的价格。如果所有者知道 Espresso 位于`jdbcRs`对象的第三行，则执行此操作的代码可能如下所示：

```java
jdbcRs.absolute(3);
jdbcRs.updateFloat("PRICE", 10.99f);
jdbcRs.updateRow();
```

代码将光标移动到第三行，并将`PRICE`列的值更改为10.99，然后使用新价格更新数据库。

调用方法`updateRow`会更新数据库，因为`jdbcRs`已经保持与数据库的连接。对于断开连接的`RowSet`对象，情况是不同的。

**插入行**

如果 Coffee Break 连锁店的所有者想要为他提供的东西添加一种或多种咖啡，那么所有者将需要为每种新咖啡在`COFFEES`表中添加一行，如下面的代码片段`JdbcRowSetSample`所示。请注意，因为`jdbcRs`对象始终连接到数据库，所以将一行插入`JdbcRowSet`对象与将一行插入`ResultSet`对象相同：您将光标移动到插入行，使用适当的 updater 方法为每列设置一个值，并调用方法`insertRow`：

```java
jdbcRs.moveToInsertRow();
jdbcRs.updateString("COF_NAME", "HouseBlend");
jdbcRs.updateInt("SUP_ID", 49);
jdbcRs.updateFloat("PRICE", 7.99f);
jdbcRs.updateInt("SALES", 0);
jdbcRs.updateInt("TOTAL", 0);
jdbcRs.insertRow();

jdbcRs.moveToInsertRow();
jdbcRs.updateString("COF_NAME", "HouseDecaf");
jdbcRs.updateInt("SUP_ID", 49);
jdbcRs.updateFloat("PRICE", 8.99f);
jdbcRs.updateInt("SALES", 0);
jdbcRs.updateInt("TOTAL", 0);
jdbcRs.insertRow();
```

当您调用方法`insertRow`时，新行将插入到`jdbcRs`对象中，并且也会插入到数据库中。前面的代码片段经历了两次这个过程，因此在`jdbcRs`对象和数据库中插入了两个新行。

**删除行**

与更新数据和插入新行一样，删除行对于`JdbcRowSet`对象和对于`ResultSet`对象来说是相同的。店主想停止销售法国烤无咖啡因咖啡，这是`jdbcRs`对象的最后一行。在下面的代码行中，第一行将光标移动到最后一行，第二行删除`jdbcRs`对象和数据库中的最后一行：

```java
jdbcRs.last();
jdbcRs.deleteRow();
```

**代码示例**

示例 `JdbcRowSetSample` 执行以下操作：

- 创建一个新的`JdbcRowSet`对象，该对象使用`ResultSet`对象初始化，该对象是由执行查询生成的，该查询检索`COFFEES`表中的所有行
- 将光标移动到`COFFEES`表的第三行，并更新该行中的`PRICE`列
- 插入两个新行，一个用于`HouseBlend`，另一个用于`HouseDecaf`
- 将光标移动到最后一行并删除它


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

- `username` ：用户提供给数据库的名称，作为获取访问权限的一部分。
- `password` ：用户的数据库密码。
- `url` ：用户想要连接的数据库的 JDBC URL。
- `datasourceName` ：用于检索已向 JNDI 命名服务注册的`DataSource`对象的名称。

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

- `cursorMoved`：定义当`RowSet`对象中的游标移动时侦听器将执行的操作（如果有）。
- `rowChanged`：定义监听器将执行的操作（如果有），行中的一个或多个列值发生更改，插入行或删除行时。
- `rowSetChanged`：定义在使用新数据填充`RowSet`对象时监听器将执行的操作（如果有）。

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

### 使用 FilteredRowSet 对象

使用`FilteredRowSet`对象可以减少`RowSet`对象中可见的行数，这样您就可以只处理与您正在执行的操作相关的数据。您可以决定要对数据设置的限制（如何“过滤”数据）并将该过滤器应用于`FilteredRowSet`对象。换句话说，`FilteredRowSet`对象仅显示符合您设置的限制的数据行。`JdbcRowSet`对象始终与其数据源有连接，可以使用对数据源的查询进行此筛选，该数据源仅选择要查看的列和行。查询的`WHERE`子句定义了过滤条件。`FilteredRowSet`对象为断开连接的`RowSet`对象提供了一种方法来进行此过滤，而无需对数据源执行查询，从而避免必须连接到数据源并向其发送查询。

例如，假设咖啡馆 Coffee Break 连锁店已经发展到美国各地的数百家商店，并且所有商店都列在名为`COFFEE_HOUSES`的表中。老板希望仅通过咖啡馆比较应用来衡量加利福尼亚州商店的成功与否，该应用不需要与数据库系统的持久连接。这种比较将考察销售商品与销售咖啡饮料的盈利能力以及各种其他成功衡量标准，并将根据咖啡饮料销售，商品销售和总销售额对加州商店进行排名。因为表`COFFEE_HOUSES`有数百行，所以如果搜索的数据量减少到`STORE_ID`列中的值表示加利福尼亚的那些行，这些比较将更快更容易。

这正是`FilteredRowSet`对象通过提供以下功能解决的问题：

- 能够根据设定的标准限制可见的行
- 能够选择哪些数据可见而无需连接到数据源

本节涵盖以下主题：

- [在 Predicate 对象中定义过滤准则](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#defining-filtering-criteria-in-predicate-object)
- [创建 FilteredRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#creating-filteredrowset-object)
- [创建并设置 Predicate 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#creating-and-setting-predicate-object)
- [使用新的 Predicate 对象设置 FilteredRowSet 对象以进一步过滤数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#filter-data-further)
- [更新 FilteredRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#updating-filteredrowset-object)
- [插入或者更新行](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#inserting-or-updating-row)
- [删除所有过滤器使所有行可见](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#removing-all-filters)
- [删除行](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#deleting-row)

**在 Predicate 对象中定义过滤准则**

要设置`FilteredRowSet`对象中哪些行可见的条件，您可以定义一个实现`Predicate`接口的类。使用此类创建的对象使用以下内容进行初始化：

- 值必须落在的范围的高端
- 值必须落在的范围的低端
- 列的列名或列号，其值必须位于由高和低边界设置的值范围内

请注意，值的范围是闭区间，这意味着边界处的值包含在范围内。例如，如果范围具有100的上限值和50的下限值，则认为值50在该范围内，值49不是。同样，100在范围内，但101不在。

根据老板想要比较加利福尼亚商店的情况，必须编写`Predicate`接口的实现，该接口用于过滤位于加利福尼亚州的 Coffee Break 咖啡馆。没有一种正确的方法可以做到这一点，这意味着在编写实现方面存在很大的自由度。例如，您可以根据需要为类及其成员命名，并以任何方式实现构造函数和三个计算方法，以实现所需的结果。

列出所有咖啡馆的表格名为`COFFEE_HOUSES`，有几百行。为了使事情更易于管理，本示例使用行少得多的表，这足以说明如何完成过滤。

`STORE_ID`列中的值是`int`值，其中指示咖啡馆所处的状态等。例如，以`10`开头的值表示该州是加利福尼亚州。以`32`开头的`STORE_ID`值表示俄勒冈州，以`33`开头的那些表示华盛顿州。

以下类 [`StateFilter`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 实现了`Predicate`接口：

```java
public class StateFilter implements Predicate {

    private int lo;
    private int hi;
    private String colName = null;
    private int colNumber = -1;

    public StateFilter(int lo, int hi, int colNumber) {
        this.lo = lo;
        this.hi = hi;
        this.colNumber = colNumber;
    }

    public StateFilter(int lo, int hi, String colName) {
        this.lo = lo;
        this.hi = hi;
        this.colName = colName;
    }

    public boolean evaluate(Object value, String columnName) {
        boolean evaluation = true;
        if (columnName.equalsIgnoreCase(this.colName)) {
            int columnValue = ((Integer)value).intValue();
            if ((columnValue >= this.lo)
                &&
                (columnValue <= this.hi)) {
                evaluation = true;
            } else {
                evaluation = false;
            }
        }
        return evaluation;
    }

    public boolean evaluate(Object value, int columnNumber) {

        boolean evaluation = true;

        if (this.colNumber == columnNumber) {
            int columnValue = ((Integer)value).intValue();
            if ((columnValue >= this.lo)
                &&
                (columnValue <= this.hi)) {
                evaluation = true;
            } else {
                evaluation = false;
            }
        }
        return evaluation;
    }


    public boolean evaluate(RowSet rs) {
    
        CachedRowSet frs = (CachedRowSet)rs;
        boolean evaluation = false;

        try {
            int columnValue = -1;

            if (this.colNumber > 0) {
                columnValue = frs.getInt(this.colNumber);
            } else if (this.colName != null) {
                columnValue = frs.getInt(this.colName);
            } else {
                return false;
            }

            if ((columnValue >= this.lo)
                &&
                (columnValue <= this.hi)) {
                evaluation = true;
            }
        } catch (SQLException e) {
            JDBCTutorialUtilities.printSQLException(e);
            return false;
        } catch (NullPointerException npe) {
            System.err.println("NullPointerException caught");
            return false;
        }
        return evaluation;
    }
}
```

这是一个非常简单的实现，它检查由`colName`或`colNumber`指定的列中的值，以查看它是否在`lo`到`hi`的范围内。来自 [`FilteredRowSetSample`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 的以下代码行创建了一个过滤器，该过滤器仅允许`STORE_ID`列所在的行值表示介于10000和10999之间的值，表示加利福尼亚州的位置：

```
StateFilter myStateFilter = new StateFilter(10000, 10999, 1);
```

请注意，刚定义的`StateFilter`类适用于一列。通过使用参数数组而不是单个值，可以将它应用于两个或更多列。例如，`Filter`对象的构造函数可能如下所示：

```java
public Filter2(Object [] lo, Object [] hi, Object [] colNumber) {
    this.lo = lo;
    this.hi = hi;
    this.colNumber = colNumber;
}
```

`colNumber`对象中的第一个元素给出第一列，其中将根据`lo`中的第一个元素和`hi`中的第一个元素检查该值。将使用`lo`和`hi`中的第二个元素检查由`colNumber`指示的第二列中的值，依此类推。因此，三个数组中的元素数应该相同。下面的代码是`evaluate(RowSet rs)`方法的实现可能看起来像`Filter2`对象，其中参数是数组：

```java
public boolean evaluate(RowSet rs) {
    CachedRowSet crs = (CachedRowSet)rs;
    boolean bool1;
    boolean bool2;
    for (int i = 0; i < colNumber.length; i++) {

        if ((rs.getObject(colNumber[i] >= lo [i]) &&
            (rs.getObject(colNumber[i] <= hi[i]) {
            bool1 = true;
        } else {
            bool2 = true;
        }

        if (bool2) {
            return false;
        } else {
            return true;
        }
    }
}
```

使用`Filter2`实现的优点是你可以使用任何`Object`类型的参数，并且可以检查一列或多列而无需编写另一个实现。但是，您必须传递一个`Object`类型，这意味着您必须将基本类型转换为其`Object`类型。例如，如果对`lo`和`hi`使用`int`值，则必须将`int`值转换为`Integer`对象，然后再将其传递给构造函数。`String`对象已经是`Object`类型，所以你不必转换它们。

**创建 FilteredRowSet 对象**

`FilteredRowSet`接口的参考实现，`FilteredRowSetImpl`，包括一个默认构造函数，在下面的代码行中使用它来创建空的`FilteredRowSet`对象`frs`：

```
FilteredRowSet frs = new FilteredRowSetImpl();
```

该实现扩展了`BaseRowSet`抽象类，因此`frs`对象具有在`BaseRowSet`中定义的默认属性。这意味着`frs`是可滚动的，可更新的，不显示已删除的行，已启用转义处理，等等。另外，因为`FilteredRowSet`接口是`CachedRowSet`，`Joinable`和`WebRowSet`的子接口，所以`frs`对象具有每个接口的能力。它可以作为断开连接的`RowSet`对象运行，可以是`JoinRowSet`对象的一部分，并且可以以 XML 格式读写自己。

**注意**：或者，您可以使用JDBC驱动程序的`WebRowSet`实现中的构造函数。但是，`RowSet`接口的实现将与参考实现不同。这些实现将具有不同的名称和构造函数。例如，Oracle JDBC 驱动程序的`WebRowSet`接口的实现名为`oracle.jdbc.rowset.OracleWebRowSet`。

您可以使用从RowSetProvider类创建的`RowSetFactory`实例来创建`FilteredRowSet`对象。请参阅 [Using JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html) 中的 [Using the RowSetFactory Interface](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#rowsetfactory) 了解更多信息。

与其他断开连接的`RowSet`对象一样，`frs`对象必须填充来自表格数据源的数据，表格数据源是参考实现中的关系数据库。来自 [`FilteredRowSetSample`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 的以下代码片段设置连接到数据库以执行其命令所需的属性。请注意，此代码使用`DriverManager`类进行连接，这样做是为了方便起见。通常，最好使用已向实现 Java 命名和目录接口 (JNDI) 的命名服务注册的`DataSource`对象：

```java
frs.setCommand("SELECT * FROM COFFEE_HOUSES");
frs.setUsername(settings.userName);
frs.setPassword(settings.password);
frs.setUrl(settings.urlString);
```

以下代码行使用存储在`COFFEE_HOUSE`表中的数据填充`frs`对象：

```java
frs.execute();
```

方法`execute`通过调用`frs`的`RowSetReader`对象来执行各种事情，它创建一个连接，执行`frs`的命令，用`ResultSet`中的数据填充`frs` 生成的对象，并关闭连接。 请注意，如果表`COFFEE_HOUSES`的行数多于`frs`对象一次可以保存在内存中，则会使用`CachedRowSet`分页方法。

在该场景中，Coffee Break 所有者将在办公室中完成上述任务，然后将存储在`frs`对象中的信息导入或下载到咖啡馆比较应用程序中。从现在开始，`frs`对象将独立运行，而无需连接到数据源。

**创建并设置 Predicate 对象**

既然`FilteredRowSet`对象`frs`包含了 Coffee Break 位置的列表，你可以设置选择标准来缩小`frs`对象中可见的行数。

下面的代码行使用先前定义的`StateFilter`类来创建对象`myStateFilter`，该对象检查列`STORE_ID`以确定哪些商店在加利福尼亚（如果商店的ID号介于10000和10999之间，则商店在加利福尼亚州）：

```java
StateFilter myStateFilter = new StateFilter(10000, 10999, 1);
```

以下行将`myStateFilter`设置为`frs`的过滤器。

```java
frs.setFilter(myStateFilter);
```

要进行实际过滤，可以调用方法`next`，它在参考实现中调用之前已实现的`Predicate.evaluate`方法的相应版本。

如果返回值为`true`，则该行将可见；如果返回值为`false`，则该行将不可见。

**使用新的 Predicate 对象设置 FilteredRowSet 对象以进一步过滤数据**

您可以串行设置多个过滤器。第一次调用方法`setFilter`并将其传递给`Predicate`对象时，您已在该过滤器中应用了过滤条件。在每行调用方法`next`后，只显示那些满足过滤器的行，你可以再次调用`setFilter`，传递一个不同的`Predicate`对象。即使一次只设置一个过滤器，效果是两个过滤器都累积应用。

例如，所有者通过将`stateFilter`设置为`frs`的`Predicate`对象来检索加利福尼亚州的 Coffee Break 商店列表。现在，店主希望比较加利福尼亚州的两个城市，旧金山（表格中为`COFFEE_HOUSES`表中的`SF`）和洛杉矶（表格中的`LA`）中的商店。首先要做的是编写一个`Predicate`实现，用于过滤`SF`或`LA`中的商店：

```java
public class CityFilter implements Predicate {

    private String[] cities;
    private String colName = null;
    private int colNumber = -1;

    public CityFilter(String[] citiesArg, String colNameArg) {
        this.cities = citiesArg;
        this.colNumber = -1;
        this.colName = colNameArg;
    }

    public CityFilter(String[] citiesArg, int colNumberArg) {
        this.cities = citiesArg;
        this.colNumber = colNumberArg;
        this.colName = null;
    }

    public boolean evaluate Object valueArg, String colNameArg) {

        if (colNameArg.equalsIgnoreCase(this.colName)) {
            for (int i = 0; i < this.cities.length; i++) {
                if (this.cities[i].equalsIgnoreCase((String)valueArg)) {
                    return true;
                }
            }
        }
        return false;
    }

    public boolean evaluate(Object valueArg, int colNumberArg) {

        if (colNumberArg == this.colNumber) {
            for (int i = 0; i < this.cities.length; i++) {
                if (this.cities[i].equalsIgnoreCase((String)valueArg)) {
                    return true;
                }
            }
        }
        return false;
    }


    public boolean evaluate(RowSet rs) {

        if (rs == null) return false;

        try {
            for (int i = 0; i < this.cities.length; i++) {

                String cityName = null;

                if (this.colNumber > 0) {
                    cityName = (String)rs.getObject(this.colNumber);
                } else if (this.colName != null) {
                    cityName = (String)rs.getObject(this.colName);
                } else {
                    return false;
                }

                if (cityName.equalsIgnoreCase(cities[i])) {
                    return true;
                }
            }
        } catch (SQLException e) {
            return false;
        }
        return false;
    }
}
```

来自 [`FilteredRowSetSample`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 的以下代码片段设置新过滤器并遍历`frs`中的行，打印出来 `CITY`列包含`SF`或`LA`的行。请注意，`frs`目前只包含商店在加利福尼亚州的行，因此当过滤器更改为另一个`Predicate`对象时，`Predicate`对象`state`的条件仍然有效。下面的代码将过滤器设置为`CityFilter`对象`city`。`CityFilter`实现使用数组作为构造函数的参数来说明如何完成：

```java
public void testFilteredRowSet() {

    FilteredRowSet frs = null;
    StateFilter myStateFilter = new StateFilter(10000, 10999, 1);
    String[] cityArray = { "SF", "LA" };

    CityFilter myCityFilter = new CityFilter(cityArray, 2);

    try {
        frs = new FilteredRowSetImpl();

        frs.setCommand("SELECT * FROM COFFEE_HOUSES");
        frs.setUsername(settings.userName);
        frs.setPassword(settings.password);
        frs.setUrl(settings.urlString);
        frs.execute();

        System.out.println("\nBefore filter:");
        FilteredRowSetSample.viewTable(this.con);

        System.out.println("\nSetting state filter:");
        frs.beforeFirst();
        frs.setFilter(myStateFilter);
        this.viewFilteredRowSet(frs);

        System.out.println("\nSetting city filter:");
        frs.beforeFirst();
        frs.setFilter(myCityFilter);
        this.viewFilteredRowSet(frs);
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    }
}
```

对于位于加利福尼亚州旧金山或加利福尼亚州洛杉矶的每个商店，输出应包含一行。如果有一行，其中`CITY`列包含`LA`而`STORE_ID`列包含40003，则它不会包含在列表中，因为当过滤器设置为`state`时它已经被过滤掉了。（40003不在10000到10999的范围内。）

**更新 FilteredRowSet 对象**

您可以对`FilteredRowSet`对象进行更改，但前提是该更改不违反当前有效的任何过滤条件。例如，如果新值或值在过滤条件内，则可以插入新行或更改现有行中的一个或多个值。

**插入或者更新行**

假设两个新的咖啡休息咖啡馆刚刚开业，店主想将它们添加到所有咖啡馆的名单中。如果要插入的行不符合有效的累积过滤条件，则将阻止添加该行。

`frs`对象的当前状态是设置了`StateFilter`对象，然后设置了`CityFilter`对象。因此，`frs`目前只显示那些满足两个过滤器条件的行。同样重要的是，除非满足两个过滤器的条件，否则不能向`frs`对象添加行。下面的代码片段试图在`frs`对象中插入两个新行，一行中`STORE_ID`和`CITY`列中的值都满足条件，一行中`STORE_ID`中的值无法通过过滤器，但`CITY`列中的值可以通过过滤器：

```java
frs.moveToInsertRow();
frs.updateInt("STORE_ID", 10101);
frs.updateString("CITY", "SF");
frs.updateLong("COF_SALES", 0);
frs.updateLong("MERCH_SALES", 0);
frs.updateLong("TOTAL_SALES", 0);
frs.insertRow();

frs.updateInt("STORE_ID", 33101);
frs.updateString("CITY", "SF");
frs.updateLong("COF_SALES", 0);
frs.updateLong("MERCH_SALES", 0);
frs.updateLong("TOTAL_SALES", 0);
frs.insertRow();
frs.moveToCurrentRow();
```

如果你使用`next`方法遍历`frs`对象，你会发现加利福尼亚州旧金山的新咖啡馆有一行数据，但华盛顿旧金山的商店没有。

**删除所有过滤器使所有行可见**

店主可以通过使过滤器无效来在华盛顿添加商店。如果没有设置过滤器，`frs`对象中的所有行都会再次可见，并且任何位置的商店都可以添加到商店列表中。下面的代码行取消了当前的过滤器，有效地消除了之前在`frs`对象上设置的两个`Predicate`实现。

```java
frs.setFilter(null);
```

**删除行**

如果店主决定关闭或出售其中一个咖啡馆，店主将希望将其从`COFFEE_HOUSES`表中删除。只要行可见，店主就可以删除表现不佳的咖啡馆的行。

例如，假设刚刚使用参数`null`调用方法`setFilter`，则`frs`对象上没有设置过滤器。这意味着所有行都是可见的，因此可以删除。但是，在设置`StateFilter`对象`myStateFilter`之后，过滤掉加利福尼亚以外的任何州，只能删除位于加利福尼亚州的店。当`CityFilter`对象`myCityFilter`被设置为`frs`对象时，只有加利福尼亚州旧金山或加利福尼亚州洛杉矶的咖啡馆才能被删除，因为它们只在可见的行中。

### 使用 WebRowSet 对象

`WebRowSet`对象非常特殊，因为除了提供`CachedRowSet`对象的所有功能外，它还可以将自身编写为 XML 文档，还可以读取该 XML 文档以将其自身转换回`WebRowSet`对象。由于 XML 是不同企业可以相互通信的语言，因此它已成为 Web 服务通信的标准。因此，`WebRowSet`对象通过使 Web 服务以 XML 文档的形式从数据库发送和接收数据来满足实际需求。

本节涵盖以下主题：

- [创建并填充 WebRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#creating-and-populating-webrowset-object)
- [将 WebRowSet 对象写入 XML 以及从 XML 读取 WebRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#writing-and-reading-webrowset-object-to-xml)
- [XML 文档中有什么？](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#what-is-in-xml-document)
- [修改 WebRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#making-changes-to-webrowset-object)

Coffee Break 公司已经扩展到在线销售咖啡。用户从 Coffee Break 网站点击咖啡，通过从公司数据库获取最新信息，定期更新价目表。本节演示如何使用`WebRowSet`对象和单个方法调用将价格数据作为 XML 文档发送。

**创建并填充 WebRowSet 对象**

使用参考实现`WebRowSetImpl`中定义的默认构造函数创建一个新的`WebRowSet`对象，如以下代码行所示：

```java
WebRowSet priceList = new WebRowSetImpl();
```

尽管`priceList`对象还没有数据，但它具有`BaseRowSet`对象的默认属性。它的`SyncProvider`object首先设置为`RIOptimisticProvider`实现，这是所有断开连接的`RowSet`对象的默认设置。但是，`WebRowSet`实现将`SyncProvider`对象重置为`RIXMLProvider`实现。

您可以使用从`RowSetProvider`类创建的`RowSetFactory`实例来创建`WebRowSet`对象。请参阅 [Using JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html) 中的 [Using the RowSetFactory Interface](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#rowsetfactory) 了解更多信息。

Coffee Break 总部定期向其网站发送价目表更新。有关`WebRowSet`对象的信息将显示一种可以在 XML 文档中发送最新价格表的方法。

价格表包含`COFFEES`表中`COF_NAME`和`PRICE`列中的数据。以下代码片段设置所需的属性，并使用价目表数据填充`priceList`对象：

```java
public void getPriceList(String username, String password) {
    priceList.setCommand("SELECT COF_NAME, PRICE FROM COFFEES");
    priceList.setURL("jdbc:mySubprotocol:myDatabase");
    priceList.setUsername(username);
    priceList.setPassword(password);
    priceList.execute();
    // ...
}
```

此时，除了默认属性之外，`priceList`对象还包含来自`COFFEES`表的`COF_NAME`和`PRICE`列中的数据以及有关这两列的元数据。

**将 WebRowSet 对象写入 XML 以及从 XML 读取 WebRowSet 对象**

要将`WebRowSet`对象编写为XML文档，请调用`writeXml`方法。要将XML文档的内容读入`WebRowSet`对象，请调用方法`readXml`。这两种方法都在后台完成它们的工作，这意味着除了结果之外的所有内容对您来说都是不可见的。

**使用 writeXml 方法**

方法`writeXml`编写`WebRowSet`对象，该对象将其作为表示其当前状态的XML文档调用。它将此XML文档写入您传递给它的流。流可以是`OutputStream`对象，例如`FileOutputStream`对象，或`Writer`对象，例如`FileWriter`对象。如果你传递给`writeXml`方法一个`OutputStream`对象，你将以字节为单位写入，它可以处理所有类型的数据；如果你传递一个`Writer`对象，你将用字符写入。下面的代码演示了将`WebRowSet`对象`priceList`作为XML文档写入`FileOutputStream`对象`oStream`：

```java
java.io.FileOutputStream oStream =
    new java.io.FileOutputStream("priceList.xml");
priceList.writeXml(oStream);
```

下面的代码将表示`priceList`的XML文档写入`FileWriter`对象`writer`而不是`OutputStream`对象。`FileWriter`类是用于将字符写入文件的便捷类。

```java
java.io.FileWriter writer =
    new java.io.FileWriter("priceList.xml");
priceList.writeXml(writer);
```

方法`writeXml`的另外两个版本允许你在将`ResultSet`对象的内容填充到一个`WebRowSet`对象之前将其写入流。在下面的代码行中，方法`writeXml`将`ResultSet`对象`rs`的内容读入`priceList`对象，然后将`priceList`作为XML文档写入`FileOutputStream`对象`oStream`。

```java
priceList.writeXml(rs, oStream);
```

在下一行代码中，`writeXml`方法使用`rs`的内容填充`price List`，但它将XML文档写入`FileWriter`对象而不是`OutputStream`对象：

```java
priceList.writeXml(rs, writer);
```

**使用 readXml 方法**

方法`readXml`解析XML文档，以构造XML文档描述的`WebRowSet`对象。与`writeXml`方法类似，您可以传递给`readXml`一个`InputStream`对象或一个`Reader`对象，从中读取XML文档。

```java
java.io.FileInputStream iStream =
    new java.io.FileInputStream("priceList.xml");
priceList.readXml(iStream);

java.io.FileReader reader = new
    java.io.FileReader("priceList.xml");
priceList.readXml(reader);
```

请注意，您可以将XML描述读入新的`WebRowSet`对象或读取调用`writeXml`方法的同一个`WebRowSet`对象。在从总部向 Web 站点发送价目表信息的场景中，您将使用新的`WebRowSet`对象，如以下代码行所示：

```java
WebRowSet recipient = new WebRowSetImpl();
java.io.FileReader reader =
    new java.io.FileReader("priceList.xml");
recipient.readXml(reader);
```

**XML 文档中是什么？**

`RowSet`对象不仅仅是它们包含的数据。它们还具有有关其列的属性和元数据。因此，表示`WebRowSet`对象的XML文档除了其数据之外还包括该其他信息。此外，XML文档中的数据包括当前值和原始值。（回想一下，原始值是在最近的数据更改之前存在的值。这些值是检查数据库中相应值是否已更改所必需的，从而产生了应该持久保存值的冲突： 您放入`RowSet`对象的新值或其他人放入数据库的新值。）

WebRowSet XML Schema 本身就是一个XML文档，它定义了表示`WebRowSet`对象的XML文档将包含的内容以及它必须呈现的格式。写入者和读取者都使用此模式，因为它告诉写入者如何编写XML文档（表示`WebRowSet`对象）和读取者如何解析XML文档。因为实际的写入和读取是通过方法`writeXml`和`readXml`的实现在内部完成的，所以作为用户，您不需要了解 WebRowSet XML Schema 文档中的内容。

XML文档包含分层结构中的元素和子元素。以下是描述`WebRowSet`对象的XML文档中的三个主要元素：

- [属性](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#properties-webrowset)
- [元数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#metadata-webrowset)
- [数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#data-webrowset)

元素标签标示元素的开头和结尾。例如，`<properties>`标记表示 properties 元素的开头，而`</properties>`标记表示它的结束。`<map/>`标签是一种简写方式，表示 map 子元素（ properties 元素中的一个子元素）尚未赋值。以下示例XML文档使用间距和缩进来使其更易于阅读，但这些不在实际的XML文档中使用，其中间距并不意味着什么。

接下来的三节将向您展示在示例 [`WebRowSetSample.java`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 中创建的`WebRowSet` `priceList`对象包含的三个主要元素。

**属性**

在`priceList`对象上调用`writeXml`方法会产生一个描述`priceList`的XML文档。此XML文档的属性部分如下所示：

```xml
<properties>
  <command>
    select COF_NAME, PRICE from COFFEES
  </command>
  <concurrency>1008</concurrency>
  <datasource><null/></datasource>
  <escape-processing>true</escape-processing>
  <fetch-direction>1000</fetch-direction>
  <fetch-size>0</fetch-size>
  <isolation-level>2</isolation-level>
  <key-columns>
    <column>1</column>
  </key-columns>
  <map>
  </map>
  <max-field-size>0</max-field-size>
  <max-rows>0</max-rows>
  <query-timeout>0</query-timeout>
  <read-only>true</read-only>
  <rowset-type>
    ResultSet.TYPE_SCROLL_INSENSITIVE
  </rowset-type>
  <show-deleted>false</show-deleted>
  <table-name>COFFEES</table-name>
  <url>jdbc:mysql://localhost:3306/testdb</url>
  <sync-provider>
    <sync-provider-name>
      com.sun.rowset.providers.RIOptimisticProvider
    </sync-provider-name>
    <sync-provider-vendor>
      Sun Microsystems Inc.
    </sync-provider-vendor>
    <sync-provider-version>
      1.0
    </sync-provider-version>
    <sync-provider-grade>
      2
    </sync-provider-grade>
    <data-source-lock>1</data-source-lock>
  </sync-provider>
</properties>
```

请注意，某些属性没有任何价值。例如，`datasource`属性用`<datasource/>`标记表示，这是表示`<datasource> </datasource>`的简写方式。没有给出值，因为设置了`url`属性。建立的任何连接都将使用此 JDBC URL 完成，因此不需要设置`DataSource`对象。此外，未列出`username`和`password`属性，因为它们必须保密。

**元数据**

描述`WebRowSet`对象的XML文档的元数据部分包含有关该`WebRowSet`对象中的列的信息。下面显示了`WebRowSet`对象`priceList`的这个部分。因为`priceList`对象有两列，所以描述它的XML文档有两个`<column-definition>`元素。每个`<column-definition>`元素都有子元素，提供有关所描述列的信息。

```xml
<metadata>
  <column-count>2</column-count>
  <column-definition>
    <column-index>1</column-index>
    <auto-increment>false</auto-increment>
    <case-sensitive>false</case-sensitive>
    <currency>false</currency>
    <nullable>0</nullable>
    <signed>false</signed>
    <searchable>true</searchable>
    <column-display-size>
      32
    </column-display-size>
    <column-label>COF_NAME</column-label>
    <column-name>COF_NAME</column-name>
    <schema-name></schema-name>
    <column-precision>32</column-precision>
    <column-scale>0</column-scale>
    <table-name>coffees</table-name>
    <catalog-name>testdb</catalog-name>
    <column-type>12</column-type>
    <column-type-name>
      VARCHAR
    </column-type-name>
  </column-definition>
  <column-definition>
    <column-index>2</column-index>
    <auto-increment>false</auto-increment>
    <case-sensitive>true</case-sensitive>
    <currency>false</currency>
    <nullable>0</nullable>
    <signed>true</signed>
    <searchable>true</searchable>
    <column-display-size>
      12
    </column-display-size>
    <column-label>PRICE</column-label>
    <column-name>PRICE</column-name>
    <schema-name></schema-name>
    <column-precision>10</column-precision>
    <column-scale>2</column-scale>
    <table-name>coffees</table-name>
    <catalog-name>testdb</catalog-name>
    <column-type>3</column-type>
    <column-type-name>
      DECIMAL
    </column-type-name>
  </column-definition>
</metadata>
```

从此元数据部分，您可以看到每行中有两列。第一列是`COF_NAME`，它包含类型为`VARCHAR`的值。第二列是`PRICE`，它包含`REAL`类型的值，依此类推。请注意，列类型是数据源中使用的数据类型，而不是Java编程语言中的类型。要获取或更新`COF_NAME`列中的值，可以使用`getString`或`updateString`方法，并且驱动程序会像往常那样转换为`VARCHAR`类型。

**数据**

数据部分给出了`WebRowSet`对象的每一行中每列的值。如果已填充`priceList`对象并且未对其进行任何更改，则XML文档的数据元素将如下所示。在下一节中，您将看到在修改`priceList`对象中的数据时XML文档如何更改。

对于每一行，都有一个`<currentRow>`元素，因为`priceList`有两列，每个`<currentRow>`元素包含两个`<columnValue>`元素。

```xml
<data>
  <currentRow>
    <columnValue>Colombian</columnValue>
    <columnValue>7.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>
      Colombian_Decaf
    </columnValue>
    <columnValue>8.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>Espresso</columnValue>
    <columnValue>9.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>French_Roast</columnValue>
    <columnValue>8.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>French_Roast_Decaf</columnValue>
    <columnValue>9.99</columnValue>
  </currentRow>
</data>
```

**修改 WebRowSet 对象**

您对`WebRowSet`对象进行更改的方式与对`CachedRowSet`对象的更改方式相同。然而，与`CachedRowSet`对象不同，`WebRowSet`对象跟踪更新，插入和删除，以便`writeXml`方法可以写入当前值和原始值。接下来的三个部分演示了对数据的更改，并显示了每次更改后描述`WebRowSet`对象的XML文档的样子。您不必对XML文档做任何事情; 对它的任何更改都是自动进行的，就像编写和读取XML文档一样。

**插入行**

如果 Coffee Break 连锁店的所有者想要在价目表中添加新咖啡，则代码可能如下所示：

```java
priceList.absolute(3);
priceList.moveToInsertRow();
priceList.updateString(COF_NAME, "Kona");
priceList.updateFloat(PRICE, 8.99f);
priceList.insertRow();
priceList.moveToCurrentRow();
```

在参考实现中，紧接在当前行之后进行插入。在前面的代码片段中，当前行是第三行，因此新行将在第三行之后添加并成为新的第四行。为了反映这种插入，XML文档将在`<data>`元素中的第三个`<currentRow>`元素之后添加以下`<insertRow>`元素。

`<insertRow>`元素将类似于以下内容。

```java
<insertRow>
  <columnValue>Kona</columnValue>
  <columnValue>8.99</columnValue>
</insertRow>
```

**删除行**

店主认为`Espresso`销售不足，应该从出售的咖啡中删除。因此，所有者想要从价目表中删除`Espresso`。`Espresso`位于`priceList`object的第三行，因此以下代码行将其删除：

```java
priceList.absolute(3); priceList.deleteRow();
```

以下`<deleteRow>`元素将出现在XML文档的数据部分的第二行之后，表示第三行已被删除。

```xml
<deleteRow>
  <columnValue>Espresso</columnValue>
  <columnValue>9.99</columnValue>
</deleteRow>
```

**修改行**

店主进一步认为哥伦比亚咖啡的价格过于昂贵，并希望将其降低至每磅6.99美元。以下代码将哥伦比亚咖啡的新价格设定为每磅6.99美元，这是第一行的价格：

```java
priceList.first();
priceList.updateFloat(PRICE, 6.99);
```

XML文档将在提供新值的`<updateRow>`元素中反映此更改。第一列的值没有改变，因此只有第二列的`<updateValue>`元素：

```xml
<currentRow>
  <columnValue>Colombian</columnValue>
  <columnValue>7.99</columnValue>
  <updateRow>6.99</updateRow>
</currentRow>
```

此时，通过插入行，删除行以及修改行，`priceList`对象的XML文档如下所示：

```xml
<data>
  <insertRow>
    <columnValue>Kona</columnValue>
    <columnValue>8.99</columnValue>
  </insertRow>
  <currentRow>
    <columnValue>Colombian</columnValue>
    <columnValue>7.99</columnValue>
    <updateRow>6.99</updateRow>
  </currentRow>
  <currentRow>
    <columnValue>
      Colombian_Decaf
    </columnValue>
    <columnValue>8.99</columnValue>
  </currentRow>
  <deleteRow>
    <columnValue>Espresso</columnValue>
    <columnValue>9.99</columnValue>
  </deleteRow>
  <currentRow>
    <columnValue>French_Roast</columnValue>
    <columnValue>8.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>
      French_Roast_Decaf
    </columnValue>
    <columnValue>9.99</columnValue>
  </currentRow>
</data>
```

**WebRowSet 代码示例**

示例 `WebRowSetSample.java` 演示了此页面上描述的所有功能。

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

### 使用大对象

`Blob`，`Clob`和`NClob` Java对象的一个重要特性是，您可以操作它们，而无需将所有数据从数据库服务器带到客户端计算机。某些实现表示这些类型的实例，其中包含实例所代表的数据库中对象的定位符（逻辑指针）。因为`BLOB`，`CLOB`或`NCLOB` SQL对象可能非常大，所以使用定位器可以显着提高性能。但是，其他实现完全实现了客户端计算机上的大对象。

如果要将`BLOB`，`CLOB`或`NCLOB`SQL值的数据带到客户端计算机，请使用为此目的提供的`Blob`，`Clob`和`NClob`Java接口中的方法。这些大对象类型对象将它们表示的对象的数据实现为流。

本章节涵盖以下主题：

- [添加大对象类型对象到数据库](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html#add_lob)
- [查询 CLOB 值](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html#retrieve_clob)
- [添加和查询 BLOB 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html#add_retrieve_blob)
- [释放大对象持有的资源](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html#release_large_objects)

**添加大对象类型对象到数据库**

以下来自`ClobSample.addRowToCoffeeDescriptions`的摘录将`CLOB`SQL值添加到表`COFFEE_DESCRIPTIONS`中。`Clob` Java对象`myClob`包含`fileName`指定的文件的内容。

```java
public void addRowToCoffeeDescriptions(
    String coffeeName, String fileName)
    throws SQLException {

    PreparedStatement pstmt = null;
    try {
        Clob myClob = this.con.createClob();
        Writer clobWriter = myClob.setCharacterStream(1);
        String str = this.readFile(fileName, clobWriter);
        System.out.println("Wrote the following: " +
            clobWriter.toString());

        if (this.settings.dbms.equals("mysql")) {
            System.out.println(
                "MySQL, setting String in Clob " +
                "object with setString method");
            myClob.setString(1, str);
        }
        System.out.println("Length of Clob: " + myClob.length());

        String sql = "INSERT INTO COFFEE_DESCRIPTIONS " +
                     "VALUES(?,?)";

        pstmt = this.con.prepareStatement(sql);
        pstmt.setString(1, coffeeName);
        pstmt.setClob(2, myClob);
        pstmt.executeUpdate();
    } catch (SQLException sqlex) {
        JDBCTutorialUtilities.printSQLException(sqlex);
    } catch (Exception ex) {
      System.out.println("Unexpected exception: " + ex.toString());
    } finally {
        if (pstmt != null)pstmt.close();
    }
}
```

以下行创建一个`Clob` Java对象：

```java
Clob myClob = this.con.createClob();
```

以下代码行检索一个流（在本例中是一个名为`clobWriter`的`Writer`对象），用于将字符流写入`Clob` Java对象`myClob`。方法`ClobSample.readFile`写入这个字符流；流来自`String` `fileName`指定的文件。方法参数`1`表示`Writer`对象将开始在`Clob`值的开头写入字符流：

```java
Writer clobWriter = myClob.setCharacterStream(1);
```

`ClobSample.readFile`方法逐行读取文件`fileName`指定的文件，并将其写入`writerArg`指定的`Writer`对象：

```java
private String readFile(String fileName, Writer writerArg)
        throws FileNotFoundException, IOException {

    BufferedReader br = new BufferedReader(new FileReader(fileName));
    String nextLine = "";
    StringBuffer sb = new StringBuffer();
    while ((nextLine = br.readLine()) != null) {
        System.out.println("Writing: " + nextLine);
        writerArg.write(nextLine);
        sb.append(nextLine);
    }
    // Convert the content into to a string
    String clobData = sb.toString();

    // Return the data.
    return clobData;
}
```

以下摘录创建了一个`PreparedStatement`对象`pstmt`，它将`Clob` Java对象`myClob`插入到`COFFEE_DESCRIPTIONS`中：

```java
PreparedStatement pstmt = null;
// ...
String sql = "INSERT INTO COFFEE_DESCRIPTIONS VALUES(?,?)";
pstmt = this.con.prepareStatement(sql);
pstmt.setString(1, coffeeName);
pstmt.setClob(2, myClob);
pstmt.executeUpdate();
```

**查询 CLOB 值**

方法`ClobSample.retrieveExcerpt`从列值`COF_NAME`等于`coffeeName`参数指定的`String`值的行中检索存储在`COFFEE_DESCRIPTIONS`的`COF_DESC`列中的`CLOB` SQL值：

```java
public String retrieveExcerpt(String coffeeName, int numChar)
    throws SQLException {

    String description = null;
    Clob myClob = null;
    PreparedStatement pstmt = null;

    try {
        String sql =
            "select COF_DESC " +
            "from COFFEE_DESCRIPTIONS " +
            "where COF_NAME = ?";

        pstmt = this.con.prepareStatement(sql);
        pstmt.setString(1, coffeeName);
        ResultSet rs = pstmt.executeQuery();

        if (rs.next()) {
            myClob = rs.getClob(1);
            System.out.println("Length of retrieved Clob: " +
                myClob.length());
        }
        description = myClob.getSubString(1, numChar);
    } catch (SQLException sqlex) {
        JDBCTutorialUtilities.printSQLException(sqlex);
    } catch (Exception ex) {
        System.out.println("Unexpected exception: " + ex.toString());
    } finally {
        if (pstmt != null) pstmt.close();
    }
    return description;
}
```

以下行从`ResultSet`对象`rs`中检索`Clob` Java值：

```java
myClob = rs.getClob(1);
```

以下行从`myClob`对象中检索子字符串。子字符串从`myClob`值的第一个字符开始，最多包含`numChar`中指定的个数的连续字符数，其中`numChar`是一个整数。

```java
description = myClob.getSubString(1, numChar);
```

**添加和查询 BLOB 对象**

添加和检索`BLOB` SQL对象类似于添加和检索`CLOB` SQL对象。使用`Blob.setBinaryStream`方法检索`OutputStream`对象，以编写`Blob` Java对象（调用该方法使用的对象）表示的`BLOB` SQL值。

**释放大对象持有的资源**

`Blob`，`Clob`和`NClob` Java对象至少在创建它们的事务期间保持有效。这可能导致应用程序在长时间运行的事务期间耗尽资源。应用程序可以通过调用`free`方法释放`Blob`，`Clob`和`NClob`资源。

在下面的代码片段中，调用方法`Clob.free`来释放为先前创建的`Clob`对象保存的资源：

```java
Clob aClob = con.createClob();
int numWritten = aClob.setString(1, val);
aClob.free();
```

### 使用 SQLXML 对象

`Connection`接口使用`createSQLXML`方法为创建`SQLXML`对象提供支持。创建的对象不包含任何数据。可以通过在`SQLXML`接口上调用`setString`，`setBinaryStream`，`setCharacterStream`或`setResult`方法将数据添加到对象中。

本章节涵盖以下主题：

- [创建 SQLXML 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#creating_sqlxml)
- [在 ResultSet 中查询 SQLXML 值](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#retrieving_sqlxml)
- [访问 SQLXML 对象数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#accessing_sqlxml)
- [存储 SQLXML 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#storing_sqlxml)
- [初始化 SQLXML 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#initializing_sqlxml)
- [释放 SQLXML 资源](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#releasing_sqlxml)
- [示例代码](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#sample_code)

**创建 SQLXML 对象**

在下面的代码摘录中，方法`Connection.createSQLXML`用于创建一个空的`SQLXML`对象。`SQLXML.setString`方法用于将数据写入创建的`SQLXML`对象。

```java
Connection con = DriverManager.getConnection(url, props);
SQLXML xmlVal = con.createSQLXML();
xmlVal.setString(val);
```

**在 ResultSet 中查询 SQLXML 值**

`SQLXML`数据类型的处理方式与更原始的内置类型相似。可以通过调用`ResultSet`或`CallableStatement`接口中的`getSQLXML`方法来检索`SQLXML`值。

例如，以下代码摘录从`ResultSet` *rs*的第一列检索`SQLXML`值：

```java
SQLXML xmlVar = rs.getSQLXML(1);
```

`SQLXML`对象至少在创建它们的事务期间保持有效，除非调用它们的`free`方法。

**访问 SQLXML 对象数据**

`SQLXML`接口提供`getString`，`getBinaryStream`，`getCharacterStream`和`getSource`方法来访问其内部内容。以下代码摘录使用`getString`方法检索`SQLXML`对象的内容：

```java
SQLXML xmlVal= rs.getSQLXML(1);
String val = xmlVal.getString();
```

`getBinaryStream`或`getCharacterStream`方法可用于获取可以直接传递给XML解析器的`InputStream`或`Reader`对象。以下代码摘录从`SQLXML`对象获取`InputStream`对象，然后使用DOM（文档对象模型）解析器处理流：

```java
SQLXML sqlxml = rs.getSQLXML(column);
InputStream binaryStream = sqlxml.getBinaryStream();
DocumentBuilder parser = 
    DocumentBuilderFactory.newInstance().newDocumentBuilder();
Document result = parser.parse(binaryStream);
```

`getSource`方法返回一个`javax.xml.transform.Source`对象。源用作XML解析器和XSLT转换器的输入。

以下摘录使用通过调用`getSource`方法返回的`SAXSource`对象从`SQLXML`对象检索和解析数据：

```java
SQLXML xmlVal= rs.getSQLXML(1);
SAXSource saxSource = sqlxml.getSource(SAXSource.class);
XMLReader xmlReader = saxSource.getXMLReader();
xmlReader.setContentHandler(myHandler);
xmlReader.parse(saxSource.getInputSource());
```

**存储 SQLXML 对象**

与其他数据类型一样，`SQLXML`对象可以作为输入参数传递给`PreparedStatement`对象。方法`setSQLXML`用`SQLXML`对象设置指定的`PreparedStatement`参数。

在下面的摘录中，`authorData`是`java.sql.SQLXML`接口的一个实例，其数据先前已初始化。

```java
PreparedStatement pstmt = conn.prepareStatement("INSERT INTO bio " +
                              "(xmlData, authId) VALUES (?, ?)");
pstmt.setSQLXML(1, authorData);
pstmt.setInt(2, authorId);
```

`updateSQLXML`方法可用于更新可更新结果集中的列值。

如果在调用`setSQLXML`或`updateSQLXML`之前，`SQLXML`对象的`java.xml.transform.Result`，`Writer`或`OutputStream`对象尚未关闭，则抛出`SQLException`。

**初始化 SQLXML 对象**

`SQLXML`接口提供方法`setString`，`setBinaryStream`，`setCharacterStream`或`setResult`来初始化通过调用`Connection.createSQLXML`方法创建的`SQLXML`对象的内容。

以下摘录使用方法`setResult`返回一个`SAXResult`对象来填充新创建的`SQLXML`对象：

```java
SQLXML sqlxml = con.createSQLXML();
SAXResult saxResult = sqlxml.setResult(SAXResult.class);
ContentHandler contentHandler = saxResult.getXMLReader().getContentHandler();
contentHandler.startDocument();
    
// set the XML elements and
// attributes into the result
contentHandler.endDocument();
```

以下摘录使用`setCharacterStream`方法获取`java.io.Writer`对象以初始化`SQLXML`对象：

```java
SQLXML sqlxml = con.createSQLXML();
Writer out= sqlxml.setCharacterStream();
BufferedReader in = new BufferedReader(new FileReader("xml/foo.xml"));
String line = null;
while((line = in.readLine() != null) {
    out.write(line);
}
```

类似地，`SQLXML` `setString`方法可用于初始化`SQLXML`对象。

如果尝试在先前已初始化的`SQLXML`对象上调用`setString`，`setBinaryStream`，`setCharacterStream`和`setResult`方法，则将抛出`SQLException`。如果对同一个`SQLXML`对象发生多次调用方法`setBinaryStream`，`setCharacterStream`和`setResult`，则抛出一个`SQLException`并返回先前返回的`javax.xml.transform.Result`，` Writer`或`OutputStream`对象不受影响。

**释放 SQLXML 资源**

`SQLXML`对象至少在创建它们的事务期间保持有效。这可能导致应用程序在长时间运行的事务期间耗尽资源。应用程序可以通过调用`free`方法释放`SQLXML`资源。

在下面的摘录中，调用`方法SQLXML.free`来释放为先前创建的`SQLXML`对象保存的资源。

```java
SQLXML xmlVar = con.createSQLXML();
xmlVar.setString(val);
xmlVar.free();
```

**示例代码**

MySQL和Java DB及其各自的JDBC驱动程序不完全支持本节所述的`SQLXML` JDBC数据类型。但是，示例`RSSFeedsTable`演示了如何使用MySQL和Java DB处理XML数据。

The Coffee Break的老板关注来自各种网站的多个RSS源，其中包括餐馆和饮料行业的新闻。RSS（Really Simple Syndication或Rich Site Summary）源是一个XML文档，其中包含一系列文章和相关元数据，例如每篇文章的发布日期和作者。老板希望将这些RSS提要存储到数据库表中，包括来自The Coffee Break博客的RSS提要。

文件`rss-the-coffee-break-blog.xml`是来自The Coffee Break博客的示例RSS源。

**在MySQL中使用XML数据**

示例`RSSFeedsTable`将RSS提要存储在表`RSS_FEEDS`中，该表是使用以下命令创建的：

```sql
create table RSS_FEEDS
    (RSS_NAME varchar(32) NOT NULL,
    RSS_FEED_XML longtext NOT NULL,
    PRIMARY KEY (RSS_NAME));
```

MySQL不支持XML数据类型。相反，此示例将XML数据存储在类型为`LONGTEXT`的列中，该列是`CLOB`SQL数据类型。MySQL有四种`CLOB`数据类型；`LONGTEXT`数据类型在四个中保存最多的字符。

方法`RSSFeedsTable.addRSSFeed`将RSS提要添加到`RSS_FEEDS`表。此方法的第一个语句将RSS提要（由此示例中的XML文件表示）转换为类型为`org.w3c.dom.Document`的对象，该对象表示DOM（文档对象模型）文档。该类以及包`javax.xml`中包含的类和接口包含使您能够操作XML数据内容的方法。例如，以下语句使用 XPath 表达式从`Document`对象检索RSS提要的标题：

```java
Node titleElement =
    (Node)xPath.evaluate("/rss/channel/title[1]",
        doc, XPathConstants.NODE);
```

XPath表达式`/rss/channel/title[1]`检索第一个`<title>`元素的内容。对于文件`rss-the-coffee-break-blog.xml`，这是字符串`The Coffee Break Blog`。

以下语句将RSS提要添加到表`RSS_FEEDS`：

```java
// For databases that support the SQLXML
// data type, this creates a
// SQLXML object from
// org.w3c.dom.Document.

System.out.println("Adding XML file " + fileName);
String insertRowQuery =
    "insert into RSS_FEEDS " +
    "(RSS_NAME, RSS_FEED_XML) values " +
    "(?, ?)";
insertRow = con.prepareStatement(insertRowQuery);
insertRow.setString(1, titleString);

System.out.println("Creating SQLXML object with MySQL");
rssData = con.createSQLXML();
System.out.println("Creating DOMResult object");
DOMResult dom = (DOMResult)rssData.setResult(DOMResult.class);
dom.setNode(doc);

insertRow.setSQLXML(2, rssData);
System.out.println("Running executeUpdate()");
insertRow.executeUpdate();
```

`RSSFeedsTable.viewTable`方法检索`RSS_FEEDS`的内容。对于每一行，该方法创建一个名为`doc`的类型为`org.w3c.dom.Document`的对象，其中将XML内容存储在列`RSS_FEED_XML`中。该方法检索XML内容并将其存储在名为`rssFeedXML`的`SQLXML`类型的对象中。`rssFeedXML`的内容被解析并存储在`doc`对象中。

**在Java DB中使用XML数据**

**注意**：有关在Java DB中使用XML数据的更多信息，请参阅 [*Java DB Developer's Guide*](http://docs.oracle.com/javadb/index_jdk8.html) 中的“XML数据类型和运算符”部分。

示例`RSSFeedsTable`将RSS提要存储在表`RSS_FEEDS`中，该表是使用以下命令创建的：

```sql
create table RSS_FEEDS
    (RSS_NAME varchar(32) NOT NULL,
    RSS_FEED_XML xml NOT NULL,
    PRIMARY KEY (RSS_NAME));
```

Java DB支持XML数据类型，但它不支持`SQLXML` JDBC数据类型。因此，您必须将任何XML数据转换为字符格式，然后使用Java DB运算符`XMLPARSE`将其转换为XML数据类型。

`RSSFeedsTable.addRSSFeed`方法将RSS提要添加到`RSS_FEEDS`表。此方法的第一个语句将RSS提要（由此示例中的XML文件表示）转换为`org.w3c.dom.Document`类型的对象。这在 [使用MySQL中的XML数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#working-with-xml-data-in-mysql) 中进行了描述。

`RSSFeedsTable.addRSSFeed`方法使用方法`JDBCTutorialUtilities.convertDocumentToString`将RSS提要转换为`String`对象。

Java DB有一个名为`XMLPARSE`的运算符，它将字符串表示形式解析为Java DB XML值，如以下摘录所示：

```java
String insertRowQuery =
    "insert into RSS_FEEDS " +
    "(RSS_NAME, RSS_FEED_XML) values " +
    "(?, xmlparse(document cast " +
    "(? as clob) preserve whitespace))";
```

`XMLPARSE`运算符要求您将XML文档的字符表示转换为Java DB识别的字符串数据类型。在此示例中，它将其转换为`CLOB`数据类型。有关Apache Xalan和Java DB要求的更多信息，请参见 [入门](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 和Java DB文档。

方法`RSSFeedsTable.viewTable`检索`RSS_FEEDS`的内容。由于Java DB不支持JDBC数据类型`SQLXML`，因此必须将XML内容检索为字符串。Java DB有一个名为`XMLSERIALIZE`的运算符，它将XML类型转换为字符类型：

```java
String query =
    "select RSS_NAME, " +
    "xmlserialize " +
    "(RSS_FEED_XML as clob) " +
    "from RSS_FEEDS";
```

与`XMLPARSE`运算符一样，`XMLSERIALIZE`运算符要求Apache Xalan列在Java类路径中。

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

### 使用自定义类型映射

**注意：**MySQL目前不支持用户定义的类型。MySQL和Java DB目前不支持结构化类型或`DISTINCT` SQL数据类型。 没有JDBC教程示例可用于演示本节中描述的功能。

随着业务的蓬勃发展，The Coffee Break 的店主定期添加新商店并对数据库进行更改。店主已决定对结构化类型`ADDRESS`使用自定义映射。这使店主能够对映射`ADDRESS`类型的Java类进行更改。Java类将为`ADDRESS`的每个属性提供一个字段。类的名称及其字段的名称可以是任何有效的Java标识符。

本章节涵盖以下主题：

- [实现 SQLData](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlcustommapping.html#implementing_sqldata)
- [使用连接的类型映射](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlcustommapping.html#using_connection_type_map)
- [使用你自己的类型映射](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlcustommapping.html#using_your_own_type_map)

**实现 SQLData**

自定义映射所需的第一件事是创建一个实现接口`SQLData`的类。

结构化类型`ADDRESS`的SQL定义如下所示：

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

为`ADDRESS`类型的自定义映射实现`SQLData`接口的类可能如下所示：

```java
public class Address implements SQLData {
    public int num;
    public String street;
    public String city;
    public String state;
    public String zip;
    private String sql_type;
    
    public String getSQLTypeName() {
        return sql_type;
    }

    public void readSQL(SQLInput stream, String type)
        throws SQLException {
        sql_type = type;
        num = stream.readInt();
        street = stream.readString();
        city = stream.readString();
        state = stream.readString();
        zip = stream.readString();
    }

    public void writeSQL(SQLOutput stream)
        throws SQLException {
        stream.writeInt(num);
        stream.writeString(street);
        stream.writeString(city);
        stream.writeString(state);
        stream.writeString(zip);
    }
}
```

**使用连接的类型映射**

在编写实现接口`SQLData`的类之后，设置自定义映射所需要做的唯一事情就是在类型映射中创建一个条目。例如，这意味着输入`ADDRESS`类型的完全限定SQL名称和类`Address`的`Class`对象。类型映射（`java.util.Map`接口的实例）在创建时与每个新连接相关联，因此您可以使用该连接。假设`con`是活动连接，以下代码片段将UDT `ADDRESS`的条目添加到与`con`关联的类型映射。

```java
java.util.Map map = con.getTypeMap();
map.put("SchemaName.ADDRESS", Class.forName("Address"));
con.setTypeMap(map);
```

每当您调用`getObject`方法以检索`ADDRESS`类型的实例时，驱动程序将检查与该连接关联的类型映射，并查看它是否具有`ADDRESS`的条目。驱动程序将记录`Address`类的`Class`对象，创建它的实例，并在后台执行许多其他操作以将`ADDRESS`映射到`Address`。除了为映射生成类之外，您不必执行任何操作，然后在类型映射中创建条目以使驱动程序知道存在自定义映射。驱动程序将完成剩下的工作。

存储具有自定义映射的结构化类型的情况类似。当您调用方法`setObject`时，驱动程序将检查要设置的值是否是实现接口`SQLData`的类的实例。如果是（意味着存在自定义映射），则驱动程序将使用自定义映射将值转换为SQL对应项，然后再将其返回到数据库。同样，驱动程序在幕后进行自定义映射；您需要做的就是为方法`setObject`提供一个具有自定义映射的参数。您将在本节后面看到此示例。

查看使用标准映射，`Struct`对象和自定义映射（Java编程语言中的类）之间的区别。以下代码片段显示了到`Struct`对象的标准映射，这是驱动程序在连接的类型映射中没有条目时使用的映射。

```java
ResultSet rs = stmt.executeQuery(
    "SELECT LOCATION " +
    "WHERE STORE_NO = 100003");
rs.next();
Struct address = (Struct)rs.getObject("LOCATION");
```

变量地址包含以下属性值：`4344`，`"First_Street"`，`"Verona"`，`"CA"`，`"94545"`。

以下代码片段显示了在连接的类型映射中存在结构化类型`ADDRESS`的条目时会发生什么。请记住，列`LOCATION`存储`ADDRESS`类型的值。

```java
ResultSet rs = stmt.executeQuery(
    "SELECT LOCATION " +
    "WHERE STORE_NO = 100003");
rs.next();
Address store_3 = (Address)rs.getObject("LOCATION");
```

变量`store_3`现在是`Address`类的实例，每个属性值都是`Address`的一个字段的当前值。请注意，在将其分配给`store_3`之前，必须记住将`getObject`方法检索的对象转换为`Address`对象。另请注意，`store_3`必须是`Address`对象。

比较使用`Struct`对象来处理`Address`类的实例。假设商店移动到邻近城镇的更好位置，因此您必须更新数据库。使用自定义映射，重置`store_3`的字段，如以下代码片段所示：

```java
ResultSet rs = stmt.executeQuery(
    "SELECT LOCATION " +
    "WHERE STORE_NO = 100003");
rs.next();
Address store_3 = (Address)rs.getObject("LOCATION");
store_3.num = 1800;
store_3.street = "Artsy_Alley";
store_3.city = "Arden";
store_3.state = "CA";
store_3.zip = "94546";
PreparedStatement pstmt = con.prepareStatement(
    "UPDATE STORES " +
    "SET LOCATION = ? " +
    "WHERE STORE_NO = 100003");
pstmt.setObject(1, store_3);
pstmt.executeUpdate();
```

`LOCATION`列中的值是`ADDRESS`类型的实例。驱动程序检查连接的类型映射，并发现有一个条目将`ADDRESS`与类`Address`相关联，因此使用`Address`中指示的自定义映射。当代码使用变量`store_3`作为第二个参数调用方法`setObject`时，驱动程序检查并看到`store_3`表示类`Address`的实例，它实现了结构化类型`ADDRESS`的接口`SQLData`，并再次自动使用自定义映射。

如果没有`ADDRESS`的自定义映射，则更新看起来更像是：

```java
PreparedStatement pstmt = con.prepareStatement(
    "UPDATE STORES " +
    "SET LOCATION.NUM = 1800, " +
    "LOCATION.STREET = 'Artsy_Alley', " + 
    "LOCATION.CITY = 'Arden', " +
    "LOCATION.STATE = 'CA', " +
    "LOCATION.ZIP = '94546' " +
    "WHERE STORE_NO = 100003");
pstmt.executeUpdate;
```

**使用你自己的类型映射**

到目前为止，您仅使用与连接关联的类型映射进行自定义映射。通常，这是大多数程序员将使用的唯一类型映射。但是，也可以创建类型映射并将其传递给某些方法，以便驱动程序将使用该类型映射而不是与连接关联的映射。这允许两个不同的映射用于相同的用户定义类型（UDT）。实际上，只要每个映射都使用实现`SQLData`接口的类和类型映射中的条目设置，就可以为同一个UDT创建多个自定义映射。如果未将类型映射传递给可接受类型映射的方法，则驱动程序将默认使用与该连接关联的类型映射。

很少有情况要求使用除与连接关联的类型映射之外的类型映射。例如，如果在JDBC应用程序上工作的几个程序员将​​其组件组合在一起并使用相同的连接，则可能需要提供带有类型映射的方法。如果两个或多个程序员为同一个SQL UDT创建了自己的自定义映射，则每个程序员都需要提供他自己的类型映射，从而覆盖连接的类型映射。

### 使用 Datalink 对象

`DATALINK`值通过URL引用基础数据源外部的资源。URL，统一资源定位符，是指向万维网上的资源的指针。资源可以是文件或目录这样简单的东西，也可以是对更复杂的对象的引用，例如对数据库或搜索引擎的查询。

本章节涵盖以下主题：

- [存储外部数据的引用](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatalink.html#storing_datalink)
- [检索外部数据的引用](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatalink.html#retrieving_datalink)

**存储外部数据的引用**

使用`PreparedStatement.setURL`方法将`java.net.URL`对象指定为预准备语句。如果Java平台不支持所设置的URL类型，请使用`setString`方法存储URL。

例如，假设 The Coffee Break 的所有者想要在数据库表中存储重要URL列表。以下示例`DatalinkSample.addURLRow`将一行数据添加到表`DATA_REPOSITORY`。该行包含一个标识URL的字符串，`DOCUMENT_NAME`和URL本身，`URL`：

```java
public void addURLRow(String description, String url)
    throws SQLException {

    PreparedStatement pstmt = null;

    try {
        pstmt = this.con.prepareStatement(
            "INSERT INTO data_repository" +
            "(document_name,url) VALUES (?,?)");

        pstmt.setString(1, description);
        pstmt.setURL(2,new URL(url));
        pstmt.execute();
    } catch (SQLException sqlex) {
        JDBCTutorialUtilities.printSQLException(sqlex);
    } catch (Exception ex) {
        System.out.println("Unexpected exception");
        ex.printStackTrace();
    } finally {
        if (pstmt != null) {
            pstmt.close();
        }
    }
}
```

**检索外部数据引用**

使用`ResultSet.getURL`方法将对外部数据的引用检索为`java.net.URL`对象。如果Java平台不支持方法`getObject`或`getURL`返回的URL类型，则通过调用方法`getString`将URL检索为`String`对象。

以下示例`DatalinkSample.viewTable`显示存储在表`DATA_REPOSITORY`中的所有URL的内容：

```java
public static void viewTable(Connection con, Proxy proxy)
    throws SQLException, IOException {

    Statement stmt = null;
    String query =
      "SELECT document_name, url " +
      "FROM data_repository";

    try {
        stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery(query);

        if ( rs.next() )  {
            String documentName = null;
            java.net.URL url = null;

            documentName = rs.getString(1);

            // Retrieve the value as a URL object.
            url = rs.getURL(2);

            if (url != null) {

                // Retrieve the contents
                // from the URL
          
                URLConnection myURLConnection =
                    url.openConnection(proxy);
                BufferedReader bReader =
                    new BufferedReader(
                        new InputStreamReader(
                            myURLConnection.
                                getInputStream()));

                System.out.println("Document name: " + documentName);

                String pageContent = null;

                while ((pageContent = bReader.readLine()) != null ) {
                    // Print the URL contents
                    System.out.println(pageContent);
                }
            } else {
                System.out.println("URL is null");
            }
        }
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } catch(IOException ioEx) {
        System.out.println("IOException caught: " + ioEx.toString());
    } catch (Exception ex) {
        System.out.println("Unexpected exception");
        ex.printStackTrace();
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

示例`DatalinkSample`将Oracle URL http://www.oracle.com 存储在表`DATA_REPOSITORY`中。之后，它显示存储在`DATA_REPOSITORY`中的URL引用的所有文档的内容，其中包括Oracle主页 http://www.oracle.com 。

该示例使用以下语句从结果集中检索URL作为`java.net.URL`对象：

```java
url = rs.getURL(2);
```

该示例使用以下语句访问URL对象引用的数据：

```java
URLConnection myURLConnection = url.openConnection(proxy);
BufferedReader bReader = new BufferedReader(
    new InputStreamReader(
        myURLConnection.getInputStream()));

System.out.println("Document name: " + documentName);

String pageContent = null;

while ((pageContent = bReader.readLine()) != null ) {
    // Print the URL contents
    System.out.println(pageContent);
}
```

`URLConnection.openConnection`方法不带参数，这意味着`URLConnection`表示与 Internet 的直接连接。如果需要代理服务器连接到 Internet，则`openConnection`方法接受`java.net.Proxy`对象作为参数。以下语句演示了如何使用服务器名称`www-proxy.example.com`和端口号`80`创建 HTTP 代理：

```
Proxy myProxy;
InetSocketAddress myProxyServer;
myProxyServer = new InetSocketAddress("www-proxy.example.com", 80);
myProxy = new Proxy(Proxy.Type.HTTP, myProxyServer);
```

### 使用 RowId 对象

**注意：**MySQL和Java DB当前不支持`RowId` JDBC接口。因此，没有JDBC教程示例可用于演示本节中描述的功能。

`RowId`对象表示数据库表中行的地址。但请注意，`ROWID`类型不是标准SQL类型。`ROWID`值非常有用，因为它们通常是访问单行的最快方式，并且是表中行的唯一标识。但是，不应将`ROWID`值用作表的主键。例如，如果从表中删除特定行，则数据库可能会将其`ROWID`值重新分配给稍后插入的行。

本章节涵盖以下主题：

- [检索 RowId 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlrowid.html#retrieving_rowid_objects)
- [使用 RowId 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlrowid.html#using_rowid_objects)
- [RowId 的有效期](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlrowid.html#lifetime_rowid_validity)

**检索 RowId 对象**

通过调用接口`ResultSet`和`CallableStatement`中定义的`getter`方法来检索`java.sql.RowId`对象。返回的`RowId`对象是一个不可变对象，您可以将其用作后续引用作为行的唯一标识符。以下是调用`ResultSet.getRowId`方法的示例：

```java
java.sql.RowId rowId_1 = rs.getRowId(1);
```

**使用 RowId 对象**

您可以将`RowId`对象设置为参数化`PreparedStatement`对象中的参数：

```java
Connection conn = ds.getConnection(username, password);
PreparedStatement ps = conn.prepareStatement(
    "INSERT INTO BOOKLIST" +
    "(ID, AUTHOR, TITLE, ISBN) " +
    "VALUES (?, ?, ?, ?)");
ps.setRowId(1, rowId_1);
```

您还可以在可更新的`ResultSet`对象中更新具有特定`RowId`对象的列：

```java
ResultSet rs = ...
rs.next();
rs.updateRowId(1, rowId_1);
```

`RowId`对象值通常在数据源之间不可移植，并且在`PreparedStatement`和`ResultSet`对象中分别使用`set`或`update`方法时应被视为特定于数据源。因此，不建议从连接到一个数据源的`ResultSet`对象获取`RowId`对象，然后尝试在连接到不同的数据源的不相关的`ResultSet`对象中使用该`RowId`对象。

**RowId 的有效期**

只要未删除标识的行并且`RowId`对象的生存期在`RowId`的数据源指定的生存期的范围内，`RowId`对象就是有效的。

要确定数据库或数据源的`RowId`对象的生存期，请调用方法`DatabaseMetaData.getRowIdLifetime`。它返回`RowIdLifetime`枚举数据类型的值。以下方法`JDBCTutorialUtilities.rowIdLifeTime`返回`RowId`对象的生存期：

```java
public static void rowIdLifetime(Connection conn)
    throws SQLException {

    DatabaseMetaData dbMetaData = conn.getMetaData();
    RowIdLifetime lifetime = dbMetaData.getRowIdLifetime();

    switch (lifetime) {
        case ROWID_UNSUPPORTED:
            System.out.println("ROWID type not supported");
            break;

        case ROWID_VALID_FOREVER:
            System.out.println("ROWID has unlimited lifetime");
            break;

        case ROWID_VALID_OTHER:
            System.out.println("ROWID has indeterminate lifetime");
            break;

        case ROWID_VALID_SESSION:
            System.out.println(
                "ROWID type has lifetime that " +
                "is valid for at least the " +
                "containing session");
            break;

        case ROWID_VALID_TRANSACTION:
            System.out.println(
                "ROWID type has lifetime that " +
                "is valid for at least the " +
                "containing transaction");
            break;
    }
}
```

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

### 将JDBC与GUI API结合使用

示例`CoffeesFrame.java`演示了如何将JDBC与GUI API集成，特别是Swing API。它在表中显示`COFFEES`数据库表的内容，并包含允许您向表中添加行的字段和按钮。以下是此示例的屏幕截图：

![Screenshot of Sample CoffeeFrames.java](https://docs.oracle.com/javase/tutorial/figures/jdbc/coffeesframe.gif)

该示例包含五个文本字段，这些字段对应于`COFFEES`表中的每个列。它还包含三个按钮：

- **向表中添加行**：根据在文本字段中输入的数据向样本表中添加行。
- **更新数据库**：根据样本表中的数据更新表`COFFEES`。
- **放弃更改**：检索`COFFEES`表的内容，替换样本表中的现有数据。

此示例（需要`CoffeesTableModel`）演示了将JDBC与Swing API集成的以下常规步骤：

1. 实现`TableModel`接口
2. 实现`RowSetListener`接口
3. 布置Swing组件
4. 为示例中的按钮添加监听器

**实现 `javax.swing.event.TableModel` 接口**

`TableModel`接口使Java Swing应用程序能够管理`JTable`对象中的数据。示例`CoffeesTableModel.java`实现了此接口。它指定`JTable`对象应如何从`RowSet`对象检索数据并将其显示在表中。

**注意：**尽管此示例在Swing应用程序中显示`COFFEES`表的内容，但`CoffeesTableModel`类应适用于任何SQL表，前提是其数据可以使用String对象表示。（但是，必须为其他SQL表修改允许用户向`COFFEES`添加行的字段，这些字段在`CoffeesFrame`类中指定。）

在实现接口`TableModel`的方法之前，`CoffeeTableModel`类的构造函数初始化这些实现的方法所需的各种成员变量，如下所示：

```java
public CoffeesTableModel(CachedRowSet rowSetArg)
    throws SQLException {

    this.coffeesRowSet = rowSetArg;
    this.metadata = this.coffeesRowSet.getMetaData();
    numcols = metadata.getColumnCount();

    // Retrieve the number of rows.
    this.coffeesRowSet.beforeFirst();
    this.numrows = 0;
    while (this.coffeesRowSet.next()) {
        this.numrows++;
    }
    this.coffeesRowSet.beforeFirst();
}
```

下面描述了在此构造函数中初始化的成员变量：

- `CachedRowSet coffeesRowSet`：存储表`COFFEES`的内容。
  此示例使用`RowSet`对象，特别是`CachedRowSet`对象，而不是`ResultSet`对象，原因有两个。`CachedRowSet`对象使应用程序的用户可以更改其中包含的数据，而无需连接到数据库。此外，由于`CachedRowSet`对象是JavaBeans组件，因此它可以在发生某些事件时通知其他组件。在此示例中，当新行添加到`CachedRowSet`对象时，它会通知正在表中呈现其数据的Swing组件以刷新自身并显示新行。
- `ResultSetMetaData`元数据：检索表`COFFEES`中的列数以及每个列的名称。
- `int numcols, numrows`：分别在表`COFFEES`中存储列数和行数。

`CoffeesTableModel.java`示例从`TableModel`接口实现以下方法：

- `Class <?> getColumnClass(int columnIndex)`：返回列中所有单元格值的最具体的超类。
- `int getColumnCount()`：返回模型中的列数。
- `String getColumnName(int columnIndex)`：返回参数`columnIndex`指定的列的名称。
- `int getRowCount()`：返回模型中的行数。
- `Object getValueAt(int rowIndex, int columnIndex)`：返回列`columnIndex`和行`rowIndex`的交集处的单元格的值。
- `boolean isCellEditable(int rowIndex, int columnIndex)`：如果可以编辑`rowIndex`列和行`columnIndex`的交集处的单元格，则返回`true`。

以下方法尚未实现，因为此示例不允许用户直接编辑表的内容：

- `void addTableModelListener(TableModelListener l)`：向每次发生数据模型更改时通知的列表添加监听器。
- `void removeTableModelListener(TableModelListener l)`：从每次发生数据模型更改时通知的列表中删除监听器。
- `void setValueAt(Object aValue, int rowIndex, int columnIndex)`：将列`columnIndex`与行`rowIndex`的交集处的单元格中的值设置为对象`aValue`。

**实现 `getColumnCount` 和 `getRowCount`**

方法`getColumnCount`和`getRowCount`分别返回成员变量`numcols`和`numrows`的值：

```java
public int getColumnCount() {
    return numcols;
}

public int getRowCount() {
    return numrows;
}
```

**实现 `getColumnClass`**

`getColumnClass`方法返回指定列的数据类型。为简单起见，此方法返回`String`类，从而将表中的所有数据转换为`String`对象。`JTable`类使用此方法确定如何在GUI应用程序中呈现数据。

```java
public Class getColumnClass(int column) {
    return String.class;
}
```

**实现 `getColumnName`**

`getColumnName`方法返回指定列的名称。`JTable`类使用此方法标记其每个列。

```java
public String getColumnName(int column) {
    try {
        return this.metadata.getColumnLabel(column + 1);
    } catch (SQLException e) {
        return e.toString();
    }
}
```

**实现 `getColumnAt`**

`getColumnAt`方法检索行集`coffeesRowSet`中指定行和列的值。`JTable`类使用此方法填充其表。请注意，SQL开始将其行和列编号为1，但`TableModel`接口从0开始；这就是为什么`rowIndex`和`columnIndex`值增加1的原因。

```java
public Object getValueAt(int rowIndex, int columnIndex) {

    try {
        this.coffeesRowSet.absolute(rowIndex + 1);
        Object o = this.coffeesRowSet.getObject(columnIndex + 1);
        if (o == null)
            return null;
        else
            return o.toString();
    } catch (SQLException e) {
        return e.toString();
    }
}
```

**实现 `isCellEditable`**

因为此示例不允许用户直接编辑表的内容（行由另一个窗口控件添加），所以无论`rowIndex`和`columnIndex`的值如何，此方法都返回`false`：

```java
public boolean isCellEditable(int rowIndex, int columnIndex) {
    return false;
}
```

**实现 `javax.sql.RowSetListener`**

类`CoffeesFrame`只从接口`RowSetListener`实现一个方法，`rowChanged`。当用户向表中添加行时，将调用此方法。

```java
public void rowChanged(RowSetEvent event) {

    CachedRowSet currentRowSet =
        this.myCoffeesTableModel.coffeesRowSet;

    try {
        currentRowSet.moveToCurrentRow();
        myCoffeesTableModel = new CoffeesTableModel(
            myCoffeesTableModel.getCoffeesRowSet());
        table.setModel(myCoffeesTableModel);

    } catch (SQLException ex) {

        JDBCTutorialUtilities.printSQLException(ex);

        // Display the error in a dialog box.

        JOptionPane.showMessageDialog(
            CoffeesFrame.this,
            new String[] {
                // Display a 2-line message
                ex.getClass().getName() + ": ",
                ex.getMessage()
            }
        );
    }
}
```

此方法更新GUI应用程序中的表。

**布置 Swing 组件**

`CoffeesFrame`类的构造函数初始化并布置Swing组件。以下语句检索`COFFEES`表的内容，将内容存储在`CachedRowSet`对象`myCachedRowSet`中，并初始化`JTable` Swing组件：

```java
CachedRowSet myCachedRowSet = getContentsOfCoffeesTable();
myCoffeesTableModel = new CoffeesTableModel(myCachedRowSet);
myCoffeesTableModel.addEventHandlersToRowSet(this);

// Displays the table   
table = new JTable(); 
table.setModel(myCoffeesTableModel);
```

如前所述，此示例使用`RowSet`对象（尤其是`CachedRowSet`对象）而不是`ResultSet`对象来表示`COFFEES`表的内容。

方法`CoffeesFrame.getContentsOfCoffeesTable`检索表`COFFEES`的内容。

方法`CoffeesTableModel.addEventHandlersToRowSet`将`CoffeesFrame`类中定义的事件处理程序（方法`rowChanged`）添加到行集成员变量`CoffeesTableModel.coffeesRowSet`。这使得类`CoffeesFrame`能够通知任何事件的行集`coffeesRowSet`，特别是当用户单击“将行添加到表”，“更新数据库”或“放弃更改”按钮时。当行集`coffeesRowSet`被通知其中一个更改时，将调用方法`CoffeesFrame.rowChanged`。

语句`table.setModel`（`myCoffeesTableModel`）指定它使用`CoffeesTableModel`对象`myCoffeesTableModel`来填充`JTable` Swing组件表。

以下语句指定`CoffeesFrame`类使用布局`GridBagLayout`来布局其Swing组件：

```java
Container contentPane = getContentPane();
contentPane.setComponentOrientation(
    ComponentOrientation.LEFT_TO_RIGHT);
contentPane.setLayout(new GridBagLayout());
GridBagConstraints c = new GridBagConstraints();
```

有关使用布局`GridBagLayout`的更多信息，请参见 [Creating a GUI With JFC/Swing](https://docs.oracle.com/javase/tutorial/uiswing/index.html)  中的 [How to Use GridBagLayout](https://docs.oracle.com/javase/tutorial/uiswing/layout/gridbag.html) 。

请参阅`CoffeesFrame.java`的源代码，以了解如何将此示例的Swing组件添加到布局`GridBagLayout`中。

**为按钮添加监听器**

以下语句将一个监听器添加到“向表中添加行”按钮：

```java
button_ADD_ROW.addActionListener(
    new ActionListener() {
      
    public void actionPerformed(ActionEvent e) {

        JOptionPane.showMessageDialog(
            CoffeesFrame.this, new String[] {
                "Adding the following row:",
                "Coffee name: [" +
                textField_COF_NAME.getText() +
                "]",
                "Supplier ID: [" +
                textField_SUP_ID.getText() + "]",
                "Price: [" +
                textField_PRICE.getText() + "]",
                "Sales: [" +
                textField_SALES.getText() + "]",
                "Total: [" +
                textField_TOTAL.getText() + "]"
            }
        );

        try {
            myCoffeesTableModel.insertRow(
                textField_COF_NAME.getText(),
                Integer.parseInt(textField_SUP_ID.getText().trim()),
                Float.parseFloat(textField_PRICE.getText().trim()),
                Integer.parseInt(textField_SALES.getText().trim()),
                Integer.parseInt(textField_TOTAL.getText().trim())
            );
        } catch (SQLException sqle) {
            displaySQLExceptionDialog(sqle);
        }
    }
});
```

当用户单击此按钮时，它将执行以下操作：

- 创建一个消息对话框，显示要添加到表中的行。
- 调用方法`CoffeesTableModel.insertRow`，它将行添加到成员变量`CoffeesTableModel.coffeesRowSet`。

如果抛出`SQLException`，则方法`CoffeesFrame.displaySQLExceptionDialog`将创建一个消息对话框，显示`SQLException`的内容。

以下语句将一个监听器添加到“更新数据库“按钮：

```java
button_UPDATE_DATABASE.addActionListener(
    new ActionListener() {
        public void actionPerformed(ActionEvent e) {
            try {
                myCoffeesTableModel.coffeesRowSet.acceptChanges();
                msgline.setText("Updated database");
            } catch (SQLException sqle) {
                displaySQLExceptionDialog(sqle);
                // Now revert back changes
                try {
                    createNewTableModel();
                    msgline.setText("Discarded changes");
                } catch (SQLException sqle2) {
                    displaySQLExceptionDialog(sqle2);
                }
            }
        }
    }
);
```

当用户单击此按钮时，将使用行集`myCoffeesTableModel.coffeesRowSet`的内容更新表`COFFEES`。

以下语句为”撤销修改“按钮添加了一个监听器：

```java
button_DISCARD_CHANGES.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        try {
            createNewTableModel();
        } catch (SQLException sqle) {
            displaySQLExceptionDialog(sqle);
        }
    }
});
```

当用户单击此按钮时，将调用方法`CoffeesFrame.createNewTableModel`，该方法使用`COFFEES`表的内容重新填充`JTable`组件。

# Java 管理扩展(JMX)

 **Java Management Extensions (JMX)** 课程提供了有关 JMX 技术的介绍。该技术包含在 Java 平台标准版中。本课程中的例子展示了如何使用 JMX 中最重要的特性。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)JMX 技术概述](https://docs.oracle.com/javase/tutorial/jmx/overview/index.html) 简要介绍了 JMX 技术，包括它的目标和主要特性。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)MBeans 介绍](https://docs.oracle.com/javase/tutorial/jmx/mbeans/index.html) 介绍 JMX 技术的基础概念，*管理 beans*，也被称为**MBeans**。本课程也将介绍MXBeans。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)通知](https://docs.oracle.com/javase/tutorial/jmx/notifs/index.html) 介绍 JMX 技术中的通知机制。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)远程管理](https://docs.oracle.com/javase/tutorial/jmx/remote/index.html) 展示如何实现 JMX API 的管理能力并创建一个 JMX 客户端应用。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)延伸学习](https://docs.oracle.com/javase/tutorial/jmx/end.html) 介绍有关 JMX 技术的更进一步的资料。

## JMX 技术概述

Java Management Extensions（JMX）技术是Java平台标准版（Java SE平台）的标准部分。JMX技术已添加到Java 2平台标准版（J2SE）5.0版本的平台中。

JMX技术提供了一种简单，标准的方式来管理应用程序，设备和服务等资源。由于JMX技术是动态的，因此您可以使用它来监视和管理资源的创建，安装和实施。您还可以使用JMX技术来监视和管理Java虚拟机（Java VM）。

JMX规范定义了Java编程语言中的体系结构，设计模式，API和服务，用于管理和监视应用程序和网络。

使用JMX技术，给定资源由一个或多个Java对象（称为 Managed Beans 或 MBeans）进行检测。这些 MBeans 在核心管理的对象服务器中注册，称为 MBean 服务器。MBean 服务器充当管理代理程序，可以在大多数已为Java编程语言启用的设备上运行。

规范定义了用于管理已正确配置以进行管理的任何资源的JMX代理。JMX代理由MBean服务器和一组用于处理MBean的服务组成，MBean服务器在其中注册MBean。通过这种方式，JMX代理可以直接控制资源并使其可用于远程管理应用程序。

检测资源的方式完全独立于管理基础结构。因此，无论管理应用程序如何实现，都可以使资源易于管理。

JMX技术定义了标准连接器（称为JMX连接器），使您可以从远程管理应用程序访问JMX代理。使用不同协议的JMX连接器提供相同的管理接口。因此，无论使用何种通信协议，管理应用程序都可以透明地管理资源。只要这些系统或应用程序支持JMX代理，JMX代理也可以由不符合JMX规范的系统或应用程序使用。

### 为什么要使用 JMX 技术？

JMX技术为开发人员提供了一种灵活的方法来检测基于Java技术的应用程序（Java应用程序），创建智能代理，实现分布式管理中间件和管理器，并将这些解决方案顺利集成到现有的管理和监视系统中。

- JMX技术使Java应用程序无需大量投资即可进行管理。
  基于JMX技术的代理（JMX代理）可以在大多数支持Java技术的设备上运行。因此，Java应用程序可以变得易于管理，而对其设计几乎没有影响。Java应用程序只需要嵌入一个托管对象服务器，并使其某些功能可用作在对象服务器中注册的一个或多个托管bean（MBean）。这就是从管理基础设施中受益所需的一切。
- JMX技术提供了管理Java应用程序，系统和网络的标准方法。
  例如，Java平台企业版（Java EE）5 Application Server符合JMX体系结构，因此可以使用JMX技术进行管理。
- JMX技术可用于Java VM的开箱即用管理。
  Java虚拟机（Java VM）使用JMX技术进行了高度定制化。您可以启动JMX代理以访问内置Java VM检测，从而远程监视和管理Java VM。
- JMX技术提供可扩展的动态管理架构。
  每个JMX代理服务都是一个独立的模块，可以根据需要插入管理代理程序。这种基于组件的方法意味着JMX解决方案可以从小型设备扩展到大型电信交换机等。 JMX规范提供了一组核心代理服务。可以在管理基础架构中开发和动态加载，卸载或更新其他服务。
- JMX技术利用现有的标准Java技术。
  只要需要，JMX规范就会引用现有的Java规范，例如Java命名和目录接口（J.N.D.I.）API。
- 可以从NetBeans IDE模块创建基于JMX技术的应用程序（JMX应用程序）。
  您可以从NetBeans更新中心（在NetBeans界面中选择工具 - >更新中心）获取模块，该模块使您可以使用NetBeans IDE创建JMX应用程序。这降低了JMX应用程序的开发成本。
- JMX技术与现有管理解决方案和新兴技术相集成。
  JMX API是任何管理系统供应商都可以实现的开放接口。 JMX解决方案可以使用查找和发现服务以及Jini网络技术和服务定位协议（SLP）等协议。

### JMX 技术架构

JMX 技术可以分为三个层次如下：

- 插桩
- JMX 代理
- 远程管理

**插桩**

要使用JMX技术管理资源，必须首先使用Java编程语言检测资源。您使用称为*MBeans*的Java对象来实现对资源插桩的访问。MBean必须遵循JMX规范中定义的设计模式和接口。这样做可确保所有MBean以标准化方式提供托管资源工具。除了标准MBean之外，JMX规范还定义了一种称为*MXBean*的特殊类型的MBean。MXBean是仅引用预定义数据类型集的MBean。存在其他类型的MBean，但本课程将集中在标准MBean和MXBeans上。

一旦资源由MBean插桩检测，就可以通过JMX代理进行管理。MBean不需要了解它们将运行的JMX代理。

MBean设计灵活，简单且易于实施。应用程序，系统和网络的开发人员可以以标准方式管理其产品，而无需了解或投资复杂的管理系统。可以用最少的努力使现有资源易于管理。

此外，JMX规范的检测层次提供了通知机制。此机制使MBean能够生成通知事件并将其传播到其他层次的组件。

**JMX 代理**

基于JMX技术的代理（JMX代理）是一种标准管理代理，可直接控制资源并使其可用于远程管理应用程序。JMX代理通常与它们控制的资源位于同一台机器上，但这种布置不是必需的。

JMX代理的核心组件是**MBean服务器**，这是一个在其中注册MBean的托管对象服务器。JMX代理还包括一组用于管理MBean的服务，以及至少一个允许管理应用程序访问的通信适配器或连接器。

实现JMX代理时，您不需要知道它将管理的资源的语义或功能。事实上，JMX代理甚至不需要知道它将服务哪些资源，因为任何符合JMX规范的资源都可以使用任何提供资源所需服务的JMX代理。同样，JMX代理不需要知道将访问它的管理应用程序的功能。

**远程管理**

可以通过许多不同方式访问JMX技术工具，可以通过现有管理协议（如简单网络管理协议 SNMP ）或通过专有协议进行访问。 MBean服务器依赖于协议适配器和连接器，以便从代理的Java虚拟机（Java VM）之外的管理应用程序访问JMX代理。

每个适配器都提供通过MBean服务器中注册的所有MBean的特定协议的视图。例如，HTML适配器可以在浏览器中显示MBean。

连接器提供管理器端接口，用于处理管理器和JMX代理之间的通信。每个连接器通过不同的协议提供相同的远程管理接口。当远程管理应用程序使用此接口时，无论协议如何，它都可以通过网络透明地连接到JMX代理。 JMX技术提供了一种标准解决方案，用于将JMX技术工具导出到基于Java远程方法调用（Java RMI）的远程应用程序。

### 虚拟机监控和管理

JMX技术还可用于监视和管理Java虚拟机（Java VM）。

Java VM具有内置检测功能，使您可以使用JMX技术监视和管理它。这些内置管理实用程序通常被称为Java VM的*开箱即用*管理工具。为了监视和管理Java VM的不同方面，Java VM包括一个平台MBean服务器和特殊的MXBeans，供符合JMX规范的管理应用程序使用。

**平台 MXBeans 和平台 MBean 服务**

*platform MXBeans*是一组MXBeans，随Java SE平台一起提供，用于监视和管理Java VM以及Java Runtime Environment（JRE）的其他组件。每个平台MXBean都封装了Java VM功能的一部分，例如类加载系统，即时（JIT）编译系统，垃圾收集器等。通过使用符合JMX规范的监视和管理工具，可以显示和交互这些MXBean，使您能够监视和管理这些不同的VM功能。一个这样的监视和管理工具是Java SE平台的 JConsole 图形用户界面。

Java SE平台提供标准的*平台MBean服务器*，其中注册了这些平台MXBean。平台MBean服务器还可以注册您要创建的任何其他MBean。

**JConsole**

Java SE平台包括 JConsole 监视和管理工具，该工具符合JMX规范。JConsole 使用Java VM的丰富工具（平台MXBeans）来提供有关Java平台上运行的应用程序的性能和资源消耗的信息。

**开箱即用的管理实践**

由于实现JMX技术的标准监视和管理实用程序内置于Java SE平台中，因此您可以在不必编写任何一行JMX API代码的情况下查看现成的JMX技术。您可以通过启动Java应用程序然后使用JConsole对其进行监视来实现。

**使用 JConsole 监控应用**

此过程说明如何监视Notepad Java应用程序。在版本6之前的Java SE平台版本下，需要使用以下选项启动要使用JConsole监视的应用程序。

```
-Dcom.sun.management.jmxremote
```

但是，随Java SE 6平台提供的JConsole版本可以附加到支持Attach API的任何本地应用程序。换句话说，JACsole会自动检测在Java SE 6 HotSpot VM中启动的任何应用程序，而不需要使用上述命令行选项启动。

1. 通过在终端窗口中使用以下命令启动Notepad Java应用程序：

   ```
   java -jar 
       jdk_home/demo/jfc/Notepad/Notepad.jar
   ```

   其中`jdk_home`是安装Java Development Kit（JDK）的目录。如果您没有运行Java SE平台的第6版，则需要使用以下命令：

   ```
   java -Dcom.sun.management.jmxremote -jar 
         jdk_home/demo/jfc/Notepad/Notepad.jar
   ```

2. 打开记事本后，在不同的终端窗口中，使用以下命令启动JConsole：

   ```
   jconsole
   ```

   将显示“新建连接”对话框。

3. 在“新建连接”对话框中，选择

   ```
   Notepad.jar
   ```

   从“本地进程”列表中，单击“连接”按钮。

   JConsole打开并将自身连接到`Notepad.jar`进程。当JConsole打开时，您将看到与记事本相关的监视和管理信息的概述。例如，您可以查看应用程序正在使用的堆内存量，应用程序当前运行的线程数以及应用程序消耗的中央处理单元（CPU）容量。

4. 单击不同的JConsole选项卡。

   每个选项卡都提供有关运行记事本的Java VM的不同功能区域的更多详细信息。所有提供的信息都是从该踪迹中提到的各种JMX技术MXBeans中获得的。所有平台MXBeans都可以显示在MBeans选项卡中。MBeans选项卡将在此跟踪的下一部分中进行检查。

5. 要关闭JConsole，请选择Connection  -> Exit。


## MBeans 介绍

本课程介绍了JMX API的基本概念，即托管bean或MBean。

MBean是一个托管Java对象，类似于JavaBeans组件，它遵循JMX规范中提出的设计模式。MBean可以表示设备，应用程序或需要管理的任何资源。MBean公开了一个由以下内容组成的管理界面：

- 一组可读或可写属性，或两者兼而有之。
- 一组可调用的操作。
- 自我描述。

管理接口在MBean实例的整个生命周期中不会更改。MBean还可以在发生某些预定义事件时发出通知。

JMX规范定义了五种类型的MBean：

- 标准MBean
- 动态MBean
- 打开MBean
- 模型MBean
- MXBeans

此课程中的示例仅演示了最简单的MBean类型，即标准MBean和MXBeans。

### 标准 MBeans

This section presents an example of a straightforward, standard MBean.

A standard MBean is defined by writing a Java interface called `SomethingMBean` and a Java class called `Something` that implements that interface. Every method in the interface defines either an attribute or an operation in the MBean. By default, every method defines an operation. Attributes and operations are methods that follow certain design patterns. A standard MBean is composed of an MBean interface and a class. The MBean interface lists the methods for all exposed attributes and operations. The class implements this interface and provides the functionality of the instrumented resource.

The following sections examine an example of a standard MBean and a simple JMX technology-enabled agent (JMX agent) that manages the MBean.

**MBean 接口**

基本 MBean 接口的例子 [`HelloMBean`](https://docs.oracle.com/javase/tutorial/jmx/examples/HelloMBean.java) ：

```java
package com.example; 
 
public interface HelloMBean { 
 
    public void sayHello(); 
    public int add(int x, int y); 
    
    public String getName(); 
     
    public int getCacheSize(); 
    public void setCacheSize(int size); 
} 
```

按照惯例，MBean接口采用实现它的Java类的名称，并添加后缀MBean。在上面例子这种情况下，接口称为`HelloMBean`。实现此接口的`Hello`类将在下一节中介绍。

根据JMX规范，除了可由MBean管理的应用程序调用的命名和类型操作之外，MBean接口还包含可读且可写的命名和类型属性。`HelloMBean`接口声明了两个操作：Java方法`add()`和`sayHello()`。

`HelloMBean`声明了两个属性：`Name`是只读字符串，`CacheSize`是一个可以读写的整数。声明了`getter`和`setter`方法，以允许托管应用程序访问并可能更改属性值。根据JMX规范的定义，`getter`是任何不返回`void`且名称以`get`开头的公共方法。`getter`使管理器能够读取属性的值，该属性的类型是返回对象的类型。`setter`是任何公共方法，它接受一个参数，其名称以`set`开头。`setter`使管理器能够在属性中写入一个新值，其类型与参数的类型相同。

以下部分显示了这些操作和属性的实现。

**MBean 实现**

下面的 [`Hello`](https://docs.oracle.com/javase/tutorial/jmx/examples/Hello.java) Java 类实现了 `HelloMBean` MBean 接口：

```java
package com.example; 
 
public class Hello ... 
    implements HelloMBean { 
    public void sayHello() { 
        System.out.println("hello, world"); 
    } 
     
    public int add(int x, int y) { 
        return x + y; 
    } 
     
    public String getName() { 
        return this.name; 
    }  
     
    public int getCacheSize() { 
        return this.cacheSize; 
    } 
     
    public synchronized void setCacheSize(int size) {
        ...
    
        this.cacheSize = size; 
        System.out.println("Cache size now " + this.cacheSize); 
    } 
    ...
     
    private final String name = "Reginald"; 
    private int cacheSize = DEFAULT_CACHE_SIZE; 
    private static final int 
        DEFAULT_CACHE_SIZE = 200; 
}
```

`Hello`类直截了当地提供了`HelloMBean`声明的操作和属性的定义。`sayHello()`和`add()`操作非常简单，但实际操作可以根据需要简单或复杂。

该类还定义了获取`Name`属性以及获取和设置`CacheSize`属性的方法。在此示例中，`Name`属性值永远不会更改。但是，在实际情况中，此属性可能会随托管资源的运行而更改。例如，该属性可能表示正常运行时间或内存使用情况等统计信息。这里，该属性仅仅是`Reginald`的名称。

调用`setCacheSize`方法使您可以从其声明的默认值`200`更改`CacheSize`属性。在实际方案中，更改`CacheSize`属性可能需要执行其他操作，例如丢弃条目或分配新条目。此示例仅打印一条消息以确认缓存大小已更改。但是，可以定义更复杂的操作，而不是简单调用`println()`。

使用`Hello` MBean及其定义的接口，它们现在可用于管理它们所代表的资源，如以下部分所示。

**创建 JMX 代理用以管理资源**

一旦资源由MBean检测，该资源的管理由JMX代理执行。

JMX代理的核心组件是MBean服务器。MBean服务器是注册MBean的托管对象服务器。JMX代理还包括一组用于管理MBean的服务。有关MBean服务器实现的详细信息，请参阅  [`MBeanServer`](https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServer.html) 接口的API文档。

后面的`Main`类表示基本的JMX代理：

```java
package com.example; 
 
import java.lang.management.*; 
import javax.management.*; 
 
public class Main { 
 
    public static void main(String[] args) 
        throws Exception { 
     
        MBeanServer mbs = ManagementFactory.getPlatformMBeanServer(); 
        ObjectName name = new ObjectName("com.example:type=Hello"); 
        Hello mbean = new Hello(); 
        mbs.registerMBean(mbean, name); 
          
        ...
     
        System.out.println("Waiting forever..."); 
        Thread.sleep(Long.MAX_VALUE); 
    } 
} 
```

JMX代理`Main`首先通过调用`java.lang.management.ManagementFactory`类的`getPlatformMBeanServer()`方法获取由平台创建和初始化的MBean服务器。如果平台尚未创建MBean服务器，则`getPlatformMBeanServer()`通过调用JMX方法`MBeanServerFactory.createMBeanServer()`自动创建MBean服务器。`Main`获取的`MBeanServer`实例名为`mbs`。

接下来，`Main`定义它将创建的MBean实例的对象名称。每个JMX MBean都必须具有对象名称。对象名称是JMX类`ObjectName`的实例，必须符合JMX规范定义的语法。即，对象名称必须包含域和键属性列表。在`Main`定义的对象名称中，域是`com.example`（包含示例MBean的包）。此外，key-property声明此对象的类型为`Hello`。

创建名为`mbean`的`Hello`对象的实例。然后，通过将对象和对象名称传递给对JMX方法`MBeanServer.registerMBean()`的调用，将名为`mbean`的`Hello`对象注册为MBean服务器`mbs`中具有对象名称的MBean。

在MBean服务器中注册了`Hello` MBean后，`Main`只是等待对`Hello`执行管理操作。在此示例中，这些管理操作正在调用`sayHello()`和`add()`，以及获取和设置属性值。

**运行该标准 MBean 示例**

在检查了示例类之后，您现在可以运行该示例。在此示例中，JConsole用于与MBean交互。

若要运行该示例，请按照下列步骤操作：

1. 将JMX API示例类包`jmx_examples.zip`保存到您的工作目录`work_dir`。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 如果您运行的是Java Development Kit（JDK）版本6，请使用以下命令启动Main应用程序。

   ```
   java com.example.Main
   ```

   如果您运行的是早于版本6的JDK版本，则需要使用指定的以下选项启动Main应用程序，以公开应用程序以进行监视和管理。

   ```
   java -Dcom.sun.management.jmxremote example.Main
   ```

   显示`Main`正在等待某事发生的确认。

5. 在同一台计算机上的另一个终端窗口中启动JConsole。

   ```
   jconsole
   ```

   将显示“新建连接”对话框，其中列出了可以连接的正在运行的JMX代理的列表。

6. 在“新建连接”对话框中，从列表中选择`com.example.Main`，然后单击“连接”。

   将显示平台当前活动的摘要。

7. 单击MBeans选项卡。

   此面板显示当前在MBean服务器中注册的所有MBean。

8. 在左侧框架中，展开MBean树中的`com.example`节点。

   您会看到Main创建并注册的示例MBean `Hello`。如果单击`Hello`，则会在MBean树中看到其关联的`Attributes`和`Operations`节点。

9. 展开MBean树中的`Hello` MBean的`Attributes`节点。

   显示由`Hello`类定义的MBean属性。

10. 将`CacheSize`属性的值更改为150。

   在您启动`Main`的终端窗口中，将生成此属性更改的确认。

11. 展开MBean树中的`Hello` MBean的`Operations`节点。

    `Hello` MBean声明的两个操作，`sayHello()`和`add()`是可见的。

12. 单击`sayHello`按钮调用`sayHello()`操作。

    JConsole对话框通知您已成功调用该方法。消息“hello，world”在`Main`运行的终端窗口中生成。

13. 为`add()`操作提供两个整数以添加并单击“添加”按钮。

    答案显示在JConsole对话框中。

14. 要关闭JConsole，请选择Connection  -> Exit。

### MXBeans

本节介绍一种特殊类型的MBean，称为MXBeans。

MXBean是一种MBean，仅引用一组预定义的数据类型。通过这种方式，您可以确保任何客户端（包括远程客户端）都可以使用您的MBean，而无需客户端访问表示MBean类型的特定于模型的类。MXBeans提供了将相关值捆绑在一起的便捷方式，而无需特别配置客户端来处理捆绑包。

与标准MBean的方式相同，MXBean是通过编写名为`SomethingMXBean`的Java接口和实现该接口的Java类来定义的。但是，与标准MBean不同，MXBeans不需要将Java类称为`Something`。接口中的每个方法都定义MXBean中的属性或操作。注解`@MXBean`也可用于修饰Java接口，而不是要求接口的名称后跟MXBean后缀。

MXBeans存在于Java 2平台标准版（J2SE）5.0软件的`java.lang.management`包中。但是，除了`java.lang.management`中定义的标准集之外，用户现在还可以定义自己的MXBean。

MXBeans背后的主要思想是MXBean接口中引用的`java.lang.management.MemoryUsage`等类型，在本例中为`java.lang.management.MemoryMXBean`，它们被映射到一组标准类型，即包`javax.management.openmbean`中定义的*Open类型*。确切的映射规则出现在MXBean规范中。但是，一般原则是简单类型（如`int`或`String`）保持不变，而复杂类型（如`MemoryUsage`）则映射到标准类型`CompositeDataSupport`。

MXBean示例包含以下文件，这些文件位于`jmx_examples.zip`中：

- `QueueSamplerMXBean`接口
- 实现MXBean接口的`QueueSampler`类
- 由MXBean接口中的`getQueueSample()`方法返回的`QueueSample` Java类型
- `Main`，设置和运行示例的程序

MXBean示例使用这些类来执行以下操作：

- 定义管理`Queue<String>`类型资源的简单MXBean
- 在MXBean中声明一个`getter`，`getQueueSample`，它在调用时获取队列的快照，并返回一个Java类`QueueSample`，它将以下值捆绑在一起：
  - 拍摄快照的时间
  - 队列大小
  - 在给定时间排队的队长
- 在MBean服务器中注册MXBean

**MXBean 接口**

下面的代码展示了示例 [`QueueSamplerMXBean`](https://docs.oracle.com/javase/tutorial/jmx/examples/QueueSamplerMXBean.java) MXBean 接口：

```java
package com.example; 
 
public interface QueueSamplerMXBean { 
    public QueueSample getQueueSample(); 
    public void clearQueue(); 
} 
```

请注意，您声明MXBean接口的方式与声明标准MBean接口的方式完全相同。`QueueSamplerMXBean`接口声明了一个`getter`，`getQueueSample`和一个`clearQueue`操作。

**定义 MXBean 操作**

MXBean操作在`QueueSampler`示例类中声明，如下所示：

```java
package com.example; 
 
import java.util.Date; 
import java.util.Queue; 
 
public class QueueSampler 
                implements QueueSamplerMXBean { 
     
    private Queue<String> queue; 
         
    public QueueSampler (Queue<String> queue) { 
        this.queue = queue; 
    } 
         
    public QueueSample getQueueSample() { 
        synchronized (queue) { 
            return new QueueSample(new Date(), 
                           queue.size(), queue.peek()); 
        } 
    } 
         
    public void clearQueue() { 
        synchronized (queue) { 
            queue.clear(); 
        } 
    } 
} 
```

`QueueSampler`定义MXBean接口声明的`getQueueSample()` `getter`和`clearQueue()`操作。 `getQueueSample()`操作返回`QueueSample` Java类型的实例，该实例是使用`java.util.Queue`方法`peek()`和`size()`返回的值以及`java.util.Date`的实例创建的。

**定义MXBean接口返回的Java类型**

`QueueSampler`返回的`QueueSample`实例在`QueueSample`类中定义，如下所示：

```java
package com.example; 
 
import java.beans.ConstructorProperties; 
import java.util.Date; 
 
public class QueueSample { 
     
    private final Date date; 
    private final int size; 
    private final String head; 
         
    @ConstructorProperties({"date", "size", "head"}) 
    public QueueSample(Date date, int size, 
                        String head) { 
        this.date = date; 
        this.size = size; 
        this.head = head; 
    } 
         
    public Date getDate() { 
        return date; 
    } 
         
    public int getSize() { 
        return size; 
    } 
         
    public String getHead() { 
        return head; 
    } 
}   
```

在`QueueSample`类中，MXBean框架调用`QueueSample`中的所有`getter`以将给定实例转换为`CompositeData`实例，并使用`@ConstructorProperties`注解从`CompositeData`实例重建`QueueSample`实例。

**在MBean Server中创建和注册MXBean**

到目前为止，已经定义了以下内容：MXBean接口和实现它的类，以及返回的Java类型。接下来，必须在MBean服务器中创建并注册MXBean。这些`Main`示例JMX代理执行的操作与标准MBean示例中使用的相同，但相关代码未显示在 [Standard MBean](https://docs.oracle.com/javase/tutorial/jmx/mbeans/standard.html) 课程中。

```java
package com.example; 
 
import java.lang.management.ManagementFactory; 
import java.util.Queue; 
import java.util.concurrent.ArrayBlockingQueue; 
import javax.management.MBeanServer; 
import javax.management.ObjectName; 
 
public class Main { 
 
    public static void main(String[] args) throws Exception { 
        MBeanServer mbs = 
            ManagementFactory.getPlatformMBeanServer(); 
                
        ...  
        ObjectName mxbeanName = new ObjectName("com.example:type=QueueSampler");
        
        Queue<String> queue = new ArrayBlockingQueue<String>(10);
        queue.add("Request-1");
        queue.add("Request-2");
        queue.add("Request-3");
        QueueSampler mxbean = new QueueSampler(queue);
        
        mbs.registerMBean(mxbean, mxbeanName);
                 
        System.out.println("Waiting..."); 
        Thread.sleep(Long.MAX_VALUE); 
    } 
} 
```

`Main`类执行以下操作：

- 获取平台MBean服务器。
- 为MXBean `QueueSampler`创建对象名称。
- 为要处理的`QueueSampler` MXBean创建`Queue`实例。
- 将`Queue`实例提供给新创建的`QueueSampler` MXBean。
- 以与标准MBean完全相同的方式在MBean服务器中注册MXBean。

**运行 MXBean 示例**

MXBean示例使用您在标准MBeans部分中使用的`jmx_examples.zip`包中的类。此示例需要Java SE平台的第6版。 要运行MXBeans示例，请执行以下步骤：

1. 如果尚未执行此操作，请将`jmx_examples.zip`保存到`work_dir`目录中。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 启动主应用程序。生成`Main`正在等待某事发生的确认。

   ```
   java com.example.Main
   ```

5. 在同一台计算机上的另一个终端窗口中启动JConsole。 将显示“新建连接”对话框，其中列出了可以连接的正在运行的JMX代理的列表。

   ```
   jconsole
   ```

6. 在“新建连接”对话框中，从列表中选择`com.example.Main`，然后单击“连接”。

   将显示平台当前活动的摘要。

7. 单击MBeans选项卡。

   此面板显示当前在MBean服务器中注册的所有MBean。

8. 在左侧框架中，展开MBean树中的`com.example`节点。

   您将看到`Main`创建并注册的示例MBean `QueueSampler`。如果单击`QueueSampler`，则会在MBean树中看到其关联的`Attributes`和`Operations`节点。

9. 展开“属性”节点。

   您会看到`QueueSample`属性出现在右窗格中，其值为`javax.management.openmbean.CompositeDataSupport`。

10. 双击`CompositeDataSupport`值。

   您会看到`QueueSample`值的日期，头部和大小，因为MXBean框架已将`QueueSample`实例转换为`CompositeData`。如果您已将`QueueSampler`定义为标准MBean而不是MXBean，则JConsole将找不到`QueueSample`类，因为它不在其类路径中。如果`QueueSampler`是标准MBean，则在检索`QueueSample`属性值时会收到`ClassNotFoundException`消息。JConsole发现`QueueSampler`的事实证明了在通过JConsole等通用JMX客户端连接到JMX代理时使用MXBeans的有用性。

11. 展开“操作”节点。

    将显示一个用于调用`clearQueue`操作的按钮。

12. 单击`clearQueue`按钮。

    显示已成功调用该方法的确认。

13. 再次展开`Attributes`节点，然后双击`CompositeDataSupport`值。

    头部和大小值已重置。

14. 要关闭JConsole，请选择Connection  -> Exit。

## 通知

JMX API定义了一种机制，使MBean能够生成通知，例如，指示状态更改，检测到的事件或问题。

要生成通知，MBean必须实现接口`NotificationEmitter`或扩展`NotificationBroadcasterSupport`。要发送通知，您需要构造类`javax.management.Notification`或子类（例如`AttributeChangedNotification`）的实例，并将实例传递给`NotificationBroadcasterSupport.sendNotification`。

每个通知都有一个来源。源是生成通知的MBean的对象名称。

每个通知都有一个序列号。当顺序很重要时，比如当存在以错误的顺序处理通知的风险时，此号码可用于对来自同一来源的通知进行排序。序列号可以是零，但最好确保来自给定MBean的每个通知的数量递增。

标准MBean中的`Hello` MBean实现实际上实现了通知机制。但是，为了简单起见，该课程中省略了此代码。`Hello`的完整代码如下：

```java
package com.example;

import javax.management.*;

public class Hello
        extends NotificationBroadcasterSupport
        implements HelloMBean {

    public void sayHello() {
        System.out.println("hello, world");
    }

    public int add(int x, int y) {
        return x + y;
    }

    public String getName() {
        return this.name;
    }

    public int getCacheSize() {
        return this.cacheSize;
    }

    public synchronized void setCacheSize(int size) {
        int oldSize = this.cacheSize;
        this.cacheSize = size;

        System.out.println("Cache size now " + this.cacheSize);

        Notification n = new AttributeChangeNotification(this,
                                sequenceNumber++, System.currentTimeMillis(),
                                "CacheSize changed", "CacheSize", "int",
                                oldSize, this.cacheSize);

        sendNotification(n);
    }

    @Override
    public MBeanNotificationInfo[] getNotificationInfo() {
        String[] types = new String[]{
            AttributeChangeNotification.ATTRIBUTE_CHANGE
        };

        String name = AttributeChangeNotification.class.getName();
        String description = "An attribute of this MBean has changed";
        MBeanNotificationInfo info = 
                new MBeanNotificationInfo(types, name, description);
        return new MBeanNotificationInfo[]{info};
    }
    
    private final String name = "Reginald";
    private int cacheSize = DEFAULT_CACHE_SIZE;
    private static final int DEFAULT_CACHE_SIZE = 200;
    private long sequenceNumber = 1;
}
```

此`Hello` MBean实现扩展了`NotificationBroadcasterSupport`类。`NotificationBroadcasterSupport`实现`NotificationEmitter`接口。

操作和属性的设置方式与标准MBean示例相同，但`CacheSize`属性的`setter`方法现在定义了`oldSize`的值。此值记录设置操作之前的`CacheSize`属性的值。

通知是从JMX类`AttributeChangeNotification`的实例n构造的，该实例扩展了`javax.management.Notification`。通知是根据以下信息在`setCacheSize()`方法的定义内构造的。此信息作为参数传递给`AttributeChangeNotification`。

- 通知源的对象名称，即`Hello` MBean，由`this`表示
- 序列号，即`sequenceNumber`，设置为`1`并逐渐增加
- 时间戳
- 通知消息的内容
- 已更改的属性的名称，在本例中为`CacheSize`
- 已更改的属性类型
- 旧属性值，在本例中为`oldSize`
- 新属性值，在本例中为`this.cacheSize`

然后将通知n传递给`NotificationBroadcasterSupport.sendNotification()`方法。

最后，定义`MBeanNotificationInfo`实例以描述MBean为给定类型的通知生成的不同通知实例的特征。在这种情况下，发送的通知类型是`AttributeChangeNotification`通知。

**运行 MBean 通知示例**

再一次，您将使用JConsole与`Hello` MBean进行交互，这次是发送和接收通知。此示例需要Java SE平台的第6版。

1. 如果尚未执行此操作，请将`jmx_examples.zip`保存到`work_dir`目录中。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 启动`Main`应用程序。

   ```
   java com.example.Main
   ```

   生成`Main`正在等待某事发生的确认。

5. 在同一台计算机上的另一个终端窗口中启动JConsole。

   ```
   jconsole
   ```

   将显示“新建连接”对话框，其中列出了可以连接的正在运行的JMX代理的列表。

6. 在“新建连接”对话框中，从列表中选择`com.example.Main`，然后单击“连接”。

   将显示平台当前活动的摘要。

7. 单击MBeans选项卡。

   此面板显示当前在MBean服务器中注册的所有MBean。

8. 在左侧框架中，展开MBean树中的`com.example`节点。

   您将看到由`Hello`创建并注册的示例MBean `Hello`。如果单击`Hello`，则会在MBean树中看到其`Notifications`节点。

9. 展开MBean树中`Hello` MBean的`Notifications`节点。

   请注意，面板为空白。

10. 单击“订阅”按钮。

   接收的当前通知数（0）显示在“通知”节点标签中。

11. 展开MBean树中`Hello` MBean的`Attributes`节点，并将`CacheSize`属性的值更改为150。

    在启动Main的终端窗口中，将显示此属性更改的确认。请注意，“通知”节点中显示的已接收通知数已更改为1。

12. 再次展开MBean树中`Hello` MBean的`Notifications`节点。

    将显示通知的详细信息。

13. 要关闭JConsole，请选择Connection  -> Exit。

## 远程管理

JMX API使您可以使用基于JMX技术的连接器（JMX连接器）执行资源的远程管理。JMX连接器使远程基于Java技术的客户端可以访问MBean服务器。连接器的客户端导出与MBean服务器基本相同的接口。

JMX连接器由连接器客户端和连接器服务器组成。连接器服务器连接到MBean服务器并侦听来自客户端的连接请求。连接器客户端负责与连接器服务器建立连接。连接器客户端通常位于与连接器服务器不同的Java虚拟机（Java VM）中，并且通常在不同的计算机上运行。JMX API定义了基于远程方法调用（RMI）的标准连接协议。此协议使您可以从远程位置将JMX客户端连接到MBean服务器中的MBean，并对MBean执行操作，就像操作是在本地执行一样。

Java SE平台提供了一种开箱即用的方法，可以使用JMX API的标准RMI连接器远程监控应用程序。开箱即用的RMI连接器自动公开应用程序以进行远程管理，而无需您自己创建专用的远程连接器服务器。通过使用正确的属性启动Java应用程序来激活开箱即用的远程管理代理。然后，与JMX技术兼容的监控和管理应用程序可以连接到这些应用程序并远程监控它们。

### 通过 JConsole 公开资源以进行远程管理

如果使用现成的远程管理代理和现有的监视和管理工具（如JConsole），则使用JMX API公开Java应用程序以进行远程管理非常简单。

要公开远程管理应用程序，需要使用正确的属性启动它。此示例显示如何公开 [`Main`](https://docs.oracle.com/javase/tutorial/jmx/examples/Main.java)  JMX代理以进行远程管理。

------

安全考虑：

为简单起见，在此示例中禁用了身份验证和加密安全机制。 但是，在实际环境中实现远程管理时，应实现这些安全机制。[What Next?](https://docs.oracle.com/javase/tutorial/jmx/end.html)  提供指向其他JMX技术文档的指针，其中显示了如何激活安全机制。

------

此示例需要Java SE平台的第6版。 要远程监视`Main` JMX代理，请按照下列步骤操作：

1. 如果尚未执行此操作，请将`jmx_examples.zip`保存到`work_dir`目录中。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 启动`Main`应用程序，指定公开`Main`以进行远程管理的属性。（对于Windows，使用`^`而不是反斜杠`\`将长命令拆分为多行）：

   ```
   java -Dcom.sun.management.jmxremote.port=9999 \
        -Dcom.sun.management.jmxremote.authenticate=false \
        -Dcom.sun.management.jmxremote.ssl=false \
        com.example.Main
   ```

   生成`Main`正在等待某事发生的确认。

5. 在另一台机器上的另一个终端窗口中启动JConsole：

   ```
   jconsole
   ```

   将显示“新建连接”对话框，其中列出了可以在本地连接的正在运行的JMX代理。

6. 选择“远程进程”，然后在“远程进程”字段中键入以下内容：

   ```
   hostname:9999
   ```

   在此地址中，`hostname`是运行`Main`应用程序的远程计算机的名称，`9999`是开箱即用的JMX连接器将连接的端口号。

7. 单击连接。

   显示`Main`正在运行与其中的Java虚拟机（Java VM）的当前活动的摘要。

8. 单击MBeans选项卡。

   此面板显示当前在远程MBean服务器中注册的所有MBean。

9. 在左侧框架中，展开MBean树中的`com.example`节点。

   您会看到`Main`创建并注册的示例MBean `Hello`。如果单击`Hello`，则会在MBean树中看到其关联的`Attributes`和`Operations`节点，即使它在另一台计算机上运行。

10. 要关闭JConsole，请选择Connection  -> Exit。

### 创建一个自定义 JMX 客户端

前面的内容向您展示了如何创建JMX技术MBean和MXBeans，以及如何使用JMX代理注册它们。但是，前面的所有示例都使用了现有的JMX客户端JConsole。本课将演示如何创建自己的自定义JMX客户端。

自定义JMX客户端的示例，客户端包含在`jmx_examples.zip`中。此JMX客户端与前面课程中看到的相同MBean，MXBean和JMX代理进行交互。由于`Client`类的大小，它将在以下部分中以分块的形式进行讲解。

**导入 JMX Remote API 类**

为了能够创建与从JMX客户端远程运行的JMX代理的连接，您需要使用 [`javax.management.remote`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/package-summary.html) 中的类。

```java
package com.example;
...

import javax.management.remote.JMXConnector;
import javax.management.remote.JMXConnectorFactory;
import javax.management.remote.JMXServiceURL;

public class Client {
...

```

`Client`类将创建 [`JMXConnector`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnector.html) 实例，它需要 [`JMXConnectorFactory`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnectorFactory.html) 和 [`JMXServiceURL`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXServiceURL.html) 。

**创建通知监听器**

JMX客户端需要一个通知处理程序，以侦听和处理可能由在JMX代理的MBean服务器中注册的MBean发送的任何通知。JMX客户端的通知处理程序是 [`NotificationListener`](https://docs.oracle.com/javase/8/docs/api/javax/management/NotificationListener.html) 接口的实例，如下所示：

```java
... 

public static class ClientListener implements NotificationListener {

    public void handleNotification(Notification notification,
            Object handback) {
        echo("\nReceived notification:");
        echo("\tClassName: " + notification.getClass().getName());
        echo("\tSource: " + notification.getSource());
        echo("\tType: " + notification.getType());
        echo("\tMessage: " + notification.getMessage());
        if (notification instanceof AttributeChangeNotification) {
            AttributeChangeNotification acn =
                (AttributeChangeNotification) notification;
            echo("\tAttributeName: " + acn.getAttributeName());
            echo("\tAttributeType: " + acn.getAttributeType());
            echo("\tNewValue: " + acn.getNewValue());
            echo("\tOldValue: " + acn.getOldValue());
        }
    }
}    
...       

```

此通知侦听器确定其收到的任何通知的来源，并检索通知中存储的信息。然后，它根据接收的通知类型对通知信息执行不同的动作。在这种情况下，当侦听器收到 [`AttributeChangeNotification`](https://docs.oracle.com/javase/8/docs/api/javax/management/AttributeChangeNotification.html) 类型的通知时，它将通过调用`AttributeChangeNotification`方法`getAttributeName`，`getAttributeType`，`getNewValue`和`getOldValue`来获取已更改的MBean属性的名称和类型，以及其旧值和新值。

下面的代码创建一个新的 `ClientListener` 实例：

```java
ClientListener listener = new ClientListener();
```

**创建 RMI 连接器客户端**

`Client`类创建一个RMI连接器客户端，该客户端配置为连接到启动JMX代理`Main`时将启动的RMI连接器服务器。这将允许JMX客户端与JMX代理进行交互，就像它们在同一台机器上运行一样。

```java
...
    
public static void main(String[] args) throws Exception {

echo("\nCreate an RMI connector client and " +
    "connect it to the RMI connector server");
JMXServiceURL url = 
    new JMXServiceURL("service:jmx:rmi:///jndi/rmi://:9999/jmxrmi");
JMXConnector jmxc = JMXConnectorFactory.connect(url, null);
...        

```

如您所见， `Client` 定义了一个名为`url`的 [`JMXServiceURL`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXServiceURL.html) ，它表示连接器客户端期望找到连接器服务器的位置。此URL允许连接器客户端从运行在本地主机的端口`9999`上的RMI注册表中检索RMI连接器服务器存根`jmxrmi`，并连接到RMI连接器服务器。

通过这样识别的RMI注册表，可以创建连接器客户端。连接器客户端`jmxc`是 [`JMXConnector`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnector.html) 接口的一个实例，由 [`JMXConnectorFactory`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnectorFactory.html) 的`connect()`方法创建。`connect()`方法在调用时传递参数`url`和`null`环境映射。

**连接到 Remote MBean Server**

在RMI连接到位后，JMX客户端必须连接到远程MBean服务器，以便它可以与远程JMX代理程序在其中注册的各种MBean进行交互。

```java
...
        
MBeanServerConnection mbsc = 
    jmxc.getMBeanServerConnection();
                
...     

```

然后通过调用`JMXConnector`实例`jmxc`的`getMBeanServerConnection()`方法创建名为`mbsc`的 [`MBeanServerConnection`](https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerConnection.html) 实例。

连接器客户端现在连接到由JMX代理创建的MBean服务器，并且可以注册MBean并对它们执行操作，连接对两端保持完全透明。

首先，客户端定义一些简单的操作来发现有关代理的MBean服务器中找到的MBean的信息。

```java
...
        
echo("\nDomains:");
String domains[] = mbsc.getDomains();
Arrays.sort(domains);
for (String domain : domains) {
    echo("\tDomain = " + domain);
}
        
...
        
echo("\nMBeanServer default domain = " + mbsc.getDefaultDomain());

echo("\nMBean count = " +  mbsc.getMBeanCount());
echo("\nQuery MBeanServer MBeans:");
Set<ObjectName> names = 
    new TreeSet<ObjectName>(mbsc.queryNames(null, null));
for (ObjectName name : names) {
    echo("\tObjectName = " + name);
}
      
...
        
```

客户端调用`MBeanServerConnection`的各种方法，以获取运行不同MBean的域，MBean服务器中注册的MBean数，以及它发现的每个MBean的对象名。

**通过代理在 Remote MBeans 上执行操作**

客户端通过创建MBean代理，通过MBean服务器连接访问MBean服务器中的`Hello` MBean。此MBean代理是客户端的本地代理，并模拟远程MBean。

```java
...

ObjectName mbeanName = new ObjectName("com.example:type=Hello");
HelloMBean mbeanProxy = JMX.newMBeanProxy(mbsc, mbeanName, 
                                          HelloMBean.class, true);

echo("\nAdd notification listener...");
mbsc.addNotificationListener(mbeanName, listener, null, null);

echo("\nCacheSize = " + mbeanProxy.getCacheSize());

mbeanProxy.setCacheSize(150);

echo("\nWaiting for notification...");
sleep(2000);
echo("\nCacheSize = " + mbeanProxy.getCacheSize());
echo("\nInvoke sayHello() in Hello MBean...");
mbeanProxy.sayHello();

echo("\nInvoke add(2, 3) in Hello MBean...");
echo("\nadd(2, 3) = " + mbeanProxy.add(2, 3));

waitForEnterPressed();
        
...
        
```

MBean代理允许您通过Java接口访问MBean，允许您在代理上进行调用，而不必编写冗长的代码来访问远程MBean。通过调用`javax.management.JMX`类中的方法`newMBeanProxy()`，向其传递MBean的`MBeanServerConnection`，对象名，MBean接口的类名和`true`，来表示代理必须表现为一个`NotificationBroadcaster` ，从而创建`Hello`的MBean代理。JMX客户端现在可以执行`Hello`定义的操作（如同它们是本地注册的MBean的操作）。JMX客户端还添加了通知侦听器并更改了MBean的`CacheSize`属性，以使其发送通知。

**通过代理在 Remote MXBeans上执行操作**

您可以使用与创建MBean代理完全相同的方式为MXBean创建代理。

```java
...
        
ObjectName mxbeanName = new ObjectName ("com.example:type=QueueSampler");
QueueSamplerMXBean mxbeanProxy = JMX.newMXBeanProxy(mbsc, 
    mxbeanName,  QueueSamplerMXBean.class);
QueueSample queue1 = mxbeanProxy.getQueueSample();
echo("\nQueueSample.Date = " + queue1.getDate());
echo("QueueSample.Head = " + queue1.getHead());
echo("QueueSample.Size = " + queue1.getSize());
echo("\nInvoke clearQueue() in QueueSampler MXBean...");
mxbeanProxy.clearQueue();

QueueSample queue2 = mxbeanProxy.getQueueSample();
echo("\nQueueSample.Date = " +  queue2.getDate());
echo("QueueSample.Head = " + queue2.getHead());
echo("QueueSample.Size = " + queue2.getSize());

...

```

如上所示，要为MXBean创建代理，您所要做的就是调用`JMX.newMXBeanProxy`而不是`newMBeanProxy`。MXBean代理`mxbeanProxy`允许客户端调用`QueueSample` MXBean的操作，就好像它们是本地注册的MXBean的操作一样。

**关闭连接**

一旦JMX客户端获得了所需的所有信息并在远程JMX代理的MBean服务器上的MBean上执行了所有必需的操作，就必须关闭连接。

```
jmxc.close();
```

通过调用 [`JMXConnector.close`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnector.html#close--) 方法关闭连接。

**运行自定义 JMX Client 示例**

This example requires version 6 of the Java SE platform. To monitor the `Main` JMX agent remotely using a custom JMX client [`Client`](https://docs.oracle.com/javase/tutorial/jmx/examples/Client.java), follow these steps:

1. 如果尚未执行此操作，请将`jmx_examples.zip`保存到`work_dir`目录中。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 启动`Main`应用程序，指定公开`Main`以进行远程管理的属性：

   ```
   java -Dcom.sun.management.jmxremote.port=9999 \
        -Dcom.sun.management.jmxremote.authenticate=false \
        -Dcom.sun.management.jmxremote.ssl=false \ 
        com.example.Main
   ```

   生成`Main`正在等待某事发生的确认。

5. 在另一个终端窗口中启动`Client`应用程序：

   ```
   java com.example.Client
   ```

   显示已获取`MBeanServerConnection`的确认。

6. 按Enter键。

   显示由`Main`启动的MBean服务器中注册的所有MBean的域。

7. 再次按Enter键。

   将显示MBean服务器中注册的MBean数，以及所有这些MBean的对象名。显示的MBean包括在Java VM中运行的所有标准平台MXBeans，以及由`Main`在MBean服务器中注册的`Hello` MBean和`QueueSampler` MXBean。

8. 再次按Enter键。

   `Hello` MBeans 的操作由`Client`调用，结果如下：

   - 向`Client`添加通知侦听器以侦听来自`Main`的通知。
   - `CacheSize`属性的值从`200`更改为`150`。
   - 在启动`Main`的终端窗口中，显示`CacheSize`属性更改的确认。
   - 在启动`Client`的终端窗口中，显示`Main`的通知，通知`Client` `ClientSize`属性更改。
   - 调用`Hello` MBean的`sayHello`操作。
   - 在您启动`Main`的终端窗口中，显示消息“Hello world”。
   - 调用`Hello` MBean的`add`操作，值为`2`和`3`作为参数。结果由`Client`显示。

9. 再次按Enter键。

   客户端调用`QueueSampler` MXBean的操作，结果如下：

   - 显示`QueueSample`值`date`，`head`和`size`。
   - 调用`clearQueue`操作。

10. 再次按Enter键。

   `Client` 关闭与MBean服务器的连接，并显示确认。

## 延伸阅读

如果您对此课程有任何意见或建议，请使用我们的 [反馈页面](https://docs.oracle.com/javase/feedback.html) 来告诉我们。

此课程的目的是为您提供JMX技术基本元素的简要介绍。其他地方可以找到更深入的材料。

如果您希望进一步研究JMX技术，以下资源将非常有用：

- [Java SE平台的JMX技术文档](https://docs.oracle.com/javase/8/docs/technotes/guides/jmx/index.html)。JMX技术文档包含在 [Java SE技术文档中](https://docs.oracle.com/javase/)。

- [JMX技术概述](https://docs.oracle.com/javase/8/docs/technotes/guides/jmx/overview/JMXoverviewTOC.html)。JMX技术的Java SE平台文档包含JMX技术概述，该概述提供了比当前路径中提供的更详细的JMX技术描述。

- [JMX技术教程](https://docs.oracle.com/javase/8/docs/technotes/guides/jmx/tutorial/tutorialTOC.html)。此课程中的课程基于JMX技术教程中使用的示例。除了本课程中介绍的基本元素外，JMX技术教程还介绍了JMX技术的更多高级方面。

- 除了上面教程中提供的示例之外，一旦安装了Java Development Kit（JDK）6，就可以在以下目录中找到演示JMX API实际实现的示例应用程序：

  ```
  jdk_home/sample/jmx/jmx-scandir
  ```

  其中的 `jdk_home` 表示JDK软件的安装目录。`jmx-scandir` 是一个高级示例，它在实际场景中提供了JMX API的高级概念。

- [Java平台的监视和管理](https://docs.oracle.com/javase/8/docs/technotes/guides/management/)。为监控和管理Java SE平台而提供的技术和API在很大程度上依赖于JMX技术。“ *Java SE监视和管理指南”*包含有关[使用JMX技术](https://docs.oracle.com/javase/8/docs/technotes/guides/management/agent.html)进行[监视和管理](https://docs.oracle.com/javase/8/docs/technotes/guides/management/agent.html)的章节 。

- [Java管理扩展（JMX）技术](http://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html)。JMX技术主页是获取有关JMX技术的所有最新新闻的地方。


# Java命名和目录接口

此课程描述了JNDI™（Java命名和目录接口），用于访问目录和命名服务的API。在这里，您将了解基本的命名和目录服务，以及如何使用JNDI编写简单的应用程序来使用这些服务。最流行的目录服务LDAP用于说明使用JNDI来访问目录服务。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**命名和目录概念**](https://docs.oracle.com/javase/tutorial/jndi/concepts/index.html) 从此处开始，了解命名和目录概念的概述。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**JNDI概述**](https://docs.oracle.com/javase/tutorial/jndi/overview/index.html) 为您提供JNDI及其架构和包装的概述。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**软件设置**](https://docs.oracle.com/javase/tutorial/jndi/software/index.html) 描述设置运行此课程中描述的示例以及任何其他JNDI应用程序所需的环境所涉及的说明和步骤。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**命名和目录操作**](https://docs.oracle.com/javase/tutorial/jndi/ops/index.html) 描述各种命名和目录操作，并通过大量使用JNDI访问命名/目录服务的示例来演示它们。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**LDAP用户的高级主题**](https://docs.oracle.com/javase/tutorial/jndi/ldap/index.html) LDAP用户的专业课程。它讨论了如何将JNDI建模为LDAP API，如何在生产环境中执行LDAP身份验证，SSL和管理连接。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**访问目录中的对象**](https://docs.oracle.com/javase/tutorial/jndi/objects/index.html) 显示如何将应用程序与目录集成，以便可以在目录中存储和检索Java对象。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**JDK 5.0和JDK 6中的功能介绍**](https://docs.oracle.com/javase/tutorial/jndi/newstuff/index.html) **JDK 5.0和JDK 6**中可用的JNDI和LDAP服务提供程序中的功能。

------

**注意：**本教程的基础是位于 <https://docs.oracle.com/javase/jndi/tutorial/> 的独立JNDI教程。最后在Java 2 SDK标准版v 1.4.2下更新的独立JNDI教程提供了有关JNDI的全面内容，但不再受支持。本教程摘录了standlone教程的基础知识，并包含Java平台标准版5.0和6版本中添加到JNDI的功能。

旧的JNDI教程在 [docs.oracle.com](https://docs.oracle.com/javase/jndi/tutorial/) 上保存为存档。

## 名称和目录概念

**命名概念**

任何计算机系统中的一个基础设施就是所谓的*命名服务*——将名称关联到对象，因而对象可以基于它们的名称被找到。在使用任何计算机程序或者系统时，你始终都会不断命名一个又一个对象。比如，当你使用一个电子邮件系统时，你必须提供收件人姓名。围殴了访问计算机中的文件，你必须提供文件名。命名服务允许你通过名称来查询对象。

![A name is used to reference an object.](https://docs.oracle.com/javase/tutorial/figures/jndi/naming-system.gif)

命名服务的最主要功能就是将人类友好的名称映射到对象，比如一个地址、标识符、或者计算机程序使用的对象。

比如，[Internet Domain Name System (DNS)](http://www.ietf.org/rfc/rfc1034.txt) 将机器名称映射到 IP 地址：

```
www.example.com ==> 192.0.2.5
```

文件系统将文件名映射到文件引用，程序可以使用文件名访问该文件的内容。

```
c:\bin\autoexec.bat ==> File Reference
```

这两个例子也展示了存在命名服务的广泛范围——从命名Internet上的对象到命名本地文件系统上的文件。

**名称**

为了在命名系统中查找对象，你给出对象的名称。命名系统决定了名称必须遵循的语法规则。该语法有时候被称为时命名系统的*命名约定*。一个名称有若干组成部分。名称的表示由标记名称组件的组件分隔符组成。

| Naming System    | Component Separator | Names                       |
| ---------------- | ------------------- | --------------------------- |
| UNIX file system | "/"                 | /usr/hello                  |
| DNS              | "."                 | sales.Wiz.COM               |
| LDAP             | "," and "="         | cn=Rosanna Lee, o=Sun, c=US |

UNIX文件系统的命名约定是文件是从其相对于文件系统根目录的路径命名的，路径中的每个组件都使用正斜杠字符（“/”）从左到右分隔。例如，UNIX路径名`/usr/hello`在文件目录`usr`中命名文件`hello`，该目录位于文件系统的根目录中。

DNS命名约定要求DNS名称中的组件从右到左排序，并由点字符（“.”）分隔。因此DNS名称`sales.Wiz.COM`命名一个名为`sales`的DNS条目，相对于DNS条目`Wiz.COM`。反过来，DNS条目`Wiz.COM`就是在`COM`条目中命名名为`Wiz`的条目。

[Lightweight Directory Access Protocol (LDAP)](http://www.ietf.org/rfc/rfc2251.txt) 命名约定名称组件顺序从右到左排列，使用逗号`,`分隔。因此 LDAP 名称`cn=Rosanna Lee, o=Sun, c=US`命名一个 LDAP 实体`cn=Rosanna Lee`，相对于实体`o=Sun`，反过来，相对于 `c=US`。LDAP 的另外一条命名规则就是每个名称组件必须是名/值对，其中名称和取值以等号`=`分隔。

**绑定**

名称与对象的关联被称为*绑定*。一个文件名被绑定到一个文件。

DNS 包含机器名称映射到 IP 地址的绑定。一个 LDAP 名称被绑定到一个 LDAP 实体。

**引用和地址**

依赖于命名服务，某些对象不能直接由命名服务存储，也就是说，对象的一份副本都能放在命名服务内部。相反，它们必须通过引用存储，也就是说，在命名服务中放置对象的*指针*或者*引用*。引用表达如何访问该对象的信息。典型地，它是一种紧凑的表示，可以被用于对象通信，对象本身可能包含更完整的状态信息。使用一弄，你可以联系对象并获取对象的更多信息。

例如，飞机对象可能包含飞机乘客和机组人员的列表，飞行计划，燃料和仪表状态，以及航班号和起飞时间。相比之下，飞机对象引用可能仅包含其航班号和起飞时间。该引用是关于飞机对象的信息的更紧凑的表示，并且可以用于获得附加信息。又例如，使用文件引用访问文件对象。又例如，打印机对象可能包含打印机的状态，例如其当前队列和纸盘中的纸张数量。另一方面，打印机对象引用可能仅包含有关如何到达打印机的信息，例如其打印服务器名称和打印协议。

尽管通常引用能够包含任意信息，将其内容视为*地址*（或者通信端点）还是有用的：也就是关于如何访问对象的特定信息。

为了简单，在不需要明确区分的情况下，本教程使用“对象”表示对象和对象引用。

**上下文**

*上下文*是名称—对象的绑定集合。每个上下文都有相应的命名约定。上下文始终会提供一个查找（解析）操作，该操作返回对象，典型地，它还提供诸如绑定名称、解绑名称、以及列出绑定名称等操作。上下文对象中的名称能够被绑定到另一个具有相同命名约定的上下文对象（称为*子上下文*）。

![Several examples of contexts, bound to subcontexts.](https://docs.oracle.com/javase/tutorial/figures/jndi/context.gif)

UNIX文件系统中的文件目录（例如`/usr`）表示上下文。相对于另一个文件目录命名的文件目录表示子上下文（UNIX用户将其称为子目录）。也就是说，在文件目录`/usr/bin`中，目录`bin`是`usr`的子上下文。DNS域（例如`COM`）表示上下文。相对于另一个DNS域命名的DNS域表示子上下文。对于DNS域`Sun.COM`，DNS域`Sun`是`COM`的子上下文。

最后，LDAP条目（例如`c=us`）表示上下文。相对于另一个LDAP条目命名的LDAP条目表示子上下文。对于LDAP条目`o=sun, c=us`，条目`o=sun`是`c=us`的子上下文。

**名称系统和命名空间**

*命名系统*是相同类型的相互连接的一组上下文（它们具有相同的命名约定）并提供一组通用操作。

实现DNS的系统是命名系统。使用LDAP进行通信的系统是命名系统。

命名系统为其客户提供*命名服务*，以执行与命名相关的操作。命名服务通过其自己的接口访问。DNS提供命名服务，将机器名称映射到IP地址。LDAP提供了一个命名服务，可将LDAP名称映射到LDAP条目。文件系统提供命名服务，将文件名映射到文件和目录。

命名空间是命名系统中所有可能名称的集合。UNIX文件系统具有一个名称空间，该名称空间由该文件系统中的所有文件和目录名称组成。DNS命名空间包含DNS域和条目的名称。LDAP名称空间包含LDAP条目的名称。

### 目录概念

很多命名服务都使用*目录服务*进行了扩展。目录服务将名称关联到对象，同时还将这些对象关联到一些*属性*。

目录服务 = 命名服务 + 对象包含的属性。

你不仅可以通过名称查找对象，还可以获得对象的属性，或者基于属性搜索对象。

![Diagram showing a directory system: a name references a directory object which contains attributes.](https://docs.oracle.com/javase/tutorial/figures/jndi/directory-system.gif)

一个例子是电话公司的目录服务。它将用户的姓名映射到他的地址和电话号码。计算机的目录服务非常类似于电话公司的目录服务，因为它们都可用于存储诸如电话号码和地址之类的信息。然而，计算机的目录服务功能更强大，因为它可以在线获得，并且可以用于存储可供用户，程序甚至计算机本身和其他计算机使用的各种信息。

*目录对象*表示计算环境中的一个对象。目录对象可以被用于，诸如，表示打印机、人、计算机、或者一个网络。目录对象包含描述它所表示的对象的*属性*。

**属性**

目录对象可以具有属性。例如，打印机可能由目录对象表示，该目录对象具有其速度，分辨率和颜色作为属性。用户可能由目录对象表示，该目录对象具有用户的电子邮件地址，各种电话号码，邮政地址和计算机帐户信息作为属性。

属性具有属性标识符和一组属性值。属性标识符是标识独立于其值的属性的标记。例如，两个不同的计算机帐户可能具有`"mail"`属性；`"mail"`是属性标识符。属性值是属性的内容。例如，电子邮件地址可能包含：

```
Attribute Identifier : Attribute Value
                 mail   john.smith@example.com
```

**目录和目录服务**

*目录*是一组相互连接的目录对象。目录服务是一种服务，它提供用于创建，添加，删除和修改与目录中的对象关联的属性的操作。该服务通过自己的接口访问。

存在许多目录服务的例子。

- 网络信息服务（NIS）
  NIS是UNIX操作系统上可用的目录服务，用于存储与系统相关的信息，例如与机器，网络，打印机和用户相关的信息。
- [Oracle Directory Server](http://www.oracle.com/technetwork/testcontent/index-085178.html)
  Oracle Directory Server是基于Internet标准LDAP的通用目录服务。

**搜索服务**

您可以通过将目录对象的名称提供给目录服务来查找目录对象。或者，许多目录（例如基于LDAP的目录）支持搜索的概念。搜索时，不能提供名称，而是提供由逻辑表达式组成的查询，在该表达式中指定一个或多个对象必须具有的属性。该查询称为搜索过滤器。这种搜索方式有时称为反向查找或基于内容的搜索。目录服务搜索并返回满足搜索过滤器的对象。

例如，您可以查询目录服务以查找：

- 属性`"age"`超过 40 的所有用户。
- 所有 IP 地址以`"192.113.50"`开头的机器。

**组合命名和目录服务**

目录通常将其对象排列在层次结构中。例如，LDAP将所有目录对象排列在树中，称为*目录信息树（DIT）*。例如，在DIT中，组织对象可能既包含人员对象又包含组对象。当以这种方式排列目录对象时，除了属性容器之外，它们还起到命名上下文的作用。

## JNDI 概述

Java命名和目录接口（JNDI）是一种应用程序编程接口（API），它为使用Java™编程语言编写的应用程序提供 [命名](https://docs.oracle.com/javase/tutorial/jndi/overview/naming.html) 和 [目录](https://docs.oracle.com/javase/tutorial/jndi/overview/dir.html) 功能。它被定义为独立于任何特定的目录服务实现。因此，可以以通用方式访问各种目录 - 新的，出现的和已经部署的目录。

**架构**

JNDI体系结构由API和服务提供者接口（SPI）组成。Java应用程序使用JNDI API来访问各种命名和目录服务。SPI允许透明地插入各种命名和目录服务，从而允许使用JNDI API的Java应用程序访问其服务。见下图：

![JNDI Architecture](https://docs.oracle.com/javase/tutorial/figures/jndi/jndiarch.gif)

**包**

JNDI包含在Java SE平台中。要使用JNDI，您必须具有JNDI类和一个或多个服务提供者。JDK包括以下命名/目录服务的服务提供者：

- 轻量级目录访问协议（LDAP）
- 公共对象请求代理体系结构（CORBA）公共对象服务（COS）名称服务
- Java远程方法调用（RMI）注册表
- 域名服务（DNS）

其它服务提供者可以从 [JNDI page](http://www.oracle.com/technetwork/java/jndi/index.html) 下载或者从各自厂商获得。

JNDI 被分为 5 个包：

- [javax.naming](https://docs.oracle.com/javase/tutorial/jndi/overview/naming.html)
- [javax.naming.directory](https://docs.oracle.com/javase/tutorial/jndi/overview/dir.html)
- [javax.naming.ldap](https://docs.oracle.com/javase/tutorial/jndi/overview/dir.html)
- [javax.naming.event](https://docs.oracle.com/javase/tutorial/jndi/overview/event.html)
- [javax.naming.spi](https://docs.oracle.com/javase/tutorial/jndi/overview/event.html)

接下面的部分简要介绍了各个 JNDI 包。

### Naming 包

[`javax.naming`](https://docs.oracle.com/javase/8/docs/api/javax/naming/package-summary.html) 包包含访问命名服务的类和接口。

**上下文**

`javax.naming` 包定义一个 [`Context`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html) 接口，它是查找，绑定/解绑，重命名对象，创建和销毁子上下文等功能的核心接口。

- Lookup

  最常用的操作就是 [`lookup()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html#lookup-javax.naming.Name-) 。你将查找的对象的名称传递给 `lookup()` 方法，它将返回绑定到该名称的对象。

- Bindings

  [`listBindings()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html#listBindings-javax.naming.Name-) 返回一个名称—对象映射的枚举。一个绑定时一个三元组，包含对象名称，对象类名，以及对象自身。

- List

  [`list()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html#list-javax.naming.Name-) 类似于 `listBindings()` ，除了它返回一个包含对象名称和对象类名的枚举。`list()` 对应用非常有用，例如浏览器希望获取上下文中绑定的对象信息，但是又不需要实际的对象本身。尽管 `listBindings()` 提供了全部的相同信息，但是它是一个潜在的更加昂贵的操作。

- Name

  `Name` 是一个表示通用名称—零个或者多个组件的有序序列的接口。命名系统使用此接口来定义遵循它的命名约定的名称。命名约定在后续的 [Naming and Directory Concepts](https://docs.oracle.com/javase/tutorial/jndi/concepts/index.html) 中描述。

- References

  对象以不同方式存储在命名和目录服务中。引用可能是对象的非常紧凑的表示。JNDI定义 [`Reference`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Reference.html) 类来表示引用。引用包含有关如何构造对象副本的信息。JNDI将尝试将从目录中查找的引用转换为它们所代表的Java对象，以便JNDI客户端可以安全地认为目录中存储的内容是Java对象。

**初始上下文**

在JNDI中，所有命名和目录操作都是相对于上下文执行的。没有绝对的根。因此，JNDI定义了一个`InitialContext`，它为命名和目录操作提供了一个起点。获得初始上下文后，可以使用它来查找其他上下文和对象。

**异常**

JNDI定义了在执行命名和目录操作过程中可以抛出的异常的类层次结构。此类层次结构的根是`NamingException`。对处理特定异常感兴趣的程序可以捕获异常的相应子类。否则，应该捕获`NamingException`。

### Directory 和 LDAP 包

**Directory 包**

[`javax.naming.directory`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/package-summary.html) 包扩展了 [`javax.naming`](https://docs.oracle.com/javase/8/docs/api/javax/naming/package-summary.html) 包，在命名服务基础上提供了访问目录服务的功能。此包允许应用程序存储在目录中的相关对象以及使用特定属性搜索对象。

**Directory 上下文**

[`DirContext`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html) 接口表示*目录上下文*。通过扩展 [`Context`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html) 接口，`Dircontext` 的行为就像一个名称上下文。这就意味着任何目录对象也可以提供命名上下文。它定义检查和更新目录实体的相关属性的方法。

- 属性

  你使用 [`getAttributes()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html#getAttributes-javax.naming.Name-) 方法来获取目录实体（需要你给定名称）的相关属性。属性可以使用 [`modifyAttributes()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html#modifyAttributes-javax.naming.Name-javax.naming.directory.ModificationItem:A-) 方法修改。你可以使用该操作添加、替换、或者而删除属性和/或属性值。

- 搜索

  `DirContext`包含用于执行基于内容的目录搜索的方法。在最简单和最常见的使用形式中，应用程序指定一组属性，这些属性可能具有匹配的特定值，并将此属性集提交给 [`search()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html#search-javax.naming.Name-javax.naming.directory.Attributes-) 方法。其他重载形式的 [`search()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html#search-javax.naming.Name-javax.naming.directory.Attributes-) 支持更复杂的搜索过滤器。

**LDAP 包**

 [`javax.naming.ldap`](https://docs.oracle.com/javase/8/docs/api/javax/naming/ldap/package-summary.html) 包中包含用于使用特定于 [LDAP v3](http://www.ietf.org/rfc/rfc2251.txt) 的功能的类和接口，这些功能尚未包含在更通用的 [`javax.naming.directory`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/package-summary.html) 包中。事实上，大多数使用LDAP的JNDI应用程序都会找到足够的`javax.naming.directory`包，根本不需要使用`javax.naming.ldap`包。此程序包主要用于需要使用“扩展”操作，控件，或未经请求的通知的应用程序。

- ”扩展“操作

  除了指定定义良好的操作（如搜索和修改）之外， [LDAP v3 (RFC 2251)](http://www.ietf.org/rfc/rfc2251.txt) 还指定了在LDAP客户端和服务器之间传输尚未定义的操作的方法。这些操作称为“扩展”操作。“扩展”操作可以由诸如因特网工程任务组（IETF）之类的标准组织或由供应商定义。

- 控件

   [LDAP v3](http://www.ietf.org/rfc/rfc2251.txt) 允许任何请求或响应通过尚未定义的修饰符（称为控件）进行扩充。与请求一起发送的控件是请求控件，而与响应一起发送的控件是响应控件。控件可以由诸如IETF的标准组织或由供应商定义。请求控件和响应控件不一定是成对的，也就是说，不需要为发送的每个请求控件都有响应控件，反之亦然。

- 未经请求的通知

  除了客户端和服务器之间正常的请求/响应交互方式之外， [LDAP v3](http://www.ietf.org/rfc/rfc2251.txt) 还指定了未经请求的通知 - 从服务器异步发送到客户端而不是响应任何客户端请求的消息。

**LDAP 上下文**

[`LdapContext`](https://docs.oracle.com/javase/8/docs/api/javax/naming/ldap/LdapContext.html) 接口表示用于执行“扩展”操作，发送请求控件和接收响应控件的上下文。JNDI教程的 [Controls and Extensions](https://docs.oracle.com/javase/jndi/tutorial/ldap/ext/index.html) 课程中介绍了如何使用这些功能的示例。

### Event 和服务提供者包

**Event 包**

 [`javax.naming.event`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/package-summary.html) 包中包含用于支持命名和目录服务中的事件通知的类和接口。事件通知在 [Event Notification](https://docs.oracle.com/javase/tutorial/jndi/overview/event.html) 中详细描述。

- 事件
   [`NamingEvent`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/NamingEvent.html) 表示由命名/目录服务生成的事件。该事件包含标识事件类型的类型。例如，事件类型分为影响命名空间的事件类型，例如“对象被添加”，和不影响命名空间的事件类型，例如“对象已更改”。
- 监听器
   [`NamingListener`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/NamingListener.html) 是一个监听`NamingEvents`的对象。每种类型的事件类型都有相应类型的`NamingListener`。例如， [`NamespaceChangeListener`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/NamespaceChangeListener.html) 表示对命名空间更改事件感兴趣的侦听器， [`ObjectChangeListener`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/ObjectChangeListener.html) 表示对对象更改事件感兴趣的侦听器。

要接收事件通知，必须使用 [`EventContext`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/EventContext.html) 或 [`EventDirContext`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/EventDirContext.html) 注册侦听器。注册后，当命名/目录服务中发生相应的更改时，侦听器将接收事件通知。有关事件通知的详细信息，请参阅 [JNDI Tutorial](https://docs.oracle.com/javase/jndi/tutorial/beyond/event/index.html) 。

**服务提供者包**

 [`javax.naming.spi`](https://docs.oracle.com/javase/8/docs/api/javax/naming/spi/package-summary.html) 包提供了不同命名/目录服务提供者的开发人员可以开发和连接其实现的方法，以便可以从使用JNDI的应用程序访问相应的服务。

- 插件架构
  `javax.naming.spi`包允许动态插入不同的实现。这些实现包括 [initial context](https://docs.oracle.com/javase/tutorial/jndi/ops/index.html) 和可以从初始上下文到达的上下文的实现。
- Java对象支持
  `javax.naming.spi`包支持 [lookup](https://docs.oracle.com/javase/tutorial/jndi/ops/lookup.html) 和相关方法的实现，以返回Java程序员自然而直观的Java对象。例如，如果从目录中查找打印机名称，那么您可能希望找回要在其上运行的打印机对象。这种支持以对象工厂的形式提供。该软件包还支持反向操作。也就是说， [`Context.bind()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html#bind-javax.naming.Name-java.lang.Object-) 和相关方法的实现者可以接受Java对象并以底层命名/目录服务可接受的格式存储对象。这种支持以 [state factories](https://docs.oracle.com/javase/tutorial/jndi/objects/index.html#STATEFAC) 的形式提供。
- 多个命名系统（联合）
  JNDI操作允许应用程序提供跨多个命名系统的名称。在完成操作的过程中，一个服务提供者可能需要与另一个服务提供者交互，例如传递要在下一个命名系统中继续的操作。该软件包支持不同的提供商合作完成JNDI操作。

有关服务提供者机制的详细信息，请参阅 [JNDI Tutorial](https://docs.oracle.com/javase/jndi/tutorial/provider/index.html) 。

## 软件设置

**需要的软件**

下面是你需要的软件/系统的列表：

- [Java 平台软件](https://docs.oracle.com/javase/tutorial/jndi/software/index.html#JDK)
- [服务提供者软件](https://docs.oracle.com/javase/tutorial/jndi/software/index.html#PROVIDER)
- [命名和目录服务器软件](https://docs.oracle.com/javase/tutorial/jndi/software/index.html#SERVER)

------

**Java 平台软件**

JNDI 包含在 Java SE Platform 中。

要运行 applet，您可以使用任何兼容 Java 的 Web 浏览器，例如 Firefox 或 Internet Explorer v5 或更高版本。为确保您的 applet 充分利用 Java 平台软件的最新功能，您可以在 Web 浏览器中使用 Java Plug-in。

**服务提供者软件**

JNDI API 是用于访问任何命名或目录服务的通用 API。通过在 JNDI下 插入服务提供程序，可以实现对命名或目录服务的实际访问。有关 JNDI 体系结构和服务提供者角色的概述，请参阅 [JNDI概述](https://docs.oracle.com/javase/tutorial/jndi/overview/index.html) 课程。

*服务提供者*是将 JNDI API 映射到命名或目录服务器的实际调用的软件。通常，服务提供者的角色与命名/目录服务器的角色不同。在客户端/服务器软件的术语中，JNDI 和服务提供者是*client*（称为*JNDI客户端*），命名/目录服务器是*server*。

客户端和服务器可以以多种方式进行交互。在一种常见的方式中，它们使用网络协议，以便客户端和服务器可以在网络环境中自主存在。只要客户端符合指定的协议，服务器通常支持许多不同的客户端，而不仅仅是 JNDI 客户端。 JNDI 没有规定 JNDI 客户端和服务器之间的任何特定交互方式。例如，极端情况下，客户端和服务器可以是同一个实体。

您需要获取将要使用的服务提供者的类。例如，如果您计划使用 JNDI 访问 LDAP 目录服务器，则需要 LDAP 服务提供程序的软件。

JDK 附带以下服务提供者：

- 轻量级目录协议（LDAP）
- CORBA 通用对象服务命名（COS 命名）
- RMI 注册
- 域名服务（DNS）

如果您对其他服务提供者感兴趣，请查看 [JNDI页面](http://www.oracle.com/technetwork/java/jndi/index.html) 获取下载信息。

本教程仅使用LDAP服务提供程序。 使用LDAP服务提供程序时，您需要设置自己的服务器或访问现有服务器，如下所述。

**命名和目录服务器软件**

获得服务提供商软件后，您需要设置或访问相应的命名/目录服务器。设置命名/目录服务器通常是网络系统管理员的工作。不同的供应商的命名/目录服务器具有不同的安装过程。有些需要特殊的机器权限才能安装服务器。您应该参考命名/目录服务器软件的安装说明。

对于本教程中的目录示例，您需要访问 LDAP 服务器。如果您想快速浏览一下 LDAP 检查的内容 [这里](http://en.wikipedia.org/wiki/LDAP) 。您可以使用您选择的任何 LDAP 兼容服务器。在许多平台（包括 Windows）上运行的 Oracle Directory Server 可在以下位置获取评估版本：[Oracle Directory Server](http://www.oracle.com/technetwork/testcontent/index-085178.html) 。

你也可以从下面地址下载免费的 LDAP 服务器：

- [OpenDS](http://opends.java.net/)
- [OpenLDAP](http://www.openldap.org/)
- [389 Directory Server](http://directory.fedoraproject.org/)
- [Apache Directory Server](http://directory.apache.org/)

一个可公开访问的服务器地址：[http://www.openldap.org/lists/#openldap-software](http://www.openldap.org/lists/#openldap-software) 。

### LDAP 设置

以下是构建访问 LDAP 目录服务器的 Java 应用程序所涉及的步骤。

1.安装 [Java Platform](https://docs.oracle.com/javase/tutorial/jndi/software/content.html) 软件。
2.获取 [之前](https://docs.oracle.com/javase/tutorial/jndi/software/index.html#SERVER) 中讨论的目录服务器软件。
3.使用所需的架构配置目录服务器。要使用本教程中的示例，需要在服务器上配置特殊的 [schema](https://docs.oracle.com/javase/tutorial/jndi/software/content.html#SCHEMA) 。
4.使用所需内容填充目录服务器。要使用本教程中的示例，需要在服务器上填充特殊的 [content](https://docs.oracle.com/javase/tutorial/jndi/software/content.html#LDIF) 。
5.编写 JNDI 应用程序以访问目录，编译并运目录服务器以获得所需的结果。 JNDI 示例将在 [下一课](https://docs.oracle.com/javase/tutorial/jndi/ops/index.html) 中介绍。

前两个步骤在上一节中介绍。本课程的其余部分将讨论步骤三和步骤四。涉及编写 JNDI 应用程序的步骤五将在下一课中介绍，该课程将介绍如何编写 JNDI 应用程序以对目录执行各种操作。

一旦您设置了目录，或者已经指示您的程序与现有目录进行通信，您可以在那里找到哪种信息？

可以将目录视为由名称到对象绑定组成。 也就是说，目录中的每个对象都具有相应的名称。您可以通过查找其名称来检索目录中的对象。

存储在目录中的还有属性。除了具有名称之外，目录中的对象还具有可选的属性集。您可以向目录询问对象的属性，并要求它搜索具有某些属性的对象。

**步骤3：目录模式**

模式指定目录可能包含的对象类型。本教程使用条目填充目录，其中一些条目需要特殊的模式定义。要容纳这些条目，您必须首先关闭服务器中的模式检查，或者将本教程附带的模式文件添加到服务器。这两项任务通常由目录服务器的管理员执行。

本教程附带两个必须安装的模式文件：

- [`Schema for Java objects`](https://docs.oracle.com/javase/tutorial/jndi/software/config/java.schema)
- [`Schema for CORBA objects`](https://docs.oracle.com/javase/tutorial/jndi/software/config/corba.schema)

这些文件的格式是正式描述，可能无法直接复制并粘贴到服务器配置文件中。具体地，属性语法以 [RFC 2252](http://www.ietf.org/rfc/rfc2252.txt) 的形式描述。

不同的目录服务器具有不同的配置其架构的方式。本教程包含一些用于在目录服务器上安装 Java 和 CORBA 模式的工具，这些模式允许通过 LDAP 修改其模式。以下是工具可以执行的任务列表。

1. [`Create Java Schema`](https://docs.oracle.com/javase/tutorial/jndi/software/config/CreateJavaSchema.java)
2. [`Create CORBA Schema`](https://docs.oracle.com/javase/tutorial/jndi/software/config/CreateCorbaSchema.java)

按照随附的 [`README文件`](https://docs.oracle.com/javase/tutorial/jndi/software/config/README-SCHEMA.TXT) 中的说明运行这些程序。

------

**注意：Windows Active Directory。**Active Directory 使用内部格式管理其架构。若要更新架构，可以按照Active Directory 的说明使用 Active Directory 管理控制台管理单元，`ADSIEdit`或`CreateJavaSchema`实用程序。

------

**步骤4：为此指引提供目录内容**

在此课程的示例中，显示的结果反映了如何使用配置文件设置 LDAP 目录（[`tutorial.ldif`](https://docs.oracle.com/javase/tutorial/jndi/software/config/tutorial.ldif) ）。如果您使用的是现有服务器或具有不同设置的服务器，则可能会看到不同的结果。在将配置文件（[`tutorial.ldif`](https://docs.oracle.com/javase/tutorial/jndi/software/config/tutorial.ldif) ）加载到目录服务器之前，必须遵循有关更新服务器架构的说明，或者您可以在 UNIX 系统上使用 *ldapadd* 或 *ldapmodify* 命令（如果可用）。

例如，您可以使用 ldapmodify（通过插入适当的主机名值，管理员DN（-D选项）和密码）：

```
ldapmodify -a -c -v -h hostname -p 389\
        -D "cn=Administrator, cn=users, dc=xxx, dc=xxx"\
        -w passwd -f tutorial.ldif
```

------

**安装注意：访问控制。**不同的目录服务器以不同方式处理访问控制。本教程中的一些示例执行目录的更新。此外，您安装教程的命名空间部分可能具有读取访问限制。因此，您需要采取特定于服务器的操作来使目录可读和/或可更新，以使这些示例起作用。对于 [Oracle Directory Server](http://www.oracle.com/technetwork/testcontent/index-085178.html) ，添加 [`sunds.aci.ldif`](https://docs.oracle.com/javase/tutorial/jndi/software/config/sunds.aci.ldif) 中建议的`aci`条目文件到 `dn: o=JNDITutorial` 条目，使整个目录可读和可更新。或者，您可以更改示例，以便它们对目录进行身份验证。有关如何执行此操作的详细信息，请参阅 [安全](https://docs.oracle.com/javase/tutorial/jndi/ldap/security.html) 课程。

**安装注意：名称空间设置。**  [`tutorial.ldif`](https://docs.oracle.com/javase/tutorial/jndi/software/config/tutorial.ldif) 文件中的条目使用尊贵名称（DN）“o=JNDITutorial”用于根命名上下文。如果您尚未将目录服务器配置为将“o=JNDITutorial”作为根命名上下文，则导入`tutorial.ldif`的尝试将失败。解决此问题的最简单方法是将现有根命名上下文的DN添加到`tutorial.ldif`文件中的每个“dn:”行。例如，如果您的服务器已经具有根命名上下文“dc=imc,dc=org”，那么您应该更改该行

```
dn: o=JNDITutorial
```

为

```
dn: o=JNDITutorial, dc=imc, dc=org
```

对文件中以“dn:”开头的每一行进行此更改。然后，在本教程的所有示例中，无论使用“o=JNDITutorial”，请使用“o=JNDITutorial,dc=imc,dc=org”。

**安装说明：文件格式。**根据您使用的操作系统平台，您可能需要编辑`tutorial.ldif`，以便它包含该平台的正确换行符。例如，如果您发现`tutorial.ldif`包含 Windows 样式的换行符（CRLF），并且您要将此文件导入到在 UNIX 平台上运行的目录服务器，则需要编辑该文件并将 CRLF 替换为 LF。此问题的一个症状是目录服务器拒绝`tutorial.ldif`中的所有条目。

**安装说明：Windows Active Directory。**

1. 根命名上下文不会是“o=jnditutorial”。它的形式为“dc=x,dc=y,dc=z”。您需要按照之前的**Namespace Setup**说明进行操作。

2. 使用 Active Directory 管理控制台管理单元`ADSIEdit`将“inetOrgPerson”和“groupOfUniqueNames”的对象类和相关属性添加到 Active Directory 架构。“groupOfUniqueNames”在 [RFC 2256](http://www.ietf.org/rfc/rfc2256.txt) 中定义，“inetOrgPerson”在 [RFC 2798](http://www.ietf.org/rfc/rfc2798.txt) 中定义。

3. 默认情况下，Active Directory 中不允许使用本教程使用的某些层次关系。要启用这些关系，请使用 Active Directory 管理控制台管理单元`ADSIEdit`添加它们。

   ```
   objectclass: organizationalUnit
   possible superiors: domainDNS
                       inetOrgPerson
                       organizaton
                       organizationalPerson
                       organizationalUnit
                       person
                       top
   
   objectclass: groupOfUniqueNames
   possible superiors: top
   
   objectclass: inetOrgPerson
   possible superiors: container
                       organizationalPerson
                       person
                       top
   ```

4. 从`tutorial.ldif`中的 Mark Twain 条目中删除两个“sn”属性中的一个。与 [RFC 2256](http://www.ietf.org/rfc/rfc2256.txt) 相反，Active Directory 将“sn”定义为单值属性。

5. 使用`dcifde`command-line实用程序加载修改后的`tutorial.ldif`文件。

   ```
   #ldif -i -v -k -f tutorial.ldif
   ```

6. 大多数示例假定已将目录设置为允许未经身份验证的读取和更新访问。您的 Active Directory 设置可能不允许您这样做。 请参阅**Access Control**安装说明。

7. 读取条目有时会产生比教程中显示的更多的属性，因为 Active Directory 通常会返回一些内部属性。

8. 创建条目可能需要指定其他特定于Active Directory的属性或使用其他对象类。

### Java 应用设置

为了在你的应用中使用 JNDI，你需要配置它的编译和执行环境。

**导入 JNDI 类**

下面是 JNDI 包：

- [`javax.naming`](https://docs.oracle.com/javase/8/docs/api/javax/naming/package-summary.html)
- [`javax.naming.directory`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/package-summary.html)
- [`javax.naming.event`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/package-summary.html)
- [`javax.naming.ldap`](https://docs.oracle.com/javase/8/docs/api/javax/naming/ldap/package-summary.html)
- [`javax.naming.spi`](https://docs.oracle.com/javase/8/docs/api/javax/naming/spi/package-summary.html)

此课程中的示例使用前两个包中的类和接口。您需要将这两个包导入您的程序或导入您使用的各个类和接口。以下两行从两个包`javax.naming`和`javax.naming.directory`导入所有类和接口。

```java
import javax.naming.*;
import javax.naming.directory.*;
```

**编译环境**

要编译使用 JNDI 的程序，您需要访问 JNDI 类。[Java SE 6](https://docs.oracle.com/javase/tutorial/jndi/software/package.html) 已经包含了 JNDI 类，因此如果您正在使用它，则无需采取进一步的操作。

**执行环境**

要运行使用 JNDI 的程序，您需要访问程序使用的任何服务提供程序的 JNDI 类和类。[Java Runtime Environment（JRE）6](https://docs.oracle.com/javase/tutorial/jndi/software/package.html) 已经包含用于 LDAP，COS 命名，RMI 注册的服务提供程序、 JNDI 类和DNS。

如果您正在使用其他服务提供程序，则需要在 *JAVA_HOME*`/jre/lib/ext` 目录中下载并安装其存档文件，其中*JAVA_HOME* 是包含 JRE 的目录。[JNDI页面](http://www.oracle.com/technetwork/java/jndi/index.html#download) 列出了一些服务提供者。您可以下载这些提供者或使用其他供应商的提供者。

----

此处略去一些章节

----

# RMI

Java 远程方法调用 (RMI) 系统允许运行在一个 Java 虚拟机中的对象调用运行在另一个 Java 虚拟机中的对象。RMI 为使用 Java 语言编写的程序提供了远程通信。

------

**注意：** 如果你想要与一个现存的 IDL 程序通信，那么你应该使用 Java IDL 而不是 RMI。

------

本课程提供了 RMI 系统的简要介绍，然后深入一个完整的客户端/服务器示例，该示例使用了 RMI 的独特能力在运行时加载并执行用户自定义的任务。例子中的服务器实现了通用计算引擎，客户端使用它来计算 ![the pi symbol](https://docs.oracle.com/javase/tutorial/figures/rmi/pi.gif) 的值。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**RMI 应用概览**](https://docs.oracle.com/javase/tutorial/rmi/overview.html) 描述 RMI 系统并列出它的优点。另外，此章节提供了由客户端和服务器构成的典型 RMI 应用的描述。同时介绍了一些重要的术语。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**编写 RMI 服务器**](https://docs.oracle.com/javase/tutorial/rmi/server.html) 深入计算引擎服务器代码。本章节将教会你如何设计实现一个 RMI 服务器。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**创建客户端程序**](https://docs.oracle.com/javase/tutorial/rmi/client.html) 分析一个可能的计算引擎客户端，并以其为例展示了一个 RMI 客户端的重要特性。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**编译并运行示例**](https://docs.oracle.com/javase/tutorial/rmi/example.html) 向你展示如何编译并运行计算引擎服务器和客户端。

## RMI 应用概览

RMI 应用通常由两个独立程序组成，服务器和客户端。典型的服务器程序创建一些远程对象，使这些对象的引用可访问，并等待客户端调用这些对象上的方法。典型的客户端程序获取服务器上一个或者多个远程对象的引用，然后调用它们上面的方法。RMI 提供了服务器和客户端之间的通信机制，并来回传递信息。这样的程序某些时候会被称为*分布式对象应用*。

分布式对象应用需要完成下列步骤：

- **定位远程对象：** 应用程序可以使用各种机制来获取对远程对象的引用。例如，应用程序可以使用 RMI 的简单命名工具 RMI 注册表注册其远程对象。或者，应用程序可以作为其他远程调用的一部分传递和返回远程对象引用。
- **与远程对象通信：** 远程对象之间的通信细节由 RMI 处理。对程序员来说，远程通信看起来与普通的 Java 方法调用没有什么不同。
- **加载传递过来的对象的类定义：** 因为 RMI 允许对象来回传递，所以它提供了加载对象的类定义以及传输对象数据的机制。

下图描绘了一个 RMI 分布式应用程序，该应用程序使用 RMI 注册表来获取对远程对象的引用。服务器调用注册表以将名称与远程对象关联（或绑定）。客户端在服务器的注册表中按名称查找远程对象，然后在其上调用方法。该图还显示 RMI 系统使用现有的 Web 服务器在需要时从服务器到客户端以及从客户端到服务器加载对象的类定义。

![the RMI system, using an existing web server, communicates from serve to client and from client to server](https://docs.oracle.com/javase/tutorial/figures/rmi/rmi-2.gif)

**动态代码加载的优点**

RMI 的核心和独特功能之一是，如果未在接收者的 Java 虚拟机中定义类，则可以下载对象类的定义。以前仅在单个 Java 虚拟机中可用的对象的所有类型和行为都可以传输到另一个可能是远程的 Java 虚拟机。RMI 按实际类传递对象，因此在将对象发送到另一个 Java 虚拟机时，不会更改对象的行为。此功能允许将新类型和行为引入远程 Java 虚拟机，从而动态扩展应用程序的行为。此课程中的计算引擎示例使用此功能向分布式程序引入新行为。

**远程接口，对象以及方法**

与任何其他 Java 应用程序一样，使用 Java RMI 构建的分布式应用程序由接口和类组成。接口声明方法。类实现了接口中声明的方法，也许还声明了其他方法。在分布式应用程序中，某些实现可能驻留在某些 Java 虚拟机中，但不存在于其它虚拟机中。具有可以跨 Java 虚拟机调用的方法的对象称为*远程对象*。

通过实现*远程接口*，对象变成远程对象，具有以下特征：

- 远程接口扩展接口 `java.rmi.Remote`。
- 接口中的每个方法都声明 `java.rmi.RemoteException` 在它的 `throws` 子句中，除了所有的特定于应用的异常。

当对象从一个 Java 虚拟机传递到另一个 Java 虚拟机时，RMI 将远程对象与非远程对象区别对待。RMI 不是在接收 Java 虚拟机中复制实现对象，而是为远程对象传递远程*stub*。该存根充当远程对象的本地代表或代理，并且基本上对客户端来说是远程引用。客户端调用本地存根上的方法，该方法负责对远程对象执行方法调用。

远程对象的存根实现远程对象实现的同一组远程接口。此属性允许将存根转换为远程对象实现的任何接口。但是，只能从接收 Java 虚拟机调用远程接口中定义的那些方法。

**使用 RMI 创建分布式应用**

使用 RMI 开发分布式应用程序涉及以下一般步骤：

1. 设计和实现分布式应用程序的组件。
2. 编译源代码。
3. 使类型网络可访问。
4. 启动应用程序。

**设计并实现应用组件**

首先，确定您的应用程序体系结构，包括哪些组件是本地对象以及哪些组件可以远程访问。这一步包括：

- **定义远程接口。**远程接口指定可由客户端远程调用的方法。客户端面向远程接口编程，而不是这些接口的实现类。这种接口的设计包括确定将用作参数的对象类型以及这些方法的返回值。如果尚不存在任何这些接口或类，则还需要定义它们。
- **实现远程对象。**远程对象必须实现一个或多个远程接口。远程对象类可以包括仅在本地可用的其他接口和方法的实现。如果要将任何本地类用于参数或返回任何这些方法的值，则必须同时实现它们。
- **实现客户端。**在定义远程接口后，包括在部署远程对象之后，可以随时实现使用远程对象的客户端。

**编译源代码**

与任何 Java 程序一样，您使用 `javac` 编译器来编译源文件。源文件包含远程接口的声明，它们的实现，任何其他服务器类和客户端类。

------

**注意：** 对于 Java Platform，Standard Edition 5.0 之前的版本，使用 `rmic` 编译器需要额外的步骤来构建存根类。但是，现在已经不再需要此步骤。

------

**使类网络可访问**

在此步骤中，您可以访问某些类定义网络，例如远程接口及其关联类型的定义，以及需要下载到客户端或服务器的类的定义。通常可以通过 Web 服务器访问类定义。

**启动应用**

启动应用程序包括运行 RMI 远程对象注册表，服务器和客户端。

本节的其余部分将介绍用于创建计算引擎的步骤。

**构建通用计算引擎**

本课程专注于一个简单但功能强大的分布式应用程序，称为*计算引擎*。计算引擎是服务器上的远程对象，它从客户端获取任务，运行任务并返回结果。任务在运行服务器的计算机上运行。这种类型的分布式应用程序可以使许多客户端机器能够使用特别强大的机器或具有专用硬件的机器。

计算引擎的新颖之处在于，在编写或启动计算引擎时，不需要定义它运行的任务。可以随时创建新类型的任务，然后将其提供给要运行的计算引擎。任务的唯一要求是其类实现特定的接口。完成任务所需的代码可以由 RMI 系统下载到计算引擎。然后，计算引擎使用运行计算引擎的计算机上的资源运行任务。

Java 平台的动态特性支持执行任意任务的能力，该平台由 RMI 扩展到网络。RMI将任务代码动态加载到计算引擎的 Java 虚拟机中，并在不事先了解实现任务的类的情况下运行任务。这种具有动态下载代码能力的应用程序通常称为*基于行为的应用程序*。此类应用程序通常需要完全启用代理程序的基础设施。使用 RMI，此类应用程序是 Java 平台上分布式计算的基本机制的一部分。

## 编写 RMI 服务器

计算引擎服务器接受来自客户端的任务，执行任务，返回结果。服务器代码由接口和类组成。接口定义了可以从客户端调用的方法。实质上，该接口定义了远程对象的客户端视图。对应的类提供了接口实现。

[设计远程接口](https://docs.oracle.com/javase/tutorial/rmi/designing.html)

本节介绍 `Compute` 接口，提供客户端和服务器之间的连接。你将同时学到 RMI API ，它支持了该通信过程。

[实现远程接口](https://docs.oracle.com/javase/tutorial/rmi/implementing.html)

本节研究实现 `Compute` 接口的类，也就是远程对象实现。该类同时提供了构成服务器程序的其它代码，包括一个 `main` 方法来创建远程对象实例，使用 RMI 注册表注册它，并配置一个安全管理器。

### 设计远程接口

计算引擎的核心是一个协议，它允许将任务提交给计算引擎，计算引擎运行这些任务，将这些任务的结果返回给客户端。此协议在计算引擎支持的接口中表示。该协议的远程通信如下图所示。

![remote communication between a client and the compute engine](https://docs.oracle.com/javase/tutorial/figures/rmi/rmi-3.gif)

每个接口都包含一个方法。计算引擎的远程接口`Compute` 可以将任务提交给引擎。客户端接口 `Task` 定义计算引擎如何执行提交的任务。

 [`compute.Compute`](https://docs.oracle.com/javase/tutorial/rmi/examples/compute/Compute.java) 接口定义了可远程访问的部分，计算引擎本身。下面是 `Compute` 接口的源代码：

```java
package compute;

import java.rmi.Remote;
import java.rmi.RemoteException;

public interface Compute extends Remote {
    <T> T executeTask(Task<T> t) throws RemoteException;
}
```

通过扩展接口`java.rmi.Remote`，`Compute`接口将自己标识为这样一个接口，其方法可以从另一个 Java 虚拟机调用。实现此接口的任何对象都可以是远程对象。

作为远程接口的成员，`executeTask`方法是一种远程方法。因此，必须将此方法定义为能够抛出`java.rmi.RemoteException`。RMI 系统从远程方法调用抛出此异常，以指示发生了通信故障或协议错误。`RemoteException`是一个已检查的异常，因此任何调用远程方法的代码都需要通过捕获它或在其`throws`子句中声明它来处理此异常。

计算引擎所需的第二个接口是`Task`接口，它是`Compute`接口中`executeTask`方法的参数类型。 [`compute.Task`](https://docs.oracle.com/javase/tutorial/rmi/examples/compute/Task.java) 接口定义了计算引擎与它需要做的工作之间的接口，提供开始工作的方式。这是`Task`接口的源代码：

```java
package compute;

public interface Task<T> {
    T execute();
}
```

`Task`接口定义了一个单独的方法`execute`，它没有参数，也没有抛出异常。因为接口不扩展`Remote`，所以此接口中的方法不需要在`throws`子句中列出`java.rmi.RemoteException`。

`Task`接口有一个类型参数`T`，它表示任务计算的结果类型。该接口的`execute`方法返回计算结果，因此其返回类型为`T`。

反过来，`Compute`接口的`executeTask`方法返回传递给它的`Task`实例的执行结果。因此，`executeTask`方法有自己的类型参数`T`，它将自己的返回类型与传递的`Task`实例的结果类型相关联。

RMI 使用 Java 对象序列化机制在 Java 虚拟机之间按值传输对象。对于要被视为可序列化的对象，其类必须实现`java.io.Serializable`标记接口。因此，实现`Task`接口的类也必须实现`Serializable`，用于任务结果的对象类也必须实现。

只要它们是`Task`类型的实现，可以通过`Compute`对象运行不同类型的任务。实现此接口的类可以包含计算任务所需的任何数据以及计算所需的任何其他方法。

以下解释 RMI 如何使这个简单的计算引擎成为可能。因为 RMI 可以假设`Task`对象是用Java编程语言编写的，所以计算引擎之前不知道的`Task`对象的实现会根据需要由 RMI 下载到计算引擎的 Java 虚拟机中。此功能使计算引擎的客户端能够定义要在服务器计算机上运行的新类型的任务，而无需在该计算机上显式安装代码。

由`ComputeEngine`类实现的计算引擎实现了`Compute`接口，通过调用`executeTask`方法，可以将不同的任务提交给它。这些任务使用任务执行的`execute`方法运行，并将结果返回给远程客户端。

