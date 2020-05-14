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

- [`expireAfterAccess(long, TimeUnit)`](https://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#expireAfterAccess-long-java.util.concurrent.TimeUnit-) 仅在自从上次通过读取或写入访问条目以来经过指定的持续时间后，条目才到期。请注意，驱逐条目的顺序将类似于 [基于大小的驱逐](https://github.com/google/guava/wiki/CachesExplained#Size-based-Eviction)。
- [`expireAfterWrite(long, TimeUnit)`](https://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#expireAfterWrite-long-java.util.concurrent.TimeUnit-) 自创建条目以来经过指定的时间或该值的最新替换之后，使条目过期。如果经过一定时间后缓存的数据持续增长，则可能需要这样做。

定时到期是在写入过程中进行定期维护的，偶尔在读取过程中进行维护，如下所述。

#### 测试定时驱逐

测试定时驱逐并不一定会很痛苦...实际上也不需要花两秒钟来测试两秒钟的到期时间。使用 [Ticker](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Ticker.html) 接口和 [`CacheBuilder.ticker(Ticker)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#ticker-com.google.common.base.Ticker-) 方法来指定缓存构建器中的时间源，而不必等待系统时钟。

