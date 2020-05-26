# 信号量

信号量是一种线程同步结构，可以用于在线程之间发送信号以避免 [信号丢失](http://tutorials.jenkov.com/java-concurrency/thread-signaling.html#missedsignals)，也可以类似于 [锁](http://tutorials.jenkov.com/java-concurrency/locks.html) 那样保护 [临界区](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html)。Java 5 在 `java.util.concurrent` 包中提供了信号量实现，你无需自己实现信号量。不过了解其背后的理论还是很有用的。

Java 5 提供了内建的 `Semaphore` 因此你无需自己实现。更多相关细节可以阅读我的 `java.util.concurrent` 教程中 [java.util.concurrent.Semaphore](http://tutorials.jenkov.com/java-util-concurrent/semaphore.html) 相关章节。

## 简单信号量

这里是一个简单的 `Semaphore` 实现：

```java
public class Semaphore {
  private boolean signal = false;

  public synchronized void take() {
    this.signal = true;
    this.notify();
  }

  public synchronized void release() throws InterruptedException{
    while(!this.signal) wait();
    this.signal = false;
  }

}
```

`take()` 方法发送一个信号，该信号内部存储在 `Semaphore` 中。`release()` 方法等待一个信号。收到信号标志后，将再次将其清除，并退出 `release()` 方法。

使用这样的信号量可以避免信号丢失。您将调用 `take()` 而不是 `notify()` 和 `release()` 而不是 `wait()`。如果对 `take()` 的调用发生在对 `release()` 的调用之前，则调用 `release()` 的线程仍会知道调用了 `take()`，因为该信号内部存储在变量 `signal` 中。`wait()` 和 `notify()` 并非如此。

使用信号量进行信号传递时，名称 `take()` 和 `release()` 可能看起来有些奇怪。名称源于使用信号量作为锁，如本文后面所述。在这种情况下，名称更有意义。