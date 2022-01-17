# kafka 消息堆积慢消费问题



一. 问题描述
        我们的物料筛选排序系统之前经常会出现操作效果延迟的情况。在筛选排序数据不对时，我们一般会查看ES里存储的数据和DB里存储的数据是否一致，发现在一段时间内确实会存在数据不一致。我们怀疑是数据流下发存在延迟，于是立刻查看了kafka里消息增量数量的监控，发现出问题时kafka消息增量一般都堆积比较严重，而且看kafka的消息数变化曲线，消息堆积被消费后下降的速度要明显慢于平时下降的速度。因为在凤巢消息堆积和增量变多有时候是业务上的流量变大导致的，比如某些特殊的活动导致广告主调用API大量编辑物料，但是消息堆积后消费者的速度不但跟不上了，反而变得更慢了，这个问题是急需解决的。

二. 排查过程
        我对消息堆积后消息被消费掉的速度变慢产生了好奇。首选我在思考是不是最近消费者模块有代码升级，导致消费者本身对业务的处理变慢了。但是看了git的提交之后,发现提交时间是在几个月前，要是是代码本身的问题，应该早就应该暴露了。
        因为我们消费者模块主要的操作就是去读取kafka下发的增量然后解析增量的内容同步修改ES，然后怀疑是增量的什么原因，导致消息堆积后消息下降变慢。然后我在遇上线的环境上线了打印解析消息内容的日志，然后让QA同学用压测工具回放出现故障时的线上流量，然后我观察日志分析出问题的原因。结果发现了不但复现了消息堆积的情况，还发现消息堆积时还出现了大量的重复消息。于是我想到可能是由于消息堆积触发了kafka对消息回滚的策略，导致了大量的消息重发，因此存在这边消费者在消费消息，另一边却在不断重发消息，因此消息的下降速度会变慢
并且查看了错误日志，有大量以下报错

````shell
08-09 11:01:11 131 pool-7-thread-3 ERROR [] - 
commit failed 
org.apache.kafka.clients.consumer.CommitFailedException: Commit cannot be completed since the group has already rebalanced and assigned the partitions to another member. This means that the time between subsequent calls to poll() was longer than the configured max.poll.interval.ms, which typically implies that the poll loop is spending too much time message processing. You can address this either by increasing the session timeout or by reducing the maximum size of batches returned in poll() with max.poll.records.
        at org.apache.kafka.clients.consumer.internals.ConsumerCoordinator.sendOffsetCommitRequest(ConsumerCoordinator.java:713) ~[MsgAgent-jar-with-dependencies.jar:na]
        at org.apache.kafka.clients.consumer.internals.ConsumerCoordinator.commitOffsetsSync(ConsumerCoordinator.java:596) ~[MsgAgent-jar-with-dependencies.jar:na]
        at org.apache.kafka.clients.consumer.KafkaConsumer.commitSync(KafkaConsumer.java:1218) ~[MsgAgent-jar-with-dependencies.jar:na]
        at com.today.eventbus.common.MsgConsumer.run(MsgConsumer.java:121) ~[MsgAgent-jar-with-dependencies.jar:na]
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149) [na:1.8.0_161]
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624) [na:1.8.0_161]
        at java.lang.Thread.run(Thread.java:748) [na:1.8.0_161]
````


错误的意思是消费者在处理完一批poll的消息后，在同步提交偏移量给broker时出错。初步分析日志是由于当前消费者线程消费的分区已经被broker给回收了，因为kafka认为这个消费者死了，那么为什么呢？

三. 原理分析
如下是我们消费者处理逻辑(省略业务相关代码)

````java
while (isRunning) {
      ConsumerRecords<KEY, VALUE> records = consumer.poll(100);
      if (records != null && records.count() > 0) {
	      for (ConsumerRecord<KEY, VALUE> record : records) {
	          dealMessage(bizConsumer, record.value());
	          try {
	                //records记录全部完成后，才提交
	                consumer.commitSync();
	          } catch (CommitFailedException e) {
	                logger.error("commit failed,will break this for loop", e);
	                  break;
	         }
	     }
	 }
 }
````

​        poll()方法该方法轮询返回消息集，调用一次可以获取一批消息。kafkaConsumer调用一次轮询方法只是拉取一次消息。客户端为了不断拉取消息，会用一个外部循环不断调用消费者的轮询方法。每次轮询到消息，在处理完这一批消息后，才会继续下一次轮询。
​        kafka的偏移量(offset)是由消费者进行管理的，偏移量有两种，拉取偏移量(position)与提交偏移量(committed)。拉取偏移量代表当前消费者分区消费进度。每次消息消费后，需要提交偏移量。在提交偏移量时，kafka会使用拉取偏移量的值作为分区的提交偏移量发送给协调者。如果没有提交偏移量，下一次消费者重新与broker连接后，会从当前消费者group已提交到broker的偏移量处开始消费。
​        我在网上查阅了消息堆积和消息重复的一些原因，发现问题可能出现在kafka的poll()设置上。
​        查阅kafka官网发现我用的那个版本的kafka主要有以下几个比较关键的指标:
​        a. max.poll.records一次poll返回的最大记录数默认是500
​        b. max.poll.interval.ms两次poll方法最大时间间隔这个参数，默认是300s
​        这次问题出现的原因为由于业务上下方的消息增量变多，导致堆积的消息过多，每一批poll()的处理都能达到500条消息，导致poll之后消费的时间过长。 服务端约定了和客户端max.poll.interval.ms，两次poll最大间隔。如果客户端处理一批消息花费的时间超过了这个限制时间，broker可能就会把消费者客户端移除掉，提交偏移量又会报错。所以拉取偏移量没有提交到broker，分区又rebalance，下一次重新分配分区时，消费者会从最新的已提交偏移量处开始消费，这里就出现了重复消费的问题。而服务注册中心zookeeper以为客户端失效进行rebalance，因此连接到另外一台消费服务器，然而另外一台服务器也出现poll()超时，又进行rebalance…如此循环，才出现了一直重发消息，导致消息数量被消费后下降很慢。

四．Rebalance介绍
        consumer订阅topic中的一个或者多个partition中的消息，一个consumer group下可以有多个consumer，一条消息只能被group中的一个consumer消费。consumer和consumer group的关系是动态维护的，并不固定，当某个consumer卡住或者挂掉时，该consumer订阅的partition会被重新分配给该group下其它consumer，用于保证服务的可用性。为维护consumer和group之间的关系，consumer会定期向服务端的coordinator(一个负责维持客户端与服务端关系的协调者)发送心跳heartbeat，当consumer因为某种原因如死机无法在session.timeout.ms配置的时间间隔内发送heartbeat时，coordinator会认为该consumer已死，它所订阅的partition会被重新分配给同一group的其它consumer，该过程叫：rebalanced。
        kafka在0.10.1之后的版本，增加了另一个概念：max.poll.interval.ms，即最大的poll时间间隔。consumer是通过拉取的方式向服务端拉取数据，当超过指定时间间隔max.poll.interval.ms没有向服务端发送poll()请求，而心跳heartbeat线程仍然在继续，会认为该consumer锁死，就会将该consumer退出group，并进行再分配。
        这是一个巧妙的设计，两个配置项对应2个线程，在0.10.0之前的版本中，是没有区分这2个线程的，即超过session.timeout.ms没有发送心跳就直接rebalance。session.timeout.ms默认值是10秒，max.poll.interval.ms默认值是300s，改进为2个线程的意义在于，heartbeat线程独立于consumer的消费能力，在后台运行，用于快速检查整个客户端服务是否可用（如发生宕机等情况），而poll线程与consumer消费能力挂勾，用于检查单个consumer是否可用，这样可以避免当某些consumer消费较久配置心跳时间很长的情况下，我们不必等到这么久才知道服务可能已经宕机了。

五. 解决方案
使用Kafka时，消费者每次poll的数据业务处理时间不能超过kafka的max.poll.interval.ms，可以考虑调大超时时间或者调小每次poll的数据量。
增加max.poll.interval.ms处理时长(默认间隔300s)

max.poll.interval.ms=300

修改分区拉取阈值(默认50,建议压测评估调小)

max.poll.records = 50

可以考虑增强消费者的消费能力，使用线程池消费或者将消费者中耗时业务改成异步，并保证对消息是幂等处理
不但要有消息积压的监控，还可以考虑做消息消费速度的监控（前后两次offset比较）
————————————————
版权声明：本文为CSDN博主「zxcodestudy」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_16681169/article/details/101081656



# [记一次线上Kafka消息堆积踩坑总结](https://www.cnblogs.com/williamjie/p/9719805.html)

  年后上线的系统，与其他业务系统的通信方式采用了第三代消息系统中间件Kafka。由于是第一次使用，踩了很多坑，通过这篇博客和大家分享一下，也算是做个总结，以便以后温故而知新。

一、线上问题

  系统平稳运行两个多月，基本上没有问题，知道最近几天，突然出现Kafka手动提交失败，堆栈信息如下：

![img](https://img-blog.csdn.net/20180530181818953?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9ndW96aTAyMTg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

通过堆栈信息可以看出，有两个重要参数： session.timeout  和 max.poll.records

session.timeout.ms : 在使用Kafka的团队管理设施时，用于检测消费者失败的超时时间。消费者定期发送心跳来向经纪人表明其活跃度。如果代理在该会话超时到期之前没有收到心跳，那么代理将从该组中删除该消费者并启动重新平衡。

max.poll.records : 在一次调用poll（）中返回的最大记录数。

根据堆栈的提示，他让增加 session.timeout.ms 时间 或者 减少 max.poll.records。

二、解决过程

  然后我琢磨，上线两个月都没有问题，为什么最近突然出现问题了。我想肯定是业务系统有什么动作，我就去问了一个下，果然头一天风控系统kafka挂掉了，并进行了数据重推，导致了数据阻塞。但是我又想即使阻塞了也会慢慢消费掉牙，不应该报错呀。后来我看了一下kafka官网上的参数介绍，发现max.poll.records默认是2147483647 （0.10.0.1版本），也就是kafka里面有多少poll多少，如果消费者拿到的这些数据在制定时间内消费不完，就会手动提交失败，数据就会回滚到kafka中，会发生重复消费的情况。如此循环，数据就会越堆越多。后来咨询了公司的kafka大神，他说我的kafka版本跟他的集群版本不一样让我升级kafka版本。于是我就升级到了0.10.2.1，查阅官网发现这个版本的max.poll.records默认是500，可能kafka开发团队也意识到了这个问题。并且这个版本多了一个max.poll.interval.ms这个参数，默认是300s。这个参数的大概意思就是kafka消费者在一次poll内，业务处理时间不能超过这个时间。后来升级了kafka版本，把max.poll.records改成了50个之后，上了一次线，准备观察一下。上完线已经晚上9点了，于是就打卡回家了，明天看结果。第二天早起满心欢喜准备看结果，以为会解决这个问题，谁曾想还是堆积。我的天，思来想去，也想不出哪里有问题。于是就把处理各个业务的代码前后执行时间打印出来看一下，添加代码，提交上线。然后观察结果，发现大部分时间都用在数据库IO上了，并且执行时间很慢，大部分都是2s。于是想可能刚上线的时候数据量比较小，查询比较快，现在数据量大了，就比较慢了。当时脑子里第一想法就是看了一下常用查询字段有没有添加索引，一看没有，然后马上添加索引。加完索引观察了一下，处理速度提高了好几倍。虽然单条业务处理的快乐， 但是堆积还存在，后来发现，业务系统大概1s推送3、4条数据，但是我kafka现在是单线程消费，速度大概也是这么多。再加上之前的堆积，所以消费还是很慢。于是业务改成多线程消费，利用线程池，开启了10个线程，上线观察。几分钟就消费完了。大功告成，此时此刻，心里舒坦了好多。不容易呀！

 

总结：

1、 使用Kafka时，消费者每次poll的数据业务处理时间不能超过kafka的max.poll.interval.ms，该参数在kafka0.10.2.1中的默认值是300s,所以要综合业务处理时间和每次poll的数据数量。

2、Java线程池大小的选择，

对于CPU密集型应用，也就是计算密集型，线程池大小应该设置为CPU核数+1；

对于IO密集型应用 ，线程池大小设置为  2*CPU核数+1.   