# [MySQL高级知识（十二）——全局查询日志](https://www.cnblogs.com/developer_chan/p/9234710.html)



前言：全局查询日志用于保存所有的sql执行记录，该功能主要用于测试环境，在生产环境中永远不要开启该功能。

------

### 1.如何开启

\#1.通过my.cnf配置开启该功能。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627161120876-1334606348.png)

注：对my.cnf文件配置后，需重启mysql。

①通过命令查看全局查询日志是否开启成功。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627161248158-1543943226.png)

②查看全log_globalquery.log文件中的内容。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627161442252-157709183.png)

该log文件记录执行过的sql语句。

\#2.通过命令开启该功能。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627161908723-804463279.png)

通过以上配置，执行过的sql语句将会记录到mysql库中general_log表里。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627162127034-762559612.png)

### 2.总结

①通过命令方式开启该功能，重启mysql后失效。

②全局查询日志只用在测试环境，切记生产环境中永远不要开启该功能。

------

by Shawn Chen，2018.6.27日，下午。