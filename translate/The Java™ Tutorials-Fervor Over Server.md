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

You cannot update a default `ResultSet` object, and you can only move its cursor forward. However, you can create `ResultSet` objects that can be scrolled (the cursor can move backwards or move to an absolute position) and updated.

The following method, `CoffeesTable.modifyPrices`, multiplies the `PRICE` column of each row by the argument `percentage`:

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

The field `ResultSet.TYPE_SCROLL_SENSITIVE` creates a `ResultSet` object whose cursor can move both forward and backward relative to the current position and to an absolute position. The field `ResultSet.CONCUR_UPDATABLE` creates a `ResultSet` object that can be updated. See the `ResultSet` Javadoc for other fields you can specify to modify the behavior of `ResultSet` objects.

The method `ResultSet.updateFloat` updates the specified column (in this example, `PRICE` with the specified `float` value in the row where the cursor is positioned. `ResultSet` contains various updater methods that enable you to update column values of various data types. However, none of these updater methods modifies the database; you must call the method `ResultSet.updateRow` to update the database.

**使用 Statement 对象进行批量更新**

`Statement`, `PreparedStatement` and `CallableStatement` objects have a list of commands that is associated with them. This list may contain statements for updating, inserting, or deleting a row; and it may also contain DDL statements such as `CREATE TABLE` and `DROP TABLE`. It cannot, however, contain a statement that would produce a `ResultSet` object, such as a `SELECT` statement. In other words, the list can contain only statements that produce an update count.

The list, which is associated with a `Statement` object at its creation, is initially empty. You can add SQL commands to this list with the method `addBatch` and empty it with the method `clearBatch`. When you have finished adding statements to the list, call the method `executeBatch` to send them all to the database to be executed as a unit, or batch.

For example, the following method `CoffeesTable.batchUpdate` adds four rows to the `COFFEES` table with a batch update:

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

The following line disables auto-commit mode for the `Connection` object con so that the transaction will not be automatically committed or rolled back when the method `executeBatch` is called.

```java
this.con.setAutoCommit(false);
```

To allow for correct error handling, you should always disable auto-commit mode before beginning a batch update.

The method `Statement.addBatch` adds a command to the list of commands associated with the `Statement` object `stmt`. In this example, these commands are all `INSERT INTO` statements, each one adding a row consisting of five column values. The values for the columns `COF_NAME`and `PRICE` are the name of the coffee and its price, respectively. The second value in each row is 49 because that is the identification number for the supplier, Superior Coffee. The last two values, the entries for the columns `SALES` and `TOTAL`, all start out being zero because there have been no sales yet. (`SALES` is the number of pounds of this row's coffee sold in the current week; `TOTAL` is the total of all the cumulative sales of this coffee.)

The following line sends the four SQL commands that were added to its list of commands to the database to be executed as a batch:

```java
int [] updateCounts = stmt.executeBatch();
```

Note that `stmt` uses the method `executeBatch` to send the batch of insertions, not the method `executeUpdate`, which sends only one command and returns a single update count. The DBMS executes the commands in the order in which they were added to the list of commands, so it will first add the row of values for Amaretto, then add the row for Hazelnut, then Amaretto decaf, and finally Hazelnut decaf. If all four commands execute successfully, the DBMS will return an update count for each command in the order in which it was executed. The update counts that indicate how many rows were affected by each command are stored in the array `updateCounts`.

If all four of the commands in the batch are executed successfully, `updateCounts` will contain four values, all of which are 1 because an insertion affects one row. The list of commands associated with `stmt` will now be empty because the four commands added previously were sent to the database when `stmt` called the method `executeBatch`. You can at any time explicitly empty this list of commands with the method `clearBatch`.

The `Connection.commit` method makes the batch of updates to the `COFFEES` table permanent. This method needs to be called explicitly because the auto-commit mode for this connection was disabled previously.

The following line enables auto-commit mode for the current `Connection` object.

```java
this.con.setAutoCommit(true);
```

Now each statement in the example will automatically be committed after it is executed, and it no longer needs to invoke the method `commit`.

**执行参数化批量更新**

It is also possible to have a parameterized batch update, as shown in the following code fragment, where `con` is a `Connection` object:

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

You will get a `BatchUpdateException` when you call the method `executeBatch` if (1) one of the SQL statements you added to the batch produces a result set (usually a query) or (2) one of the SQL statements in the batch does not execute successfully for some other reason.

You should not add a query (a `SELECT` statement) to a batch of SQL commands because the method `executeBatch`, which returns an array of update counts, expects an update count from each SQL statement that executes successfully. This means that only commands that return an update count (commands such as `INSERT INTO`, `UPDATE`, `DELETE`) or that return 0 (such as `CREATE TABLE`, `DROP TABLE`, `ALTER TABLE`) can be successfully executed as a batch with the `executeBatch` method.

A `BatchUpdateException` contains an array of update counts that is similar to the array returned by the method `executeBatch`. In both cases, the update counts are in the same order as the commands that produced them. This tells you how many commands in the batch executed successfully and which ones they are. For example, if five commands executed successfully, the array will contain five numbers: the first one being the update count for the first command, the second one being the update count for the second command, and so on.

`BatchUpdateException` is derived from `SQLException`. This means that you can use all of the methods available to an `SQLException` object with it. The following method, `JDBCTutorialUtilities.printBatchUpdateException` prints all of the `SQLException` information plus the update counts contained in a `BatchUpdateException` object. Because `BatchUpdateException.getUpdateCounts` returns an array of `int`, the code uses a `for` loop to print each of the update counts:

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

**Note**: Not all JDBC drivers support inserting new rows with the `ResultSet` interface. If you attempt to insert a new row and your JDBC driver database does not support this feature, a `SQLFeatureNotSupportedException` exception is thrown.

The following method, `CoffeesTable.insertRow`, inserts a row into the `COFFEES` through a `ResultSet` object:

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

This example calls the `Connection.createStatement` method with two arguments, `ResultSet.TYPE_SCROLL_SENSITIVE` and `ResultSet.CONCUR_UPDATABLE`. The first value enables the cursor of the `ResultSet` object to be moved both forward and backward. The second value, `ResultSet.CONCUR_UPDATABLE`, is required if you want to insert rows into a `ResultSet` object; it specifies that it can be updatable.

The same stipulations for using strings in getter methods also apply to updater methods.

The method `ResultSet.moveToInsertRow` moves the cursor to the insert row. The insert row is a special row associated with an updatable result set. It is essentially a buffer where a new row can be constructed by calling the updater methods prior to inserting the row into the result set. For example, this method calls the method `ResultSet.updateString` to update the insert row's `COF_NAME` column to `Kona`.

The method `ResultSet.insertRow` inserts the contents of the insert row into the `ResultSet` object and into the database.

**Note**: After inserting a row with the `ResultSet.insertRow`, you should move the cursor to a row other than the insert row. For example, this example moves it to before the first row in the result set with the method `ResultSet.beforeFirst`. Unexpected results can occur if another part of your application uses the same result set and the cursor is still pointing to the insert row.