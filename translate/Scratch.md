### 显式删除

任何时刻，你都可以显式废除缓存实体，而不需要等待实体被驱逐。可以通过以下方法：

- 单个废除，使用 [`Cache.invalidate(key)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#invalidate-java.lang.Object-)
- 批量废除，使用 [`Cache.invalidateAll(keys)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#invalidateAll-java.lang.Iterable-)
- 全部废除，使用 [`Cache.invalidateAll()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#invalidateAll--)

### 删除监听器

你可以为你的缓存指定删除监听器以在实体被删除时执行一些操作，通过 [`CacheBuilder.removalListener(RemovalListener)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#removalListener-com.google.common.cache.RemovalListener-)。 [`RemovalListener`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/RemovalListener.html) 传递了一个 [`RemovalNotification`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/RemovalNotification.html)，指定了 [`RemovalCause`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/RemovalCause.html)，键，和值。

注意， `RemovalListener` 抛出的所有异常都会被写入日志 (使用 `Logger`) 并被吞掉。

```java
CacheLoader<Key, DatabaseConnection> loader = new CacheLoader<Key, DatabaseConnection> () {
  public DatabaseConnection load(Key key) throws Exception {
    return openConnection(key);
  }
};
RemovalListener<Key, DatabaseConnection> removalListener = new RemovalListener<Key, DatabaseConnection>() {
  public void onRemoval(RemovalNotification<Key, DatabaseConnection> removal) {
    DatabaseConnection conn = removal.getValue();
    conn.close(); // tear down properly
  }
};

return CacheBuilder.newBuilder()
  .expireAfterWrite(2, TimeUnit.MINUTES)
  .removalListener(removalListener)
  .build(loader);
```

**警告**：默认情况下，删除侦听器操作是同步执行的，并且由于缓存维护通常是在常规缓存操作期间执行的，因此耗时的删除侦听器会降低正常的缓存功能！如果您有耗时的删除监听器，请使用 [`RemovalListeners.asynchronous(RemovalListener, Executor)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/RemovalListeners.html#asynchronous-com.google.common.cache.RemovalListener-java.util.concurrent.Executor-) 来装饰 `RemovalListener` 以进行异步操作。

