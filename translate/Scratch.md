## 特性

### 统计

通过使用 [`CacheBuilder.recordStats()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/cache/CacheBuilder.html#recordStats--)，你可以为 Guava 缓存打开统计量收集。 [`Cache.stats()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#stats--) 方法返回 [`CacheStats`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheStats.html) 对象，提供诸如如下统计量：

- [`hitRate()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheStats.html#hitRate--)，返回请求的命中率
- [`averageLoadPenalty()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheStats.html#averageLoadPenalty--)，加载新值的平均耗时，单位纳秒
- [`evictionCount()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheStats.html#evictionCount--)，缓存驱逐的数量

以及很多其他统计量。这些统计量都是缓存调优的关键指标，建议为关键性能应用保持对这些统计量的监控。

### `asMap`

你可以使用其 `asMap` 视图将任何 `Cache` 视作 `ConcurrentMap` ，但是 `asMap` 视图与 `Cache` 之间的交互细节还需要一些解释：

- `cache.asMap()` 包含目前已经被加载到缓存中的所有实体。比如， `cache.asMap().keySet()` 包含所有目前已加载的键。
- `asMap().get(key)` 基本上等价于 `cache.getIfPresent(key)`，同时不会导致值被加载。这一点遵循了 `Map` 契约。
- 访问时间由所有缓存读写操作（包括 `Cache.asMap().get(Object)`  和 `Cache.asMap().put(K, V)` ）重置，但不会被 `containsKey(Object)` 重置，也不会被对 `Cache.asMap()` 的集合视图进行操作重置。因此，例如，通过 `cache.asMap().entrySet()` 进行迭代不会重置您检索到的条目的访问时间。

## 中断

加载方法（如 `get`）永远不会抛出 `InterruptedException`。我们本来可以设计这些方法来支持 `InterruptedException`，但是我们的支持将是不完整的，迫使所有用户付出代价，但只有部分受益。有关详细信息，请继续阅读。

请求未缓存值的 `get` 调用分为两大类：那些加载值的调用和等待正在进行的另一个线程加载的调用。两者在支持中断的能力上有所不同。最简单的情况是等待另一个线程的正在进行的加载：在这里我们可以输入一个可中断的等待。困难的情况是我们自己加载值。在这里，我们受用户提供的 `CacheLoader` 的支配。如果碰巧支持中断，我们可以支持中断；如果没有，我们就不能。

那么，为什么在提供的 `CacheLoader` 支持时不支持中断呢？从某种意义上讲，我们可以这样做（但请参见下文）：如果 `CacheLoader` 抛出 `InterruptedException`，则对键的所有 `get` 调用将立即返回（与其他异常一样）。另外，`get` 将恢复加载线程中的中断位。令人惊讶的部分是，`InterruptedException` 被包装在 `ExecutionException` 中。

原则上，我们可以为您解开此异常。然而，这迫使所有的 `LoadingCache` 用户都必须处理 `InterruptedException`，即使大多数的 `CacheLoader` 实现从未抛出它。当您考虑所有 *non-loading* 线程的等待仍可能被中断时，也许这仍然值得。但是许多缓存仅在单个线程中使用，他们的用户仍必须捕获不可能的 `InterruptedException`。而且，即使是那些在线程间共享缓存的用户，也可以 *有时* 中断 `get` 调用，这取决于哪个线程首先发出请求。

在此决策中，我们的指导原则是使缓存的行为就像所有值都已加载到调用线程中一样。通过此原理，可以轻松地将缓存引入到先前在每次调用时重新计算其值的代码中。而且，如果旧代码不可中断，那么也可以不要新代码。

我说过，我们在某种意义上支持中断。换个角度讲，那就是使 `LoadingCache` 成为泄漏的抽象。如果加载线程被中断，我们将其与其他任何异常一样对待。在许多情况下都可以，但是当多个 `get` 调用正在等待该值时，这不是正确的选择。尽管恰好正在计算该值的操作被中断，但其他需要该值的操作可能并未中断。然而，所有这些调用者都接收到 `InterruptedException`（被包装在 `ExecutionException` 中），即使加载没有“失败”也没有“中止”。正确的行为是让其余线程之一重试加载。我们有 [为此提交的错误](https://github.com/google/guava/issues/1122) 。但是，修复可能会有风险。除了解决问题外，我们还可能在拟议的 `AsyncLoadingCache` 中投入更多的精力，它将返回具有正确中断行为的 `Future` 对象。

