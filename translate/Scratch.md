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

### 公平锁

下面的例子将上面的 `Lock` 类修改成了一个称为 `FairLock` 的公平锁。您会注意到，与前面所示的 `Lock` 类相比，下面的实现在同步和 `wait()`/`notify()` 方面有所变化。

确切地说，从上一个 `Lock` 类开始的，是一个较长的故事，涉及几个增量设计步骤，每个步骤都解决了上一步的问题：[嵌套监视器锁定](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html)，[Slipped Conditions](http://tutorials.jenkov.com/java-concurrency/slipped-conditions.html) 和 [Missed Signals](http://tutorials.jenkov.com/java-concurrency/thread-signaling.html#missedsignals)。为了使文本简短，该讨论被省略了，但是在该主题的相应文本中讨论了每个步骤（请参见上面的链接）。重要的是，每个调用 `lock()` 的线程现在都已排队，并且只有队列中的第一个线程才可以锁定 `FairLock` 实例（如果已解锁）。所有其他线程将被阻塞，直到它们到达队列的顶部。

```java
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

首先，您可能会注意到不再将 `lock()` 方法声明为 `synchronized`。取而代之的是，仅将所需同步的块嵌套在 `synchronized` 块中。

`FairLock` 创建一个新的 `QueueObject` 实例，并为每个调用 `lock()` 的线程将其添加到队列中排队。调用 `unlock()` 的线程将获取队列中的顶端 `QueueObject` 并在其上调用 `doNotify()`，以唤醒在该对象上等待的线程。这样，一次仅唤醒一个等待线程，而不唤醒所有等待线程。这部分决定着 `FairLock` 的公平性。

请注意，在同一同步块内测试并设置锁的状态，以免发生 slipped conditions。

还要注意，`QueueObject` 实际上是一个信号量。`doWait()` 和 `doNotify()` 方法将信号内部存储在 `QueueObject` 中。这样做是为了避免由于线程在调用 `queueObject.doWait()` 之前，另一个线程调用 `unlock()` 和 `queueObject.doNotify()` 而被抢占而导致的信号丢失。`queueObject.doWait()` 调用放置在 ` synchronized(this)` 块的外部，以避免嵌套的监视器锁定。因此，当没有任何线程在锁中的 `synchronized(this)` 块内执行时，另一个线程实际上可以调用 `unlock()` 方法。

最后，请注意在 `try-catch` 块中如何调用 `queueObject.doWait()` 。如果抛出 `InterruptedException`，线程将离开 `lock()` 方法，我们需要将其出队。

### 性能分析

如果比较 `Lock` 和 `FairLock` 类，您会注意到 `FairLock` 类中的 `lock()` 和 `unlock()` 内部还有更多操作。这个额外的代码将导致 `FairLock` 成为比 `Lock` 慢得多的同步机制。这将对您的应用程序产生多大影响，取决于执行 `FairLock` 保护的临界区中的代码需要花费多长时间。执行时间越长，同步器增加的开销就越小。当然，这也取决于此代码被调用的频率。

