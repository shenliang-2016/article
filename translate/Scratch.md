# 缓存

## 示例

```java
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .maximumSize(1000)
       .expireAfterWrite(10, TimeUnit.MINUTES)
       .removalListener(MY_LISTENER)
       .build(
           new CacheLoader<Key, Graph>() {
             @Override
             public Graph load(Key key) throws AnyException {
               return createExpensiveGraph(key);
             }
           });
```

## 适用性

缓存有非常广泛的应用场景。比如，你应该为那些计算或者查询代价高昂的数据使用缓存，或者你需要某个输入数据很多次的场景。

一个 `Cache` 类似于 `ConcurrentMap`，不过并不完全相同。基本的差异在于， `ConcurrentMap` 持久化所有添加进来的元素直到它们被显式删除。另一方面，通常将 `Cache` 配置为自动淘汰条目，以限制其内存占用量。在某些情况下， `LoadingCache` 会很有用，虽然它不淘汰条目，但是可以自动加载缓存。

通常，Guava 缓存工具可以适用与下列场景：

- 你希望使用一些内存空间来改善速度。
- 您希望多次查询某些键。
- 您的缓存将不需要存储超出 RAM 容量的数据。（Guava 缓存的作用范围局限于在应用程序的一次运行中。它们不将数据存储在文件中或外部服务器上。如果这不符合您的需求，请考虑使用 [Memcached](http://memcached.org/)。）

如果这些都适用于您的应用场景，那么 Guava 缓存实用程序将很适合您！

如上面的示例代码所示，使用 `CacheBuilder` 生成器模式可以获取 `Cache`，但是自定义缓存是有趣的部分。

*注意：* 如果不需要 `Cache` 的功能，则 `ConcurrentHashMap` 的内存使用效率更高——但是很难用任何旧的 `ConcurrentMap`来复制大多数 `Cache` 的功能。

