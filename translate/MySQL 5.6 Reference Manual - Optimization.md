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

Besides [`SELECT`](https://dev.mysql.com/doc/refman/5.6/en/select.html) statements, the tuning techniques for queries also apply to constructs such as [`CREATE TABLE...AS SELECT`](https://dev.mysql.com/doc/refman/5.6/en/create-table-select.html), [`INSERT INTO...SELECT`](https://dev.mysql.com/doc/refman/5.6/en/insert-select.html), and `WHERE` clauses in[`DELETE`](https://dev.mysql.com/doc/refman/5.6/en/delete.html) statements. Those statements have additional performance considerations because they combine write operations with the read-oriented query operations.

NDB Cluster supports a join pushdown optimization whereby a qualifying join is sent in its entirety to NDB Cluster data nodes, where it can be distributed among them and executed in parallel. For more information about this optimization, see [Conditions for NDB pushdown joins](https://dev.mysql.com/doc/refman/5.6/en/mysql-cluster-options-variables.html#ndb_join_pushdown-conditions),

The main considerations for optimizing queries are:

- To make a slow `SELECT ... WHERE` query faster, the first thing to check is whether you can add an [index](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_index). Set up indexes on columns used in the `WHERE` clause, to speed up evaluation, filtering, and the final retrieval of results. To avoid wasted disk space, construct a small set of indexes that speed up many related queries used in your application.

  Indexes are especially important for queries that reference different tables, using features such as [joins](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_join) and [foreign keys](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_foreign_key). You can use the [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) statement to determine which indexes are used for a [`SELECT`](https://dev.mysql.com/doc/refman/5.6/en/select.html). See [Section 8.3.1, “How MySQL Uses Indexes”](https://dev.mysql.com/doc/refman/5.6/en/mysql-indexes.html) and [Section 8.8.1, “Optimizing Queries with EXPLAIN”](https://dev.mysql.com/doc/refman/5.6/en/using-explain.html).

- Isolate and tune any part of the query, such as a function call, that takes excessive time. Depending on how the query is structured, a function could be called once for every row in the result set, or even once for every row in the table, greatly magnifying any inefficiency.

- Minimize the number of [full table scans](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_full_table_scan) in your queries, particularly for big tables.

- Keep table statistics up to date by using the [`ANALYZE TABLE`](https://dev.mysql.com/doc/refman/5.6/en/analyze-table.html) statement periodically, so the optimizer has the information needed to construct an efficient execution plan.

- Learn the tuning techniques, indexing techniques, and configuration parameters that are specific to the storage engine for each table. Both `InnoDB` and `MyISAM` have sets of guidelines for enabling and sustaining high performance in queries. For details, see [Section 8.5.6, “Optimizing InnoDB Queries”](https://dev.mysql.com/doc/refman/5.6/en/optimizing-innodb-queries.html) and [Section 8.6.1, “Optimizing MyISAM Queries”](https://dev.mysql.com/doc/refman/5.6/en/optimizing-queries-myisam.html).

- You can optimize single-query transactions for `InnoDB` tables, using the technique in [Section 8.5.3, “Optimizing InnoDB Read-Only Transactions”](https://dev.mysql.com/doc/refman/5.6/en/innodb-performance-ro-txn.html).

- Avoid transforming the query in ways that make it hard to understand, especially if the optimizer does some of the same transformations automatically.

- If a performance issue is not easily solved by one of the basic guidelines, investigate the internal details of the specific query by reading the [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) plan and adjusting your indexes, `WHERE` clauses, join clauses, and so on. (When you reach a certain level of expertise, reading the [`EXPLAIN`](https://dev.mysql.com/doc/refman/5.6/en/explain.html) plan might be your first step for every query.)

- Adjust the size and properties of the memory areas that MySQL uses for caching. With efficient use of the `InnoDB` [buffer pool](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_buffer_pool), `MyISAM` key cache, and the MySQL query cache, repeated queries run faster because the results are retrieved from memory the second and subsequent times.

- Even for a query that runs fast using the cache memory areas, you might still optimize further so that they require less cache memory, making your application more scalable. Scalability means that your application can handle more simultaneous users, larger requests, and so on without experiencing a big drop in performance.

- Deal with locking issues, where the speed of your query might be affected by other sessions accessing the tables at the same time.