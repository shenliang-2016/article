# [MySQL高级知识（八）——ORDER BY优化](https://www.cnblogs.com/developer_chan/p/9225638.html)



前言：在使用order by时，经常出现Using filesort，因此对于此类sql语句需尽力优化，使其尽量使用Using index。

------

### 0.准备

\#1.创建test表。



```
drop table if exists test;
create table test(
id int primary key auto_increment,
c1 varchar(10),
c2 varchar(10),
c3 varchar(10),
c4 varchar(10),
c5 varchar(10)
) ENGINE=INNODB default CHARSET=utf8;

insert into test(c1,c2,c3,c4,c5) values('a1','a2','a3','a4','a5');
insert into test(c1,c2,c3,c4,c5) values('b1','b2','b3','b4','b5');
insert into test(c1,c2,c3,c4,c5) values('c1','c2','c3','c4','c5');
insert into test(c1,c2,c3,c4,c5) values('d1','d2','d3','d4','d5');
insert into test(c1,c2,c3,c4,c5) values('e1','e2','e3','e4','e5');
```



\#2.创建索引。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625223438203-1033999353.png)

### 1.根据Case分析order by的使用情况

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625223944999-13584041.png)

分析：

①在c1,c2,c3,c4上创建了索引，直接在c1上使用范围，导致了索引失效，全表扫描：type=ALL，ref=Null。因为此时c1主要用于排序，并不是查询。

②使用c1进行排序，出现了Using filesort。

③解决方法：使用覆盖索引。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625225150972-757485019.png)

Case 1.1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625225605390-1287916353.png)

分析：

排序时按照索引的顺序，所以不会出现Using filesort。

Case 1.2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625230033609-1505851091.png)

分析：

出现了Using filesort。原因：排序用的c2，与索引的创建顺序不一致，对比Case1.1可知，排序时少了c1（带头大哥），因此出现Using filesort。

Case 1.3：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625230403937-1781972191.png)

分析：

出现了Using filesort。因为排序索引列与索引创建的顺序相反，从而产生了重排，也就出现了Using filesort。

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625231117168-925966033.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625231342815-2077452190.png)

分析：

直接使用c2进行排序，出现Using filesort，因为不是从最左列索引开始排序的（没有带头大哥）。

Case 2.1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625231451690-583449657.png)

分析：

排序使用了索引顺序（带头大哥在），因此不会出现Using filesort。

Case 2.2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625231710896-1971557040.png)

分析：

虽然排序的字段列与索引顺序一样，且order by默认升序，这里c2 desc变成了降序，导致与索引的排序方式不同，从而产生Using filesort。

### 总结：

①MySQL支持两种方式的排序filesort和index，Using index是指MySQL扫描索引本身完成排序。index效率高，filesort效率低。

②order by满足两种情况会使用Using index。

\#1.order by语句使用索引最左前列。

\#2.使用where子句与order by子句条件列组合满足索引最左前列。

③尽量在索引列上完成排序，遵循索引建立（索引创建的顺序）时的最佳左前缀法则。

④如果order by的条件不在索引列上，就会产生Using filesort。

\#1.filesort有两种排序算法：双路排序和单路排序。

双路排序：在MySQL4.1之前使用双路排序，就是两次磁盘扫描，得到最终数据。读取行指针和order by列，对他们进行排序，然后扫描已经排好序的列表，按照列表中的值重新从列表中读取对应的数据输出。即从磁盘读取排序字段，在buffer进行排序，再从磁盘取其他字段。

如果使用双路排序，取一批数据要对磁盘进行两次扫描，众所周知，I/O操作是很耗时的，因此在MySQL4.1以后，出现了改进的算法：单路排序。

单路排序：从磁盘中查询所需的列，按照order by列在buffer中对它们进行排序，然后扫描排序后的列表进行输出。它的效率更高一些，避免了第二次读取数据，并且把随机I/O变成了顺序I/O，但是会使用更多的空间，因为它把每一行都保存在内存中了。

\#2.单路排序出现的问题。

当读取数据超过sort_buffer的容量时，就会导致多次读取数据，并创建临时表，最后多路合并，产生多次I/O，反而增加其I/O运算。

解决方式：

a.增加sort_buffer_size参数的设置。

b.增大max_length_for_sort_data参数的设置。

⑤提升order by速度的方式：

\#1.在使用order by时，不要用select *，只查询所需的字段。

因为当查询字段过多时，会导致sort_buffer不够，从而使用多路排序或进行多次I/O操作。

\#2.尝试提高sort_buffer_size。

\#3.尝试提高max_length_for_sort_data。

⑥附上一张从视频中截取出来的总结图。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180626091734130-496909449.png)

⑦group by与order by很类似，其实质是先排序后分组，遵照索引创建顺序的最佳左前缀法则。当无法使用索引列的时候，也要对sort_buffer_size和max_length_for_sort_data参数进行调整。注意where高于having，能写在where中的限定条件就不要去having限定了。

------

by Shawn Chen，2018.6.26日，上午。