### 清理何时发生？

用 `CacheBuilder` 构建的缓存不会“自动”或在值过期后立即执行清除和逐出值，或类似的任何操作。取而代之的是，它在写操作期间或偶尔进行的读操作（如果很少进行写操作）中执行少量维护。

这样做的原因如下：如果我们要连续执行 `Cache` 维护，则需要创建一个线程，并且该线程的操作将与用户操作竞争共享锁。另外，某些环境限制了线程的创建，这会使 `CacheBuilder` 在该环境中无法使用。

相反，我们会将选择权交给您。如果您的缓存是高吞吐量的，那么您不必担心执行缓存维护以清理过期的条目等。 如果您的缓存确实很少写入，并且您不想清理来阻止缓存读取，则您可能希望创建自己的维护线程，该线程定期调用  [`Cache.cleanUp()`](http://google.github.io/guava/releases/11.0.1/api/docs/com/google/common/cache/Cache.html#cleanUp--) 。

如果要为很少写入的缓存安排定期的缓存维护，只需使用 [`ScheduledExecutorService`](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledExecutorService.html) 调度维护操作。