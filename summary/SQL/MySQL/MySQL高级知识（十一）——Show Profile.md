# [MySQL高级知识（十一）——Show Profile](https://www.cnblogs.com/developer_chan/p/9231761.html)



前言：Show Profile是mysql提供的可以用来分析当前会话中sql语句执行的资源消耗情况的工具，可用于sql调优的测量。默认情况下处于关闭状态，并保存最近15次的运行结果。

------

### 1.分析步骤

\#1.开启Show Profile功能，默认该功能是关闭的，使用前需开启。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627143317144-1044896037.png)

\#2.根据[MySQL高级知识（十）——批量插入数据脚本](https://www.cnblogs.com/morewindows0/p/9229845.html)中的数据脚本向tb_emp_bigdata表中插入50w条数据。然后执行如下查询语句：

```
select *from tb_emp_bigdata group by id%10 limit 150000;
select *from tb_emp_bigdata group by id%20 order by 5;
```

\#3.通过show profiles查看结果。

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627145732670-1634553020.png)

\#4.使用show profile对sql语句进行诊断。

```
show profile cpu,block io for query Query_ID;/*Query_ID为#3步骤中show profiles列表中的Query_ID*/
```

比如执行：show profile cpu,block io for query 15;

![img](https://images2018.cnblogs.com/blog/706569/201806/706569-20180627151015512-40109674.png)

\#5.show profile的常用查询参数。

①ALL：显示所有的开销信息。

②BLOCK IO：显示块IO开销。

③CONTEXT SWITCHES：上下文切换开销。

④CPU：显示CPU开销信息。

⑤IPC：显示发送和接收开销信息。

⑥MEMORY：显示内存开销信息。

⑦PAGE FAULTS：显示页面错误开销信息。

⑧SOURCE：显示和Source_function，Source_file，Source_line相关的开销信息。

⑨SWAPS：显示交换次数开销信息。

\#6.日常开发需注意的结论。

①converting  HEAP to MyISAM：查询结果太大，内存不够，数据往磁盘上搬了。

②Creating tmp table：创建临时表。先拷贝数据到临时表，用完后再删除临时表。

③Copying to tmp table on disk：把内存中临时表复制到磁盘上，危险！！！

④locked。

如果在show profile诊断结果中出现了以上4条结果中的任何一条，则sql语句需要优化。

### 2.总结

\#1.show profile默认是关闭的，并且开启后只存活于当前会话，也就说每次使用前都需要开启。

\#2.通过show profiles查看sql语句的耗时时间，然后通过show profile命令对耗时时间长的sql语句进行诊断。

\#3.注意show profile诊断结果中出现相关字段的含义，判断是否需要优化sql语句。

\#4.可更多的关注MySQL官方文档，获取更多的知识。

------

by Shawn Chen，2018.6.27日，下午。