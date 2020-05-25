## 在 Java 中实现公平

在 Java 中做到完全的公平是不可能的，但是我们仍然可以实现对线程尽可能公平的同步结构。

首先来分析一个简单的同步代码块：

```java
public class Synchronizer{

  public synchronized void doSynchronized(){
    //do a lot of work which takes a long time
  }

}
```

如果超过一个线程调用 `doSynchronized()` 方法，其中一些将阻塞直到第一个获取到访问权的线程离开该方法。如果超过一个线程阻塞等待访问，下一步哪个线程将得到访问权实际上没有任何保证。

### 使用锁替代同步块

为了增加等待线程的公平性，首先我们将修改上面的代码块，使用锁替换同步块：

```java
public class Synchronizer{
  Lock lock = new Lock();

  public void doSynchronized() throws InterruptedException{
    this.lock.lock();
      //critical section, do a lot of work which takes a long time
    this.lock.unlock();
  }

}
```

注意，此时 `doSynchronized()` 方法没有声明为同步块。现在临界区使用 `lock.lock()` 和 `lock.unlock()` 调用守卫。

一个简单的 `Lock` 类实现可能是下面这个样子：

```java
public class Lock{
  private boolean isLocked      = false;
  private Thread  lockingThread = null;

  public synchronized void lock() throws InterruptedException{
    while(isLocked){
      wait();
    }
    isLocked      = true;
    lockingThread = Thread.currentThread();
  }

  public synchronized void unlock(){
    if(this.lockingThread != Thread.currentThread()){
      throw new IllegalMonitorStateException(
        "Calling thread has not locked this lock");
    }
    isLocked      = false;
    lockingThread = null;
    notify();
  }
}
```

如果您查看上面的 `Synchronizer` 类并研究此 `Lock` 实现，您将注意到，如果多个线程同时调用 `lock()`，则线程现在试图访问 `lock()` 方法时被阻塞。其次，如果锁被锁定，则线程在 `lock()` 方法的 `while(isLocked)` 循环内的 `wait()` 调用中被阻塞。请记住，调用 `wait()` 的线程会释放 `Lock` 实例上的同步锁，因此等待进入 `lock()` 的线程现在可以这样做。结果是多个线程最终可能在 `lock()` 内部调用了 `wait()`。

如果回头看 `doSynchronized()` 方法，您会注意到 `lock()` 和 `unlock()` 状态之间的注释，这两个调用之间的代码需要很长时间才能执行完成。让我们进一步假设，与进入 `lock()` 方法和调用 `wait()` 相比，此代码需要花费较长的时间执行，因为该锁已被锁定。这意味着等待锁定锁并进入临界区的大部分时间都花在了 `lock()` 方法内部的 `wait()` 调用中，而不是在尝试进入 `lock()` 方法时被阻塞。

如前所述，如果有多个线程正在等待进入，则同步块不能保证首先授予哪个线程访问权限。 `wait()` 也不保证在调用 `notify()` 时唤醒了哪个线程。因此，当前的 `Lock` 类版本与 `doSynchronized()` 的同步版本在公平性方面没有不同的保证。但是我们可以改变这一点。

当前版本的 `Lock` 类将调用其自己的 `wait()` 方法。相反，如果每个线程在一个单独的对象上调用 `wait()`，从而只有一个线程在每个对象上调用了 `wait()`，则 `Lock` 类可以决定在哪个对象上调用 `notify()`，从而有效地准确选择要唤醒的线程。

### A Fair Lock

Below is shown the previous Lock class turned into a fair lock called FairLock. You will notice that the implementation has changed a bit with respect to synchronization and `wait()` / `notify()` compared to the Lock class shown earlier.

Exactly how I arrived at this design beginning from the previous Lock class is a longer story involving several incremental design steps, each fixing the problem of the previous step: [Nested Monitor Lockout](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html), [Slipped Conditions](http://tutorials.jenkov.com/java-concurrency/slipped-conditions.html), and [Missed Signals](http://tutorials.jenkov.com/java-concurrency/thread-signaling.html#missedsignals). That discussion is left out of this text to keep the text short, but each of the steps are discussed in the appropriate texts on the topic ( see the links above). What is important is, that every thread calling `lock()` is now queued, and only the first thread in the queue is allowed to lock the FairLock instance, if it is unlocked. All other threads are parked waiting until they reach the top of the queue.

```
public class FairLock {
    private boolean           isLocked       = false;
    private Thread            lockingThread  = null;
    private List<QueueObject> waitingThreads =
            new ArrayList<QueueObject>();

  public void lock() throws InterruptedException{
    QueueObject queueObject           = new QueueObject();
    boolean     isLockedForThisThread = true;
    synchronized(this){
        waitingThreads.add(queueObject);
    }

    while(isLockedForThisThread){
      synchronized(this){
        isLockedForThisThread =
            isLocked || waitingThreads.get(0) != queueObject;
        if(!isLockedForThisThread){
          isLocked = true;
           waitingThreads.remove(queueObject);
           lockingThread = Thread.currentThread();
           return;
         }
      }
      try{
        queueObject.doWait();
      }catch(InterruptedException e){
        synchronized(this) { waitingThreads.remove(queueObject); }
        throw e;
      }
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
      waitingThreads.get(0).doNotify();
    }
  }
}
public class QueueObject {

  private boolean isNotified = false;

  public synchronized void doWait() throws InterruptedException {
    while(!isNotified){
        this.wait();
    }
    this.isNotified = false;
  }

  public synchronized void doNotify() {
    this.isNotified = true;
    this.notify();
  }

  public boolean equals(Object o) {
    return this == o;
  }
}
```

First you might notice that the `lock()` method is no longer declared `synchronized`. Instead only the blocks necessary to synchronize are nested inside `synchronized` blocks.

FairLock creates a new instance of `QueueObject` and enqueue it for each thread calling `lock()`. The thread calling `unlock()` will take the top `QueueObject` in the queue and call `doNotify()` on it, to awaken the thread waiting on that object. This way only one waiting thread is awakened at a time, rather than all waiting threads. This part is what governs the fairness of the `FairLock`.

Notice how the state of the lock is still tested and set within the same synchronized block to avoid slipped conditions.

Also notice that the `QueueObject` is really a semaphore. The `doWait()` and `doNotify()` methods store the signal internally in the `QueueObject`. This is done to avoid missed signals caused by a thread being preempted just before calling `queueObject.doWait()`, by another thread which calls `unlock()` and thereby `queueObject.doNotify()`. The `queueObject.doWait()` call is placed outside the synchronized(this) block to avoid nested monitor lockout, so another thread can actually call unlock() when no thread is executing inside the `synchronized(this)` block in `lock()` method.

Finally, notice how the `queueObject.doWait()` is called inside a `try - catch` block. In case an InterruptedException is thrown the thread leaves the lock() method, and we need to dequeue it.

### A Note on Performance

If you compare the `Lock` and `FairLock` classes you will notice that there is somewhat more going on inside the `lock()` and `unlock()` in the `FairLock` class. This extra code will cause the `FairLock` to be a sligtly slower synchronization mechanism than `Lock`. How much impact this will have on your application depends on how long time the code in the critical section guarded by the `FairLock` takes to execute. The longer this takes to execute, the less significant the added overhead of the synchronizer is. It does of course also depend on how often this code is called.