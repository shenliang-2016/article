# [MySQL高级知识（一）——基础](https://www.cnblogs.com/developer_chan/p/9205401.html)



前言：MySQL高级知识主要来自[尚硅谷](http://www.atguigu.com/download.shtml)中MySQL的视频资源。对于网上视频资源来说，尚硅谷是一个非常好的选择。通过对相应部分的学习，笔者可以说收益颇丰，非常感谢尚硅谷。

------

### 1.关于MySQL的一些文件

MySQL如何安装、如何配置自启动，这里不进行讲述，可自行搜索相关安装教程进行处理。这里主要介绍MySQL的主要配置文件。

①二进制日志log-bin：用于主从复制。

②错误日志log-error：默认关闭，记录严重的警告和错误信息，每次启动和关闭的详细信息等。

③查询日志show-log：默认关闭，记录查询的sql语句，如果开启会降低mysql的整体性能，因为记录日志也是需要消耗系统资源的。

④frm文件：存放表结构。

⑤myd文件：存放表数据。

⑥myi文件：存放表索引。

特别提出MySQL中的重要配置文件：Windows下名为my.ini，Linux下为/etc/my.cnf。对于服务器的调优相关过程都在改配置文件中，需要特别掌握。

### 2.MySQL的逻辑架构

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621091238334-962479342.png)

MySQL是架构非常优良，主要体现在存储引擎上。MySQL是插件式的存储引擎，它可以将查询处理和其他的系统任务以及数据的存储提取相分离。

从上图可知，MySQL的逻辑框架主要分为四层：

①连接层；②服务层（主要进行sql语句相关的操作）；③引擎层（注意引擎层是可拔插的）；④存储层。

通过分层和可插拔式的架构，可以根据不同的生产环境构建最优的系统。

### 3.MyISAM和InnoDB之间的区别

直接通过show engines命令可以查看MySQL支持的存储引擎。也可通过show variables like '%storage_engine%'查看MySQL的当前默认存储引擎。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621092611759-1069250967.png)

这里主要对MyISAM和InnoDB进行比较，主要区别如下表：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621092957719-1735602443.png)

注：MyISAM主要关注性能，因为其查询速度快。

### 4.SQL语句的执行顺序

sql语句的执行顺序可通过下图了解，注意sql是从from开始执行的。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621095336251-966027615.png)

### 5.总结

这里主要对MySQL的基础信息，做一个粗略的介绍，以便为后续的学习打下基础，主要关注点：

①mysql的配置相关文件。

②mysql逻辑架构。

③mysql存储引擎。

④mysql中sql语句的执行顺序。

------

by Shawn Chen，2018.6.21日，上午。