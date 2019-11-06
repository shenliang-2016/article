# [MySQL高级知识（五）——索引分析](https://www.cnblogs.com/developer_chan/p/9219239.html)



前言：前面已经学习了explain(执行计划)的相关知识，这里利用explain对索引进行优化分析。

------

### 0.准备

首先创建三张表：tb_emp(职工表)、tb_dept(部门表)和tb_desc(描述表)

1）tb_emp表。



```
DROP TABLE IF EXISTS `tb_emp`;
CREATE TABLE `tb_emp` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(20) NOT NULL,
   `deptid` int(11) NOT NULL,
   PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
-- ----------------------------
INSERT INTO `tb_emp`(username,deptid) VALUES ('Tom', '1');
INSERT INTO `tb_emp`(username,deptid) VALUES ('Jack', '1');
INSERT INTO `tb_emp`(username,deptid) VALUES ('Mary', '2');
INSERT INTO `tb_emp`(username,deptid) VALUES ('Rose', '3');
```



2）tb_dept表。



```
DROP TABLE IF EXISTS `tb_dept`;
CREATE TABLE `tb_dept` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
-- ----------------------------
INSERT INTO `tb_dept`(name) VALUES ('综合部');
INSERT INTO `tb_dept`(name) VALUES ('研发');
INSERT INTO `tb_dept`(name) VALUES ('测试');
INSERT INTO `tb_dept`(name) VALUES ('总裁');
```



3）tb_desc表。



```
DROP TABLE IF EXISTS `tb_desc`;
CREATE TABLE `tb_desc` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `empid` int(11) DEFAULT NULL,
  `deptid` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
-- ----------------------------
INSERT INTO `tb_desc`(empid,deptid) VALUES (1, 1);
INSERT INTO `tb_desc`(empid,deptid) VALUES (2, 1);
INSERT INTO `tb_desc`(empid,deptid) VALUES (3, 2);
INSERT INTO `tb_desc`(empid,deptid) VALUES (4, 3);
```



注：这里强行将员工表与部门表不直接关联，通过第三张表（描述表）进行关联，主要为了进行join的分析。

### 1.left join

\#1.首先执行查询。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180623224006263-1736705921.png)

\#2.通过explain进行分析。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180623224241091-315300339.png)

分析：从explain执行结果可以看出对两表都是用了全表扫描（ALL），并且在tb_desc表中还使用了join连接缓存，需要进行优化。但是如何优化？是在左表建立索引还是右表建立索引呢？因为左连接左表是全有，所以应该在右表建立索引。

\#3.右表创建索引。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180623225044004-1072568408.png)

通过explain执行可以看到，在创建索引后，获得了比较不错的结果。（type=ref,Extra=Using index）。

结论：left join（左连接）情况下，应该在右表（tb_desc）创建索引。

### 2.right join

通过上面left join的例子，我们直接交换两表位置，并将left join改变成right join。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180623230522781-2103775574.png)

分析：

与left join进行对比，可以得到如下结论：

\#1.在left join下，首先执行tb_emp（左表），type=ALL，因为左连接情况下左表全有，因此我们在tb_desc（右表）创建索引，得到比较理想的效果。

\#2.在right join下（我们交换了tb_emp和tb_desc的位置），执行顺序：tb_emp（右表）→ tb_desc（左表）。右表type=ALL，因为右连接情况下右表全有，因此在左表（tb_desc，我们交换了位置）创建索引，效果肯定和left join一样。

### 总结

**left join（左连接）：右表创建索引。**

**right join（右连接）：左表创建索引。**

**简记：左右外连接，索引相反建（left：右表建，right：左表建）。**

------

by Shawn Chen，2018.6.23日，晚。