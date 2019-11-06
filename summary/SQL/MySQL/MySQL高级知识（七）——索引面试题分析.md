# [MySQL高级知识（七）——索引面试题分析](https://www.cnblogs.com/developer_chan/p/9223671.html)



前言：该篇随笔通过一些案例，对索引相关的面试题进行分析。

------

### 0.准备

\#1.创建test表（测试表）。



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

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625114139843-688761483.png)

### 1.根据以下Case分析索引的使用情况

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625140904127-1302395868.png)

分析：

①创建复合索引的顺序为c1,c2,c3,c4。

②上述四组explain执行的结果都一样：type=ref，key_len=132，ref=const,const,const,const。

结论：在执行常量等值查询时，改变索引列的顺序并不会更改explain的执行结果，因为mysql底层优化器会进行优化，但是推荐按照索引顺序列编写sql语句。

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625141728146-1257154425.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625141904917-1270183615.png)

分析：

当出现范围的时候，type=range，key_len=99，比不用范围key_len=66增加了，说明使用上了索引，但对比Case1中执行结果，说明c4上索引失效。

结论：范围右边索引列失效，但是范围当前位置（c3）的索引是有效的，从key_len=99可证明。

Case 2.1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625142519493-1707681115.png)

分析：

与上面explain执行结果对比，key_len=132说明索引用到了4个，因为对此sql语句mysql底层优化器会进行优化：范围右边索引列失效（c4右边已经没有索引列了），注意索引的顺序（c1,c2,c3,c4），所以c4右边不会出现失效的索引列，因此4个索引全部用上。

结论：范围右边索引列失效，是有顺序的：c1,c2,c3,c4，如果c3有范围，则c4失效；如果c4有范围，则没有失效的索引列，从而会使用全部索引。

Case 2.2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625143231208-1151707823.png)

分析：

如果在c1处使用范围，则type=ALL，key=Null，索引失效，全表扫描，这里违背了最佳左前缀法则，带头大哥已死，因为c1主要用于范围，而不是查询。

解决方式使用覆盖索引。

结论：在最佳左前缀法则中，如果最左前列（带头大哥）的索引失效，则后面的索引都失效。

Case 3：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625144706615-1341146854.png)

分析：

利用最佳左前缀法则：中间兄弟不能断，因此用到了c1和c2索引（查找），从key_len=66，ref=const,const，c3索引列用在排序过程中。

Case 3.1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625145159536-1785441356.png)

分析：

从explain的执行结果来看：key_len=66，ref=const,const，从而查找只用到c1和c2索引，c3索引用于排序。

Case 3.2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625145803516-50840484.png)

分析：

从explain的执行结果来看：key_len=66，ref=const,const，查询使用了c1和c2索引，由于用了c4进行排序，跳过了c3，出现了Using filesort。

Case 4：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625150919633-1308783530.png)

分析：

查找只用到索引c1，c2和c3用于排序，无Using filesort。

Case 4.1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625151236317-567907639.png)

分析：

和Case 4中explain的执行结果一样，但是出现了Using filesort，因为索引的创建顺序为c1,c2,c3,c4，但是排序的时候c2和c3颠倒位置了。

Case 4.2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625151917739-1865022943.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625152104703-1743341270.png)

分析：

在查询时增加了c5，但是explain的执行结果一样，因为c5并未创建索引。

Case 4.3：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625152716821-2133479526.png)

分析：

与Case 4.1对比，在Extra中并未出现Using filesort，因为c2为常量，在排序中被优化，所以索引未颠倒，不会出现Using filesort。

Case 5：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625153146225-2012259748.png)

分析：

只用到c1上的索引，因为c4中间间断了，根据最佳左前缀法则，所以key_len=33，ref=const，表示只用到一个索引。

Case 5.1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625153605318-963088595.png)

分析：

对比Case 5，在group by时交换了c2和c3的位置，结果出现Using temporary和Using filesort，极度恶劣。原因：c3和c2与索引创建顺序相反。

### 总结：

通过以上Case的分析，进行如下总结：

①最佳左前缀法则。

\#1.在等值查询时，更改索引列顺序，并不会影响explain的执行结果，因为mysql底层会进行优化。

\#2.在使用order by时，注意索引顺序、常量，以及可能会导致Using filesort的情况。

②group by容易产生Using temporary。

③通俗理解口诀：

   全值匹配我最爱，最左前缀要遵守；

   带头大哥不能死，中间兄弟不能断；

   索引列上少计算，范围之后全失效；

   LIKE百分写最右，覆盖索引不写星；

   不等空值还有or，索引失效要少用。

------

by Shawn Chen，2018.6.25日，下午。