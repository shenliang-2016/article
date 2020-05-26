## 更现实的例子

您可能会辩称，您将永远不会像本文中所示的第一个实现那样实现 `Lock`，因此声称滑移条件是一个相当理论上的问题。但是第一个示例是特意保持相当简单，以更好地传达滑移条件的概念。

一个更现实的例子是在实施公平锁定期间，如 [饥饿和公平](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 中所述。如果我们从 [嵌套监视器锁定](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html) 看简单的实现，并尝试消除嵌套监视器锁定问题， 很容易遇到滑移条件问题。下面是嵌套监视器锁定章节中的示例：

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
      QueueObject queueObject = waitingThread.get(0);
      synchronized(queueObject){
        queueObject.notify();
      }
    }
  }
}
public class QueueObject {}
```

注意，`synchronized(queueObject)` 和 `queueObject.wait()` 调用嵌套在 `synchronized(this)` 同步块内部，导致嵌套监视器问题。为了避免该问题，`synchronized(queueObject)` 块必须被移出 `synchronized(this)` 同步块。如下所示：

```java
//Fair Lock implementation with slipped conditions problem

public class FairLock {
  private boolean           isLocked       = false;
  private Thread            lockingThread  = null;
  private List<QueueObject> waitingThreads =
            new ArrayList<QueueObject>();

  public void lock() throws InterruptedException{
    QueueObject queueObject = new QueueObject();

    synchronized(this){
      waitingThreads.add(queueObject);
    }

    boolean mustWait = true;
    while(mustWait){

      synchronized(this){
        mustWait = isLocked || waitingThreads.get(0) != queueObject;
      }

      synchronized(queueObject){
        if(mustWait){
          try{
            queueObject.wait();
          }catch(InterruptedException e){
            waitingThreads.remove(queueObject);
            throw e;
          }
        }
      }
    }

    synchronized(this){
      waitingThreads.remove(queueObject);
      isLocked = true;
      lockingThread = Thread.currentThread();
    }
  }
}
```

注意：仅展示 `lock()` 方法，因为它是我更改过的唯一方法。

注意 `lock()` 方法现在如何包含 3 个同步块。

第一个 `synchronized(this)` 块通过设置`mustWait = isLocked || waitingThreads.get(0) != queueObject` 来检查条件。

第二个 `synchronized（queueObject）` 块检查线程是否要等待。此时，另一个线程可能已经解除了锁定，但是暂时不需要关心。假设锁已解锁，那么线程立即退出 `synchronized(queueObject)` 块。

仅在 `mustWait = false` 时才执行第三个 `synchronized(this)` 块。这会将条件 `isLocked` 设置回 `true` 等，并离开 `lock()` 方法。

想象一下，如果两个线程在解锁时同时调用 `lock()` 会发生什么。第一个线程 1 将检查 `isLocked` 状态，并发现它为假。然后线程 2 将执行相同的操作。然后它们都不等待，并且都将状态 `isLocked` 设置为 `true`。这是滑倒条件的典型例子。

### 解决滑动条件问题

为了解决上面例子中的滑动条件问题，最后一个 `synchronized(this)` 块的内容必须被移动到第一个同步块中。代码也需要相应地微调，以适应这种移动。如下所示：

```java
//Fair Lock implementation without nested monitor lockout problem,
//but with missed signals problem.

public class FairLock {
  private boolean           isLocked       = false;
  private Thread            lockingThread  = null;
  private List<QueueObject> waitingThreads =
            new ArrayList<QueueObject>();

  public void lock() throws InterruptedException{
    QueueObject queueObject = new QueueObject();

    synchronized(this){
      waitingThreads.add(queueObject);
    }

    boolean mustWait = true;
    while(mustWait){

        
        synchronized(this){
            mustWait = isLocked || waitingThreads.get(0) != queueObject;
            if(!mustWait){
                waitingThreads.remove(queueObject);
                isLocked = true;
                lockingThread = Thread.currentThread();
                return;
            }
        } 

      synchronized(queueObject){
        if(mustWait){
          try{
            queueObject.wait();
          }catch(InterruptedException e){
            waitingThreads.remove(queueObject);
            throw e;
          }
        }
      }
    }
  }
}
```

注意现在如何在同一个同步代码块中测试和设置局部变量 `mustWait`。还要注意，即使还在 `synchronized(this)` 代码块之外检查了 `mustWait` 局部变量，在 `while(mustWait)` 子句中，`mustWait` 变量的值也不会在 `synchronized(this)` 之外改变。一个将 `mustWait` 评估为 `false` 的线程也会自动设置内部条件（`isLocked`），以便其他任何检查条件的线程都将其评估为 `true`。

不必在 `synchronized(this)` 块中使用 `return;` 语句。这只是一个小的优化。如果线程不必等待（`mustWait == false`），则没有理由进入 `synchronized(queueObject)` 块并执行 `if(mustWait)` 子句。

细心的读者会注意到，公平锁的上述实现仍然遭受信号丢失的困扰。想象一下，当线程调用 `lock()` 时，`FairLock` 实例被锁定。在第一个 `synchronized(this)` 块之后，`mustWait` 为真。然后想象一下，调用 `lock()` 的线程被抢占了，而锁定了锁的线程则调用了 `unlock()`。如果查看前面的 `unlock()` 实现，您会注意到它调用了 `queueObject.notify()`。但是，由于等待在 `lock()` 中的线程尚未调用 `queueObject.wait()`，因此对 `queueObject.notify()` 的调用被遗忘了，信号丢失。当线程在调用 `queueObject.wait()` 之后立即调用 `lock()` 时，它将保持阻塞状态，直到其他线程调用 `unlock()` ，这可能永远不会发生。

遗漏的信号问题是文本 [饥饿和公平](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 中展示的 `FairLock` 实现已使用两种方法将 `QueueObject` 类转化为信号量： `doWait()` 和 `doNotify()`。这些方法在 `QueueObject` 内部存储并响应信号。这样，即使在 `doWait()` 之前调用了 `doNotify()`，也不会丢失信号。

