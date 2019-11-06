# [MySQL高级知识（十三）——表锁](https://www.cnblogs.com/developer_chan/p/9234925.html)



前言：锁是计算机协调多个进程或线程并发访问某一资源的机制。在数据库中，除传统的计算机资源（如CPU、RAM、I/O等）的争用外，数据也是一种供许多用户共享的资源。如何保证数据并发访问的一致性、有效性是所有数据库必须解决的一个问题，锁冲突也是影响数据并发访问性能的一个重要因素。从这个角度来说，锁对数据库而言显得尤其重要，也更加复杂。

------

### 1.锁的分类

\#1.从对数据操作的类型来分

读锁（共享锁）和写锁（排它锁）

\#2.从对数据操作的粒度来分

表锁和行锁

### 2.表锁（偏读）

特点：偏向MyISAM存储引擎，开销小，加锁快，无死锁，锁定粒度大，发生锁冲突的概率最高，并发度低。下面通过案例来说明表锁的一些情况。

\#1.创建mylock表，并插入5条数据。注意数据引擎使用的是MyISAM。

```
drop table if exists mylock;
CREATE TABLE mylock (
    id INT PRIMARY KEY auto_increment,
    name VARCHAR (20) NOT NULL
) ENGINE MyISAM DEFAULT charset = utf8;
insert into mylock (name) values ('a');
insert into mylock (name) values ('b');
insert into mylock (name) values ('c');
insert into mylock (name) values ('d');
insert into mylock (name) values ('e');
```

\#2.手动增加表锁命令。

```
lock table tablename1 read(write),tablename2 read(write);
```

\#3.查看表是否被加锁。![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627175021771-1214290081.png)

如果In_use显示不为0，则表示表被加锁。

\#4.释放表锁命令

```
unlock tables；
```

### 3.表锁（read）案例

\#1.在mylock表上加读锁。将当前会话命名为A。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627232558014-1171590446.png)

在A会话中查询mylock中的数据。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627233047753-1095579074.png)

数据查询正常，没有任何问题。

\#2.再开一个会话，命名为B，查询mylock中的数据。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627233405663-1301042942.png)

数据查询正常，没有任何问题。

\#3.进行其他操作。

①在A会话中进行更新操作。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628091204955-443054808.png)

分析：

提示mylock表被加锁，不能进行更新操作。原因：mylock正被读锁锁住，未解锁不能进行更新操作。

②在B会话中读其他表。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628091906104-1228916951.png)

分析：

A会话mylock表的读锁，并不影响B会话对mylock表和其他表的读操作。

③在A会话中读其他表。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628092239466-888735883.png)

分析：

由于A会话对mylock表加了读锁，在未解锁前，不能操作其他表。

④在B会话中修改mylock表中的内容。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628092853706-2051478985.png)

分析：

出现了阻塞情况，原因：由于A会话对mylock表加锁，在锁未释放时，其他会话是不能对mylock表进行更新操作的。

⑤在A会话中对mylock表进行解锁操作，注意观察B会话中的变化。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628095129283-16074511.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628095207068-851762906.png)

分析：

在A会话中对mylock表解锁后，B会话更新操作成功，可看到B会话中的更新操作等待了22分钟。

### 4.表锁（write）案例

\#1.在A会话中对mylock表加写锁。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628101246648-852848773.png)

\#2.在A会话中对mylock表进行读写操作。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628101512558-1292513400.png)

分析：

由于A会话对mylock表加的写锁，所以读写操作都执行正常。

\#3.在A会话中对其他表进行操作。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628101744642-19489631.png)

分析：

在A会话中对其他表进行读写操作都失败，因为A会话中mylock表的写锁并未被释放。

\#4.在B会话中对mylock表进行读操作。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628102119942-1125486321.png)

分析：

由于mylock表已经加写锁，而写锁为排它锁，因此在B会话中对mylock表进行读操作阻塞。

由于B会话中对mylock的读操作都阻塞，所以其他操作也是阻塞的。

### 5.表锁定分析

\#1.使用如下命令查看是否有表被锁定。

```
show open tables where In_use>0;
```

\#2.使用如下命令分析表锁。

```
show status like 'table%';
```

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180628113227049-295467643.png)

主要注意两个变量的值：

①Table_locks_immediate：产生表级锁定的次数，表示可立即获取锁的查询次数，每立即获取锁一次该值加1。

②Table_locks_waited：出现表级锁定争用而发生等待的次数（不能立即获取锁的次数，每等待一次锁该值加1），此值高则说明存在较严重的表级锁争用情况。

### 总结

注意数据库引擎为MyISAM。

①对MyISAM表加读锁，不会阻塞其他进程对同一表（mylock）的读操作，但是会阻塞对同一表的写请求，只有当读锁释放后，才会执行其他进程的写操作。

②在加读锁并未释放锁时，该进程不能对同一表（mylock）进行写操作，并且也不能对其他表进行操作。

③对MyISAM表加写锁，会阻塞其他进程对同一表（mylock）的读和写操作，只有当读锁释放后，才会执行其他进程的写操作。

④在加写锁并未释放锁时，该进程不能对其他表进行操作。

简而言之：读锁会阻塞写，但是不会阻塞读，而写锁会把读和写都阻塞。

此外，MyISAM的读写锁调度是写优先，这也是MyISAM不适合做写为主的表的引擎，因为写锁后，其他线程不能做任何操作，大量的更新会使查询很难得到锁，从而造成长时间阻塞。

------

by Shawn Chen，2018.6.28日，上午。