# [Kafka导致重复消费原因和解决方案](https://segmentfault.com/a/1190000023282843)

[![img](https://avatar-static.segmentfault.com/868/271/868271510-54cb382abb7a1_small) java](https://segmentfault.com/t/java)[后端](https://segmentfault.com/t/后端)[kafka](https://segmentfault.com/t/kafka)

发布于 7月18日

![img](https://sponsor.segmentfault.com/lg.php?bannerid=0&campaignid=0&zoneid=25&loc=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000023282843&referer=https%3A%2F%2Fwww.baidu.com%2Flink%3Furl%3Dkq9zKThdbCSNbnmcY5wwX9zKz45QYijXDrLofiZDd1W0E2dULhk7RWGDIUQDTgNF5jdCTKYuyIX3NGBuGBF3e_%26wd%3D%26eqid%3Dc12a3e0d000ed12d000000065fb1d350&cb=9d6a8c3426)

## 问题分析

导致kafka的重复消费问题原因在于，已经消费了数据，但是offset没来得及提交（比如Kafka没有或者不知道该数据已经被消费）。
总结以下场景导致Kakfa重复消费：

**原因1：强行kill线程，导致消费后的数据，offset没有提交（消费系统宕机、重启等）。**
**原因2：设置offset为自动提交，关闭kafka时，如果在close之前，调用 consumer.unsubscribe() 则有可能部分offset没提交，下次重启会重复消费。**
例如：

```
try {
    consumer.unsubscribe();
} catch (Exception e) {
}

try {
    consumer.close();
} catch (Exception e) {
}
```

上面代码会导致部分offset没提交，下次启动时会重复消费。

**解决方法：设置offset自动提交为false**

整合了Spring配置的修改如下配置
spring配置：

```
spring.kafka.consumer.enable-auto-commit=false
spring.kafka.consumer.auto-offset-reset=latest
```

整合了API方式的修改enable.auto.commit为false
API配置：

```
 Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("group.id", "test");
props.put("enable.auto.commit", "false");
```

一旦设置了 enable.auto.commit 为 true，Kafka 会保证在开始调用 poll 方法时，提交上次 poll 返回的所有消息。从顺序上来说，poll 方法的逻辑是先提交上一批消息的位移，再处理下一批消息，因此它能保证不出现消费丢失的情况。

**原因3:（重复消费最常见的原因）：消费后的数据，当offset还没有提交时，partition就断开连接。比如，通常会遇到消费的数据，处理很耗时，导致超过了Kafka的session timeout时间（0.10.x版本默认是30秒），那么就会re-blance重平衡，此时有一定几率offset没提交，会导致重平衡后重复消费。**

**原因4：当消费者重新分配partition的时候，可能出现从头开始消费的情况，导致重发问题。**

**原因5：当消费者消费的速度很慢的时候，可能在一个session周期内还未完成，导致心跳机制检测报告出问题。**

**原因6：并发很大，可能在规定的时间（session.time.out默认30s）内没有消费完，就会可能导致reblance重平衡，导致一部分offset自动提交失败，然后重平衡后重复消费**

问题描述：
我们系统压测过程中出现下面问题：异常rebalance，而且平均间隔3到5分钟就会触发rebalance，分析日志发现比较严重。错误日志如下：

```
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
```

这个错误的意思是，消费者在处理完一批poll的消息后，在同步提交偏移量给broker时报的错。初步分析日志是由于当前消费者线程消费的分区已经被broker给回收了，因为kafka认为这个消费者死了，那么为什么呢？

问题分析：

这里就涉及到问题是消费者在创建时会有一个属性max.poll.interval.ms（默认间隔时间为300s），
该属性意思为kafka消费者在每一轮poll()调用之间的最大延迟,消费者在获取更多记录之前可以空闲的时间量的上限。如果此超时时间期满之前poll()没有被再次调用，则消费者被视为失败，并且分组将重新平衡，以便将分区重新分配给别的成员。

## 处理重复数据

因为offset此时已经不准确，生产环境不能直接去修改offset偏移量。
所以重新指定了一个消费组（group.id=order_consumer_group），然后指定auto-offset-reset=latest这样我就只需要重启我的服务了，而不需要动kafka和zookeeper了！

```
#consumer
spring.kafka.consumer.group-id=order_consumer_group
spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.value-deserializer=org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.enable-auto-commit=false
spring.kafka.consumer.auto-offset-reset=latest
```

注：如果你想要消费者从头开始消费某个topic的全量数据，可以重新指定一个全新的group.id=new_group，然后指定auto-offset-reset=earliest即可



# 如何搞定Kafka重复消费？

[奈学运营小编](https://www.zhihu.com/people/www.naixuejiaoyu.com)

4 人赞同了该文章

如何保证 Kafka 消息不重复消费？我们在做开发的时候为了程序的健壮性，在使用 Kafka 的时候一般都会设置重试的次数，但是因为网络的一些原因，设置了重试就有可能导致有些消息重复发送了（当然导致消息重复也有可能是其他原因），那么怎么解决消息重复这个问题呢？关于这个问题，我这儿提供了如下三种解决方案，供大家参考。

解决方案

方案一 / 保存并查询

给每个消息都设置一个独一无二的 key，消费的时候把 key 记录下来，然后每次消费新的消息的时候都查询一下，看当前消息的这个 key 是否消费过，如果没有消费过才进行消费。（这种方式好想，但是其实实现起来一点也不简单）

![img](https://pic2.zhimg.com/80/v2-779e5f47903f1dce30e9b0133bb9c281_720w.jpg)

方案二 / 利用幂等

幂等（Idempotence）在数学上是这样定义的，如果一个函数 f(x) 满足：f(f(x)) = f(x)，则函数 f(x) 满足幂等性。

这个概念被拓展到计算机领域，被用来描述一个操作、方法或者服务。一个幂等操作的特点是，其任意多次执行所产生的影响均与一次执行的影响相同。一个幂等的方法，使用同样的参数，对它进行多次调用和一次调用，对系统产生的影响是一样的。所以，对于幂等的方法，不用担心重复执行会对系统造成任何改变。

我们举个例子来说明一下。在不考虑并发的情况下，“将 X 老师的账户余额设置为 100 万元”，执行一次后对系统的影响是，X 老师的账户余额变成了 100 万元。只要提供的参数 100万元不变，那即使再执行多少次，X 老师的账户余额始终都是 100万元，不会变化，这个操作就是一个幂等的操作。

再举一个例子，“将 X 老师的余额加 100 万元”，这个操作它就不是幂等的，每执行一次，账户余额就会增加 100 万元，执行多次和执行一次对系统的影响（也就是账户的余额）是不一样的。

所以，通过这两个例子，我们可以想到如果系统消费消息的业务逻辑具备幂等性，那就不用担心消息重复的问题了，因为同一条消息，消费一次和消费多次对系统的影响是完全一样的。也就可以认为，消费多次等于消费一次。

那么，如何实现幂等操作呢？最好的方式就是，从业务逻辑设计上入手，将消费的业务逻辑设计成具备幂等性的操作。但是，不是所有的业务都能设计成天然幂等的，这里就需要一些方法和技巧来实现幂等。

下面我们介绍一种常用的方法：利用数据库的唯一约束实现幂等。

例如，我们刚刚提到的那个不具备幂等特性的转账的例子：将 X 老师的账户余额加 100 万元。在这个例子中，我们可以通过改造业务逻辑，让它具备幂等性。

首先，我们可以限定，对于每个转账单每个账户只可以执行一次变更操作，在分布式系统中，这个限制实现的方法非常多，最简单的是我们在数据库中建一张转账流水表，这个表有三个字段：转账单 ID、账户 ID 和变更金额，然后给转账单 ID 和账户 ID 这两个字段联合起来创建一个唯一约束，这样对于相同的转账单 ID 和账户 ID，表里至多只能存在一条记录。

这样，我们消费消息的逻辑可以变为：“在转账流水表中增加一条转账记录，然后再根据转账记录，异步操作更新用户余额即可。”在转账流水表增加一条转账记录这个操作中，由于我们在这个表中预先定义了“账户 ID 转账单 ID”的唯一约束，对于同一个转账单同一个账户只能插入一条记录，后续重复的插入操作都会失败，这样就实现了一个幂等的操作。

![img](https://pic1.zhimg.com/80/v2-af953c2bc55ff9e9c584070481c4b2a4_720w.jpg)

方案三 / 设置前置条件

为更新的数据设置前置条件另外一种实现幂等的思路是，给数据变更设置一个前置条件，如果满足条件就更新数据，否则拒绝更新数据，在更新数据的时候，同时变更前置条件中需要判断的数据。

这样，重复执行这个操作时，由于第一次更新数据的时候已经变更了前置条件中需要判断的数据，不满足前置条件，则不会重复执行更新数据操作。

比如，刚刚我们说过，“将 X 老师的账户的余额增加 100 万元”这个操作并不满足幂等性，我们可以把这个操作加上一个前置条件，变为：“如果X老师的账户当前的余额为 500万元，将余额加 100万元”，这个操作就具备了幂等性。

对应到消息队列中的使用时，可以在发消息时在消息体中带上当前的余额，在消费的时候进行判断数据库中，当前余额是否与消息中的余额相等，只有相等才执行变更操作。

但是，如果我们要更新的数据不是数值，或者我们要做一个比较复杂的更新操作怎么办？用什么作为前置判断条件呢？更加通用的方法是，给你的数据增加一个版本号属性，每次更数据前，比较当前数据的版本号是否和消息中的版本号一致，如果不一致就拒绝更新数据，更新数据的同时将版本号 +1，一样可以实现幂等。

![img](https://pic3.zhimg.com/80/v2-e1bc22f737e308d999496d77df1f8926_720w.jpg)

最后

今天给大家提供的消息重复的解决方案，也参考了《消息队列高手课》里的思路，大家如果有什么好的解决方案，欢迎讨论！

发布于 05-18