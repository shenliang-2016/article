# ReadWriteLock

`java.util.concurrent.locks.ReadWriteLock` 是一种高级线程锁定机制。同一时刻，它允许多个线程读取某个资源，但只能有一个线程写入该资源。

基本想法是，多个线程可以从共享资源读取而不会引起并发错误。并发错误首先发生在对共享资源的读写同时发生，或者并发发生多个写入时。

在本文中，我仅介绍 Java 的内置 `ReadWriteLock`。如果您想阅读更多有关实现 `ReadWriteLock` 的理论，请参考我的 Java 并发教程中 [Read Write Locks](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) 部分。

## ReadWriteLock 锁定规则

允许线程锁定 `ReadWriteLock` 以读取或写入受保护资源的规则如下：

| **Read Lock**  | 如果没有线程锁定`ReadWriteLock`进行写操作，并且没有线程请求写锁（但尚未获得写锁）。因此，多个线程可以锁定该锁以进行读取。 |
| -------------- | ------------------------------------------------------------ |
| **Write Lock** | **如果没有线程正在读取或写入。因此，一次只能有一个线程可以锁定该锁以进行写入。** |

## ReadWriteLock 实现

`ReadWriteLock` 是一个接口，因此，你需要使用它的一个实现。

`java.util.concurrent.locks` 包含下列 `ReadWriteLock` 实现：

- ReentrantReadWriteLock

## ReadWriteLock 代码示例

下面的例子展示了如何创建 `ReadWriteLock` 以及如何为了读取或者写入而锁定它：

```java
ReadWriteLock readWriteLock = new ReentrantReadWriteLock();


readWriteLock.readLock().lock();

    // multiple readers can enter this section
    // if not locked for writing, and not writers waiting
    // to lock for writing.

readWriteLock.readLock().unlock();


readWriteLock.writeLock().lock();

    // only one writer can enter this section,
    // and only if no threads are currently reading.

readWriteLock.writeLock().unlock();
```

注意 `ReadWriteLock` 实际上如何在内部维护两个 `Lock` 实例，分别负责守卫读操纵和写操作。

