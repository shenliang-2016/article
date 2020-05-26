# Java 中的锁

锁是类似于同步块的另外一种线程同步机制，相对于同步块，锁可以进行更加负责的同步控制。锁(以及其他更先进的同步机制)使用同步块创建，所以，我们当然无法彻底摆脱 `synchronized` 关键字。

从 Java 5 开始，`java.util.concurrent.locks` 包就包含了若干锁实现，所以你不必实现自己的锁。不过，你还是需要了解如何使用它们，同时，理解这些实现背后的理论也是非常有用的。更多细节，参考 [`java.util.concurrent.locks.Lock`](http://tutorials.jenkov.com/java-util-concurrent/lock.html) 接口文档。

## 简单锁

让我们从分析 Java 同步代码块开始：

```java
public class Counter{

  private int count = 0;

  public int inc(){
    synchronized(this){
      return ++count;
    }
  }
}
```

注意 `inc()` 方法中的 `synchronized(this)` 块。这个同步块保证同一时刻只能有一个线程执行 `return ++count`。同步块内部的代码可以更加复杂，但是这个简单的 `++count` 已经足够说明问题。

`Counter` 类可以改写成下面这样，使用 `Lock` 替换同步块：

```java
public class Counter{

  private Lock lock = new Lock();
  private int count = 0;

  public int inc(){
    lock.lock();
    int newCount = ++count;
    lock.unlock();
    return newCount;
  }
}
```

`lock()` 方法锁定 `Lock` 实例，因而所有其他调用 `lock()` 的线程都会阻塞，直到 `unlock()` 被执行。

下面是一个简单的 `Lock` 实现：

```java
public class Lock{

  private boolean isLocked = false;

  public synchronized void lock()
  throws InterruptedException{
    while(isLocked){
      wait();
    }
    isLocked = true;
  }

  public synchronized void unlock(){
    isLocked = false;
    notify();
  }
}
```

注意其中的 `while(isLocked)` 循环，就是所谓的"自旋锁"。自旋锁和方法 `wait()` 和 `notify()` 方法的解释详见  [Thread Signaling](http://tutorials.jenkov.com/java-concurrency/thread-signaling.html) 章节。当 `isLocked` 为 `true`，调用 `lock()` 的线程会被阻塞等待在 `wait()` 调用中。万一线程在没有接收到 `notify()` 调用信号的时候意外从 `wait()` 调用返回(也就是所谓的 [Spurious Wakeup](http://tutorials.jenkov.com/java-concurrency/thread-signaling.html#spuriouswakeups) )，线程将会重新检查 `isLocked` 条件以确认后续执行是否安全，而不是假定只要被唤醒就意味着可以安全执行。如果 `isLocked` 是 `false` ，线程退出 `while(isLocked)` 循环，并将 `isLocked` 设置回 `true`，以为调用 `lock()` 的其他新城锁定 `Lock` 实例。

当线程执行完 [critical section](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) 代码(`lock()` 和 `unlock()` 之间的代码)，线程调用 `unlock()`。执行 `unlock()` 将 `isLocked` 设置回 `false`，同时通知(唤醒)等待在 `lock()` 方法中的 `wait()` 调用中的线程之一，如果存在的话。