## Population

The first question to ask yourself about your cache is: is there some *sensible default* function to load or compute a value associated with a key? If so, you should use a `CacheLoader`. If not, or if you need to override the default, but you still want atomic "get-if-absent-compute" semantics, you should pass a `Callable` into a `get` call. Elements can be inserted directly, using `Cache.put`, but automatic cache loading is preferred as it makes it easier to reason about consistency across all cached content.

#### From a CacheLoader

A `LoadingCache` is a `Cache` built with an attached [`CacheLoader`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheLoader.html). Creating a `CacheLoader` is typically as easy as implementing the method `V load(K key) throws Exception`. So, for example, you could create a `LoadingCache` with the following code:

```
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

The canonical way to query a `LoadingCache` is with the method [`get(K)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/LoadingCache.html#get-K-). This will either return an already cached value, or else use the cache's `CacheLoader` to atomically load a new value into the cache. Because `CacheLoader` might throw an `Exception`, `LoadingCache.get(K)` throws `ExecutionException`. (If the cache loader throws an *unchecked* exception, `get(K)` will throw an `UncheckedExecutionException` wrapping it.) You can also choose to use `getUnchecked(K)`, which wraps all exceptions in `UncheckedExecutionException`, but this may lead to surprising behavior if the underlying `CacheLoader` would normally throw checked exceptions.

```
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

Bulk lookups can be performed with the method `getAll(Iterable<? extends K>)`. By default, `getAll` will issue a a separate call to `CacheLoader.load` for each key which is absent from the cache. When bulk retrieval is more efficient than many individual lookups, you can override [`CacheLoader.loadAll`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheLoader.html#loadAll-java.lang.Iterable-) to exploit this. The performance of `getAll(Iterable)` will improve accordingly.

Note that you can write a `CacheLoader.loadAll` implementation that loads values for keys that were not specifically requested. For example, if computing the value of any key from some group gives you the value for all keys in the group, `loadAll` might load the rest of the group at the same time.

#### From a Callable

All Guava caches, loading or not, support the method [`get(K, Callable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#get-java.lang.Object-java.util.concurrent.Callable-). This method returns the value associated with the key in the cache, or computes it from the specified `Callable` and adds it to the cache. No observable state associated with this cache is modified until loading completes. This method provides a simple substitute for the conventional "if cached, return; otherwise create, cache and return" pattern.

```
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

#### Inserted Directly

Values may be inserted into the cache directly with [`cache.put(key, value)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#put-K-V-). This overwrites any previous entry in the cache for the specified key. Changes can also be made to a cache using any of the `ConcurrentMap` methods exposed by the `Cache.asMap()` view. Note that no method on the `asMap` view will ever cause entries to be automatically loaded into the cache. Further, the atomic operations on that view operate outside the scope of automatic cache loading, so `Cache.get(K, Callable<V>)` should always be preferred over `Cache.asMap().putIfAbsent` in caches which load values using either `CacheLoader` or `Callable`.