# Lock

`java.util.concurrent.locks.Lock` 是一种线程同步机制，类似于 `synchronized` 块。不过，`Lock` 相比于同步块更加灵活和复杂。

顺便说一下，在我的 [Java Concurrency tutorial](http://tutorials.jenkov.com/java-concurrency/index.html) 中描述了如何实现你自己的锁，参考 [Locks](http://tutorials.jenkov.com/java-concurrency/locks.html) 了解更多细节。

## Java Lock 示例

由于 `Lock` 是一个接口，你需要在应用中使用它的某个实现。下面是个简单的例子：

```java
Lock lock = new ReentrantLock();

lock.lock();

//critical section

lock.unlock();
```

首先创建一个 `Lock`。然后调用它的 `lock()` 方法。现在，`Lock` 实例已被锁定。任何其他调用 `lock()` 的线程都将被阻塞，直到锁定该锁的线程调用 `unlock()`。最后调用 `unlock()`，则 `Lock` 现在被解锁，以便其他线程可以锁定它。

## Java Lock 实现

`java.util.concurrent.locks` 包中包含以下 `Lock` 接口实现：

- ReentrantLock

## Locks 与同步块的主要差异

`Lock` 与同步块之间的主要差异：

- 同步块无法保证等待进入的同步块的线程最终的访问顺序。
- 您不能将任何参数传递给同步块。因此，无法对同步块设置超时。
- 同步块必须完整包含在单个方法中。 `Lock` 的 `lock()` 和 `unlock()` 调用可以分开存在于不同的方法中。

## Lock 方法

 `Lock` 接口拥有以下重要方法：

- lock()
- lockInterruptibly()
- tryLock()
- tryLock(long timeout, TimeUnit timeUnit)
- unlock()

如果可能的话，`lock()` 方法会锁定 `Lock` 实例。如果 `Lock` 实例已经被锁定，则调用 `lock()` 的线程将被阻塞，直到 `Lock` 实例被解锁。

除非调用该方法的线程已被中断，否则 `lockInruptible()` 方法将锁定 `Lock`。另外，如果某个线程被阻塞，等待通过此方法锁定 `Lock`，如果该线程被中断，则退出此方法调用。

`tryLock()` 方法尝试立即锁定 `Lock` 实例。如果锁定成功，则返回 `true`，如果已经锁定 `Lock`，则返回 `false`。此方法永远不会阻塞。

`tryLock(long timeout, TimeUnit timeUnit)` 的工作方式与 `tryLock()` 方法类似，只是它在放弃给定的锁之前尝试等待给定的超时时间。

`unlock()` 方法解锁 `Lock` 实例。通常。`Lock` 实现仅允许锁定了 `Lock` 的线程调用此方法。其他调用此方法的线程可能会导致未经检查的异常（`RuntimeException`）。

