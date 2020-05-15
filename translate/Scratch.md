## Features

### Statistics

By using [`CacheBuilder.recordStats()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/cache/CacheBuilder.html#recordStats--), you can turn on statistics collection for Guava caches. The [`Cache.stats()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#stats--) method returns a [`CacheStats`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheStats.html) object, which provides statistics such as

- [`hitRate()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheStats.html#hitRate--), which returns the ratio of hits to requests
- [`averageLoadPenalty()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheStats.html#averageLoadPenalty--), the average time spent loading new values, in nanoseconds
- [`evictionCount()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheStats.html#evictionCount--), the number of cache evictions

and many more statistics besides. These statistics are critical in cache tuning, and we advise keeping an eye on these statistics in performance-critical applications.

### `asMap`

You can view any `Cache` as a `ConcurrentMap` using its `asMap` view, but how the `asMap` view interacts with the `Cache` requires some explanation.

- `cache.asMap()` contains all entries that are *currently loaded* in the cache. So, for example, `cache.asMap().keySet()` contains all the currently loaded keys.
- `asMap().get(key)` is essentially equivalent to `cache.getIfPresent(key)`, and never causes values to be loaded. This is consistent with the `Map` contract.
- Access time is reset by all cache read and write operations (including `Cache.asMap().get(Object)` and `Cache.asMap().put(K, V)`), but not by `containsKey(Object)`, nor by operations on the collection-views of `Cache.asMap()`. So, for example, iterating through `cache.asMap().entrySet()` does not reset access time for the entries you retrieve.

## Interruption

Loading methods (like `get`) never throw `InterruptedException`. We could have designed these methods to support `InterruptedException`, but our support would have been incomplete, forcing its costs on all users but its benefits on only some. For details, read on.

`get` calls that request uncached values fall into two broad categories: those that load the value and those that await another thread's in-progress load. The two differ in our ability to support interruption. The easy case is waiting for another thread's in-progress load: Here we could enter an interruptible wait. The hard case is loading the value ourselves. Here we're at the mercy of the user-supplied `CacheLoader`. If it happens to support interruption, we can support interruption; if not, we can't.

So why not support interruption when the supplied `CacheLoader` does? In a sense, we do (but see below): If the `CacheLoader` throws `InterruptedException`, all `get` calls for the key will return promptly (just as with any other exception). Plus, `get` will restore the interrupt bit in the loading thread. The surprising part is that the `InterruptedException` is wrapped in an `ExecutionException`.

In principle, we could unwrap this exception for you. However, this forces all `LoadingCache` users to handle `InterruptedException`, even though the majority of `CacheLoader` implementations never throw it. Maybe that's still worthwhile when you consider that all *non-loading* threads' waits could still be interrupted. But many caches are used only in a single thread. Their users must still catch the impossible `InterruptedException`. And even those users who share their caches across threads will be able to interrupt their `get` calls only *sometimes*, based on which thread happens to make a request first.

Our guiding principle in this decision is for the cache to behave as though all values are loaded in the calling thread. This principle makes it easy to introduce caching into code that previously recomputed its values on each call. And if the old code wasn't interruptible, then it's probably OK for the new code not to be, either.

I said that we support interruption "in a sense." There's another sense in which we don't, making `LoadingCache` a leaky abstraction. If the loading thread is interrupted, we treat this much like any other exception. That's fine in many cases, but it's not the right thing when multiple `get` calls are waiting for the value. Although the operation that happened to be computing the value was interrupted, the other operations that need the value might not have been. Yet all of these callers receive the `InterruptedException` (wrapped in an `ExecutionException`), even though the load didn't so much "fail" as "abort." The right behavior would be for one of the remaining threads to retry the load. We have [a bug filed for this](https://github.com/google/guava/issues/1122). However, a fix could be risky. Instead of fixing the problem, we may put additional effort into a proposed `AsyncLoadingCache`, which would return `Future` objects with correct interruption behavior.