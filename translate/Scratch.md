## 驱逐

冷酷的现实是，我们几乎*肯定*没有足够的内存来缓存我们可以缓存的所有内容。您必须决定：什么时候不值得保留缓存条目？Guava 提供三种基本的驱逐类型：基于大小的驱逐，基于时间的驱逐和基于引用的驱逐。

### 基于大小的驱逐

如果你的缓存在达到某个大小之后就不应该继续增长，可以使用 [`CacheBuilder.maximumSize(long)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#maximumSize-long-)。缓存将会尝试驱逐最近最少使用的缓存数据实体。*警告*：缓存可能会在大小达到限制之前驱逐实体——通常是在缓存大小接近限制时。

另外，如果不同的缓存实体具有不同的“权重”——比如，如果你的缓存值具有不同的内存空间占用——你可以使用 [`CacheBuilder.weigher(Weigher)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#weigher-com.google.common.cache.Weigher-) 指定权重函数，同时使用 [`CacheBuilder.maximumWeight(long)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#maximumWeight-long-) 指定最大缓存权重。除了需要与 `maximumSize` 相同的限制外，请注意，权重是在条目创建时计算的，此后是静态的。

```java
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .maximumWeight(100000)
       .weigher(new Weigher<Key, Graph>() {
          public int weigh(Key k, Graph g) {
            return g.vertices().size();
          }
        })
       .build(
           new CacheLoader<Key, Graph>() {
             public Graph load(Key key) { // no checked exception
               return createExpensiveGraph(key);
             }
           });
```

### 基于时间的驱逐

`CacheBuilder` 提供了两种基于时间的驱逐方法：

- [`expireAfterAccess(long, TimeUnit)`](https://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#expireAfterAccess-long-java.util.concurrent.TimeUnit-) Only expire entries after the specified duration has passed since the entry was last accessed by a read or a write. Note that the order in which entries are evicted will be similar to that of [size-based eviction](https://github.com/google/guava/wiki/CachesExplained#Size-based-Eviction).
- [`expireAfterWrite(long, TimeUnit)`](https://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#expireAfterWrite-long-java.util.concurrent.TimeUnit-) Expire entries after the specified duration has passed since the entry was created, or the most recent replacement of the value. This could be desirable if cached data grows stale after a certain amount of time.

Timed expiration is performed with periodic maintenance during writes and occasionally during reads, as discussed below.

#### Testing Timed Eviction

Testing timed eviction doesn't have to be painful...and doesn't actually have to take you two seconds to test a two-second expiration. Use the [Ticker](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Ticker.html) interface and the [`CacheBuilder.ticker(Ticker)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#ticker-com.google.common.base.Ticker-) method to specify a time source in your cache builder, rather than having to wait for the system clock.