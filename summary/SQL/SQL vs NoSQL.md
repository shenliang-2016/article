# [阿里P8架构师谈（数据库系列）：NoSQL使用场景和选型比较，以及与SQL的区别](https://zhuanlan.zhihu.com/p/49972313)

[![优知学院](https://pic4.zhimg.com/v2-bcef53dc146ec2627170aca723e51ef8_xs.jpg)](https://www.zhihu.com/org/you-zhi-xue-yuan)

[优知学院](https://www.zhihu.com/org/you-zhi-xue-yuan)

已认证的官方帐号

9 人赞同了该文章

## **一、什么是NoSQL**

NoSQL，指的是非关系型的数据库。NoSQL有时也称作Not Only SQL的缩写，是对不同于传统的关系型数据库的数据库管理系统的统称,它具有非关系型、分布式、不提供ACID的数据库设计模式等特征。

NoSQL用于超大规模数据的存储。（例如谷歌或Facebook每天为他们的用户收集万亿比特的数据）。这些类型的数据存储不需要固定的模式，无需多余操作就可以横向扩展。

## **二、SQL 和 NoSQL 的区别**

![img](https://pic1.zhimg.com/80/v2-37a08f96c102ca39b99b5f746d33b914_hd.jpg)

SQL数据库适合那些需求确定和对数据完整性要去严格的项目。NoSQL数据库适用于那些对速度和可扩展性比较看重的那些不相关的，不确定和不断发展的需求。简单来说就是：

- **SQL是精确的**。它最适合于具有精确标准的定义明确的项目。典型的使用场景是在线商店和银行系统。
- **NoSQL是多变的**。它最适合于具有不确定需求的数据。典型的使用场景是社交网络，客户管理和网络分析系统。

## **三、SQL和Nosql的选型和比较**

**1.关系型数据库和非关系型数据库**

SQL (Structured Query Language) 数据库，指关系型数据库。主要代表：SQL Server，Oracle，MySQL等。

NoSQL（Not Only SQL）泛指非关系型数据库，主要代表：MongoDB，Redis等。

**2.关系型数据库适合存储结构化数据**

如用户的帐号、地址等：

1）这些数据通常需要做结构化查询，比如join，这时候，关系型数据库就要胜出一筹

2）这些数据的规模、增长的速度通常是可以预期的

3）保证数据的事务性、一致性要求。

**3.NoSQL适合存储非结构化数据**

如发微博、文章、评论：

1）这些数据通常用于模糊处理，如全文搜索、机器学习

2）这些数据是海量的，而且增长的速度是难以预期的，

3）根据数据的特点，NoSQL数据库通常具有无限（至少接近）伸缩性

4）按key获取数据效率很高，但是对join或其他结构化查询的支持就比较差

目前许多大型互联网项目都会选用MySQL（或任何关系型数据库） + NoSQL的组合方案。

## **四、NoSQL的常见类型和比较**

有四种常见的 NoSQL 数据库类型：列式、文档、图形和内存键值。

![img](https://pic2.zhimg.com/80/v2-751908e0546c036929f45a78f47c3bfd_hd.jpg)

**1.列式数据**

顾名思义，是按列存储数据的。最大的特点是方便存储结构化和半结构化数据，方便做数据压缩，对针对某一列或者某几列的查询有非常大的IO优势。

1）对应的nosql： HBase,BigTable等。

2）典型应用场景：按列存储，针对某一列或者某几列的查询有非常大的IO优势。

3）优点：查找速度快，可扩展性强，更容易进行分布式扩展。

4）缺点：功能相对局限。

**2.文档数据库**

旨在将半结构化数据存储为文档，通常采用 JSON 或 XML 格式。与传统关系数据库不同的是，每个 NoSQL 文档的架构是不同的，可让您更加灵活地整理和存储应用程序数据并减少可选值所需的存储。

1）对应的nosql：CouchDB, MongoDb

2）典型应用场景：存储类似JSON格式的内容，可对某些字段建立索引功能，是最像关系型的数据库。

3）优点：数据结构要求不严格，表结构可变，不需要像关系型数据库一样需要预先定义表结构。

4）缺点：查询性能不高，而且缺乏统一的查询语法。

**3.图形数据库**

可存储顶点以及称为边缘的直接链路。图形数据库可以在 SQL 和 NoSQL 数据库上构建。顶点和边缘可以拥有各自的相关属性。

1）数据模型：图结构

2）典型应用场景：社交网络，推荐系统等。专注于构建关系图谱，善于处理大量复杂、互连接、低结构化的数据，数据往往变化迅速，且查询频繁。

3）优点：利用图结构相关算法。比如最短路径寻址，N度关系查找等。

4）缺点：很多时候需要对整个图做计算才能得出需要的信息，而且这种结构不太好做分布式的集群方案。

**4.内存键值存储**

可以通过key快速查询到其value。一般来说，存储不管value的格式，照单全收，是针对读取密集型应用程序工作负载（例如社交网络、游戏、媒体共享和 Q&A 门户）。内存缓存可将重要数据存储在内存中以实现低延迟访问，从而提高应用程序性能。

1）对应的nosql：Redis,Memcached等

2）典型应用场景：内容缓存，主要用于处理大量数据的高访问负载，也用于一些日志系统等等。

3）优点：查找速度快。

4）缺点：数据无结构化，通常只被当作字符串或者二进制数据。



# [关系型与非关系型数据库对比讲解](https://www.2cto.com/database/201804/735426.html)

2018-04-04 11:12:35          来源：[hhhanpan的博客](https://blog.csdn.net/hhhanpan)  

主要分析了关系型[数据库](https://www.2cto.com/database/)和非关系型数据库进行了比较。

关系型数据库：

书中的解释是：在实体以及实体间的联系用关系来表示，在一个给定的应用领域中，所有关系的集合构成一个关系数据库。关系数据库的值是这些关系模式的某一个时刻对应的关系的集合，通常称为关系数据库。

关系型数据库以行和列的二元形式存储数据。

常见的有MySQL，SQL Server，[Oracle](https://www.2cto.com/database/Oracle/)，还有[DB2](https://www.2cto.com/database/DB2/)，Access(我只了解MySQL，SQL Server，所以很多还在不断地学习中)

关系型数据库通常包含下列[组件](https://www.2cto.com/kf/all/zujian/)：

客户端应用程序(Client)

数据库服务器(Server)

数据库(Database)

特点

基于单一关系模型，结构化存储，有完整性约束 通过二维表建立数据间的联系 采用结构化查询语言进行数据读写 操作保存数据的一致性(事务处理)

优点

保持数据的一致性。由于高并发，数据同步需要采用锁来保证一致性 数据更新的开销很小 可以进行Join等复杂查询 SQL语言使得操作数据库方便 易于维护：丰富的完整性(实体完整性、参照完整性和用户定义的完整性)，减低了数据冗余和数据不一致的概率

缺点

为了维护一致性就会使读写性能变差; 固定的表结构，不适合为有数据更新的表做索引或表结构变更; 不适用高并发读写需求，读写性能不足; 不适用海量数据的写入处理; 为保证数据一致性，需要加锁，影响并发操作，开销大; 涉及联表查询会变得复杂和慢。

非关系型数据库

又称为NoSQL(Not Only SQL,即不仅仅是SQL)。

采用Key-Value的方式存储数据，即无关联(no relational)。

典型的NoSQL数据库有

临时性键值存储(Memcached，Redis) 永久性键值存储(ROMA、Redis) 面向文档的数据库(MongoDB) 面向列的数据库(Cassandra，HBase)

键值存储

数据以键值形式存储的，只能通过键的完全一致查询获取数据，根据数据的保存方式可分为临时性、永久性和两者兼具。

(1)临时性——memcached

数据有可能丢失 在内存中保存数据(memcached把所有数据都保存在内存中) 保存和读取速度非常快

(2)永久性

数据不会丢失 在硬盘上保存数据 保存和读取处理速度较快(但无法与memcached相比)

(3)两者兼备——Redis

同时在内存和硬盘上保存数据 可以进行非常快速的保存和读取处理 保存在硬盘上的数据不会消失(可以恢复) 适合于处理数组类型的数据

面向文档的数据库

MongoDB、Couch DB属于这种类型。

(1)不定义表结构

(2)可以使用复杂的查询条件

面向列的数据库

Cassandra、HBae、HyperTable属于这种类型。

普通的关系型数据库是以行为单位存储数据，以行为单位的读入处理，比如特定条件数据的获取。

因此，关系型数据库也被称为面向行的数据库。相反，面向列的数据库是以列为单位存储数据的，

擅长以列为单位读入数据。

![这里写图片描述](https://www.2cto.com/uploadfile/Collfiles/20180404/20180404092259153.png)

特性

使用键值Key-Value存储数据; 分布式 一般不支持ACID特性 非关系型数据库严格上来说不是一种数据库，是一种数据结构化存储方法的集合，每个数据都可以有不同的结构;

优点

无需经过sql层的解析，读写性能高; 基于键值对，数据没有耦合性，易于扩展和查询; 存储数据的格式：key-val形式、文档形式、图片形式等等，而关系型数据库则支持基础类型; 降低了一致性的要求，查询速度很快 可以处理海量数据，可运行在便宜的PC服务器集群上，而

缺点

不提供sql支持; 无事务处理，附加功能表和报表等。
