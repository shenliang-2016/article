# [一文说清 InnoDB 的事务机制](https://www.cnblogs.com/rickiyang/p/13652664.html)

我们从一个转账的故事开始。

隔壁小王从美团上找到了一家水饺店，准备中午吃水饺。下单成功，支付20元。

商家这里响了一下：叮叮，您有美团外卖新订单啦，请及时处理。水饺一份，好嘞，下锅。

很快小王吃到外卖了，吃完美美地躺下开始睡觉。

突然手机一顿猛响。一个陌生的号码打过来的，又是卖房的吧。小王想想没理他，继续睡。

可是这哥么锲而不舍，一会又打过来了。小王忍无可忍准备接过电话骂他一顿。刚接电话听到对面一阵急促的声音传来：你好你中午是不是点了一份我们店的水饺？

小王这才意识到感情是水饺店的。赶忙回复到是的啊，咋了。

老板说：你中午下单付款了吗？

小王：我肯定付款了啊，不然怎么下单。

老板说：我没收到钱啊。你把付款的截图发给我。

小王说：我吃饭还能不付钱吗，你等着。

于是小王给老板截图了，老板拿着截图去找了美团技术，美团技术一查，转账失败。跟老板说不好意思，今天这代码是实习生写的，我们马上开除他，稍后转给你。这时候老板一颗悬着的心才放下，可不能一天就卖一份水饺还没收到钱，这不亏大了呢！

以上纯属虚构，没有诋毁美团实习生的意思。

从上面的问题看，付款成功了，转账失败了，这时候用户吃到了饭，但是老板没收到钱。放在正常的堂食，你不先付款，估计人儿就的赶你出去，一手交钱一手交货买卖不变的道理。

我们引申出一个概念：**最小操作单元**。即我们人为定义了一个业务场景，这个场景中的操作要么全部成功，要么全部失败。

英语原文中把这种最小操作单元定义为：transaction ，在英语中的解释是：

> an occasion when someone buys or sells something, or when money is exchanged or the activity of buying or selling something:
>
> - a business transaction
> - Each transaction at the foreign exchange counter seems to take forever
> - We need to monitor the transaction of smaller deals.

通俗的说就是我们做某事所发生的这个时机或这个场景，代指这整个的发生过程。在 MySQL 中我们把 transaction 翻译为 **事务**，个人感觉中文意思总和英文有点不搭。

上面这个例子中我们可以了解到 transaction 存在的主要意图：

1. 在最小操作单元中保持稳定的操作，即使在故障时也能恢复到操作之前的状态保持数据一致性。
2. 保持各个最小操作单元之前互相隔离，以防止互相交互产生的覆盖性错误。

一般需要事务来控制的场景发生在：

**更新--插入--选择--插入--**

即一个最小操作单元中保持两个及以上的非查询操作。

事务结束的两种可能方式：

- commit：提交最小操作单元中的所有操作。
- terminate：操作终止，最小操作单元中所有修改无效。

数据库操作的环境：

- 共享-多用户并发访问
- 不稳定-潜在的硬件/软件故障

事务所需环境：

- 不共享 - 一个事务内的操作不受其他事务影响
- 稳定 - 即使面对系统故障，当前事务的操作也能保留现场

一个事务一旦开始，则必须确保：

- 所有操作必须可回溯
- 所有操作对后续操作的影响必须是可见的

一个事务开始的过程中必须确保：

在该事务结束之前其他事务看不到它的结果。

如果事务中止：

必须确保当前事务所有可能影响数据一致性的操作都会被清理。

如果系统出现故障：

必须确保重新启动时所有未提交的事务都会被清理。

针对以上事务操作过程中可能会出现的问题，抽象出事务如果满足以下条件，则可以保证数据完整性：

- Automicity（原子性）

  要么事务中的所有任务都必须发生，要么都不发生。

- Consistency（一致性）

  每个事务都必须保留数据库的完整性约束（已声明的一致性规则）。它不能使数据处于矛盾状态。在执行期间，一系列数据库操作不会违反任何完整性约束。

- Isolation（隔离性）

  两个同时进行的事务不能互相干扰。交易中的中间结果必须对其他交易不可见。其他一系列数据库操作无法看到一系列数据库操作的中间状态。

- Durability（持久性）

  已完成的事务以后不能中止或放弃其结果。它们必须在崩溃后通过（例如）重新启动DBMS持续存在。保证已提交的一系列数据库操作将永久保留。

特意查证了一下，关于事务四大特性的提出最早是在 1983 年由 Andreas Reuter 和 Theo Haerder 两位关系型数据库研发的鼻祖在论文：`Principles of transaction-oriented database recovery` 中提出。[论文链接](https://dl.acm.org/doi/10.1145/289.291)，感兴趣的可以下载来看看。

事务的 ACID 特性概念简单，但不是很好理解，主要是因为这几个特性不是一种平级关系：

- 只有满足一致性，事务的执行结果才是正确的。
- 在无并发的情况下，事务串行执行，隔离性一定能够满足。此时只要能满足原子性，就一定能满足一致性。 在并发的情况下多个事务并行执行，事务不仅要满足原子性，还需要满足隔离性，才能满足一致性。
- 事务满足持久化是为了能应对数据库崩溃的情况。

#### InnoDB 如何实现事务[#](https://www.cnblogs.com/rickiyang/p/13652664.html#4265618923)

鉴于 MyISAM 引擎不支持事务，支持事务的引擎只有 InnoDB，所以下面关于事务的讲解都是基于 InnoDB引擎。

在 InnoDB引擎中实现事务最重要的东西就是日志文件，保证事务的四大特性主要依靠这两大日志：

- redo log ：保证事务持久性
- undo log：回滚日志，保证事务原子性

两大日志系统分别保证了持久性和原子性，另外还有两大特性是通过什么来保证的呢？

一致性 和 隔离性 是通过 MVCC 机制 和 锁机制来一起控制。先提前介绍，后面我们详解讨论。

典型的事务操作会遵循如下流程：

```sql
Copystart transaction;
...... # do your business
commit;
```

`start transaction` 标识事务的开始，直到遇到 `commit` 才会提交事务。在该事务过程中如果出现问题，会自动调用 rollback 逻辑回滚该事物已完成的 sql。

**非显式开启事务**

MySQL 中默认采用的是自动提交的模式：

```sql
Copymysql > show variables like 'autocommit';
+------------------+-------+
|   Variable_name  | Value |
+------------------+-------+
|   autocomment    | ON    |
+------------------+-------+
```

自动模式下，你无需显式的输入 `start transaction` 作为开头和使用 `commit` 作为结尾来标识一个事务。每个sql 语句都会被作为一个事务提交。

当然你也可以关闭自动提交事务机制：

```sql
Copymysql > set autocommit = 0;
```

需要注意的是：`autocommit` 参数的修改指**只针对当前连接**，在一个连接中修改该属性并不会影响别的连接。

**不被 autocommit 影响的操作**

MySQL 中提供了一些不会被 autocommit 属性值所影响的特殊指令，这些指定即使在事务中执行，他们也会立刻执行而不是等到 commit 语句之后再提交，这些特殊指令包括：`DDL(create table / drop table / alter table)`、`lock tables`等等。

**我们探讨事务到底在探讨什么？**

事务的定义我们已经了解，无非就是把几个有上下文关联的 sql 放在一起操作要么全部成功，要么全部失败。道理很简单，那我们分析这么多到底在分析什么呢？貌似难的点不在于打包执行，在于如果让这些打包命中不互相影响，事务执行过程中失败如何回滚操作且不污染现有数据。这些才是我们讨论事务应该关注的地方。

这些问题的根本其实又回到了事务的四大特性，不得不说 Theo Haerder 在 1983 年就能抽象出来如此高度凝练的总结实在是让当下汗颜。

下面我就从 InnoDB 如何保证四大特性入手，逐一分析事务机制的实现。

#### 保证原子性的关键技术 - undo log[#](https://www.cnblogs.com/rickiyang/p/13652664.html#3352576151)

对于事务的原子性来说，该事务内所有操作要么全部成功要么全部失败就是事务的原子性。

全部成功这个毋庸置疑，如果中间突然失败，原子性该如何保证呢？是否该回滚当前已经执行成功的操作。

InnoDB 提供了一种日志：undo log，它有两个作用：提供 回滚 和 多个行版本控制(MVCC)。

比如一条 delete 操作在 undo log 中会对应一条 insert 记录，反之亦然。当 update 操作时，它会记录一条相反的 update 记录。

当执行 rollback 时，就可以从 undo log 中的逻辑记录读取到相应的内容并进行回滚。

有时候应用到行版本控制的时候，也是通过 undo log 来实现的：当读取的某一行被其他事务锁定时，它可以从 undo log 中分析出该行记录以前的数据是什么，从而提供该行版本信息，让用户实现非锁定一致性读取。

**undo log 的存储方式**

InnoDB 存储引擎对 undo log 的管理采用段的方式。rollback segment 称为回滚段，每个回滚段中有 1024 个 undo log slot 。

在以前老版本，只支持 1 个 rollback segment，这样就只能记录 1024 个 undo log slot。后来 MySQL5.5 可以支持 128 个 rollback slot，即支持 128 * 1024 个 undo log 操作。

MySQL5.6 之前，undo log 表空间位于共享表空间的回滚段中，共享表空间的默认的名称是 ibdata，位于数据文件目录中。
MySQL5.6 之后，undo log 表空间可以配置成独立的文件，但是提前需要在配置文件中配置，完成数据库初始化后生效且不可改变 undo log 文件的个数。如果初始化数据库之前没有进行相关配置，那么就无法配置成独立的表空间了。
MySQL5.7 之后的独立 undo log 表空间配置参数如下：

```text
Copyinnodb_undo_directory = /data/undospace/ #undo独立表空间的存放目录
innodb_undo_logs = 128 #回滚段为128KB
innodb_undo_tablespaces = 4 #指定有4个undo log文件
```

**undo log 的删除时机**

undo log 文件的个数是有限制的，所以不用无限堆积日志文件。undo log 记录的是当前事务操作的反向记录，理论上当前事务结束，undo log 日志就可以废弃。上面也提到过的多版本并发控制机制在隔离级别为 `repeatable read` 的时候事务读取的数据都是该事务最新提交的版本，那么只要该事务不结束，行版本记录就不能删除。

另外不同的 sql 语句对应的 undo log 类型也不一样，比如：

- insert 语句：因为 insert 操作本身只对该事务可见，事务提交之前别的连接是看不到的，所以 insert 操作产生的 undo log 日志在事务提交之后会马上直接删除，后续不会再被别的功能使用。
- update / delete 语句：delete 操作在事务中并不会真的先删除数据，而是将该条数据打上 “delete_bit” 标识，后续的删除操作是在事务提交后的 purge 线程独立操作。这两种操作产生的 undo log 日志都可以用反向的 update 来代替，这种操作上面说过 MVCC 机制可能会用上，所以就不能在事务结束之后直接删除。

在事务提交之后，也不是马上就删除该事务对应的 undo log 日志，而是将该事务对应的文件块放入到删除列表中，未来通过 purge 来删除。并且提交事务时，还会判断 undo log 分配的页是否可以重用，如果可以重用，则会分配给后面来的事务，避免为每个独立的事务分配独立的 undo log 页而浪费存储空间和性能。

#### 持久性 - redo log[#](https://www.cnblogs.com/rickiyang/p/13652664.html#182700068)

redo log 即重做日志，重做日志记录每次操作的物理修改。

说 redo log 之前其实是要先说一下 binlog，不然就不知道为什么要引入 redo log。

bin log = binary log，二进制日志，它记录了除了 select 之外所有的 DDL 和 DML 语句。以事件形式记录，还包含语句所执行的消耗的时间，MySQL 的二进制日志是事务安全型的。

binlog日志有两个最重要的使用场景：

1. mysql 主从复制： mysql replication 在 master 端开启 binlog，master 把它的二进制日志传递给 slaves 来达到 master-slave 数据一致的目的。
2. 数据恢复： 通过 mysqlbinlog 工具来恢复数据。

binlog 日志包括两类文件：

1. 二进制日志索引文件（文件名后缀为 .index）用于记录所有的二进制文件。
2. 二进制日志文件（文件名后缀为 .00000*）记录数据库所有的 DDL 和 DML 语句事件。

binlog 文件是通过追加的方式写入的，可通过配置参数`max_binlog_size`设置每个 binlog 文件的大小，当文件大小大于给定值后，日志会发生滚动，之后的日志记录到新的文件上。
binlog 有两种记录模式，statement 格式的话是记 sql 语句，row 格式会记录行的内容。

持久性问题一般在发生故障的情况才会重视。在启动 MySQL 之后无论上次是否正常关闭都会进行恢复操作，我们假设现在没有 redo log 只有 binlog，那么数据文件的更新和写入 binlog 只有两种情况：

- 先更新数据文件，再写入 binlog；
- 先写入 binlog，再更新数据文件。

如果先更新数据文件，接着服务器宕机，则导致 binlog 中缺少最后的更新信息；如果先写 binlog 再更新数据则可能导致数据文件未被更新。

所以在只有 binlog 的环境中 MySQL 是不具备 crash-safe 的能力。另外一开始的 MySQL 使用 MyISAM 引擎，它只有 binlog，所以自然不支持事务。后面引入了 InnoDB 之后才开始使用另外一套日志系统- redo log 来实现 crash-safe 功能。

redo log 和 binlog 的区别：

- redo log 是 InnoDB 引擎特有的，binlog 是MySQL server 层实现的功能，与引擎无关。
- redo log 是物理日志，记录 “在某个数据页做了什么修改”；binlog 是逻辑日志，记录 sql 语句的原始逻辑，比如 “给 ID = 1 这一行的 name value set ‘xiaoming’ ”。
- redo log 空间是固定的，用完之后会覆盖之前的数据；binlog 是追加写，当前文件写完之后会开启一个新文件继续写。

redo log 由两部分组成：

- 内存中的重做日志缓冲(redo log buffer)
- 重做日志文件(redo log file)

**一个更新事务的整体流程**

![2](https://tva1.sinaimg.cn/large/007S8ZIlgy1gimsswons7j31gk0pgwjh.jpg)

从一个事务的更新过程出发看看一个事务更新过程中 redo log 处于什么地位。

1. 首先检查 Buffer cache 中是否存在这条数据，如果存在直接返回，如果不存在则去索引树中读取这条数据并加载到 Buffer Cache。
2. 执行器拿到这条行数据之后对它执行相应的更新操作。
3. 将这条待更新的行数据调用执行引擎更新到 Buffer Cache 中，同时将这个记录更新到 redo log 里面，redo log 包含两个部分的更新，更新完毕，此时 redo log 处于 prepare 的状态，然后告诉执行器，你可以提交事务。
4. 执行器生成这个操作的 binlog 日志，并把 binlog 写入磁盘。
5. 执行器调用引擎的提交事务接口，引擎把刚写入的 redo log 改为 commit 状态，整个事务提交完成。

这里我们注意到在 redo log 的提交过程中引入了**两阶段提交**。

**两阶段提交**

为什么必须有 “两阶段提交” 呢？这是为了让两份日志之间的逻辑一致。

前面我们说过了，binlog 会记录所有的逻辑操作，并且是采用 “追加写” 的形式。如果你的 DBA 承诺说半个月内可以恢复，那么备份系统中一定会保存最近半个月的所有binlog，同时系统会定期做整库备份。

由于 redo log 和 binlog 是两个独立的逻辑，如果不用两阶段提交，要么就是先写完 redo log 再写 binlog，或者采用反过来的顺序，我们看看这两种方式会有什么问题，用上面的 update 示例做假设：

1. **先写 redo log 后写 binlog**。假设在 redo log 写完，binlog 还没有写完的时候，MySQL 进程异常重启。因为 redo log 已经写完，系统即使崩溃仍然能够把数据恢复回来。但是 binlog 里面就没有记录这个语句，因此备份日志的时候 binlog 里面就没有这条语句。

   但是如果需要用这个 binlog 来恢复临时库的话，由于这个语句的 binlog 丢失，恢复出来的值就与原库值不同。

2. **先写 binlog 后写 redo log**。如果在 binlog 写完之后宕机，由于 redo log 还没写，崩溃恢复以后这个事务无效，所以这一行的值还是未更新以前的值。但是 binlog 里面已经记录了崩溃前的更新记录， binlog 来恢复的时候就多了一个事务出来与原库的值不同。

可以看到，两阶段提交就是为了防止 binlog 和 redo log 不一致发生。同时我们也注意到为了这个崩溃恢复的一致性问题引入了很多新的东西，也让系统复杂了很多，所以有得有失。

InnoDB通过 `Force Log at Commit` 机制保证持久性：当事务提交(COMMIT)时，必须先将该事务的所有日志缓冲写入到重做日志文件进行持久化，才能 COMMIT 成功。

为了确保每次日志都写入 redo log 文件，在每次将 redo log buffer cache 写入重做日志文件后，InnoDB 引擎都需要调用一次 fsync 操作。因此磁盘的性能决定了事务提交的性能，也就是数据库的性能。

`innodb_flush_log_at_trx_commit` 参数控制重做日志刷新到磁盘的策略：

- 0：事务提交时不进行写入重做日志操作，仅在 master thread 每秒进行一次。
- 1：事务提交时必须调用一次`fsync`操作。
- 2：仅写入文件系统缓存，不进行`fsync`操作。

log buffer 根据如下规则写入到磁盘重做日志文件中：

- 事务提交时。
- 当 log buffer 中有一半的内存空间已经被使用。
- log checkpoint 时，**checkpoint在一定程度上代表了刷到磁盘时日志所处的LSN位置。**

#### 一致性 和 隔离性实现 - 锁机制 和 MVCC[#](https://www.cnblogs.com/rickiyang/p/13652664.html#3133079829)

实现一致性和隔离性是保证数据准确性的关键一环，前面两个特性保证数据恢复不出问题，这两个特性要保证数据插入和读取不出问题。实现一致性和隔离性主要使用了两个机制：

- 锁机制
- 多版本并发控制

下面我们就事务会产生哪些问题，MySQL 提出什么方式来解决问题，这些方式的实现方案又是什么来讲解。

##### 并发下事务会产生哪些问题

事务 A 和 事务 B 同时操作一个资源，根据不同的情况可能会出现不同问题，总结下来有以下几种：

- 脏读

  事务 A 读到了事务 B 还未提交的数据。

- 幻读

  在当前事务中发现了不属于当前事务操作的数据。幻读是针对数据 insert 操作来说的。假设事务A对某些行的内容作了更改，但是还未提交，此时事务 B 插入了与事务 A 更改前的记录相同的记录行，并且在事务 A 提交之前先提交了，而这时，在事务A中查询，会发现好像刚刚的更改对于某些数据未起作用，但其实是事务 B 刚插入进来的，让用户感觉出现了幻觉，这就叫幻读。

- 可重复读

  可重复读指的是在一个事务内，最开始读到的数据和事务结束前的任意时刻读到的同一批数据都是一致的。通常针对数据 update 操作。

- 不可重复读

  在同一个事务中两次读取一个数据的结果不一样。对比可重复读，不可重复读指的是在同一事务内，不同的时刻读到的同一批数据可能是不一样的，可能会受到其他事务的影响，比如其他事务改了这批数据并提交了。

##### 为什么会提出隔离级别的概念

为了解决事务并发过程中可能会产生的这些问题，SQL 标准定义的四种隔离级别被 ANSI（美国国家标准学会）和 ISO/IEC（国际标准）采用，每种级别对事务的处理能力会有不同程度的影响。

SQL 标准定义了四种隔离级别，MySQL 全都支持。这四种隔离级别分别是：

1. 读未提交（READ UNCOMMITTED）
2. 读提交 （READ COMMITTED）
3. 可重复读 （REPEATABLE READ）
4. 串行化 （SERIALIZABLE）

从上往下，隔离强度逐渐增强，性能逐渐变差。采用哪种隔离级别要根据系统需求权衡决定，其中，**可重复读**是 MySQL 的默认级别。

事务隔离其实就是为了解决上面提到的脏读、不可重复读、幻读这几个问题，下面展示了 4 种隔离级别对这三个问题的解决程度。

| 隔离级别 | 脏读     | 不可重复读 | 幻读     |
| -------- | -------- | ---------- | -------- |
| 读未提交 | 会发生   | 会发生     | 会发生   |
| 读提交   | 不会发生 | 会发生     | 会发生   |
| 可重复读 | 不会发生 | 不会发生   | 会发生   |
| 串行化   | 不会发生 | 不会发生   | 不会发生 |

只有串行化的隔离级别解决了全部这 3 个问题，其他的 3 个隔离级别都有缺陷。

##### 如何设置事务隔离级别

我们可以通过以下语句查看当前数据库的隔离级别，通过下面语句可以看出我使用的 MySQL 的隔离级别是 `REPEATABLE-READ`，也就是可重复读，这也是 MySQL 的默认级别。

```sql
Copymysql> show variables like 'transaction_isolation';
+-----------------------+-----------------+
| Variable_name         | Value           |
+-----------------------+-----------------+
| transaction_isolation | REPEATABLE-READ |
+-----------------------+-----------------+
1 row in set (0.02 sec)

或者：

mysql> SELECT @@transaction_isolation;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| REPEATABLE-READ         |
+-------------------------+
1 row in set (0.00 sec)
```

当然我们也能手动修改事务的隔离级别：

```sql
Copyset [作用域] transaction isolation level [事务隔离级别];
作用域包含：
SESSION：SESSION 只针对当前回话窗口
GLOBAL：全局生效

隔离级别包含：
READ UNCOMMITTED | READ COMMITTED | REPEATABLE READ | SERIALIZABLE
```

我们来测试一下各个隔离级别对事务的影响。

新建表：

```sql
CopyCREATE TABLE `test_db` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) NOT NULL DEFAULT '' COMMENT 'name',
  PRIMARY KEY (`id`),
  KEY `name_idx` (`name`(191))
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 ROW_FORMAT=COMPACT COMMENT='测试表';
```

插入一些测试数据。

##### 读未提交（READ UNCOMMITTED）

首先设置事务隔离级别：

```sql
Copyset global transaction isolation level READ UNCOMMITTED;
```

注意：**设置完全局隔离级别只对新打开的 session 有效，历史打开的是不会受到影响的。**

首先关闭事务自动提交：

```sql
Copyset autocommit = 0;
```

开启事务 A：

```sql
CopyQuery OK, 0 rows affected (0.00 sec)

mysql>
mysql> insert test_db (name) values ('xiaocee');
Query OK, 1 row affected (0.01 sec)
```

在事务A 中插入一条数据，并未提交事务。

接着开启事务B：

```sql
Copymysql> select * from test_db;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaocee   |
+----+-----------+
9 rows in set (0.00 sec)
```

事务 B 中能够查到这条数据。**即不同的事务能读到对方未提交的数据**。连脏读都无法解决，可重复读和幻读更没法解决。

##### 读已提交

读已提交的数据肯定能解决脏读问题，但是对于幻读和不可重复读无法将解决。

首先设置事务隔离级别：

```sql
Copyset global transaction isolation level READ COMMITTED;
```

现在数据库数据如下：

```sql
Copymysql> select * from test_db;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming2 |
|  2 | xiaohong  |
|  3 | xiaowei   |
|  4 | xiaowei1  |
|  5 | xiaoli    |
|  6 | xiaoche   |
|  8 | xiaoche   |
| 10 | xiaoche   |
| 12 | xiaocee   |
+----+-----------+
9 rows in set (0.00 sec)
```

开启事务 A 将 `id=1` 的数据改为 “xiaoming3”：

```sql
Copymysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> update test_db set name = 'xiaoming3' where id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

这里事务 A 未提交，接着开启事务B 做第一次查询：

```sql
Copymysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from test_db where id = 1;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming2 |
+----+-----------+
9 rows in set (0.00 sec)
```

事务B查询还是原始值。

下面提交事务 A：

```sql
Copymysql> commit;
Query OK, 0 rows affected (0.00 sec)
```

接着在事务 B 中再查询一次：

```sql
Copymysql> select * from test_db where id = 1;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming3 |
+----+-----------+
1 row in set (0.00 sec)
```

当然这次查到的肯定是人家已提交的数据。这里发生的问题就是不可重复读：即同一个事务内每次读取同一条数据的结果不一样。

##### 可重复读

可重复读隔离级别的含义就是重读每次都一样不会有问题。这就意味着一个事务不会读取到别的事务未提交的修改。但是这里就会有另一个问题：在别的事务提交之前它读到的数据不会发生变化，那么另一个事务如果将结果 a 改为 b，接着又改为了 a，对于当前事务来说直到另一个事务提交之后它再读才会获取到最新结果，但是它并不知道这期间别的事务对数据做了更新，**这就是幻读的问题**。

首先设置事务隔离级别：

```sql
Copyset global transaction isolation level REPEATABLE READ;
```

现在数据库数据如下：

现在数据库数据如下：

```sql
Copymysql> select * from test_db;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming3 |
|  2 | xiaohong  |
|  3 | xiaowei   |
|  4 | xiaowei1  |
|  5 | xiaoli    |
|  6 | xiaoche   |
|  8 | xiaoche   |
| 10 | xiaoche   |
| 12 | xiaocee   |
+----+-----------+
9 rows in set (0.00 sec)
```

开启事务 A 将 `id=1` 的数据改为 “xiaoming4”：

```sql
Copymysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> update test_db set name = 'xiaoming4' where id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

这里事务 A 未提交，接着开启事务B 做第一次查询：

```sql
Copymysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from test_db where id = 1;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming3 |
+----+-----------+
9 rows in set (0.00 sec)
```

事务B查询还是原始值。

下面提交事务 A：

```sql
Copymysql> commit;
Query OK, 0 rows affected (0.00 sec)
```

接着在事务 B 中再查询一次：

```sql
Copymysql> select * from test_db where id = 1;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming3 |
+----+-----------+
1 row in set (0.00 sec)
```

查询到还是一样的结果，下面提交事务B ，然后再查询：

```sql
Copymysql> commit;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from test_db where id = 1;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming4 |
+----+-----------+
1 row in set (0.00 sec)
```

提交完之后再查就是 “xiaoming4”。

这也意味着在事务B未提交期间，事务A做任何操作对B来说都是盲视的。

##### 串行化读

串行化读意味着将所有事务变为顺序执行，所以就不存在上述的四种问题，当然这也意味着效率是最低的。

有了隔离级别的概念，那隔离级别又是怎么实现的呢？我们接下来要讲的锁机制就是实现隔离级别的重要手段。

##### 锁的类型

从锁定资源的角度看， MySQL 中的锁分类：

- 表级锁
- 行级锁
- 页面锁

**表级锁** 的特点是每次都整张表加锁，加锁速度快，但是锁的粒度太大，并发性就低，发生锁冲突的概率大。

表锁的种类主要包含两种：

- 读锁 （共享锁）：同一份数据多个读操作同时进行不会互相影响，但是读操作会阻塞写操作。
- 写锁（排他锁）：当前写操作没有完成之前会阻塞其他读和写操作。

**行级锁** 的特点是对一行数据加锁，加锁的开销会大但是锁粒度小发生锁冲突的概率就低并发度提高了。

行锁的种类包含：

- 读锁（S 共享锁）：允许一个事务读取某一行，其他事务在读取期间无法修改该行数据但可以读。
- 写锁（X 排他锁）：允许当前获得排它锁的事务操作数据，其他事务在操作期间无法更改或者读取。
- 意向排它锁（IX）：一个事务给该数据行加排它锁之前，必须先获得 IX 锁。
- 意向共享锁（IS）：一个事务给该数据行加共享锁之前必须先获得 IS 锁。

**页面锁** 因为MySQL 数据文件存储是按照页去划分的，所以这个锁是 MySQL 特有的。开销和加锁时间界于表锁和行锁之间，锁定粒度界于表锁和行锁之间，并发度一般。

在 InnoDB 引擎中默认使用行级锁，我们重点就行级锁的加锁、解锁来做一些说明。

行级锁上锁分为 隐式上锁 和 显式上锁。

隐式上锁是默认的上锁方式，`select`不会自动上锁，`insert`、`update`、`delete` 都会自动加排它锁。在语句执行完毕会释放。

显式上锁即通过手动的方式给 sql 语句加锁，比如：

共享锁：

```sql
Copyselect * from tableName lock in share mode;
```

排他锁：

```sql
Copyselect * from tableName for update;
```

##### 行级锁的实现方式

在 InnoDB 中行级锁的具体实现分为三种类型：

- 锁定单个行记录：Record Lock。
- 锁定一个范围，不包含记录本身：Gap Lock。
- 同时锁住一行数据 + 该数据上下浮动的间隙 ：next-Key Lock。

接下来我们通过一个示例来测试 InnoDB 中这三种锁的实现。

先创建一个测试表：

```sql
CopyCREATE TABLE `test_db` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) NOT NULL DEFAULT '' COMMENT 'name',
  PRIMARY KEY (`id`),
  KEY `name_idx` (`name`(191))
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 ROW_FORMAT=COMPACT COMMENT='测试表';
```

插入两条数据：

![3](https://tva1.sinaimg.cn/large/007S8ZIlgy1gimssvpvj7j30h8072jri.jpg)

还记得我们上面说过 MySQL 是自动提交事务，为了测试锁我们需要关闭自动提交：

```sql
Copyset autocommit = 0;
```

这个设置只在当前连接中生效，记得每开一个连接都要设置一下。

**Record Lock 测试**

开启一个事务：

```sql
Copymysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> update test_db set name = 'xiaoming1' where id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

查看事务状态：

```txt
Copymysql> show engine innodb status;
------------
TRANSACTIONS
------------
Trx id counter 25355
Purge done for trx's n:o < 0 undo n:o < 0 state: running but idle
History list length 0
LIST OF TRANSACTIONS FOR EACH SESSION:
---TRANSACTION 283540073944880, not started
0 lock struct(s), heap size 1136, 0 row lock(s)
---TRANSACTION 25354, ACTIVE 40 sec
2 lock struct(s), heap size 1136, 1 row lock(s)
MySQL thread id 5, OS thread handle 12524, query id 757 localhost ::1 root starting
show engine innodb status
--------
```

事务状态显示有一行在被锁定。

下面我们在当前连接中查询一下现在的数据库：

```sql
Copymysql> select * from test_db;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming1 |
|  2 | xiaohong  |
+----+-----------+
2 rows in set (0.00 sec)
```

发现当前数据库已经被修改了，是事务并没有提交。别急我们继续看看。

下面在一个新的连接开启第二个事务：

```sql
Copymysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> mysql>  update test_db set name = 'xiaoming2' where id = 1;
```

这时候发现这一条语句卡住了无法执行。

查看事务状态：

```txt
Copymysql> show engine innodb status;
......

------- TRX HAS BEEN WAITING 6 SEC FOR THIS LOCK TO BE GRANTED:
RECORD LOCKS space id 2 page no 4 n bits 72 index PRIMARY of table `test_db`.`test_db` trx id 2072 lock_mode X locks rec but not gap waiting
Record lock, heap no 4 PHYSICAL RECORD: n_fields 4; compact format; info bits 0
 0: len 4; hex 80000001; asc     ;;
 1: len 6; hex 000000000817; asc       ;;
 2: len 7; hex 02000001080422; asc       ";;
 3: len 9; hex 7869616f6d696e6732; asc xiaoming2;;

------------------
---TRANSACTION 2071, ACTIVE 50318 sec
2 lock struct(s), heap size 1136, 1 row lock(s), undo log entries 2
MySQL thread id 10, OS thread handle 123145423929344, query id 96 localhost 127.0.0.1 root starting
show engine innodb status
Trx read view will not see trx with id >= 2073, sees < 2072
```

从事务状态上可以看到对 id = 1 的这一行加了 record lock。

再看这一句：

> trx id 2072 lock_mode X locks rec but not gap waiting

X 锁就是我们上面说的排它锁，只对当前记录加锁，并不对间隙加锁。

**Gap Lock 测试**

测试 Gap Lock 我发现如果 where 条件是主键的时候，只会有 record lock 不会有gap lock。

所以 gap lock 的条件是 where 条件必须是非唯一键。

首先查询一下当前的数据:

```sql
Copymysql> set autocommit = 0;
Query OK, 0 rows affected (0.00 sec)

mysql>
mysql> select * from test_db;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | xiaoming4 |
|  2 | xiaohong  |
|  3 | xiaowei   |
|  4 | xiaowei1  |
|  5 | xiaoli    |
|  6 | xiaoche   |
| 10 | xiaohai   |
| 12 | xiaocee   |
+----+-----------+
8 rows in set (0.00 sec)
```

开启事务A：

```sql
Copymysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from test_db where name ='xiaohai' for update;
+----+---------+
| id | name    |
+----+---------+
| 10 | xiaohai |
+----+---------+
1 row in set (0.00 sec)
```

这里我们做的事情是对 name 列做查询条件，它是非唯一索引可以被间隙锁命中。现在的 `id=10` 列 `name=xiaohai`，如果被间隙锁命中的话，`xiaoc*` -- `xiaoh*`中间的字符应该都是不能插入的。所以我们就用这种方式来试试。

开启事务B：

```sql
Copymysql> set autocommit = 0;
Query OK, 0 rows affected (0.00 sec)

mysql> insert test_db (id, name) values (8, 'xiaodai');
```

插入“xiaodai”，可以发现“卡住了”，查询一下事务状态：

```sql
Copymysql> show engine innodb status;
------------
TRANSACTIONS
------------
......
mysql tables in use 1, locked 1
LOCK WAIT 2 lock struct(s), heap size 1136, 1 row lock(s), undo log entries 1
MySQL thread id 32, OS thread handle 123145425444864, query id 385 localhost 127.0.0.1 root update
insert test_db (id, name) values (8, 'xiaodai')
------- TRX HAS BEEN WAITING 24 SEC FOR THIS LOCK TO BE GRANTED:
RECORD LOCKS space id 2 page no 5 n bits 80 index name_idx of table `test_db`.`test_db` trx id 2133 lock_mode X locks gap before rec insert intention waiting
Record lock, heap no 2 PHYSICAL RECORD: n_fields 2; compact format; info bits 0
 0: len 7; hex 7869616f686169; asc xiaohai;;
 1: len 4; hex 8000000a; asc     ;;
......
------------------
```

这里的事务日志说了在插入之前这个索引已经被gap lock 锁住了，所以我们的测试是有效的。

那么 gap lock 的边界是多少呢？这里我实测是当前记录往前找到一个边界和往后找到一个边界，对于上面的测试数据来说就是：往前到 "xiaoche" ，往后到 “xiaohong”， 且你再插入一个等于当前锁定记录 “xiaohai” 的值也是可以的，这个就留给大家动手试试。

Gap Lock 解决了什么问题呢？上面我们说到 读已提交级别有不可重复读的问题。Gap Lock 就是为了防止在本事务还未提交之前，别的事务在当前事务周边插入或修改了数据造成读不一致。

**Next-key Lock 测试**

Next-key Lock 实际上是 Record Lock 和 gap Lock 的组合。

Next-key Lock 是在下一个索引记录本身和索引之前的 gap Lock 加上 S 锁或是 X 锁 ( 如果是读就加上 S 锁，如果是写就加 X 锁)。

**默认情况下，InnoDB 的事务隔离级别为 RR，系统参数 `innodb_locks_unsafe_for_binlog=false`。InnoDB 使用 next-key Lock 对索引进行扫描和搜索，这样就读取不到幻象行，避免了幻读的发生。**

这就相当于对当前数据和当前数据周围的数据都做了保护，当前数据不会发生幻读，当前数据周围的数据不会出现修改或新增从而导致读不一致。

但是需要注意的是，上面测试 Gap Lock 也说过，Gap Lock 只对非唯一索引列生效，同样 Next-key Lock如果也是作用于非唯一索引那么会自动降级为 Record Lock。

##### MVCC机制

什么是 MVCC?

MVCC，`Multi-Version Concurrency Control`，多版本并发控制。同一份数据临时保留多版本的一种方式，进而实现并发控制，简称一致性非锁定读。

上面我们讨论过在多个事务的场景下，通过锁机制可以保证当前事务读不到未提交的事务。但是加锁也会带来坏处，那就是阻塞，只有读读之间可以并发，读写，写读，写写都不能并发操作。引入多版本机制就是为了解决这个问题，减少阻塞时间，通过这个机制，只有写写是会阻塞，其余情况都不会阻塞操作。

比如我们还用 RR 隔离级别下的例子来说，事务A写了一个数据未提交，事务B读取数据，这时候是读不到A事务未提交的记录。B事务只能读到A事务未提交之前的版本。这里就使用了版本管理机制，每个连接在某个瞬间看到的是是数据库在当前的一个快照，每个事务在提交之前对其他的读者来说是不可见的。

一般来说 MVCC 只在 Read Committed 和 Repeatable Read 两个隔离级别下工作。Read Uncommitted 总是能读取到未提交的记录，不需要版本控制；Serializable 对所有的读取都对加锁，单独靠 MVCC 无法完成。

MVCC 的实现，是通过保存数据在某一个时间点的快照来实现的。因此每一个事务无论执行多长时间看到的数据，都是一样的。所以 MVCC 实现可重复读。

**MVCC 的实现**

**隐藏字段**

为了实现多版本控制，InnoDB 引擎在每一行数据中都添加了几个隐藏字段：

- `DB_TRX_ID`：记录最近一次对本记录做（insert/upadte）的事务 ID，大小为 6 字节；
- `DB_ROLL_PTR`：回滚指针，指向回滚段的 undo log，大小为 7 字节；
- `DB_ROW_ID`：单调递增的行 ID，大小为 6 字节，当表没有主键索引或者非空唯一索引的时候 InnoDB 就用这个字段创聚簇索引，这个字段跟MVCC的实现没有关系。

MVCC 在 InnoDB 的实现依赖 undo log 和 read view。undo log 中记录的是数据表记录行的多个版本，也就是事务执行过程中的回滚段,其实就是MVCC 中的一行原始数据的多个版本镜像数据。read view 主要用来判断当前版本数据的可见性。

**undo log**

undo log 上面讲解的时候说go会用于 MVCC 机制。因为 undo log 中存储的是老版本的数据，如果一个事务读取当前行，但是当前行记录不可见，那么可以顺着 undo log 链表找到满足其可见性的版本。

版本链

每条 undo log 也都有一个 old_trx_id 属性和一个 old_roll_pointer 属性（INSERT 操作对应的 undo log 没有这些属性，因为该记录没有更早的版本）用于记录上一个 undo log。最终这些 undo log 就连接起来形成了一个链表，这个链表称之为版本链，版本链的头节点就是当前记录的最新值。

**Read View（读视图）**

如果一个事务修改了记录但尚未提交，其他事务是不能读取记录的最新版本的。此时就需要判断版本链中的哪个版本是可以被当前事务访问的，为此 InnoDB 提出了 ReadView 的概念。 Read View 里面保存了“**对本事务不可见的其他活跃事务**”，主要是用来做可见性判断。

Read View 底层定义了一些关键字段：

| ReadView 字段  | 描述                                                         |
| :------------- | :----------------------------------------------------------- |
| trx_ids        | 在生成 ReadView 时当前系统中活跃的读写事务，即Read View初始化时当前未提交的事务列表。所以当进行RR读的时候，trx_ids中的事务对于本事务是不可见的（除了自身事务，自身事务对于表的修改对于自己当然是可见的）。理解起来就是创建RV时，将当前活跃事务ID记录下来，后续即使他们提交对于本事务也是不可见的。 |
| low_limit_id   | 在生成 ReadView 时当前系统中活跃的读写事务中最小的事务 ID，事务号 >= low_limit_id 的记录，对于当前 Read View 都是不可见的 |
| up_limit_id    | 系统应该给下一个事务分配的 ID 值，事务号 < up_limit_id ，对于当前Read View都是可见的 |
| creator_trx_id | 生成该 ReadView 的事务 ID                                    |

**一旦一个 Read View 被创建，这三个参数将不再发生变化，**理解这点很重要，其中 low_limit_id 和 up_limit_id 分别是 trx_Ids 数组的上下界。

**记录行修改的具体流程**

1. 首先当前事务对记录行加排他锁；
2. 然后把该行数据拷贝到 undo log 中，作为旧版本；
3. 拷贝完毕后，修改该行的数据，并且修改记录行最新的修改事务 id ，也就是 DB_TRX_ID 为当前事务 id；
4. 事务提交，提交前用 CAS 机制判断记录行当前最新修改的事务 id 是否发生了变化，如果没变，则提交成功；如果变了，说明存在其他事务修改了这个记录行，那么就应该回滚这个事务。也就是当前事务没有生效。

**记录行查询时的可见性判断算法**

在 InnoDB 中创建一个新事务后，执行第一个 select 语句的时候，InnoDB 会创建一个快照(ReadView)，快照中会保存系统当前不应该被本事务看到的其他活跃事务 id 列表（即trx_ids）。当用户在这个事务中要读取某个记录行的时候，InnoDB 会将该记录行的 DB_TRX_ID 与该 ReadView 中的一些变量进行比较，判断是否满足可见性条件。

具体的比较算法如下:

1. 如果 trx_id < up_limit_id, 那么表明 “最新修改该行的事务” 在 “当前事务” 创建快照之前就提交了，所以该记录行的值对当前事务是可见的。直接标识为可见，返回 true；
2. 如果 trx_id >= low_limit_id, 那么表明 “最新修改该行的事务” 在 “当前事务” 创建快照之后才被创建且修改该行的，所以该记录行的值对当前事务不可见。应该通过回滚指针找到上个记录行版本，判断是否可见。循环往复，直到可见；
3. 如果 up_limit_id <= trx_id < low_limit_id, 那就得通过二分查找判断 trx_id 是否在 trx_ids 列表出现过。
   1. 如果出现过，说明是当前 read view 中某个活跃的事务提交了，那当然是不可见的，应该通过回滚指针找到上个记录行版本，判断是否可见，循环往复，直到可见；
   2. 如果没有出现过，说明这个事务是已经提交了的，表示为可见，返回 true。

**需要注意的是，新建事务(当前事务)与正在内存中 commit 的事务不在活跃事务链表中。**

**不同隔离级别下 read view 生成原则**：

RC 级别

每个快照读操作都会生成最新的 read view，所以在 RC 级别中能看到别的事务提交的记录。

RR 级别

同一个事务中的第一个快照读才会创建 Read View, 之后的快照读获取的都是同一个Read View。

**关于MVCC 的总结**

上面介绍了 MVCC 在 innoDB 中的实现，我们回顾一下理想中的 MVCC 应该是什么样的：

- 每行数据都有一个版本，每次更新都更新该版本
- 每个事务只在当前版本上更新，各个事务无干扰
- 多个事务提交时比较版本号，如果成功则覆盖原纪录，否则放弃

MVCC 的理论听起来和 乐观锁一致。但是反观 InnoDB 中的实现，事务修改数据首先借助排它锁，事务失败还借助到 undo log 来实现回滚。理论上如果一个完整的 MVCC 实现应该借助版本号就可以，如果使用上了 X 锁那何必还浪费时间再使用 乐观锁呢？

事实上理想的 MVCC 可能会引发bug，单纯依靠版本控制无法完成一致性非锁定读。任何一个复杂的系统在掺杂各种变量的情况总会引发一些旁支问题。

比如，在理想的MVCC 模式下，TX1执行修改 Row1成功，修改Row2失败，此时需要回滚Row1；

但因为Row1没有被锁定，其数据可能又被 TX2 修改，如果此时回滚 Row1的内容，则会破坏 TX2 的修改结果。

MVCC 机制提供了读的非阻塞能力，对于写来说如果不用锁，肯定会出错。但是对于数据库系统来说，读才是大头，这已经解决了生产力的要求。

#### 总结[#](https://www.cnblogs.com/rickiyang/p/13652664.html#196552436)

以上从数据库多事务并发可能会产生什么问题分析，数据库奠基者总结出事务的四大特性，为了性能和数据准确性的协调总结出不同的隔离级别，为了实现不同的隔离级别分别使用了什么技术。这些问题环环相扣，从问题出发寻找解决思路，锁机制，MVCC机制，都是为了解决数据一致性问题同时兼顾读效率而存在。为了持久性提出了两阶段提交弄出了 redo log，为了实现 原子性 和 MVCC 又多出了 undo log。所有的实现都是基于特定的场景和需求，站在需求场景下去理解这些概念就会更容易感受到设计者的初衷。