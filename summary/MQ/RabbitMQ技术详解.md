# **RabbitMQ技术详解**

## RabbitMQ是什么

### 定义

RabbitMQ是一个开源的AMQP实现，服务器端用Erlang语言编写，支持多种客户端，如：Python、Ruby、.NET、Java、JMS、C、PHP、ActionScript、XMPP、STOMP等，支持AJAX。用于在分布式系统中存储转发消息，在易用性、扩展性、高可用性等方面表现不俗。

### AMPQ

AMQP，即Advanced Message Queuing Protocol，高级消息队列协议，是应用层协议的一个开放标准，为面向消息的中间件设计。消息中间件主要用于组件之间的解耦，消息的发送者无需知道消息使用者的存在，反之亦然。

它可以使对应的客户端（client）与对应的消息中间件（broker）进行交互。消息中间件从发布者（publisher）那里收到消息（发布消息的应用，也称为producer），然后将他们转发给消费者（consumers，处理消息的应用）。由于AMQP是一个网络协议，所以发布者、消费者以及消息中间件可以部署到不同的物理机器上面。

虽然在同步消息通讯的世界里有很多公开标准（如 COBAR的 IIOP ，或者是 SOAP 等），但是在异步消息处理中却不是这样，只有大企业有一些商业实现（如微软的 MSMQ ，IBM 的 Websphere MQ 等），因此，在 2006 年的 6 月，Cisco 、Redhat、iMatix 等联合制定了 AMQP 的公开标准。

RabbitMQ是由RabbitMQ Technologies Ltd开发并且提供商业支持的。该公司在2010年4月被SpringSource（VMWare的一个部门）收购。在2013年5月被并入Pivotal。其实VMWare，Pivotal和EMC本质上是一家的。不同的是VMWare是独立上市子公司，而Pivotal是整合了EMC的某些资源，现在并没有上市。

## 同类产品

消息中间件是一种由消息传送机制或消息队列模式组成的中间件技术，利用高效可靠的消息传递机制进行平台无关的数据交流，并基于数据通信来进行分布式系统的集成。

### Redis

是一个Key-Value的NoSQL数据库，开发维护很活跃，虽然它是一个Key-Value数据库存储系统，但它本身支持MQ功能，所以完成可以当做一个轻量级的队列服务来使用。对于RabbitMQ和Redis的入队和出队操作，各执行100万次，每10万次记录一次执行时间。测试数据分为128Bytes、512Bytes、1K和10K四个不同大小的数据。实验表明：入队时，当数据比较小时，Redis的性能要高于RabbitMQ，而如否数据大小超过了10K，Redis则慢的无法忍受；出队时，无论数据大小，Redis都表现出非常好的性能，而RabbitMQ的出队性能则远低于Redis。

### MemcacheQ

持久化消息队列（简称mcq）是一个轻量级的消息队列，特性如下：

简单易用

处理速度快

多条队列

并发性能好

与memcache的协议兼容。意味着只要装了前者的extension即可，不需要额外的插件

在zend framework中使用很方便

### MSMQ

这是微软的产品力唯一被认为有价值的东西。如果MSMQ能证明可以应对这种任务，他们将选择使用它。

关键是它并不复杂，除了接收和发送，没有别的；它有一些硬性限制，比如最大消息体积是4MB。

然而，通过和一些想MassTransit或NServiceBus这样的软件的连接，它完全可以解决这些问题。

![img](http://www.uml.org.cn/zjjs/images/2018052341.png)

### ZeroMQ

ZeroMQ是一个非常轻量级的消息系统，号称最快的消息队列系统，专门为高吞吐量/低延迟的场景开发，在金融界的应用中经常可以发现它。

与RabbitMQ相比，ZeroMQ支持许多高级消息场景，能够实现RabbitMQ不擅长的高级/复杂的队列，但是你必须实现ZeroMQ框架中的各个块（比如Socket或Device等）。

ZeroMQ具有一个独特的非中间件的模式，你不需要安装和运行一个消息服务器或中间件，因为你的应用程序将扮演这个服务角色。你只需要简单地引用ZeroMQ程序库，可以使用NuGet安装，然后你就可以愉快地在应用程序之间发送消息了。

但是ZeroMQ仅提供非持久性的队列，即没有地方可以观察它是否有问题出现，也就是说如果down机，数据将会丢失。

ZeroMQ非常灵活，但是你必须学习它的80页的手册（如果你要写一个分布式系统，一定要阅读它）。

![img](http://www.uml.org.cn/zjjs/images/2018052342.png)

### Jafka/Kafka

Kafka（能将消息分散到不同的节点上）是LinkedIn于2010年12月开发并开源的一个分布式MQ系统，现在是Apache的一个孵化项目，是一个高性能跨语言分布式Publish/Subscribe消息队列系统，而Jafka是在Kafka之上孵化而来的，即Kafka的一个升级版。具有以下特性：

快速持久化，可以在O(1)的系统开销下进行消息持久化；

高吞吐，在一台普通的服务器上既可以打到10W/s的吞吐速率；

完全的分布式系统，Broker、Producer、Consumer都原生自动支持分布式，自动实现复杂均衡；

支持Hadoop数据并行加载，统一了在线和离线的消息处理，对于像Hadoop一样的日志数据和离线分析系统，但又要求实时处理的限制，这是一个可行的解决方案。

相对于ActiveMQ是一个非常轻量级的消息系统，除了性能非常好之外，还是一个工作良好的分布式系统。

![img](http://www.uml.org.cn/zjjs/images/2018052343.png)

### Apache ActiveMQ

ActiveMQ居于（RabbitMQ&ZeroMQ）之间，类似于ZemoMQ，它可以部署于代理模式和P2P模式。

ActiveMQ被誉为Java世界的中坚力量。它有很长的历史，且被广泛使用。它还是跨平台的，给那些非微软平台的产品提供了一个天然的集成接入点。

然而它只有跑过了MSMQ才有可能被考虑。如需配置ActiveMQ则需要在目标机器上安装Java环境。

类似于RabbitMQ，它易于实现高级场景，而且只需付出低消耗。它被誉为消息中间件的“瑞士军刀”。

![img](http://www.uml.org.cn/zjjs/images/2018052344.png)

### RabbitMQ

RabbitMQ是使用Erlang编写的一个开源消息队列，本身支持很多的协议：AMQP， XMPP， SMTP， STONP，也正是如此，使的它变的非常重量级，更适合于企业级的开发。

它实现了代理(Broker)架构，意味着消息在发送到客户端之前可以在中央节点上排队。此特性使得RabbitMQ易于使用和部署，适宜于很多场景如路由、负载均衡或消息持久化等，用消息队列只需几行代码即可搞定。

但是，这使得它的可扩展性差，速度较慢，因为中央节点增加了延迟，消息封装后也比较大。

如需配置RabbitMQ则需要在目标机器上安装Erlang环境。

![img](http://www.uml.org.cn/zjjs/images/2018052345.png)

### 总结

最终，上述同类产品：

1. 都有各自客户端API或支持多种编程语言

2. 都有大量的文档

3. 都提供了积极的支持

4. ActiveMQ、RabbitMQ、MSMQ、Redis都需要启动服务进程，这些都可以监控和配置，其他几个就有问题了

5. 都相对提供了良好的可靠性（一致性）、扩展性和负载均衡，当然还有性能

下面是网友的对四种消息队列的具体测试结果，显示的是发送和接受的每秒钟的消息数，整个过程共产生1百万条1K的消息，测试的执行是在WIndows Vista上进行的。（有待自己验证）

![img](http://www.uml.org.cn/zjjs/images/2018052346.png)

如上图所见，ZeroMQ和其他的不是一个级别，它的性能惊人的高。结论很清楚：如果希望一个应用程序发送消息越快越好，选择ZeroMQ，并且在你不太在意偶然会丢失某些消息的情况下更有价值。

## RabbitMQ为何会出现

或者说AMPQ为何会出现，它的应用场景又是什么？

### 解决什么问题

你是否遇到过两个（多个）系统间需要通过定时任务来同步某些数据？你是否在为异构系统的不同进程间相互调用、通讯的问题而苦恼、挣扎？

在Web应用高并发环境下，由于来不及同步处理，请求往往会发生堵塞。比如说，大量的insert、update请求同时到达mysql，会带来无数的行锁表锁，最后导致请求数过多，触发too many connections错误。

消息服务擅长于解决多系统、异构系统间的数据交换（消息通知/通讯）问题，你也可以把它用于系统间服务的相互调用（RPC）通过使用消息队列，我们可以异步处理请求，从而缓解系统的压力。

### 应用场景

对于一个大型的软件系统来说，它会有很多的组件或者说模块或者说子系统或者（Subsystem or Component or Submodule）。那么这些模块的如何通信？这和传统的IPC有很大的区别。传统的IPC很多都是在单一系统上的，模块耦合性很大，不适合扩展（Scalability）；如果使用socket那么不同的模块的确可以部署到不同的机器上，但是还是有很多问题需要解决。比如：

1. 信息的发送者和接收者如何维持这个连接，如果一方的连接中断，这期间的数据如何方式丢失？

2. 如何降低发送者和接收者的耦合度？

3. 如何让Priority高的接收者先接到数据？

4. 如何做到Load balance？有效均衡接收者的负载？

5. 如何有效的将数据发送到相关的接收者？也就是说将接收者subscribe 不同的数据，如何做有效的filter。

6. 如何做到可扩展，甚至将这个通信模块发到cluster上？

7. 如何保证接收者接收到了完整，正确的数据？

AMDQ协议解决了以上的问题，而RabbitMQ实现了AMQP。

## RabbitMQ基础概念

应用场景架构

![img](http://www.uml.org.cn/zjjs/images/2018052347.png)

RabbitMQ Server：也叫broker server，它不是运送食物的卡车，而是一种传输服务。原话是RabbitMQ isn’t a food truck, it’s a delivery service. 他的角色就是维护一条从Producer到Consumer的路线，保证数据能够按照指定的方式进行传输。但是这个保证也不是100%的保证，但是对于普通的应用来说这已经足够了。当然对于商业系统来说，可以再做一层数据一致性的guard，就可以彻底保证系统的一致性了。

Client A & B：也叫Producer，数据的发送方。Create messages and Publish (Send) them to a broker server (RabbitMQ)。一个Message有两个部分：Payload（有效载荷）和Label（标签）。Payload顾名思义就是传输的数据，Label是Exchange的名字或者说是一个tag，它描述了payload，而且RabbitMQ也是通过这个label来决定把这个Message发给哪个Consumer。AMQP仅仅描述了label，而RabbitMQ决定了如何使用这个label的规则。

Client 1，2，3：也叫Consumer，数据的接收方。Consumers attach to a broker server (RabbitMQ) and subscribe to a queue。把queue比作是一个有名字的邮箱。当有Message到达某个邮箱后，RabbitMQ把它发送给它的某个订阅者即Consumer。当然可能会把同一个Message发送给很多的Consumer。在这个Message中，只有payload，label已经被删掉了。对于Consumer来说，它是不知道谁发送的这个信息的。就是协议本身不支持。但是当然了如果Producer发送的payload包含了Producer的信息就另当别论了。

对于一个数据从Producer到Consumer的正确传递，还有三个概念需要明确：exchanges, queues and bindings。

Exchanges are where producers publish their messages. 消息交换机，它指定消息按什么规则，路由到哪个队列

Queues are where the messages end up and are received by consumers. 消息队列载体，每个消息都会被投入到一个或多个队列

Bindings are how the messages get routed from the exchange to particular queues. 绑定，它的作用就是把exchange和queue按照路由规则绑定起来

Routing Key：路由关键字，exchange根据这个关键字进行消息投递

还有几个概念是上述图中没有标明的，那就是Connection（连接），Channel（通道，频道），Vhost（虚拟主机）。

Connection：就是一个TCP的连接。Producer和Consumer都是通过TCP连接到RabbitMQ Server的。以后我们可以看到，程序的起始处就是建立这个TCP连接。

Channel：虚拟连接。它建立在上述的TCP连接中。数据流动都是在Channel中进行的。也就是说，一般情况是程序起始建立TCP连接，第二步就是建立这个Channel。

Vhost：虚拟主机，一个broker里可以开设多个vhost，用作不同用户的权限分离。每个virtual host本质上都是一个RabbitMQ Server，拥有它自己的queue，exchagne，和bings rule等等。这保证了你可以在多个不同的application中使用RabbitMQ。

### Channel的选择

那么，为什么使用Channel，而不是直接使用TCP连接？

对于OS来说，建立和关闭TCP连接是有代价的，频繁的建立关闭TCP连接对于系统的性能有很大的影响，而且TCP的连接数也有限制，这也限制了系统处理高并发的能力。但是，在TCP连接中建立Channel是没有上述代价的。对于Producer或者Consumer来说，可以并发的使用多个Channel进行Publish或者Receive。

有实验表明，1s的数据可以Publish10K的数据包。当然对于不同的硬件环境，不同的数据包大小这个数据肯定不一样，但是我只想说明，对于普通的Consumer或者Producer来说，这已经足够了。如果不够用，你考虑的应该是如何细化split你的设计。

消息队列执行过程

1. 客户端连接到消息队列服务器，打开一个Channel。

2. 客户端声明一个Exchange，并设置相关属性。

3. 客户端声明一个Queue，并设置相关属性。

4. 客户端使用Routing key，在Exchange和Queue之间建立好绑定关系。

5. 客户端投递消息到Exchange。

Exchange接收到消息后，就根据消息的key和已经设置的Binding，进行消息路由，将消息投递到一个或多个队列里。有三种类型的Exchanges：direct，fanout，topic，每个实现了不同的路由算法（routing algorithm）：

Direct exchange：完全根据key进行投递的叫做Direct交换机。如果Routing key匹配, 那么Message就会被传递到相应的queue中。其实在queue创建时，它会自动的以queue的名字作为routing key来绑定那个exchange。例如，绑定时设置了Routing key为”abc”，那么客户端提交的消息，只有设置了key为”abc”的才会投递到队列。

Fanout exchange：不需要key的叫做Fanout交换机。它采取广播模式，一个消息进来时，投递到与该交换机绑定的所有队列。

Topic exchange：对key进行模式匹配后进行投递的叫做Topic交换机。比如符号”#”匹配一个或多个词，符号””匹配正好一个词。例如”abc.#”匹配”abc.def.ghi”，”abc.”只匹配”abc.def”。

更多消息队列相关设计介绍请参考：

RabbitMQ系列二（构建消息队列）

RabbitMQ系列三 （深入消息队列）

### 消息队列的创建

Consumer和Procuder都可以通过 queue.declare 创建queue。对于某个Channel来说，Consumer不能declare一个queue，却订阅其他的queue。当然也可以创建私有的queue。这样只有app本身才可以使用这个queue。queue也可以自动删除，被标为auto-delete的queue在最后一个Consumer unsubscribe后就会被自动删除。那么如果是创建一个已经存在的queue呢？那么不会有任何的影响。需要注意的是没有任何的影响，也就是说第二次创建如果参数和第一次不一样，那么该操作虽然成功，但是queue的属性并不会被修改。

那么谁应该负责创建这个queue呢？是Consumer，还是Producer？

如果queue不存在，当然Consumer不会得到任何的Message。但是如果queue不存在，那么Producer Publish的Message会被丢弃。所以，还是为了数据不丢失，Consumer和Producer都try to create the queue！反正不管怎么样，这个接口都不会出问题。

Queue对load balance的处理是完美的。对于多个Consumer来说，RabbitMQ 使用循环的方式（round-robin）的方式均衡的发送给不同的Consumer。

### 消息的ack机制

默认情况下，如果Message 已经被某个Consumer正确的接收到了，那么该Message就会被从queue中移除。当然也可以让同一个Message发送到很多的Consumer。

如果一个queue没被任何的Consumer Subscribe（订阅），那么，如果这个queue有数据到达，那么这个数据会被cache，不会被丢弃。当有Consumer时，这个数据会被立即发送到这个Consumer，这个数据被Consumer正确收到时，这个数据就被从queue中删除。

那么什么是正确收到呢？通过ack。

每个Message都要被acknowledged（确认，ack）。我们可以显示的在程序中去ack（Consumer的basic.ack），也可以自动的ack（订阅Queue时指定auto_ack为true）。

如果有数据没有被ack，那么RabbitMQ Server会把这个信息发送到下一个Consumer。

如果这个app有bug，忘记了ack，那么RabbitMQ Server不会再发送数据给它，因为Server认为这个Consumer处理能力有限。

而且ack的机制可以起到限流的作用（Benefit to throttling）：在Consumer处理完成数据后发送ack，甚至在额外的延时后发送ack，将有效的balance Consumer的load。

当然对于实际的例子，比如我们可能会对某些数据进行merge，比如merge 4s内的数据，然后sleep 4s后再获取数据。特别是在监听系统的state，我们不希望所有的state实时的传递上去，而是希望有一定的延时。这样可以减少某些IO，而且终端用户也不会感觉到。

没有正确响应呢？

如果Consumer接收了一个消息就还没有发送ack就与RabbitMQ断开了，RabbitMQ会认为这条消息没有投递成功会重新投递到别的Consumer。

如果Consumer本身逻辑有问题没有发送ack的处理，RabbitMQ不会再向该Consumer发送消息。RabbitMQ会认为这个Consumer还没有处理完上一条消息，没有能力继续接收新消息。

我们可以善加利用这一机制，如果需要处理过程是相当复杂的，应用程序可以延迟发送ack直到处理完成为止。这可以有效控制应用程序这边的负载，不致于被大量消息冲击。

### 消息拒绝

由于要拒绝消息，所以ack响应消息还没有发出，这里拒绝消息可以有两种选择:

Consumer直接断开RabbitMQ这样RabbitMQ将把这条消息重新排队，交由其它Consumer处理。这个方法在RabbitMQ各版本都支持，这样做的坏处就是连接断开增加了RabbitMQ的额外负担，特别是consumer出现异常每条消息都无法正常处理的时候。

RabbitMQ 2.0.0可以使用 basic.reject 命令，收到该命令RabbitMQ会重新投递到其它的Consumer。如果设置requeue为false，RabbitMQ会直接将消息从queue中移除。

其实还有一种选择就是直接忽略这条消息并发送ACK，当你明确知道这条消息是异常的不会有Consumer能处理，可以这样做抛弃异常数据。

为什么要发送basic.reject消息而不是ACK？RabbitMQ后面的版本可能会引入”dead letter”队列，如果想利用dead letter做点文章就使用basic.reject并设置requeue为false。

### 消息持久化

RabbitMQ支持消息的持久化，也就是数据写在磁盘上，为了数据安全考虑，大多数用户都会选择持久化。消息队列持久化包括3个部分：

1. Exchange持久化，在声明时指定durable => 1

2. Queue持久化，在声明时指定durable => 1

3. 消息持久化，在投递时指定delivery_mode => 2（1是非持久化）

若Exchange和Queue都是持久化的，那么它们之间的Binding也是持久化的；而Exchange和Queue两者之间有一个持久化，一个非持久化，就不允许建立绑定。

Consumer从durable queue中取回一条消息之后并发回了ack消息，RabbitMQ就会将其标记，方便后续垃圾回收。如果一条持久化的消息没有被consumer取走，RabbitMQ重启之后会自动重建exchange和queue(以及bingding关系)，消息通过持久化日志重建再次进入对应的queues，exchanges。

## RabbitMQ集群

由于RabbitMQ是用erlang开发的，RabbitMQ完全依赖erlang的Cluster，因为erlang天生就是一门分布式语言，集群非常方便，但其本身并不支持负载均衡。Erlang的集群中各节点是经由过程一个magic cookie来实现的，这个cookie存放在 $home/.erlang.cookie中(像我的root用户安装的就是放在我的root/.erlang.cookie中)，文件是400的权限。所以必须保证各节点cookie内容一致，不然节点之间就无法通信。

### 集群方式

Rabbitmq集群大概分为二种方式：

1. 普通模式：默认的集群模式。

对于Queue来说，消息实体只存在于其中一个节点，A、B两个节点仅有相同的元数据，即队列结构，但队列的元数据仅保存有一份，即创建该队列的rabbitmq节点（A节点），当A节点宕机，你可以去其B节点查看，./rabbitmqctl list_queues 发现该队列已经丢失，但声明的exchange还存在。

当消息进入A节点的Queue中后，consumer从B节点拉取时，RabbitMQ会临时在A、B间进行消息传输，把A中的消息实体取出并经过B发送给consumer，所以consumer应平均连接每一个节点，从中取消息。

该模式存在一个问题就是当A节点故障后，B节点无法取到A节点中还未消费的消息实体。如果做了队列持久化或消息持久化，那么得等A节点恢复，然后才可被消费，并且在A节点恢复之前其它节点不能再创建A节点已经创建过的持久队列；如果没有持久化的话，消息就会失丢。

这种模式更适合非持久化队列，只有该队列是非持久的，客户端才能重新连接到集群里的其他节点，并重新创建队列。假如该队列是持久化的，那么唯一办法是将故障节点恢复起来。

2. 镜像模式：把需要的队列做成镜像队列，存在于多个节点。

该模式解决了普通模式的问题，其实质不同之处在于，消息实体会主动在镜像节点间同步，而不是在consumer取数据时临时拉取。

该模式带来的副作用也很明显，除了降低系统性能外，如果镜像队列数量过多，加之大量的消息进入，集群内部的网络带宽将会被这种同步通讯大大消耗掉。

所以在对可靠性要求较高的场合中适用，一个队列想做成镜像队列，需要先设置policy，然后客户端创建队列的时候，rabbitmq集群根据“队列名称”自动设置是普通集群模式或镜像队列。具体如下：

队列通过策略来使能镜像。策略能在任何时刻改变，rabbitmq队列也近可能的将队列随着策略变化而变化；非镜像队列和镜像队列之间是有区别的，前者缺乏额外的镜像基础设施，没有任何slave，因此会运行得更快。

为了使队列称为镜像队列，你将会创建一个策略来匹配队列，设置策略有两个键“ha-mode和 ha-params（可选）”。ha-params根据ha-mode设置不同的值，下面表格说明这些key的选项。

![img](http://www.uml.org.cn/zjjs/images/2018052348.png)

为什么RabbitMQ不将队列复制到集群里每个节点呢？这与它的集群的设计本意相冲突，集群的设计目的就是增加更多节点时，能线性的增加性能（CPU、内存）和容量（内存、磁盘）。理由如下：

Storage Space: If every cluster node had a full copy of every queue, adding nodes wouldn’t give you more storage capacity. For example, if one node could store 1GB of messages, adding two more nodes would simply give you two more copies of the same 1GB of messages.（存储空间：如果每个集群节点每个队列的一个完整副本，增加节点需要更多的存储容量。例如，如果一个节点可以存储1 gb的消息，添加两个节点需要两份相同的1gb的消息）

Performance: Publishing messages would require replicating those messages to every cluster node. For durable messages that would require triggering disk activity on all nodes for every message. Your network and disk load would increase every time you added a node, keeping the performance of the cluster the same (or possibly worse).（性能：发布消息需要将这些信息复制到每个集群节点。对持久消息，要求为每条消息触发磁盘活动在所有节点上。每次添加一个节点都会带来 网络和磁盘的负载。）

当然RabbitMQ新版本集群也支持队列复制（有个选项可以配置）。比如在有五个节点的集群里，可以指定某个队列的内容在2个节点上进行存储，从而在性能与高可用性之间取得一个平衡（应该就是指镜像模式）。

### 集群节点

RabbitMQ的集群节点包括内存节点、磁盘节点。顾名思义内存节点就是将所有数据放在内存，磁盘节点将数据放在磁盘。不过，如果在投递消息时，打开了消息的持久化，那么即使是内存节点，数据还是安全的放在磁盘。

一个rabbitmq集 群中可以共享 user，vhost，queue，exchange等，所有的数据和状态都是必须在所有节点上复制的，一个例外是，那些当前只属于创建它的节点的消息队列，尽管它们可见且可被所有节点读取。rabbitmq节点可以动态的加入到集群中，一个节点它可以加入到集群中，也可以从集群环集群会进行一个基本的负载均衡。

集群中有两种节点：

1. 内存节点：只保存状态到内存（一个例外的情况是：持久的queue的持久内容将被保存到disk）

2. 磁盘节点：保存状态到内存和磁盘。

内存节点虽然不写入磁盘，但是它执行比磁盘节点要好。集群中，只需要一个磁盘节点来保存状态 就足够了如果集群中只有内存节点，那么不能停止它们，否则所有的状态，消息等都会丢失。