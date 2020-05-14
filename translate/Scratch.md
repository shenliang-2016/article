## 填充

你需要问自己有关缓存的第一个问题是：是否有一些*合理的默认*函数来加载或计算与键关联的值？如果是这样，您应该使用 `CacheLoader`。如果不是这样，或者如果您需要覆盖默认值，但是仍然需要原子的 "get-if-absent-compute" 语义，则应该将 `Callable` 传递给 `get` 调用。可以使用 `Cache.put` 直接插入元素，但是首选自动加载缓存，因为这样可以更轻松地推断所有缓存内容的一致性。

#### 使用 CacheLoader

 `LoadingCache` 是一个通过附属的 [`CacheLoader`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheLoader.html) 构建的 `Cache`。创建一个 `CacheLoader` 通常与实现 `V load(K key) throws Exception` 方法一样。因此，比如，你可以使用下面的代码创建一个 `LoadingCache` ：

```java
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .maximumSize(1000)
       .build(
           new CacheLoader<Key, Graph>() {
             public Graph load(Key key) throws AnyException {
               return createExpensiveGraph(key);
             }
           });

...
try {
  return graphs.get(key);
} catch (ExecutionException e) {
  throw new OtherException(e.getCause());
}
```

查询 `LoadingCache` 的规范方法是使用 [`get(K)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/LoadingCache.html#get-K-) 方法。这将返回一个已经缓存的值，或者使用缓存的 `CacheLoader` 原子地将新值加载到缓存中。由于 `CacheLoader` 可能会抛出 `Exception`，因此 `LoadingCache.get(K)` 会抛出 `ExecutionException`。（如果缓存加载器抛出 *unchecked* 异常，则`get(K)` 会引发包装了 `UncheckedExecutionException` 的异常。）您还可以选择使用 `getUnchecked(K)` 将所有异常包装在 `UncheckedExecutionException` 中， 但是如果底层的 `CacheLoader` 通常会抛出受检查异常，这可能会导致令人惊讶的行为。

```java
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .expireAfterAccess(10, TimeUnit.MINUTES)
       .build(
           new CacheLoader<Key, Graph>() {
             public Graph load(Key key) { // no checked exception
               return createExpensiveGraph(key);
             }
           });

...
return graphs.getUnchecked(key);
```

可以使用 `getAll(Iterable<? extends K>)` 方法执行批量查找。默认情况下，`getAll` 将为缓存中不存在的每个键单独发出 `CacheLoader.load` 调用。如果批量检索比许多单个查询更有效，则可以覆盖 [`CacheLoader.loadAll`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheLoader.html#loadAll-java.lang.Iterable-) 来利用这一点。 `getAll(Iterable)` 的性能将相应提高。

请注意，您可以编写一个 `CacheLoader.loadAll` 实现，该实现加载未明确要求的键的值。例如，如果计算某个组中任何键的值给您该组中所有键的值，则 `loadAll` 可能会同时加载其余组。

#### 使用 Callable

所有 Guava 缓存（无论是否加载）均支持方法 [`get(K, Callable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#get-java.lang.Object-java.util.concurrent.Callable-) 。此方法返回与缓存中的键关联的值，或从指定的 `Callable` 中计算出该值并将其添加到缓存中。在加载完成之前，不会修改与此缓存关联的可观察状态。此方法为常规的“如果已缓存，则返回；否则创建，缓存并返回”模式提供了简单的替代方法。

```java
Cache<Key, Value> cache = CacheBuilder.newBuilder()
    .maximumSize(1000)
    .build(); // look Ma, no CacheLoader
...
try {
  // If the key wasn't in the "easy to compute" group, we need to
  // do things the hard way.
  cache.get(key, new Callable<Value>() {
    @Override
    public Value call() throws AnyException {
      return doThingsTheHardWay(key);
    }
  });
} catch (ExecutionException e) {
  throw new OtherException(e.getCause());
}
```

#### 直接插入

可以直接使用 [`cache.put(key, value)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#put-K-V-) 。这将覆盖高速缓存中指定键的任何先前条目。也可以使用  `Cache.asMap()` 视图公开的任何 `ConcurrentMap` 方法对缓存进行更改。注意，`asMap` 视图上的任何方法都不会导致条目自动加载到缓存中。此外，该视图上的原子操作在自动缓存加载范围之外运行，因此在使用 `CacheLoader` 或 `Callable` 加载值的缓存中，始终应优先选择 `Cache.get(K, Callable<V>)` 而不是 `Cache.asMap().putIfAbsent` 。