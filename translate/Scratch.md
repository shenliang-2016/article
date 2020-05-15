### 基于引用的驱逐

Guava 允许你设置你的缓存以允许数据实体的垃圾收集，通过对键或者值使用的 [weak references](http://docs.oracle.com/javase/6/docs/api/java/lang/ref/WeakReference.html) ，或者对值使用的 [soft references](http://docs.oracle.com/javase/6/docs/api/java/lang/ref/SoftReference.html) 进行设置。

- [`CacheBuilder.weakKeys()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#weakKeys--) 使用弱引用存储键。这允许实体在没有其他引用（强引用或者软引用）指向其键时被垃圾收集。由于垃圾收集基于 id 相等规则，这就导致整个缓存多需要使用 id （`==`）相等来比较键，而不是使用 `equals()`。
- [`CacheBuilder.weakValues()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#weakValues--) 使用弱引用存储值。这允许实体在没有其他引用（强引用或者软引用）指向其值时被垃圾收集。由于垃圾收集基于 id 相等规则，这就导致整个缓存多需要使用 id （`==`）相等来比较值，而不是使用 `equals()`。
- [`CacheBuilder.softValues()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#softValues--) 将值包装进入软引用。软引用对象以全局最近最少使用规则进行垃圾收集，以响应内存需求。由于使用软引用可能会有些性能问题，我们通常推荐使用更加容易预测的 [maximum cache size](https://github.com/google/guava/wiki/CachesExplained#Size-based-Eviction) 替代。使用 `softValues()` 将导致值被通过 id (`==`) 相等比较，而不是使用 `equals()`。

