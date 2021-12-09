# 构建微服务之使用API网关

**原文链接:[\*Building Microservices: Using an API Gateway\*](https://link.jianshu.com?t=https://www.nginx.com/blog/building-microservices-using-an-api-gateway/?utm_source=introduction-to-microservices&utm_medium=blog&utm_campaign=Microservices)**

1. *[微服务介绍](https://www.jianshu.com/p/8d2cfa1fa633)*
2. *构建微服务之使用API网关(本文)*
3. *[构建微服务之:微服务架构中的进程间通信](https://www.jianshu.com/p/9c03081bc0d9)*
4. *[微服务中的服务发现](https://www.jianshu.com/p/1bf9a46efe7a)*
5. *[微服务之事件驱动的数据管理](https://www.jianshu.com/p/9a440c5ea1db)*
6. *[选择一种微服务部署策略](https://www.jianshu.com/p/31c2a5a8b764)*
7. *[重构单体应用到微服务](https://www.jianshu.com/p/29f4d788e3bb)*

对于设计、构建和部署微服务系列七篇文章的第一篇，我们介绍了微服务架构风格，讨论了微服务的优势和劣势，尽管微服务有些复杂，但仍然是构建复杂应用的一个明智选择，第二篇文章将讨论使用API网关构建微服务。

当我们选择把应用构建成一组微服务的时候，我们需要决定应用的客户端如何与这些微服务进行交互。传统单体应用中，往往只是一组（一般是replicated，负载均衡）的节点，而在微服务架构中，每个微服务都会暴露一组细粒度的节点。这篇文章中，我们将检验这种方式如何影响客户端与应用端的通信，并且提出使用API网关的方式来解决这个问题。

# 介绍

假设我们正在为一个商品应用开发一个原生移动客户端，我们应该提供一个产品明细页来展示指定产品的信息。
 正如下图所示，当我们在亚马逊的安卓移动应用中滚动产品明细页时，它将会呈现给我们：



![img](https:////upload-images.jianshu.io/upload_images/3912920-04d9729084dae96f.png?imageMogr2/auto-orient/strip|imageView2/2/w/640/format/webp)

尽管这是移动应用，产品明细页依然展示给我们很多信息，比如它不仅仅展示了产品的基本信息（比如名称、描述、价格等），还展示了：

- 购物车中的条目数
- 订单历史记录
- 用户点评
- 低库存预警
- 配送选项
- 各项推荐,包括购买本产品还经常一起购买了其它某产品，客户买了这个产品同时还买了其他某产品，购买该产品的用户还浏览了哪些产品
- 替代购买选项

当我们使用单体架构模式的时候，一个移动客户端可能通过发送单一的REST调用请求(GET api.company.com/productdetails/*productId*) 来获取展示的数据，负载均衡器会把该请求路由到多个相同应用实例的其中一台，应用继续查询不同的数据库表并返回请求数据给客户端。

对应的，在使用微服务架构模式的时候，需要在产品明细页展示的数据被多个微服务所拥有，下面是一些可能拥有需要展示数据在产品明细页的微服务：

- 购物车服务：购物车中的产品条目

- 订单服务：订单历史

- 目录服务：基本产品信息，比如名称、图片、价格等

- 点评服务：用户点评

- 库存服务：低库存预警

- 配送服务：配送选项、时限以及来自配送提供者API计算出的费用

- 推荐服务：建议购买项

  ![img](https:////upload-images.jianshu.io/upload_images/3912920-d2475b5d36a0f476.png?imageMogr2/auto-orient/strip|imageView2/2/w/484/format/webp)

  我们需要决定移动端如何访问这些服务，先看下面的选项：

# 客户端直接与微服务通信

理论上客户端可以直接与每一个微服务进行通信，每个微服务将会有一个公开的节点（**https://\*serviceName*.api.company.name**)），这个URL将会映射到负载均衡器，然后被分发到可用的实例上被处理，为了获取产品明细，移动客户端需要向上面列出的各个微服务发送请求。

非常不幸的是，这种方案有诸多挑战和限制，问题之一就是客户端与每个微服务暴露出的细粒度API之间的不匹配，本例子中的客户端需发送七个不同的请求，在一个更加复杂的应用中请求数可能更多，比如亚马逊在渲染产品页的时候可能要调用上百个服务来渲染页面，一个客户端可以在LAN中发送多个请求，但是在公网上就特别低效，那就不用提在移动设备上了，当然，这种方式也使得客户端异常的复杂。

客户端直接调用微服务的另一个问题是，一些服务可能使用对web并不友好的协议实现。一个服务可能使用Thrift二进制的RPC而另一个服务可能使用AMQP消息协议。这些协议都不是浏览器和防火墙友好的，最好是在应用内部被使用。防火墙之外呢，应用最好使用HTTP或者WebSocket。

这种方式另一个劣势是使得微服务重构变得困难，随着时间推移，我们可能需要重新划分、组织微服务，比如我们可能合并两个微服务，也可能把某微服务拆分为两个或多个，如果客户端直接与微服务交互的话，对这些微服务进行重构变得异常困难。

正是由于这些问题，采用客户端直接调用微服务的方式并不明智。

# 使用API网关

通常更好的方式是使用大家都熟知的API网关，API网关是提供系统唯一入口的一台服务器，它和面向对象设计模式中的门面类似：API网关封装了内部的系统架构并向每个客户端提供裁剪的API，它也可能负责诸如用户验证、监控、负载均衡、缓存、请求改造和管理以及静态内容响应等职责。

下图展示了API网关通常适应的架构：



![img](https:////upload-images.jianshu.io/upload_images/3912920-df6b13ad41a9ce3d.png?imageMogr2/auto-orient/strip|imageView2/2/w/484/format/webp)



API网关负责请求路由、组合以及协议转换。所有来自客户端的请求都先经过API网关，然后被路由分配到相应的微服务中，API网关通常调用多个微服务并聚合其结果来处理请求，它可以在HTTP或者WebSocket这些web友好协议与内部使用的web不友好协议间相互转换。

API网关可以为每个客户提供定制化的API，它通常为移动客户端暴露粗粒度的API，比如提供（**/productdetails?productid=\*xxx***）节点使得移动应用单一请求就能获取所有的产品明细。API网关调用产品信息、推荐、评分等服务，组合这些结果来处理客户端请求。

一个非常牛的例子就是Netflix API网关，Netflix 流服务在上百种包含电视、机顶盒、智能手机、游戏系统、平板电脑等设备上都可用。起初Netflix想为它们的流服务提供一种 [one‑size‑fits‑all](https://link.jianshu.com?t=http://www.programmableweb.com/news/why-rest-keeps-me-night/2012/05/15) API，然而，他们发现由于设备的不同划分以及独特需求，这样设计是不现实的。现在他们使用API网关通过运行设备相关的适配器代码为客户端提供裁剪的API，适配器通常为每个请求调用平均六到七个后台服务， Netflix API网关现在每天处理上亿请求。

# 使用API网关的优势与劣势

正如你所想，使用API网关有优势也有劣势。一个巨大优势就是它封装了应用的内部结构，而不是让客户端直接调用每个服务，客户端只需要简单的与网关交互即可，另外API网关为不同客户提供定制的API，并且减少了客户端和应用间的网络调用，这也大大简化了客户端代码实现。

API网关也有一些劣势，它本身是一个新的高可用的组件，需要被开发、部署和管理，同时API网关有可能成为开发的瓶颈。开发者为了暴露新的微服务节点必须更新API网关，把更新网关的流程做的尽量轻量级是很重要的，不然的话，开发者更新网关的时候就要被迫在线等待。尽管它有这些劣势，在实战中，应用使用API网关还是明智的选择！

# 实现一个API网关

现在我们讨论了API网关的动机和一些权衡，现在来考虑一些设计的问题吧：

## 性能与扩展性

只有少数类似Netflix的公司需要每天处理上亿的请求，然而，对大多数应用来讲，API网关的性能和扩展性通常也非常的重要。在一个支持异步非阻塞IO的平台上构建API网关是明智的选择，我们有多种技术可以用来实现可扩展的API网关。基于JVM你可以选择基于NIO的诸如Netty、Vertx、Spring Reactor或JBoss Undertow等框架，Node.js也是一个流行的选项，它是一个构建于Chrome JS引擎的平台，另一选择是使用NGINX Plus，它提供了成熟、可扩展、高性能的web服务器和反向代理，并可以方便的被部署、配置和编程， NGINX Plus 可以管理用户校验、权限控制、请求负载均衡、响应缓存以及应用级别的健康检查和监控。

## 使用响应式编程模型

API网关通过简单路由到相应后台服务来处理请求，通过调用多个后台服务并聚合结果来处理它。对于一些请求，比如产品明细请求，后端对应的服务是彼此独立的，为减少请求时间，API网关应该并行的处理这些请求。然而有时候，请求之间是有依赖关系的，API网关可能在路由请求到后台服务之前先去调用用户校验服务验证请求的合理性，类似的，在获取用户心愿单中的上的产品信息的时候，API网关必须先获取包含那些信息的用户档案再去获取每个产品的信息，另一个有趣的例子就是[Netflix Video Grid](https://link.jianshu.com?t=http://techblog.netflix.com/2013/02/rxjava-netflix-api.html)。

使用传统的异步回调方式来写API组合代码很快就会把你带进回调地狱。代码将会变得纠缠不清、难以理解也容易出错。更好的方式是使用响应式方法来写声明式风格的API网关代码，比如，响应式抽象包括Scala中的 [Future](https://link.jianshu.com?t=http://docs.scala-lang.org/overviews/core/futures.html) 、Java 8中的[CompletableFuture](https://link.jianshu.com?t=https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html) 以及JavaScript中的[Promise](https://link.jianshu.com?t=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) ，还有微软为.NET开发的[Reactive Extensions](https://link.jianshu.com?t=http://reactivex.io/) (also called Rx or ReactiveX)， Netflix为了API网关的使用为基于JVM规范创造了RxJava，当然还有为JavaScript创造的RxJS ，可以运行在浏览器和Node.js中。使用响应式风格将会使你写出更简单更高效的API网关代码。

## 服务调用

微服务架构的应用是采用进程间通信的分布式系统，存在两种进程间通讯的方式：一种是采用异步基于消息机制的通信，比如使用消息中介产品 JMS 或者AMQP，当然还有 Zeromq服务直接调用的无中介消息产品；另一种方式是使用HTTP或者Thrift这种同步机制进行通信，一个系统应该同时使用同步和异步风格，甚至为每种方式使用不同的实现，因此，API网关也必须支持这些不同的通信机制。

## 服务发现

API网关需要知道和它通信的每个服务的地址（IP地址和端口），在一个传统应用中，你可能硬编码，但在一个流行的，基于云的微服务应用中，这就是一个大问题了。基础架构服务，比如消息中介，通常有一个静态地址，我们可以在系统环境变量中之指定，然而，获取一个应用服务的地址就不是一件简单的事情了，应用服务拥有动态分配的地址，而且，一组服务实例可能因为自动扩展或升级而动态的变化，因此，API网关应该像系统中的其他服务客户端一样，需要服务发现机制：要么是[服务端发现](https://link.jianshu.com?t=http://microservices.io/patterns/server-side-discovery.html) 或者是 [客户端发现](https://link.jianshu.com?t=http://microservices.io/patterns/client-side-discovery.html)。稍后的文章将会详细介绍服务发现的问题，现在，我们有必要意识到，如果系统使用客户端服务发现的话，API网关应该能够查询服务注册 [Service Registry](https://link.jianshu.com?t=http://microservices.io/patterns/service-registry.html)，服务注册是所有服务实例登记其地址的数据库。

## 处理局部故障

实现API网关时需要强调的另一个问题是局部故障。这个问题在分布式系统中很常见，比如一个服务可能调用另一个响应很慢或者不可用的服务，API网关千万不要在等待已经挂掉服务响应的时候阻塞。当然，如何处理错误取决于具体的应用场景或者具体因为哪个服务挂掉：比如，如果产品明细场景中的推荐服务挂掉了，那么API网关还是应该返回其他的产品信息，保障产品对用户仍然可以使用，推荐列表可以返回空或者预先硬编码的Top 10商品，但是如果产品信息服务挂掉的话，API网关就要返回客户一个错误了。

API网关如果可能话也可以返回缓存的数据，比如，由于产品价格很少变化，API网关可以在价格服务不可用时使用缓存，数据可能是API网关自己缓存，也可能缓存在诸如Redis和Memcached这样的外部缓存中。通过返回默认值或者缓存值，API网关确保局部故障不会影响用户体验。

[Netflix Hystrix](https://link.jianshu.com?t=https://github.com/Netflix/Hystrix)在写调用远端服务代码时候是非常有用的，Hystrix 会标记超过特定阈值的调用为超时，它还实现了断路器模式来阻止更多请求继续调用没有响应的服务，如果一个服务的出错率超过了指定阈值，它会触发断路器，使得所有的请求快速失败一段时间，Hystrix也允许你定义请求失败时的fallback动作 ，比如读取缓存或者返回一个默认值。如果你使用JVM，那么希望你一定考虑使用Hystrix，如果你不使用JVM，那也要有类似的工具来帮助你。

# 总结

对大多数基于微服务的应用来讲，实现API网关是明智的，API网关就是一个应用的单一入口，它还负责路由请求、组合、协议转换等工作，它为每个应用的客户端提供定制化的API，它也可以通过返回默认值或缓存值来处理失败，下篇文章我们讨论服务间的通信问题。



作者：nonumber1989
链接：https://www.jianshu.com/p/9e90b2a5df7b
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。