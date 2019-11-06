# [MySQL高级知识（六）——索引优化](https://www.cnblogs.com/developer_chan/p/9219934.html)



前言：索引优化的目的主要是让索引不失效，本篇通过相关案例对索引优化进行讲解。

------

### 0.准备

创建经典的tb_emp表。



```
DROP TABLE IF EXISTS `tb_emp`;
CREATE TABLE `tb_emp` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL,
  `age` int(11) NOT NULL,
  gender varchar(10) NOT NULL,
  email varchar(20),
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
-- ----------------------------
INSERT INTO `tb_emp` (name,age,gender,email) VALUES ('Tom', '22','male','1@qq.com');
INSERT INTO `tb_emp` (name,age,gender,email) VALUES ('Mary', '21','female','2@qq.com');
INSERT INTO `tb_emp` (name,age,gender,email) VALUES ('Jack', '27','male','3@qq.com');
INSERT INTO `tb_emp` (name,age,gender,email) VALUES ('Rose', '23','female','4@qq.com');
```



注：创建了tb_emp表，并插入了4条数据。

### 1.最佳左前缀法则

\#1.定义：在创建了多列索引的情况下，查询从索引的最左前列开始且不能跳过索引中的列。

最佳左前缀法则就是说如果创建了多个索引，在使用索引时要按照创建索引的顺序来使用，不能缺少或跳过，当然如果只使用最左边的索引列，也就是第一个索引是可以的，通俗理解：“带头大哥不能死，中间兄弟不能断”。要点：“头不能掉”。下面将用案例进行说明。

\#2.创建组合索引，并执行explain。

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624190401218-1458339822.png)

分析：

①索引的创建顺序为name，age，gender；

②直接使用name（带头大哥）作为条件，可以看到type=ref，key_len=82，ref=const，效果还不错。

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624185802408-1782895054.png)

分析：

没使用带头大哥（name），直接用兄弟，type=ALL，为全表扫描。

Case 3：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624190657577-1365748955.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624190850424-708535844.png)

分析：

①对比上面两句sql语句可发现：我们使用：火车头（name）和中间车厢（age）、火车头（name）和车尾（gender）。

②虽然type=ref，但是观察key_len和ref两项，并对比Case1中的结果，可得出在使用火车头（name）和车尾（gender）时，只使用了部分索引也就是火车头（name）的索引。

③通俗理解：火车头单独跑没问题，火车头与直接相连的车厢一起跑也没问题，但是火车头与车尾，如果中间没有车厢，只能火车头自己跑。

Case 4：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624191100260-341044144.png)

分析：

火车头加车厢加车尾，三者串联，就变成了奔跑的小火车。type=ref，key_len=128，ref=const，const，const。

最佳左前缀法则总结：**带头大哥不能死，中间兄弟不能断；带头大哥可跑路，老二也可跟着跑，其余兄弟只能死**。

### 2.不要在索引列上做任何操作

在索引列上做任何操作（计算、函数、（自动or手动）类型转换），会导致索引失效从而转向全表扫描。

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624191237299-1410230014.png)

分析：

这里使用了函数计算，type=ALL，导致索引失效。

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624191458173-125228980.png)

分析：

将name=‘Tom’的值修改为‘123’，使用sql后，发生了类型转换，type=ALL，导致全表扫描。

结论：在索引列上做任何操作，都会导致索引失效转向全表扫描。

### 3.范围右边全失效

存储引擎不能使用索引中范围右边的列，也就是说范围右边的索引列会失效。

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624191712959-1140058576.png)

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624191815745-1537412474.png)

Case 3：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624191925423-1749109401.png)

Case 4：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624192605853-282101338.png)

对以上4个case进行分析：

①条件单独使用name时，type=ref，key_len=82，ref=const。

②条件加上age时（使用常量等值），type=ref，key_len=86，ref=const，const。

③当全值匹配时，type=ref，key_len=128，ref=const，const，const。说明索引全部用上，从key_len与ref可以看出。

④当使用范围时（age>27），type=range，key_len=86，ref=Null，与Case 1、Case2和Case3可知，使用了部分索引，但gender索引没用上（与Case 3对比）。

结论：范围右边的索引列失效。

### 4.尽量使用覆盖索引

尽量使用覆盖索引（查询列和索引列尽量一致，通俗说就是对A、B列创建了索引，然后查询中也使用A、B列），减少select *的使用。

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624192929239-899471122.png)

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624193029492-1650110216.png)

分析：

对比Case1和Case2，Case1使用select *，Case2使用覆盖索引（查询列与条件列对应），可看到Extra从Null变成了Using index，提高检索效率。

### 5.使用不等于（！=或<>）会使索引失效

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624194116625-767179219.png)

结论：使用！=会使type=ALL，key=Null，导致全表扫描，并且索引失效。

### 6.is null 或 is not null也无法使用索引

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624130623677-583786719.png)

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624194257642-1518030986.png)

分析：

在使用is null的时候，索引完全失效，使用is not null的时候，type=ALL全表扫描，key=Null索引失效。

这里的例子可能有点特殊，具体情况肯能和case上的有所不同，但是还是要注意is null和is not null的使用。

### 7.like通配符以%开头会使索引失效

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624194447502-761307758.png)

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624194526161-160167315.png)

Case 3：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624194639651-1224411136.png)

分析：

①like的%位置不同，所产生的效果不一样，当%出现在左边的时候，type=ALL，key=Null（全表扫描，索引失效），当%出现在右边的时候，type=range，索引未失效。

②like查询为范围查询，%出现在左边，则索引失效。%出现在右边索引未失效。口诀：like百分加右边。

但是在实际生产环境中，%仅出现在右边可能不能够解决我们的问题，所以解决%出现在左边索引失效的方法：使用覆盖索引。

Case 4：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624213722548-723610021.png)

分析：对比Case1可知，通过覆盖索引type=index，并且使用了Using index，从全表扫描变成了全索引扫描，还是不错的。

Case 5：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624213945856-1428453394.png)

分析：这里出现type=index，因为主键自动创建唯一索引。

Case 6：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624214457372-1223558264.png)

分析：上面四组explain执行的结果都相同，表明都使用了索引，从这里可以深刻的体会到覆盖索引：完全吻合或者沾边（age），都可以使type=index。

Case 7：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180624214834571-217778598.png)

分析：由于只在（name，age，gender）上创建索引，当包含email时，导致结果集偏大（email未建索引）【锅大，锅盖小，不能匹配】，所以type=ALL。

### 8.字符串不加单引号导致索引失效

Case 1：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625094310677-222554677.png)

分析：上述两条sql语句都能查询出相同的数据。

Case 2：

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625094533249-1839887486.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625094658710-214376473.png)

分析：

通过explain执行结果可以看出，字符串（name）不加单引号在查询的时候，导致索引失效（type=ref变成了type=ALL，并且key=Null），并全表扫描。

结论：varchar类型的字段，在查询的时候不加单引号导致索引失效，转向全表扫描。

### 9.少用or，用or连接会使索引失效

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180625095249155-591889103.png)

结论：通过上述explain的执行结果可看出，在使用or连接的时候type=ALL，key=Null，索引失效，并全表扫描。

### 总结

①全值匹配。

②最佳左前缀法则：**带头大哥不能死，中间兄弟不能断；带头大哥可跑路，老二也可跟着跑，其余兄弟只能死**。

③索引列上不计算。

④覆盖索引记住用。

⑤不等于、is null、is not null导致索引失效。

⑥like百分加右边，加左边导致索引失效，解决方法：使用覆盖索引。

⑦字符串不加单引号导致索引失效。

⑧少用or，用or导致索引失效。

------

by Shawn Chen，2018.6.25日，上午。