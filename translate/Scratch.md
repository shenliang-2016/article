# 重入闭锁

重入闭锁是类似于 [deadlock](http://tutorials.jenkov.com/java-concurrency/deadlock.html) 和 [nested monitor lockout](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html) 的情况。重入闭锁的部分介绍已经涵盖在 [Locks](http://tutorials.jenkov.com/java-concurrency/locks.html) 和 [Read / Write Locks](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) 章节中。

重入闭锁可能发生在一个线程多次进入 [Lock](http://tutorials.jenkov.com/java-concurrency/locks.html)， [ReadWriteLock](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) 或者某些其他不可重入的同步器时。可重入意味着已经持有一个锁的线程可以重复持有该锁。Java 的同步块是可重入的。因此下面的代码可以正常工作：

```java
public class Reentrant{

  public synchronized outer(){
    inner();
  }

  public synchronized inner(){
    //do something
  }
}
```

注意，`outer()` 和 `inner()` 都被声明为同步的，在 Java 中等价于 `synchronized(this)` 块。如果线程调用 `outer()`，则从 `outer()` 内部调用 `inner()` 没问题，因为两个方法（或块）都在同一个监视对象（`this`）上同步。如果线程已经拥有监视对象上的锁，则它可以访问在同一监视对象上同步的所有块。这称为重入。线程可以重新进入已经为其持有锁的任何代码块。

下面的 `Lock` 实现就不是可重入的：

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

如果一个线程调用两次 `lock()`，而在两次调用之间没有调用 `unlock()`，则第二次 `lock()` 调用将会阻塞。重入闭锁就发生了。

有两种选择可以避免重入闭锁：

1. 避免编写重新进入锁的代码
2. 使用可重入锁

哪种选择最适合您的项目，取决于您的具体情况。可重入锁的性能通常不如不可重入锁，并且很难实现，但这在您的具体情况下可能不是问题。无论有没有重入，代码是否易于实现都必须视情况而定。