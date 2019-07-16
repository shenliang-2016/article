## 目录

- [8.1 优化概览](https://dev.mysql.com/doc/refman/5.6/en/optimize-overview.html)
- [8.2 SQL 语句优化](https://dev.mysql.com/doc/refman/5.6/en/statement-optimization.html)
- [8.3 索引和优化](https://dev.mysql.com/doc/refman/5.6/en/optimization-indexes.html)
- [8.4 优化数据库结构](https://dev.mysql.com/doc/refman/5.6/en/optimizing-database-structure.html)
- [8.5 优化 InnoDB 表](https://dev.mysql.com/doc/refman/5.6/en/optimizing-innodb.html)
- [8.6 优化 MyISAM 表](https://dev.mysql.com/doc/refman/5.6/en/optimizing-myisam.html)
- [8.7 优化 MEMORY 表](https://dev.mysql.com/doc/refman/5.6/en/optimizing-memory-tables.html)
- [8.8 理解查询执行计划](https://dev.mysql.com/doc/refman/5.6/en/execution-plan-information.html)
- [8.9 控制查询优化器](https://dev.mysql.com/doc/refman/5.6/en/controlling-optimizer.html)
- [8.10 缓冲和缓存](https://dev.mysql.com/doc/refman/5.6/en/buffering-caching.html)
- [8.11 优化锁操作](https://dev.mysql.com/doc/refman/5.6/en/locking-issues.html)
- [8.12 优化 MySQL 服务器](https://dev.mysql.com/doc/refman/5.6/en/optimizing-server.html)
- [8.13 性能度量 (Benchmarking)](https://dev.mysql.com/doc/refman/5.6/en/optimize-benchmarking.html)
- [8.14 查看线程信息](https://dev.mysql.com/doc/refman/5.6/en/thread-information.html)

本章介绍如何优化MySQL性能并提供示例。优化涉及在多个级别配置，调整和测量性能。根据您的工作角色（开发人员，DBA或两者的组合），您可以在单个SQL语句，整个应用程序，单个数据库服务器或多个联网数据库服务器的级别进行优化。有时您可以主动并提前计划性能，而有时您可能会在出现问题后解决配置或代码问题。优化CPU和内存使用还可以提高可伸缩性，允许数据库处理更多负载而不会降低速度。

## 8.1 优化概述

数据库性能取决于数据库层面的若干因素，比如表、查询以及配置等。这些软件结构产生硬件层面的 CPU 和 I/O 操作，你可能会希望减少并尽可能提高这些操作的效率。为了改进数据库性能，你会开始学习软件层面的高级规则和指南，同时使用执行时间来度量性能。当你成为专家之后，你将了解更多内部信息，同时开始使用诸如 CPU 周期或者 I/O 操作等度量性能。

典型用户的目标时基于他们现有的软硬件配置获得最好的数据库性能。高级用户寻找改善他们 MySQL 软件性能的可能，或者开发他们自己的存储引擎或者硬件设备来扩展 MySQL 生态。

- [在数据库层面优化](https://dev.mysql.com/doc/refman/5.6/en/optimize-overview.html#optimize-database-level)
- [在硬件层面优化](https://dev.mysql.com/doc/refman/5.6/en/optimize-overview.html#optimize-hardware-level)
- [平衡可移植性和性能](https://dev.mysql.com/doc/refman/5.6/en/optimize-overview.html#optimize-portability-performance)

**在数据库层面优化**

使数据库应用更快的最重要因素时它的基本设计：

- 数据表结构是否合理？特别是，列是否具有正确的数据类型，每个表是否拥有合适类型的列？比如，执行频繁更新的应用通常拥有很多列数很少的表，而分析大量数据的应用通常拥有少数几个具有大量列的表。

- 是否存在正确的 [索引](https://dev.mysql.com/doc/refman/5.6/en/optimization-indexes.html) 来保证高效查询？

- 你是否为每个表使用了合适的存储引擎，同时利用了你所使用的存储引擎的能力和特性优势？特别是，选择诸如`InnoDB`之类的事务性的存储引擎或者诸如`MyISAM`之类的非事务性存储引擎将对性能和可扩展性产生重要影响。

  > **注意：** `InnoDB`是新表的默认存储引擎。在实际生产中，高级的`InnoDB`性能特性意味着`InnoDB`表通常会比更简单的`MyISAM`表的性能更好，特别是在繁忙的数据库中。

- 是否每个表都采用了合适的行格式？该选择也取决于该表采用的存储引擎。特别地，压缩表以使用更少的磁盘空间，同时读写数据都需要更少的磁盘 I/O 操作。压缩对于各种负载的`InnoDB`表以及只读的`MyISAM`表是可用的。

- 应用是否采用了合适的 [锁策略](https://dev.mysql.com/doc/refman/5.6/en/locking-issues.html) ？比如，通过尽可能允许共享访问，数据库操作可以并发运行，同时在适当的时候也可以请求独占式访问，因而关键的操作可以得到最高的优先级。再次，存储引擎选择意义重大。`InnoDB`存储引擎帮你处理了大量的锁问题，允许数据库层面更好的并发性，而不需要你对代码反复试验和调试。

- 是否所有的 [用于缓存的内存区域](https://dev.mysql.com/doc/refman/5.6/en/buffering-caching.html) 大小都是合适的？也就是说，足够大来容纳频繁访问的数据，但是又不会大到超过物理存储空间而导致分页。要配置的主要内存区域是`InnoDB`缓冲池，`MyISAM`键缓存和MySQL查询缓存。

**硬件层面的优化**

所有数据库应用随着数据库越来越繁忙最终都会抵达硬件极限。DBA 必须分析是否可以通过调整应用或者数据库服务器的配置来避免遇到的这些 [瓶颈](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_bottleneck) ，否则就需要更多的硬件资源。系统瓶颈通常来自以下来源：

- 磁盘查找。在磁盘上寻找特定数据片段需要消耗一定的时间。对现代磁盘而言，平均查找时间通常低于 10 ms，也即是说理论上每秒可以执行大约 100 次查找。这个时间随着磁盘技术的更新而缓慢提升，并且非常难以针对单个的表进行优化。优化查找时间的方法是将数据分布到多个磁盘上。
- 磁盘读取和写入。当磁盘位于正确的位置，我们需要读取或者写入数据。对于现代磁盘，一个磁盘驱动器至少可以支持 10~20MB/s 的数据吞吐量。相对与寻找时间，可以简单地通过从多个磁盘并发读取来优化读取时间。
- CPU 周期。当数据已经在主内存中，我们必须处理它来得到我们需要的结果。对大表来说，内存空间是最重要的限制因素，但是对于小表来说，速度通常不是问题。
- 内存带宽。当 CPU 需要更多数据，而这些数据又不在 CPU 缓存中，主存的带宽就会成为瓶颈。这对大多数系统来说都不会出现，但是需要有这个意识。

**平衡可移植性和性能**

要在可移植的MySQL程序中使用面向性能的SQL扩展，您可以用 `/*! */`注释分隔符包围语句中包含的特定于MySQL的关键字。其他SQL服务器忽略注释的关键字。有关编写注释的信息，请参见 [第9.6节“注释语法”](https://dev.mysql.com/doc/refman/5.6/en/comments.html) 。

## 8.2 SQL 语句优化

- [8.2.1 优化 SELECT 语句](https://dev.mysql.com/doc/refman/5.6/en/select-optimization.html)
- [8.2.2 优化子查询和驱动表](https://dev.mysql.com/doc/refman/5.6/en/subquery-optimization.html)
- [8.2.3 优化 INFORMATION_SCHEMA 查询](https://dev.mysql.com/doc/refman/5.6/en/information-schema-optimization.html)
- [8.2.4 优化数据修改语句](https://dev.mysql.com/doc/refman/5.6/en/data-change-optimization.html)
- [8.2.5 优化数据库权限](https://dev.mysql.com/doc/refman/5.6/en/permission-optimization.html)
- [8.2.6 其它优化建议](https://dev.mysql.com/doc/refman/5.6/en/miscellaneous-optimization-tips.html)

数据库应用程序的核心逻辑是通过SQL语句执行的，无论是直接通过解释器发出还是通过API在后台提交。本节中的调整准则有助于加速各种MySQL应用程序。这些准则涵盖了读取和写入数据的SQL操作，一般SQL操作的幕后开销，以及特定方案（如数据库监视）中使用的操作。

### 8.2.1 SELECT 语句优化

- [8.2.1.1 WHERE 子句优化](https://dev.mysql.com/doc/refman/5.6/en/where-optimization.html)
- [8.2.1.2 Range 优化](https://dev.mysql.com/doc/refman/5.6/en/range-optimization.html)
- [8.2.1.3 索引合并优化](https://dev.mysql.com/doc/refman/5.6/en/index-merge-optimization.html)
- [8.2.1.4 引擎条件下推优化](https://dev.mysql.com/doc/refman/5.6/en/condition-pushdown-optimization.html)
- [8.2.1.5 索引条件下推优化](https://dev.mysql.com/doc/refman/5.6/en/index-condition-pushdown-optimization.html)
- [8.2.1.6 嵌套循环连接算法](https://dev.mysql.com/doc/refman/5.6/en/nested-loop-joins.html)
- [8.2.1.7 嵌套连接优化](https://dev.mysql.com/doc/refman/5.6/en/nested-join-optimization.html)
- [8.2.1.8 外连接优化](https://dev.mysql.com/doc/refman/5.6/en/outer-join-optimization.html)
- [8.2.1.9 外连接简化](https://dev.mysql.com/doc/refman/5.6/en/outer-join-simplification.html)
- [8.2.1.10 Multi-Range 读优化](https://dev.mysql.com/doc/refman/5.6/en/mrr-optimization.html)
- [8.2.1.11 块嵌套循环和批量键访问连接](https://dev.mysql.com/doc/refman/5.6/en/bnl-bka-optimization.html)
- [8.2.1.12 IS NULL 优化](https://dev.mysql.com/doc/refman/5.6/en/is-null-optimization.html)
- [8.2.1.13 ORDER BY 优化](https://dev.mysql.com/doc/refman/5.6/en/order-by-optimization.html)
- [8.2.1.14 GROUP BY 优化](https://dev.mysql.com/doc/refman/5.6/en/group-by-optimization.html)
- [8.2.1.15 DISTINCT 优化](https://dev.mysql.com/doc/refman/5.6/en/distinct-optimization.html)
- [8.2.1.16 LIMIT 查询优化](https://dev.mysql.com/doc/refman/5.6/en/limit-optimization.html)
- [8.2.1.17 函数调用优化](https://dev.mysql.com/doc/refman/5.6/en/function-optimization.html)
- [8.2.1.18 行构造器表达式优化](https://dev.mysql.com/doc/refman/5.6/en/row-constructor-optimization.html)
- [8.2.1.19 避免全表扫描](https://dev.mysql.com/doc/refman/5.6/en/table-scan-avoidance.html)

[`SELECT`](https://dev.mysql.com/doc/refman/5.6/en/select.html) 语句形式的查询执行数据库中的所有查找操作。调整这些语句是首要任务，无论是为动态网页实现亚秒响应时间，还是为了产生巨大的隔夜报告而缩短工作时间。

除了 [`SELECT`](https://dev.mysql.com/doc/refman/5.6/en/select.html) 语句，查询优化技术也适用于诸如 [`CREATE TABLE...AS SELECT`](https://dev.mysql.com/doc/refman/5.6/en/create-table-select.html), [`INSERT INTO...SELECT`](https://dev.mysql.com/doc/refman/5.6/en/insert-select.html) ，以及[`DELETE`](https://dev.mysql.com/doc/refman/5.6/en/delete.html) 语句中的 `WHERE` 子句。那些语句需要额外的性能考量因为它们将写入操作与面向读取的查询操作结合了起来。

NDB Cluster支持连接下推优化，从而将合格连接完整地发送到NDB Cluster数据节点，在NDB Cluster数据节点中可以将连接操作分布在它们之间并且并行执行。有关此优化的更多信息，请参阅 [NDB下推连接的条件](https://dev.mysql.com/doc/refman/5.6/en/mysql-cluster-options-variables.html#ndb_join_pushdown-conditions) 。

查询优化的主要考量有：

- 为了让一个执行缓慢的 `SELECT ... WHERE` 查询更快，首先应该检查你是否为其添加了 [索引](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_index) 。在`WHERE`子句使用的列上设置索引，来加速评估、过滤以及最终结果的查询。为了避免磁盘空间的浪费，构造一个小的索引集合来加速你的应用用到的尽可能多的相关查询。

  索引对那些引用不同的表的查询特别重要，这些查询使用了诸如 [joins](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_join) 和 [foreign keys](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_foreign_key) 等特性。你可以使用 [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 语句来确定一个查询语句用到了哪些索引。参考 [Section 8.3.1, “How MySQL Uses Indexes”](https://dev.mysql.com/doc/refman/5.6/en/mysql-indexes.html) 和 [Section 8.8.1, “Optimizing Queries with EXPLAIN”](https://dev.mysql.com/doc/refman/5.6/en/using-explain.html) 。

- 隔离并微调查询的各个部分，比如函数调用，它可能耗费过多时间。按照查询的结构，一个函数可能为结果集中的每一行数据调用一次，或者甚至会为表中的每一行都调用一次，显著放大低效操作。

- 最小化你的查询导致的 [全表扫描](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_full_table_scan) ，特别是对于大表。

- 定期使用[`ANALYZE TABLE`](https://dev.mysql.com/doc/refman/5.6/en/analyze-table.html) 语句更新表统计，以便优化器具有构建有效的执行计划所需的信息。

- 了解特定于每个表的存储引擎的调优技术，索引技术和配置参数。`InnoDB` 和 `MyISAM` 都有一套启用和维持查询高性能的指南。有关详细信息，请参见 [第8.5.6节“优化InnoDB查询”](https://dev.mysql.com/doc/refman/5.6/en/optimizing-innodb-queries.html) 和 [第8.6.1节 “优化MyISAM查询”](https://dev.mysql.com/doc/refman/5.6/en/optimizing-queries-myisam.html) 。

- 您可以使用 [第8.5.3节“优化InnoDB只读事务”](https://dev.mysql.com/doc/refman/5.6/en/innodb-performance-ro-txn.html) 中的技术优化`InnoDB`表的单查询事务。

- 避免以难以理解的方式转换查询，尤其是在优化程序自动执行某些相同转换的情况下。

- 如果其中一个基本准则无法轻松解决性能问题，请阅读 [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 计划来调查特定查询的内部详细信息，进而调整索引，`WHERE`子句，join子句等。（当您达到一定的专业水平时，阅读 [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 计划可能是您进行每个查询的第一步。）

- 调整MySQL用于缓存的内存区域的大小和属性。有效地使用`InnoDB` [缓冲池](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_buffer_pool) ，`MyISAM`键缓存和MySQL查询缓存，重复查询运行得更快，因为第二次及以后的查询都会从内存中检索结果。

- 即使对于使用高速缓存存储区域快速运行的查询，您仍可以进一步优化，以便它们需要更少的高速缓存，从而使您的应用程序更具可伸缩性。可伸缩性意味着您的应用程序可以处理更多的并发用户，更大的请求等，而不会出现性能大幅下降的情况。

- 处理锁问题，其中查询的速度可能会受到同时访问表的其他会话的影响。

#### 8.2.1.1 WHERE 子句优化

本章节讨论可以用于`WHERE`子句的优化技术。这里使用 [`SELECT`](https://dev.mysql.com/doc/refman/5.6/en/select.html) 语句为例说明，不过这种优化技术同样可以用于 [`DELETE`](https://dev.mysql.com/doc/refman/5.6/en/delete.html) 和 [`UPDATE`](https://dev.mysql.com/doc/refman/5.6/en/update.html) 语句中的`WHERE`子句。

> **注意：** 由于 MySQL 优化器在不断进化中，本手册中并不会包含所有的优化技术。

您可能想要重写查询以更快地进行算术运算，同时牺牲可读性。因为MySQL会自动执行类似的优化，所以通常应该避免这种工作，并使查询保持更易理解和可维护的形式。MySQL自动执行的一些优化如下：

- 删除不必要的括号：

  ```sql
     ((a AND b) AND c OR (((a AND b) AND (c AND d))))
  -> (a AND b AND c) OR (a AND b AND c AND d)
  ```

- 常量折叠：

  ```sql
     (a<b AND b=c) AND a=5
  -> b>5 AND b=c AND a=5
  ```

- 恒定条件消除：

  ```sql
     (b>=5 AND b=5) OR (b=6 AND 5=5) OR (b=7 AND 5=6)
  -> b=5 OR b=6
  ```

- 索引使用的常量表达式仅计算一次。

- 在单个表上执行没有`WHERE`子句的 [`COUNT(*)`](https://dev.mysql.com/doc/refman/5.6/en/group-by-functions.html#function_count) 查询直接从 `MyISAM` 和 `MEMORY`表的表信息中获取结果。这种操作同样应用于任何在单个表上执行的`NOT NULL` 表达式。

- 尽早检测无效常量表达式。MySQL快速检测到某些 [`SELECT`](https://dev.mysql.com/doc/refman/5.6/en/select.html) 语句是不可能的，并且不返回任何行。

- 如果你没有使用`GROUP BY`或者聚合函数，[`COUNT()`](https://dev.mysql.com/doc/refman/5.6/en/group-by-functions.html#function_count), [`MIN()`](https://dev.mysql.com/doc/refman/5.6/en/group-by-functions.html#function_min) 等等，`HAVING`就会与`WHERE`合并。

- 对于连接中的每个表，构造一个更简单的`WHERE`以获得对表的快速`WHERE`评估，并且还尽可能跳过行。

- 查询中涉及到的所有常量表都会首先读取。常量表是指：

  - 空表或者只有一行数据的表。An empty table or a table with one row.
  - 与`PRIMARY KEY`或者`UNIQUE`索引上的`WHERE`子句共同使用的表，其中所有的索引部分都与常量表达式比较并且定义为`NOT NULL` 。

  以下所有表都用作常量表：

  ```sql
  SELECT * FROM t WHERE primary_key=1;
  SELECT * FROM t1,t2
    WHERE t1.primary_key=1 AND t2.primary_key=t1.id;
  ```

- 通过尝试所有可能的组合以找到待连接表的最优连接组合方式。如果`GROUP BY`和`ORDER BY`子句中的所有列都来自同一张表，则该表在连接中就会作为第一张表。

- 如果存在`ORDER BY`子句和不同的`GROUP BY`子句，或者`ORDER BY`或`GROUP BY`包含连接队列中第一个表以外的表中的列，则会创建临时表。

- 如果使用`SQL_SMALL_RESULT`修饰符，MySQL将使用内存中的临时表。

- 查询每个表索引，并使用最佳索引，除非优化器认为使用表扫描更有效。曾经有段时间，优化器会根据最佳索引是否能够跳过超过表的30％来决定是否使用表扫描，但如今固定百分比不再决定使用索引或表扫描之间的选择。优化器现在更复杂，并且基于其他因素（例如表大小，行数和I/O块大小）进行评估。

- 在某些情况下，MySQL甚至无需查询数据文件即可从索引中读取行。如果索引中使用的所有列都是数字，则仅使用索引树来解析查询。

- 在输出每一行之前，将跳过与`HAVING`子句不匹配的行。

一些执行非常快的查询示例：

```sql
SELECT COUNT(*) FROM tbl_name;

SELECT MIN(key_part1),MAX(key_part1) FROM tbl_name;

SELECT MAX(key_part2) FROM tbl_name
  WHERE key_part1=constant;

SELECT ... FROM tbl_name
  ORDER BY key_part1,key_part2,... LIMIT 10;

SELECT ... FROM tbl_name
  ORDER BY key_part1 DESC, key_part2 DESC, ... LIMIT 10;
```

MySQL仅使用索引树解析以下查询，假设索引列是数字：

```sql
SELECT key_part1,key_part2 FROM tbl_name WHERE key_part1=val;

SELECT COUNT(*) FROM tbl_name
  WHERE key_part1=val1 AND key_part2=val2;

SELECT key_part2 FROM tbl_name GROUP BY key_part1;
```

以下查询使用索引来按排序顺序检索行，而不使用单独的排序传递：

```sql
SELECT ... FROM tbl_name
  ORDER BY key_part1,key_part2,... ;

SELECT ... FROM tbl_name
  ORDER BY key_part1 DESC, key_part2 DESC, ... ;
```
#### 8.2.1.2 Range 优化

[`range`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_range) 访问方法使用单个索引来检索包含在一个或多个索引值间隔内的表行的子集。它可用于单部分或多部分索引。 以下部分详细说明了如何从`WHERE`子句中提取间隔。

- [单部分索引的 Range 访问方法](https://dev.mysql.com/doc/refman/5.6/en/range-optimization.html#range-access-single-part)
- [多部分索引的 Range 访问方法](https://dev.mysql.com/doc/refman/5.6/en/range-optimization.html#range-access-multi-part)
- [多值比较的等值 Range 优化](https://dev.mysql.com/doc/refman/5.6/en/range-optimization.html#equality-range-optimization)

**单部分索引的 Range 访问方法**

对一个单部分索引，索引值间隔能够用`WHERE`子句中的对应条件方便地表示，表示范围条件而不是“间隔”。

单部分索引的范围条件定义如下：

- 对`BTREE`和`HASH`索引，当使用 [`=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal), [`<=>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal-to), [`IN()`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_in), [`IS NULL`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_is-null), 或者 [`IS NOT NULL`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_is-not-null) 等操作符时，键部分与常量值的比较就是范围条件。
- 另外，对`BTREE`索引，当使用[`>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_greater-than), [`<`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_less-than), [`>=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_greater-than-or-equal), [`<=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_less-than-or-equal), [`BETWEEN`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_between), [`!=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_not-equal), 或者 [`<>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_not-equal) 操作符时，或者 [`LIKE`](https://dev.mysql.com/doc/refman/5.6/en/string-comparison-functions.html#operator_like) 比较，如果 [`LIKE`](https://dev.mysql.com/doc/refman/5.6/en/string-comparison-functions.html#operator_like) 的参数是不以通配符开头的字符串常量，键部分与常量值的比较就是范围条件。
- 对所有类型的索引，多个范围条件由 [`OR`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_or) 或者 [`AND`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_and) 组合形成一个范围条件。

上面描述的提到的“常量值”代表如下含义：

- 来自查询字符串的常量
- 来自同一连接的 [`const`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_const) 或者 [`system`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_system) 表的列
- 不相关子查询的结果
- 完全由前面任何类型的子表达式组成的任何表达式

下面是一些`WHERE`子句中包含范围条件的查询示例：

```sql
SELECT * FROM t1
  WHERE key_col > 1
  AND key_col < 10;

SELECT * FROM t1
  WHERE key_col = 1
  OR key_col IN (15,18,20);

SELECT * FROM t1
  WHERE key_col LIKE 'ab%'
  OR key_col BETWEEN 'bar' AND 'foo';
```

在优化器常量传播阶段，一些非常量值可以转换为常量。

MySQL尝试为每个可能的索引从`WHERE`子句中提取范围条件。在提取过程期间，丢弃不能用于构建范围条件的条件，组合产生重叠范围的条件，并且去除产生空范围的条件。

考虑下面的语句，其中 `key1` 是索引列，而 `nonkey` 未被索引：

```sql
SELECT * FROM t1 WHERE
  (key1 < 'abc' AND (key1 LIKE 'abcde%' OR key1 LIKE '%b')) OR
  (key1 < 'bar' AND nonkey = 4) OR
  (key1 < 'uux' AND key1 > 'z');
```

键 `key1` 的范围条件抽取过程如下：

1. 初始的 `WHERE` 子句：

   ```sql
   (key1 < 'abc' AND (key1 LIKE 'abcde%' OR key1 LIKE '%b')) OR
   (key1 < 'bar' AND nonkey = 4) OR
   (key1 < 'uux' AND key1 > 'z')
   ```

2. 删除 `nonkey = 4` 和 `key1 LIKE '%b'` 因为它们不能被用来进行范围扫描。正确的删除方法是用`TRUE`替换它们。这样我们进行范围扫描时就不会丢失任何匹配的行。替换之后得到：

   ```sql
   (key1 < 'abc' AND (key1 LIKE 'abcde%' OR TRUE)) OR
   (key1 < 'bar' AND TRUE) OR
   (key1 < 'uux' AND key1 > 'z')
   ```

3. 消除始终为`true`或者`false`的条件：

   - `(key1 LIKE 'abcde%' OR TRUE)` 永远为`true`
   - `(key1 < 'uux' AND key1 > 'z')` 永远为`false`

   用常量替换这些条件后得到：

   ```sql
   (key1 < 'abc' AND TRUE) OR (key1 < 'bar' AND TRUE) OR (FALSE)
   ```

   删除没必要的 `TRUE` 和 `FALSE` 常量得到：

   ```sql
   (key1 < 'abc') OR (key1 < 'bar')
   ```

4. 组合重叠的间隔成为一个以得到最终的范围扫描条件：

   ```sql
   (key1 < 'bar')
   ```

通常（如同上面这个例子所示），用于范围扫描的条件相对于初始的`WHERE`子句是放松了限制。MySQL 执行额外的检查来过滤掉那些满足范围条件但是不满足`WHERE`子句的行。

范围条件抽取算法能够处理任意深度的 [`AND`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_and)/[`OR`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_or) 嵌套结构，同时，抽取的结果并不取决于这些条件出现在初始`WHERE`子句中的顺序。

MySQL不支持合并空间索引的 [`range`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_range) 访问方法的多个范围。要解决此限制，除了将每个空间谓词放在不同的[`SELECT`](https://dev.mysql.com/doc/refman/5.6/en/select.html) 中之外，您可以使用具有相同[`SELECT`](https://dev.mysql.com/doc/refman/5.6/en/select.html) 语句的 [`UNION`](https://dev.mysql.com/doc/refman/5.6/en/union.html) 。

**多部分索引的 Range 访问方法**

多部分索引的范围条件是单部分索引的范围条件的扩展。多部分索引上的范围条件将索引行限制在一个或多个键元组间隔内。使用索引中的排序在一组键元组上定义键元组间隔。

比如，考虑这样的多部份索引 `key1(*key_part1*, *key_part2*, *key_part3*)` ，同时下列键元组集合按照键顺序列出：

```
key_part1  key_part2  key_part3
  NULL       1          'abc'
  NULL       1          'xyz'
  NULL       2          'foo'
   1         1          'abc'
   1         1          'xyz'
   1         2          'abc'
   2         1          'aaa'
```

条件 `*key_part1* = 1` 定义如下间隔：

```sql
(1,-inf,-inf) <= (key_part1,key_part2,key_part3) < (1,+inf,+inf)
```

该间隔涵盖上面数据集中的第四个、第五个以及第六个键元组并可以被用于范围访问方法。

相反，条件 `*key_part3* = 'abc'` 没有定义单个间隔因而不能被用于范围访问方法。

下面的描述更详细地说明了如何对多部份索引进行范围访问。

- 对 `HASH` 索引，每个包含相同值的间隔都可以被使用。这意味着该间隔能够产生如下形式的条件：

  ```sql
      key_part1 cmp const1
  AND key_part2 cmp const2
  AND ...
  AND key_partN cmp constN;
  ```

  这里， *const1*, *const2*, … 都是常量，*cmp*是 [`=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal), [`<=>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal-to), 或者 [`IS NULL`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_is-null) 比较操作之一，同时该条件涵盖所有索引部分。（也就是说，存在N个条件，每个条件对应于N部分索引的一部分。）比如，下面是一个三部分`HASH`索引的范围条件：

  ```sql
  key_part1 = 1 AND key_part2 IS NULL AND key_part3 = 'foo'
  ```

  什么会被认为是常量的定义，参考 [单部分索引的范围访问方法](https://dev.mysql.com/doc/refman/5.6/en/range-optimization.html#range-access-single-part) 。

- 对于`BTREE`索引，间隔可以用于与 [`AND`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_and) 组合的条件，其中每个条件使用 [`=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal), [`<=>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal-to), [`IS NULL`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_is-null), [`>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_greater-than), [`<`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_less-than), [`>=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_greater-than-or-equal), [`<=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_less-than-or-equal), [`!=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_not-equal), [`<>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_not-equal), [`BETWEEN`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_between), 或者 [`LIKE '*pattern*'`](https://dev.mysql.com/doc/refman/5.6/en/string-comparison-functions.html#operator_like) (其中'\*pattern\*'不以通配符开头)来比较键部分和常量值。可以使用间隔，只要可以确定包含与条件匹配的所有行的单个键元组（或者如果使用 [`<>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_not-equal) 或者 [`!=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_not-equal) 则为两个间隔）。

  只要比较运算符为[`=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal), [`<=>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal-to), or [`IS NULL`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_is-null) ，优化器就会尝试使用其他键部分来确定间隔。如果运算符是 [`>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_greater-than), [`<`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_less-than), [`>=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_greater-than-or-equal), [`<=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_less-than-or-equal), [`!=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_not-equal),[`<>`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_not-equal), [`BETWEEN`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_between), or [`LIKE`](https://dev.mysql.com/doc/refman/5.6/en/string-comparison-functions.html#operator_like) ，优化程序将使用它，而不再考虑更多键部分。对于以下表达式，优化程序使用来自第一次比较的 [`=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_equal) 。它还使用了来自第二次比较的 [`>=`](https://dev.mysql.com/doc/refman/5.6/en/comparison-operators.html#operator_greater-than-or-equal) ，但没有考虑其他键部分，也没有使用第三个比较进行间隔构造：

  ```sql
  key_part1 = 'foo' AND key_part2 >= 10 AND key_part3 > 10
  ```

  单个间隔是：

  ```sql
  ('foo',10,-inf) < (key_part1,key_part2,key_part3) < ('foo',+inf,+inf)
  ```

  创建的间隔可能包含比初始条件更多的行。例如，前面的间隔包括值 `('foo', 11, 0)`，它不满足原始条件。

- 如果覆盖区间中包含的行集合的条件通过 [`OR`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_or) 组合，则它们形成一个条件，该条件覆盖其间隔的并集中包含的一组行。如果条件通过 [`AND`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_and) 组合，则它们形成一个条件，该条件覆盖其间隔的交集中包含的一组行。例如，对于这个由两部分组成的索引：

  ```sql
  (key_part1 = 1 AND key_part2 < 2) OR (key_part1 > 5)
  ```

  间隔是：

  ```sql
  (1,-inf) < (key_part1,key_part2) < (1,2)
  (5,-inf) < (key_part1,key_part2)
  ```

  在此示例中，第一行的间隔使用一个键部分作为左边界的，而使用两个键部分作为右边界。第二行的间隔仅使用一个键部分。[`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 输出中的`key_len`列指示使用的键前缀的最大长度。

  某些情况下，`key_len`可以表示一个键部分被使用，但是这并不一定是你期望的效果。假设*key_part1*和*key_part2*可以为`NULL`。然后`key_len`列显示下面条件的两个键部分长度：

  ```sql
  key_part1 >= 1 AND key_part2 < 2
  ```

  然而，实际上，该条件被转化为如下形式：

  ```sql
  key_part1 >= 1 AND key_part2 IS NOT NULL
  ```

有关如何执行优化以组合或消除单部分索引上的范围条件的间隔的说明，请参阅 [单部分索引的范围访问方法](https://dev.mysql.com/doc/refman/5.6/en/range-optimization.html#range-access-single-part) 。对多部分索引的范围条件执行类似步骤。

**多值比较的等值 Range 优化**

考虑下面的表达式，其中 *col_name* 是一个索引列：

```sql
col_name IN(val1, ..., valN)
col_name = val1 OR ... OR col_name = valN
```

如果*col-name*等于这几个值中的任何一个，则每个表达式的值都是`true`。这些比较就是等值范围比较（其中的“范围”是单个值）。优化器度量读取取限定行的成本以进行相等范围比较，如下所示：

- 如果*col_name*列上存在一个唯一索引，每个范围的行度量值就是1，因为至多有一行具有给定的值。
- 否则，*col_name*列上的所有索引都不是唯一索引，优化器可以使用潜入索引或索引统计信息来估计每个范围的行数。

使用索引潜入时，优化程序会在范围的每一端进行潜入，并使用范围中的行数作为估计值。例如，表达式 `*col_name* IN (10, 20, 30)` 具有三个相等范围，优化器对每个范围进行两次潜入以生成行估计。每对潜入产生具有给定值的行的数量的估计。

索引潜入提供准确的行估计，但随着表达式中比较值的数量增加，优化器需要更长时间才能生成行估计。索引统计的结果不如索引潜入准确，但允许对巨大列表进行更快的行估计。

[`eq_range_index_dive_limit`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_eq_range_index_dive_limit) 系统变量使您可以配置优化器从一个行估计策略切换到另一个行估计策略的值的数量。要允许使用索引潜入进行最多N个相等范围的比较，请将 [`eq_range_index_dive_limit`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_eq_range_index_dive_limit) 设置为N + 1。要禁用统计数据并始终使用索引潜入而不考虑N，请将 [`eq_range_index_dive_limit`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_eq_range_index_dive_limit) 设置为0。

更新表索引统计来获得最优估计，使用 [`ANALYZE TABLE`](https://dev.mysql.com/doc/refman/5.6/en/analyze-table.html) 。

即使在以其他方式使用索引潜入的情况下，也会跳过满足所有这些条件的查询：

- 存在单索引`FORCE INDEX`索引提示。我们的想法是，如果强制使用索引，那么从索引潜入中产生的额外开销就无法获得任何好处。
- 索引是非唯一性索引而且也不是`FULLTEXT`索引。
- 不存在子查询。
- 不存在 `DISTINCT`, `GROUP BY`, or `ORDER BY` 子句。

这种索引潜入的跳过只会应用于单表查询，而不会应用于多表连接查询。

#### 8.2.1.3 索引合并优化

索引合并访问方法基于多个 [`range`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_range) 扫描检索行数据并将结果合并为一个。这个访问方法只会合并来自单个表的索引扫描，而不会合并跨越多个表的索引扫描。合并可以生成其基础扫描的联合，交叉或交叉联合。

可能会使用索引合并的查询示例：

```sql
SELECT * FROM tbl_name WHERE key1 = 10 OR key2 = 20;

SELECT * FROM tbl_name
  WHERE (key1 = 10 OR key2 = 20) AND non_key = 30;

SELECT * FROM t1, t2
  WHERE (t1.key1 IN (1,2) OR t1.key2 LIKE 'value%')
  AND t2.key1 = t1.some_col;

SELECT * FROM t1, t2
  WHERE t1.key1 = 1
  AND (t2.key1 = t1.some_col OR t2.key2 = t1.some_col2);
```

> 注意：
>
> 索引合并优化算法具有以下已知限制：
>
> - 如果你的查询包含复杂的`WHERE`子句，其中包含很深的[`AND`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_and)/[`OR`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_or) 嵌套，而MySQL并没有选择相应的优化方案，请尝试将该嵌套进行如下等价转化：
>
>   ```sql
>   (x AND y) OR z => (x OR z) AND (y OR z)
>   (x OR y) AND z => (x AND z) OR (y AND z)
>   ```
>
> - 索引合并不适用于全文本索引。

在 [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 输出中，索引合并方法作为 [`index_merge`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_index_merge) 出现的`type`列中。这种情况下，`key`列包含一个使用到的索引列表，而`key_len`包含这些索引中最常的索引部分的列表。

索引合并访问方法包含几种算法，展现在 [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 输出的`Extra`列中：

- `Using intersect(...)`
- `Using union(...)`
- `Using sort_union(...)`

下面章节详细描述了这些算法。优化器根据各种可用选项的成本估算在不同的可能索引合并算法和其他访问方法之间进行选择。

索引合并的使用受制于 `index_merge`, `index_merge_intersection`, `index_merge_union`, 和 `index_merge_sort_union` 等几个 [`optimizer_switch`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_optimizer_switch) 系统变量标记的值。参考 [Section 8.9.2, “Switchable Optimizations”](https://dev.mysql.com/doc/refman/5.6/en/switchable-optimizations.html) 。默认情况下，所有这些标记值都为`on`。想要只启用某种算法，设置`index_merge`为`off`，并只启用想要启用的其它算法。

- [Index Merge Intersection Access Algorithm](https://dev.mysql.com/doc/refman/5.6/en/index-merge-optimization.html#index-merge-intersection)
- [Index Merge Union Access Algorithm](https://dev.mysql.com/doc/refman/5.6/en/index-merge-optimization.html#index-merge-union)
- [Index Merge Sort-Union Access Algorithm](https://dev.mysql.com/doc/refman/5.6/en/index-merge-optimization.html#index-merge-sort-union)

**索引合并交集访问算法**

这种访问算法适用于当`WHERE`子句被转化为由 [`AND`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_and) 连接的不同键上的若干范围条件，同时每个条件都是下列之一：

* 此形式的*N*-part表达式，其中索引具有正好*N*个部分（即，所有索引部分都被覆盖）：

- ```sql
  key_part1 = const1 AND key_part2 = const2 ... AND key_partN = constN
  ```

- 任何范围条件都是在`InnoDB`表的主键上。

例子：

```sql
SELECT * FROM innodb_table
  WHERE primary_key < 10 AND key_col1 = 20;

SELECT * FROM tbl_name
  WHERE key1_part1 = 1 AND key1_part2 = 2 AND key2 = 2;
```

索引合并交集算法在所有用到的索引上执行模拟扫描，同时产生它从合并之后的索引扫描查询得到的行数据序列交集。

如果查询中用到的所有列都被用到的索引覆盖，则不会检索所有的行（这种情况下 [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 输出结果中`Extra`列包含`Using index`）。下面是这种查询的例子：

```sql
SELECT COUNT(*) FROM t1 WHERE key1 = 1 AND key2 = 1;
```

如果使用的索引未涵盖查询中使用的所有列，则仅在所有使用的键的范围条件都被满足时才检索所有行。

如果其中一个合并条件是`InnoDB`表的主键上的条件，则它不用于行检索，而是用于过滤掉使用其他条件检索的行。

**索引合并并集访问算法**

此算法的规则类似于索引合并交集算法。此算法适用于当表的`WHERE`子句被转化为若干由 [`OR`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_or) 连接的不同键上的若干范围条件，同时每个条件是下列之一：

- 此形式的*N*-part表达式，其中索引具有正好*N*个部分（即，所有索引部分都被覆盖）：

  ```sql
  key_part1 = const1 AND key_part2 = const2 ... AND key_partN = constN
  ```

- 任何范围条件都是在`InnoDB`表的主键上。

- 索引合并交集算法适用的条件。

例子：

```sql
SELECT * FROM t1
  WHERE key1 = 1 OR key2 = 2 OR key3 = 3;

SELECT * FROM innodb_table
  WHERE (key1 = 1 AND key2 = 2)
     OR (key3 = 'foo' AND key4 = 'bar') AND key5 = 5;
```

**索引合并有序并集访问算法**

此算法适用于当表的`WHERE`子句被转化为若干由 [`OR`](https://dev.mysql.com/doc/refman/5.6/en/logical-operators.html#operator_or) 连接的不同键上的若干范围条件，但是索引合并并集算法不适用。

例子：

```sql
SELECT * FROM tbl_name
  WHERE key_col1 < 10 OR key_col2 < 20;

SELECT * FROM tbl_name
  WHERE (key_col1 > 10 OR key_col2 = 20) AND nonkey_col = 30;
```

有序并集算法与并集算法的区别在于，有序并集算法必须首先获取行主键并在返回任何行之前对其进行排序。

#### 8.2.1.4 引擎条件下推优化

此优化改进未索引的列与常量直接比较的效率。这种情况下，该条件会被“下推”给存储引擎去解析。此优化只能被 [`NDB`](https://dev.mysql.com/doc/refman/5.6/en/mysql-cluster.html) 存储引擎使用。

对于NDB Cluster，此优化可以消除在集群的数据节点和发出查询的MySQL服务器之间通过网络发送不匹配行的需要，并且可以将查询速度提高5到10倍，相对于条件下推可用但不使用的情况。

假设NDB Cluster表定义如下：

```sql
CREATE TABLE t1 (
    a INT,
    b INT,
    KEY(a)
) ENGINE=NDB;
```

条件下推可以用于查询，例如此处展示的查询，其中包括非索引列和常量之间的比较：

```sql
SELECT a, b FROM t1 WHERE b = 10;
```

条件下推的使用可以在 [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 的输出中看到：

```sql
mysql> EXPLAIN SELECT a,b FROM t1 WHERE b = 10\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: t1
         type: ALL
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 10
        Extra: Using where with pushed condition
```

然而，条件下推不能被用于下面两个查询：

```sql
SELECT a,b FROM t1 WHERE a = 10;
SELECT a,b FROM t1 WHERE b + 1 = 10;
```

条件下推不适用于第一个查询，因为列`a`上存在索引。（索引访问方法将更有效，因此将优先于选择条件下推。）条件下推不能用于第二个查询，因为涉及非索引列`b`的比较是间接的。（但是，如果要在`WHERE`子句中将`b + 1 = 10`修改`b = 9`，则可以应用条件下推。）

当使用`>`或`<`运算符将索引列与常量进行比较时，也可以使用条件下推：

```sql
mysql> EXPLAIN SELECT a, b FROM t1 WHERE a < 2\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: t1
         type: range
possible_keys: a
          key: a
      key_len: 5
          ref: NULL
         rows: 2
        Extra: Using where with pushed condition
```

条件下推支持的其他比较包括以下内容：

- `column [NOT] LIKE pattern`

  其中*pattern* 必须是包含待匹配的模式的字符串字面量；其语法参见 [Section 12.5.1, “String Comparison Functions and Operators”](https://dev.mysql.com/doc/refman/5.6/en/string-comparison-functions.html).

- `column IS [NOT] NULL`

- `column IN (value_list)`

  *value_list* 中的每个元素都必须是字面值常量。

- `column BETWEEN constant1 AND constant2`

  *constant1* and *constant2* 都必须是字面值常量。

在前面列表中的所有情况中，查询条件可以转换为列和常量之间的一个或多个直接比较的形式。

默认情况下引擎条件下推是开启的。要在服务器启动时禁用它，请设置 [`optimizer_switch`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_optimizer_switch) 系统变量。例如，在`my.cnf`文件中，使用以下行：

```ini
[mysqld]
optimizer_switch=engine_condition_pushdown=off
```

在运行时，禁用条件下推，如下所示：

```sql
SET optimizer_switch='engine_condition_pushdown=off';
```

**局限性**  引擎条件下推有以下局限性：

- 引擎条件下推仅由 [`NDB`](https://dev.mysql.com/doc/refman/5.6/en/mysql-cluster.html) 存储引擎支持。
- 列只能与常量值比较，包括其值可以解析为常量的表达式。
- 用于比较的列不能是 [`BLOB`](https://dev.mysql.com/doc/refman/5.6/en/blob.html) 或者 [`TEXT`](https://dev.mysql.com/doc/refman/5.6/en/blob.html) 类型。
- 要与列进行比较的字符串值必须使用与列相同的排序规则。
- 不直接支持联接；涉及多个表的条件在可能的情况下分别下推。使用扩展的 [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) 输出来确定实际下推了哪些条件。请参见 [Section 8.8.3, “Extended EXPLAIN Output Format”](https://dev.mysql.com/doc/refman/5.6/en/explain-extended.html) 。

#### 8.2.1.5 索引条件下推优化

Index Condition Pushdown (ICP) is an optimization for the case where MySQL retrieves rows from a table using an index. Without ICP, the storage engine traverses the index to locate rows in the base table and returns them to the MySQL server which evaluates the `WHERE` condition for the rows. With ICP enabled, and if parts of the `WHERE` condition can be evaluated by using only columns from the index, the MySQL server pushes this part of the `WHERE` condition down to the storage engine. The storage engine then evaluates the pushed index condition by using the index entry and only if this is satisfied is the row read from the table. ICP can reduce the number of times the storage engine must access the base table and the number of times the MySQL server must access the storage engine.

Applicability of the Index Condition Pushdown optimization is subject to these conditions:

- ICP is used for the [`range`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_range), [`ref`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_ref), [`eq_ref`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_eq_ref), and [`ref_or_null`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_ref_or_null) access methods when there is a need to access full table rows.
- ICP can be used for [`InnoDB`](https://dev.mysql.com/doc/refman/5.6/en/innodb-storage-engine.html) and [`MyISAM`](https://dev.mysql.com/doc/refman/5.6/en/myisam-storage-engine.html) tables. (Exception: ICP is not supported with partitioned tables in MySQL 5.6; this issue is resolved in MySQL 5.7.)
- For `InnoDB` tables, ICP is used only for secondary indexes. The goal of ICP is to reduce the number of full-row reads and thereby reduce I/O operations. For `InnoDB` clustered indexes, the complete record is already read into the `InnoDB` buffer. Using ICP in this case does not reduce I/O.
- Conditions that refer to subqueries cannot be pushed down.
- Conditions that refer to stored functions cannot be pushed down. Storage engines cannot invoke stored functions.
- Triggered conditions cannot be pushed down. (For information about triggered conditions, see [Section 8.2.2.3, “Optimizing Subqueries with the EXISTS Strategy”](https://dev.mysql.com/doc/refman/5.6/en/subquery-optimization-with-exists.html).)

To understand how this optimization works, first consider how an index scan proceeds when Index Condition Pushdown is not used:

1. Get the next row, first by reading the index tuple, and then by using the index tuple to locate and read the full table row.
2. Test the part of the `WHERE` condition that applies to this table. Accept or reject the row based on the test result.

Using Index Condition Pushdown, the scan proceeds like this instead:

1. Get the next row's index tuple (but not the full table row).
2. Test the part of the `WHERE` condition that applies to this table and can be checked using only index columns. If the condition is not satisfied, proceed to the index tuple for the next row.
3. If the condition is satisfied, use the index tuple to locate and read the full table row.
4. Test the remaining part of the `WHERE` condition that applies to this table. Accept or reject the row based on the test result.

[`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) output shows `Using index condition` in the `Extra` column when Index Condition Pushdown is used. It does not show `Using index` because that does not apply when full table rows must be read.

Suppose that a table contains information about people and their addresses and that the table has an index defined as `INDEX (zipcode, lastname, firstname)`. If we know a person's `zipcode` value but are not sure about the last name, we can search like this:

```sql
SELECT * FROM people
  WHERE zipcode='95054'
  AND lastname LIKE '%etrunia%'
  AND address LIKE '%Main Street%';
```

MySQL can use the index to scan through people with `zipcode='95054'`. The second part (`lastname LIKE '%etrunia%'`) cannot be used to limit the number of rows that must be scanned, so without Index Condition Pushdown, this query must retrieve full table rows for all people who have `zipcode='95054'`.

With Index Condition Pushdown, MySQL checks the `lastname LIKE '%etrunia%'` part before reading the full table row. This avoids reading full rows corresponding to index tuples that match the `zipcode` condition but not the `lastname` condition.

Index Condition Pushdown is enabled by default. It can be controlled with the [`optimizer_switch`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_optimizer_switch) system variable by setting the`index_condition_pushdown` flag:

```sql
SET optimizer_switch = 'index_condition_pushdown=off';
SET optimizer_switch = 'index_condition_pushdown=on';
```

See [Section 8.9.2, “Switchable Optimizations”](https://dev.mysql.com/doc/refman/5.6/en/switchable-optimizations.html).

#### 8.2.1.6 嵌套循环连接算法

MySQL 使用嵌套循环算法或者其变体执行表连接。

- [嵌套循环连接算法](https://dev.mysql.com/doc/refman/5.6/en/nested-loop-joins.html#nested-loop-join-algorithm)
- [块嵌套循环连接算法](https://dev.mysql.com/doc/refman/5.6/en/nested-loop-joins.html#block-nested-loop-join-algorithm)

##### 嵌套循环连接算法

简单的嵌套循环算法（NLJ）从第一个表中循环读取行，每次循环读取一行，将每一行传递给嵌套循环，该嵌套循环处理连接的下一个表。这个嵌套过程重复多少次取决于连接的表的数量。

假定连接3个表`t1`，`t2`和`t3`，该连接将以下面的连接类型被执行：

```
Table   Join Type
t1      range
t2      ref
t3      ALL
```

如果使用简单的 NLJ 算法，则该连接将会被如下处理：

```java
for each row in t1 matching range {
  for each row in t2 matching reference key {
    for each row in t3 {
      if row satisfies join conditions, send to client
    }
  }
}
```

由于 HLJ 算法每次都将一行数据从外层循环传入内层循环，显然就会读取内层循环处理的表很多次。

##### 块嵌套循环连接算法

块嵌套循环（BNL）连接算法使用从外层循环读取而来的表行数据的缓冲来减少内层循环中表的读取次数。比如，如果10行数据被读取缓冲，然后该缓冲被传入下一层内循环，则内层循环读取的每一行都能与所有这10行数据进行比较。这就将内层循环读取表的次数降低了一个数量级。

MySQL 连接缓冲具有这些特点：

- 连接缓冲可以被用在类型为 [`ALL`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_all) 或者 [`index`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_index) (换句话说，当不能使用任何可能的键，并且分别完成数据或索引行的完全扫描时)，或者 [`range`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_range) 的连接上。连接缓冲同样适用于外连接，具体细节参见 [Section 8.2.1.11, “Block Nested-Loop and Batched Key Access Joins”](https://dev.mysql.com/doc/refman/5.6/en/bnl-bka-optimization.html) 。
- 永远不会为第一个非常量表分配连接缓冲区，即使连接类型是 [`ALL`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_all) 或者 [`index`](https://dev.mysql.com/doc/refman/5.6/en/explain-output.html#jointype_index).
- 连接缓冲区只会保存连接相关的列，而不是整行。
- [`join_buffer_size`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_join_buffer_size) 系统变量决定了用于处理每个查询的每个连接缓冲区的大小。
- 为每个可以被缓冲的连接分配缓冲区，因此一个给定的查询可能会使用多个连接缓冲区来处理。
- 连接缓冲区在执行连接之前分配，在查询完成之后释放。

上面描述的例子连接使用了 NLJ 算法（没有缓冲），如果使用连接缓冲，就会是下面这个样子：

```java
for each row in t1 matching range {
  for each row in t2 matching reference key {
    store used columns from t1, t2 in join buffer
    if buffer is full {
      for each row in t3 {
        for each t1, t2 combination in join buffer {
          if row satisfies join conditions, send to client
        }
      }
      empty join buffer
    }
  }
}

if buffer is not empty {
  for each row in t3 {
    for each t1, t2 combination in join buffer {
      if row satisfies join conditions, send to client
    }
  }
}
```

如果`S`表示连接缓冲区中存储的每个`t1, t2`组合的大小，而`C`表示缓冲区中这种租车的数量，则表`t3`被扫描的次数就是：

```
(S * C)/join_buffer_size + 1
```

`t3`表扫描次数会随着  [`join_buffer_size`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_join_buffer_size) 值的增大而减小，极限是  [`join_buffer_size`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_join_buffer_size) 大到足以容纳所有的行组合。此时，继续增大  [`join_buffer_size`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_join_buffer_size) 就不再能获得任何速度提升。

