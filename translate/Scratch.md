## 更现实的例子

你可能声称你永远不会自己实现上面所说的那种锁。你也不会在内部监视器对象上调用 `wait()` 和 `notify()` ，而是在 `this` 上调用。这些都是可能的。但是，还是存在某些情况，类似于上面介绍的设计还是会出现。比如，如果你想要在一个 `Lock` 中实现 [fairness](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 。这个过程中你希望每个线程都在它们各自的排队对象上调用 `wait()`。因此，你可以一次唤醒这些线程之一。

下面是公平锁的简单实现：

```java
//Fair Lock implementation with nested monitor lockout problem

public class FairLock {
  private boolean           isLocked       = false;
  private Thread            lockingThread  = null;
  private List<QueueObject> waitingThreads =
            new ArrayList<QueueObject>();

  public void lock() throws InterruptedException{
    QueueObject queueObject = new QueueObject();

    synchronized(this){
      waitingThreads.add(queueObject);

      while(isLocked || waitingThreads.get(0) != queueObject){

        synchronized(queueObject){
          try{
            queueObject.wait();
          }catch(InterruptedException e){
            waitingThreads.remove(queueObject);
            throw e;
          }
        }
      }
      waitingThreads.remove(queueObject);
      isLocked = true;
      lockingThread = Thread.currentThread();
    }
  }

  public synchronized void unlock(){
    if(this.lockingThread != Thread.currentThread()){
      throw new IllegalMonitorStateException(
        "Calling thread has not locked this lock");
    }
    isLocked      = false;
    lockingThread = null;
    if(waitingThreads.size() > 0){
      QueueObject queueObject = waitingThreads.get(0);
      synchronized(queueObject){
        queueObject.notify();
      }
    }
  }
}
public class QueueObject {}
```

乍一看，这种实现看起来不错，但是请注意 `lock()` 方法如何从两个同步块内部调用 `queueObject.wait()`。一个在 `this` 上同步，并嵌套在 `queueObject` 局部变量上同步的一个同步块中。当线程调用 `queueObject.wait()` 时，它释放 `QueueObject` 实例上的锁，但不释放与 `this` 关联的锁。

还要注意，`unlock()` 方法被声明为 `synchronized`，它等于 `synchronized(this)` 块。这意味着，如果一个线程在 `lock()` 内部等待，则与 `this` 关联的监视器对象将被等待的线程锁定。所有调用 `unlock()` 的线程将无限期地阻塞，等待正在等待的线程释放对 `this` 的锁定。但这永远不会发生，因为只有在线程成功向等待的线程发送信号时才会发生，并且只能通过执行 `unlock()` 方法来发送。

因此，上面的 `FairLock` 实现可能导致嵌套的监视器锁定。文本 [饥饿和公平](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 中描述了公平锁定的更好实现。

## 嵌套监视器锁定 vs. 死锁

嵌套监视器锁定的结果和死锁非常像：线程陷入无止境的阻塞相互等待。

但是两种情况并不完全相同。如 [Deadlock](http://tutorials.jenkov.com/java-concurrency/deadlock.html) 章节中所述，死锁发生的时机是两个线程以不同的顺序获取相同的一组锁。线程 1 锁定 A，等待 B。线程 2 锁定 B，等待 A。如 [Deadlock Prevention](http://tutorials.jenkov.com/java-concurrency/deadlock-prevention.html) 章节中所述，死锁可以通过保证所有线程以相同的顺序获取同一组锁来避免。然而，嵌套监视器锁定刚好就是发生在两个线程以相同的顺序获取同一组锁的时候。线程 1 锁定 A 和 B，然后释放 B 并等待来自线程 2 的信号。线程 2 需要同时锁定 A 和 B 才能发送信号给线程 1。因此，一个线程等待信号，另一个线程等待一个锁被释放。

主要的不同总结如下：

```
In deadlock, two threads are waiting for each other to release locks.

In nested monitor lockout, Thread 1 is holding a lock A, and waits
for a signal from Thread 2. Thread 2 needs the lock A to send the
signal to Thread 1.
```

