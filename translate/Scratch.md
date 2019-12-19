## 8. 缓存抽象

从 3.1 版开始，Spring 框架提供了对将缓存透明添加到现有 Spring 应用程序的支持。与 [transaction](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction) 支持类似，缓存抽象允许各种对现有代码影响最小的缓存解决方案的一致使用。

从 Spring 4.1 开始，通过 [JSR-107 注解](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-jsr-107) 的支持，缓存抽象得到了显着扩展。同时添加了更多自定义选项。

### 8.1. 理解缓存抽象

> 缓存 vs 缓冲
>
> 术语“缓冲”和“缓存”倾向于互换使用。但是请注意，它们代表不同的事物。传统上，缓冲区用作快速实体和慢速实体之间的数据的中间临时存储。由于一方必须等待另一方（这会影响性能），因此缓冲区允许一次移动整个数据块而不是小块数据来缓解这种情况。数据只能从缓冲区写入和读取一次。此外，缓冲区对于至少一个知道缓冲区的一方是可见的。
>
> 另一方面，根据定义，缓存是隐藏的，任何一方都不知道发生了缓存。它可以提高性能，但是也可以通过快速读取多次相同数据来实现。
>
> 您可以在 [此处](https://en.wikipedia.org/wiki/Cache_(computing)#The_difference_between_buffer_and_cache) 中找到有关缓冲区和缓存之间差异的进一步说明。

缓存抽象的核心是将缓存应用于 Java 方法，从而根据缓存中可用的信息减少执行次数。也就是说，每次调用目标方法时，抽象都会应用缓存行为，该行为检查给定参数是否已经执行了该方法。如果已执行，则返回缓存的结果，而不必执行实际的方法。如果尚未执行该方法，则将执行该方法，并将结果缓存并返回给用户，以便下次调用该方法时，将返回缓存的结果。这样，对于给定的一组参数，成本高昂的方法（无论是受 CPU 限制还是与 IO 绑定）只能执行一次，结果可以重复使用，而不必再次实际执行该方法。缓存逻辑是对应用透明的，不会对调用方造成任何干扰。

> 该方法仅适用于保证无论给定输入（或参数）执行多少次都返回相同输出（结果）的方法。

缓存抽象提供了其他与缓存相关的操作，例如更新缓存内容或删除一个或所有条目的能力。如果高速缓存处理在应用程序过程中可能更改的数据，则这些功能很有用。

与 Spring 框架中的其他服务一样，缓存服务是一种抽象（不是缓存实现），并且需要使用实际的存储来存储缓存数据。也就是说，抽象使您不必编写缓存逻辑，但是没有提供实际的数据存储。这种抽象是通过 `org.springframework.cache.Cache和org.springframework.cache.CacheManager` 接口实现的。

Spring提供了该抽象的 [一些实现](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-store-configuration) ：基于 JDK ` java.util.concurrent.ConcurrentMap` 的缓存，[Ehcache 2.x](https://www.ehcache.org/)，Gemfire 缓存，[Caffeine](https://github.com/ben-manes/caffeine/wiki) 和符合 JSR-107 的缓存（例如 Ehcache 3.x）。有关更多信息，请参见 [插入不同的后端缓存](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-plug) 插入其他缓存存储区和提供程序。

> 对于多线程和多进程环境，缓存抽象没有特殊处理，因为此类功能由缓存实现处理。

如果您具有多进程环境（即，一个应用程序部署在多个节点上），则需要相应地配置缓存提供程序。根据您的应用场景，在几个节点上复制相同数据就足够了。但是，如果在应用程序过程中更改数据，则可能需要启用其他传播机制。

高速缓存特定数据项等同于通过程序化高速缓存交互找到该数据项的典型的“如果找不到，然后继续处理并放入”代码块。没有应用锁，几个线程可能会尝试同时加载同一数据项。缓存淘汰同样如此。如果多个线程试图同时更新或逐出数据，则可以使用陈旧数据。某些缓存提供程序在该区域提供高级功能。有关更多详细信息，请参见缓存提供程序的文档。

为了使用缓存抽象，你需要注意两个方面：

- 缓存声明：确定需要缓存的方法及其策略。
- 缓存配置：数据存储和读取的后备缓存。

