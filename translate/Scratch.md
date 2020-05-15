### 刷新

刷新与驱逐并不完全相同。如  [`LoadingCache.refresh(K)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/LoadingCache.html#refresh-K-) 所述，刷新键可能会异步加载该键的新值。与驱逐相反，旧键（如果有的话）在刷新键时仍会返回，这迫使检索要等到重新加载该值。

如果刷新时引发异常，则将保留旧值，并记录并吞下该异常。

`CacheLoader` 可以通过覆盖  [`CacheLoader.reload(K, V)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheLoader.html#reload-K-V-) 指定某些将要在刷新时执行的聪明的行为，它允许您在计算新值时使用旧值。

```java
// Some keys don't need refreshing, and we want refreshes to be done asynchronously.
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .maximumSize(1000)
       .refreshAfterWrite(1, TimeUnit.MINUTES)
       .build(
           new CacheLoader<Key, Graph>() {
             public Graph load(Key key) { // no checked exception
               return getGraphFromDatabase(key);
             }

             public ListenableFuture<Graph> reload(final Key key, Graph prevGraph) {
               if (neverNeedsRefresh(key)) {
                 return Futures.immediateFuture(prevGraph);
               } else {
                 // asynchronous!
                 ListenableFutureTask<Graph> task = ListenableFutureTask.create(new Callable<Graph>() {
                   public Graph call() {
                     return getGraphFromDatabase(key);
                   }
                 });
                 executor.execute(task);
                 return task;
               }
             }
           });
```

可以使用  [`CacheBuilder.refreshAfterWrite(long, TimeUnit)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#refreshAfterWrite-long-java.util.concurrent.TimeUnit-) 将自动定时刷新添加到缓存中。与 `expireAfterWrite` 相比，`refreshAfterWrite` 在指定的持续时间后将使键“具有资格”进行刷新，但实际上仅在查询条目时才会启动刷新。（如果将 `CacheLoader.reload` 实现为异步，则刷新不会降低查询的速度。）因此，例如，您可以在同一缓存上同时指定 `refreshAfterWrite` 和 `expireAfterWrite`，以便只要条目符合刷新资格，就不会盲目地重置条目的过期计时器，因此，如果在符合刷新资格后不查询条目，则允许它过期。