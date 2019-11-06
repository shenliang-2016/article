# [MySQL高级知识（三）——索引](https://www.cnblogs.com/developer_chan/p/9208404.html)



前言：索引在sql调优部分占据着重要的位置，了解并深入索引对我们来说也是非常重要的。本篇主要介绍MySQL中索引的相关知识点。

------

### 1.索引是什么

MySQL官方对索引的定义：索引（Index）是帮助MySQL高效获取数据的数据结构。因此索引的本质就是数据结构。索引的目的在于提高查询效率，可类比字典、书籍的目录等这种形式。

可简单理解为“排好序的快速查找数据结构”。在数据之外，数据库系统还维护着满足特定查找算法的数据结构，这些数据结构以某种方式指向数据，这样就可以在这些数据结构上实现高级查找算法，这种数据结构就是索引。

一般来说，索引本身也很大，不可能全部存储在内存中，因此索引往往以索引文件的形式存储在磁盘上。

平常所说的索引，如果没有特别指明，都是B树索引。其中聚集索引、次要索引、覆盖索引、前缀索引、唯一索引默认都是用B树。

通过show index from tablename可以查看表的索引情况。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621151607219-1437230180.png)

### 2.索引的优缺点

优点

①类似大学图书馆的书目索引，提高数据的检索效率，降低数据库的IO成本。

②通过索引列对数据进行排序，降低数据的排序成本，从而降低CPU的消耗。

缺点

①索引实际上也是一张表，该表保存了主键与索引字段，并指向实体表的记录，所以索引列也要占用空间。

②虽然索引大大提高了查询效率，但是降低了更新表的速度，如insert、update和delete操作。因为更新表时，MySQL不仅要保存数据，还要保存索引文件每次更新的索引列字段，并且在更新操作后，会更新相应字段索引的信息。

③索引只是提高查询效率的一个因素，如果你的MySQL有大量的数据表，就需要花时间研究建立最优秀的索引或优化查询语句。

### 3.索引分类

索引主要分为以下三类：

①单值索引：一个索引只包含单个列，一个表可以有多个单值索引。

②唯一索引：索引列的值必须唯一，但允许有空值，主键就是唯一索引。

③复合索引：一个索引包含多个列

索引的结构：

①BTREE索引；②Hash索引；③Full-Text索引；④R-Tree索引。

### 4.基本语法

①创建索引

```
create [unique] index indexname on tablename(columnname(length));

alter table tablename add index indexname (columnname(length));
```

注：如果是char、varchar类型的字段，length可以小于字段实际长度；如果是blob、text类型，必须指定length。

②删除索引

```
drop index indexname on tablename;
```

③查看索引

```
show index from tablename;
```

④其他创建索引的方式

```
1.添加主键索引 
ALTER TABLE `table_name` ADD PRIMARY KEY (`column`) 

2.添加唯一索引
ALTER TABLE `table_name` ADD UNIQUE (`column`) 

3.添加全文索引
ALTER TABLE `table_name` ADD FULLTEXT (`column`) 

4.添加普通索引
ALTER TABLE `table_name` ADD INDEX index_name (`column` ) 

5.添加组合索引 
ALTER TABLE `table_name` ADD INDEX index_name (`column1`, `column2`, `column3`)
```



### 5.建立索引与否的具体情况

①需建立索引的情况

\#1.主键自动建立唯一索引。

\#2.频繁作为查询条件的字段。

\#3.查询中与其他表关联的字段，外键关系建立索引。

\#4.高并发下趋向创建组合索引。

\#5.查询中排序的字段，排序字段若通过索引去访问将大大提高排序速度。

\#6.查询中统计或分组字段。

②不需要创建索引的情况

\#1.表记录太少。（数据量太少MySQL自己就可以搞定了）

\#2.经常增删改的表。

\#3.数据重复且平均分配的字段，如国籍、性别，不适合创建索引。

\#4.频繁更新的字段不适合建立索引。

\#5.Where条件里用不到的字段不创建索引。

------

by Shawn Chen，2018.6.21日，下午。