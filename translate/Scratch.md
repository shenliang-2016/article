## 锁的公平性

Java 的同步块无法保证尝试进入线程的线程被授予访问的顺序。因此，如果许多线程一直在争夺对同一同步块的访问权，则存在一个或多个线程永远不会被授予访问权的风险——该访问权始终会授予其他线程。这称为饥饿。为了避免这种情况，`Lock` 应该是公平的。由于本文中展示的 `Lock` 实现在内部使用同步块，因此它们不能保证公平。饥饿和公平在 [饥饿和公平](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 中进行了详细讨论。

## 从 finally 子句中调用 unlock()

当一个临界区使用 `Lock` 进行守卫，而且该临界区中可能抛出异常，从 `finally` 子句中调用 `unlock()` 方法就是非常重要的。这样做才能保证临界区抛出异常情况下 `Lock` 仍然能够正常解锁，然后其他线程才能锁定它。如下所示：

```java
lock.lock();
try{
  //do critical section code, which may throw exception
} finally {
  lock.unlock();
}
```

这个小结构可以确保在临界区的代码抛出异常的情况下，可以解锁 `Lock`。如果未从 `finally` 子句中调用 `unlock()`，并且从临界区引发了异常，则 `Lock` 将永远保持锁定状态，从而导致所有对该 `Lock` 实例调用 `lock()` 的线程无限期阻塞。