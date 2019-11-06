# [MySQL高级知识（二）——Join查询](https://www.cnblogs.com/developer_chan/p/9207687.html)



前言：该篇主要对MySQL中join语句的七种情况进行总结。

------

### 0.准备

join主要根据两表或多表之间列的关系，从这些表中进行数据的查询。

首先创建两张表：tb_emp(员工表)和tb_dept(部门表)，并插入相关测试数据。

1.tb_emp表。

```
DROP TABLE IF EXISTS `tb_emp`;
CREATE TABLE `tb_emp` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL,
  `deptid` int(11) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `idx_tb_emp_name` (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO `tb_emp`(name,deptid) VALUES ('jack', '1');
INSERT INTO `tb_emp`(name,deptid) VALUES ('tom', '1');
INSERT INTO `tb_emp`(name,deptid) VALUES ('tonny', '1');
INSERT INTO `tb_emp`(name,deptid) VALUES ('mary', '2');
INSERT INTO `tb_emp`(name,deptid) VALUES ('rose', '2');
INSERT INTO `tb_emp`(name,deptid) VALUES ('luffy', '3');
INSERT INTO `tb_emp`(name,deptid) VALUES ('outman', '14');
```

2.tb_dept表。

```
DROP TABLE IF EXISTS `tb_dept`;
CREATE TABLE `tb_dept` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `deptname` varchar(20) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO `tb_dept`(deptname) VALUES ('研发');
INSERT INTO `tb_dept`(deptname) VALUES ('测试');
INSERT INTO `tb_dept`(deptname) VALUES ('运维');
INSERT INTO `tb_dept`(deptname) VALUES ('经理');
```

从上表插入的数据可知outman是没有对应部门的。

### 1.inner join

注：A表示左表，B表示右表，下同。

inner join：A、B共有，也就是交集。

   ![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621102153321-1096428769.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621102459561-1669926910.png)

### 2.left join

left jion：A独有+AB共有（交集）

   ![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621102924891-768238348.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621103346416-943998578.png)

### 3.right join

right join：B独有+AB共有（交集）

   ![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621103759640-303056357.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621103718653-1396393882.png)

### 4.A独有

   ![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621104329421-109433734.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621104545003-582468281.png)

注：参照left join，A独有只是将AB交集部分去掉。

### 5.B独有

   ![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621104744833-2072459534.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621104921428-1659279197.png)

注：参照right join，B独有只是将AB交集部分去掉。

### 6.AB全有（并集）

   ![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621110144548-704012923.png)

由于mysql中不支持full outer join，所以这里通过union进行转换。AB并集：AB交集+A独有+B独有。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621110545977-2083791147.png)

### 7.A、B独有并集

   ![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621110919839-869053949.png)

A、B独有并集，相当于A、B全有去掉AB的共有（交集）。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180621111429409-1493367532.png)

### 总结

这里主要对MySQL中join语句的7中用法进行了总结，主要注意MySQL不支持full outer join，所以需要对其进行转换变形，最终达到效果。

------

by Shawn Chen，2018.6.21日，上午。 