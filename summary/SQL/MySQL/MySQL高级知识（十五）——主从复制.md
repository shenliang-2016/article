# [MySQL高级知识（十五）——主从复制](https://www.cnblogs.com/developer_chan/p/9240052.html)



前言：本章主要讲解MySQL主从复制的操作步骤。由于环境限制，主机使用Windows环境，从机使用用Linux环境。另外MySQL的版本最好一致，笔者采用的MySQL5.7.22版本，具体安装过程请查询相关资料。

------

### 1.主从复制的基本原理

slave会从master读取binlog来进行数据同步。主要有以下三个步骤：

①master将改变记录到二进制日志（binary log），这些记录过程叫做二进制日志事件（binary log events）。

②slave将master的binary log events拷贝到中继日志（relay log）。

③slave重做中继日志中的事件，将改变应用到自己的数据库中。MySQL的复制是异步且串行化的。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180630100101056-666555235.png)

### 2.主从复制的规则

①每个slave只能有一个master。（一对一）

②每个slave只能有一个唯一的服务器ID。

③每个master可以有多个slave。（一对多）

在主从复制过程中，最大的问题就是延时。

### 3.一主一从的常见配置

\#1.要求。

MySQL版本最好一致且后台以服务运行。并且保证主机与从机互相ping通。主从配置都在[mysqld]结点下，都是小写。

\#2.主机修改my.ini配置文件

①server-id=1，主机服务器id。（必须）

②必须启用二进制文件。

```
log-bin="E:\devSoft\mysql-5.7.22-winx64\data\mysql-bin"
```

配置该项后，重新启动mysql服务，可看到如下内容。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180630103727168-1004774476.png)

③启用错误日志。（可选）

```
log_error ="E:\devSoft\mysql-5.7.22-winx64\data\log\errorlog\log_error.log"
```

④根目录、数据目录。（可选）

```
#mysql安装根目录
basedir ="E:\devSoft\mysql-5.7.22-winx64"
 
#mysql数据文件所在位置
datadir ="E:\devSoft\mysql-5.7.22-winx64\data"
```

⑤临时目录。（可选）

```
tmpdir  ="E:\devSoft\mysql-5.7.22-winx64\"
```

⑥read-only=0，表示主机读写都可以。

⑦可设置不需要复制的数据库。（可选）

```
binlog-ignore-db=mysql
```

⑧可设置需要复制的数据库。（可选）

```
binlog-do-db=databasename
```

\#3.从机修改my.cnf配置文件

①从服务器ID。（必须）

②启用二进制日志。（可选）

\#4.主机与从机都关闭防火墙，其实也可配置ip规则，但关闭防火墙更快速。

\#5.在Windows主机上建立账户并授权给slave。

a.首先在主机上创建账户：

```
 #%表示任何客户端都可以连接
 grant all privileges on *.* to slaveaccount（用户名）@"%(或者指定ip)" identified by '你想设置的密码' with grant option;
```

b.然后刷新权限表：

```
flush privileges;
```

c.然后授权给slave：

```
GRANT REPLICATION SLAVE ON *.* TO 'slaveaccount（上面创建的用户名）'@'从机数据库ip' IDENTIFIED BY '你想设置的密码'
```

d.利用b步骤命令再次刷新权限表。

\#6.查询master的状态。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180630111240913-127840494.png)

File和Position这两个字段非常重要，File告诉从机需要从哪个文件进行复制，Position告诉从机从文件的哪个位置开始复制，在从机上配置时需用到。执行完此操作后，尽量不要在操作主服务器MySQL，防止主服务器状态变化（File和Position状态变化）。

\#7.在Linux从机上配置需要的主机。

```
CHANGE MASTER TO MASTER_HOST='主机IP',MASTER_USER='salveaccount',MASTER_PASSWORD='主机授权的密码',MASTER_LOG_FILE='File名字',MASTER_LOG_POS=Position数字;
```

\#8.启动从服务器复制功能。

```
start slave；
```

启动复制功能后，需要查看主从复制配置是否成功。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180630114657015-1803232349.png)

注：只有当Slave_IO_Running:Yes和Slave_SQL_Running:Yes，这两个都为Yes的时候，主从复制配置才成功。

\#9.进行测试。

①首先在主机上建立数据库并插入数据。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180630115212138-1951438170.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180630115233414-1497139490.png)

②在从机中查看是否有相应数据库。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180630115324951-875955290.png)

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180630115413227-1780770996.png)

通过从机上查看相应数据，可知主从复制配置成功。

\#10.停止从服务复制功能。

```
stop slave；
```

### 4.总结

\#1.主从复制的配置，大部分都在主机上，注意查看相关步骤。

\#2.这里将主从机的防火墙都关闭是为了更好的演示，实际生产环境中一般不会出现windows主机和linux从机这种情况，因此不应该关闭防火墙，而是根据具体情况配置防火墙规则。

------

by Shawn Chen，2018.6.30日，下午。