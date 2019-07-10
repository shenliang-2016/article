# 目录

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

  In this example, the interval on the first line uses one key part for the left bound and two key parts for the right bound. The interval on the second line uses only one key part. The `key_len` column in the [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) output indicates the maximum length of the key prefix used.

  In some cases, `key_len` may indicate that a key part was used, but that might be not what you would expect. Suppose that *key_part1* and *key_part2* can be `NULL`. Then the `key_len` column displays two key part lengths for the following condition:

  ```sql
  key_part1 >= 1 AND key_part2 < 2
  ```

  But, in fact, the condition is converted to this:

  ```sql
  key_part1 >= 1 AND key_part2 IS NOT NULL
  ```

For a description of how optimizations are performed to combine or eliminate intervals for range conditions on a single-part index, see [Range Access Method for Single-Part Indexes](https://dev.mysql.com/doc/refman/5.6/en/range-optimization.html#range-access-single-part). Analogous steps are performed for range conditions on multiple-part indexes.

**Equality Range Optimization of Many-Valued Comparisons**

Consider these expressions, where *col_name* is an indexed column:

```sql
col_name IN(val1, ..., valN)
col_name = val1 OR ... OR col_name = valN
```

Each expression is true if *col_name* is equal to any of several values. These comparisons are equality range comparisons (where the “range” is a single value). The optimizer estimates the cost of reading qualifying rows for equality range comparisons as follows:

- If there is a unique index on *col_name*, the row estimate for each range is 1 because at most one row can have the given value.
- Otherwise, any index on *col_name* is nonunique and the optimizer can estimate the row count for each range using dives into the index or index statistics.

With index dives, the optimizer makes a dive at each end of a range and uses the number of rows in the range as the estimate. For example, the expression `*col_name* IN (10, 20, 30)` has three equality ranges and the optimizer makes two dives per range to generate a row estimate. Each pair of dives yields an estimate of the number of rows that have the given value.

Index dives provide accurate row estimates, but as the number of comparison values in the expression increases, the optimizer takes longer to generate a row estimate. Use of index statistics is less accurate than index dives but permits faster row estimation for large value lists.

The [`eq_range_index_dive_limit`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_eq_range_index_dive_limit) system variable enables you to configure the number of values at which the optimizer switches from one row estimation strategy to the other. To permit use of index dives for comparisons of up to *N* equality ranges, set [`eq_range_index_dive_limit`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_eq_range_index_dive_limit) to *N* + 1. To disable use of statistics and always use index dives regardless of *N*, set [`eq_range_index_dive_limit`](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html#sysvar_eq_range_index_dive_limit) to 0.

To update table index statistics for best estimates, use [`ANALYZE TABLE`](https://dev.mysql.com/doc/refman/5.6/en/analyze-table.html).

Even under conditions when index dives would otherwise be used, they are skipped for queries that satisfy all these conditions:

- A single-index `FORCE INDEX` index hint is present. The idea is that if index use is forced, there is nothing to be gained from the additional overhead of performing dives into the index.
- The index is nonunique and not a `FULLTEXT` index.
- No subquery is present.
- No `DISTINCT`, `GROUP BY`, or `ORDER BY` clause is present.

Those dive-skipping conditions apply only for single-table queries. Index dives are not skipped for multiple-table queries (joins).