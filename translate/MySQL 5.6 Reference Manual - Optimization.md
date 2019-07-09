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

Any database application eventually hits hardware limits as the database becomes more and more busy. A DBA must evaluate whether it is possible to tune the application or reconfigure the server to avoid these [bottlenecks](https://dev.mysql.com/doc/refman/5.6/en/glossary.html#glos_bottleneck), or whether more hardware resources are required. System bottlenecks typically arise from these sources:

- Disk seeks. It takes time for the disk to find a piece of data. With modern disks, the mean time for this is usually lower than 10ms, so we can in theory do about 100 seeks a second. This time improves slowly with new disks and is very hard to optimize for a single table. The way to optimize seek time is to distribute the data onto more than one disk.
- Disk reading and writing. When the disk is at the correct position, we need to read or write the data. With modern disks, one disk delivers at least 10–20MB/s throughput. This is easier to optimize than seeks because you can read in parallel from multiple disks.
- CPU cycles. When the data is in main memory, we must process it to get our result. Having large tables compared to the amount of memory is the most common limiting factor. But with small tables, speed is usually not the problem.
- Memory bandwidth. When the CPU needs more data than can fit in the CPU cache, main memory bandwidth becomes a bottleneck. This is an uncommon bottleneck for most systems, but one to be aware of.

### Balancing Portability and Performance

To use performance-oriented SQL extensions in a portable MySQL program, you can wrap MySQL-specific keywords in a statement within `/*! */` comment delimiters. Other SQL servers ignore the commented keywords. For information about writing comments, see [Section 9.6, “Comment Syntax”](https://dev.mysql.com/doc/refman/5.6/en/comments.html).