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

