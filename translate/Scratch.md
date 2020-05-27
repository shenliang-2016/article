## 状态

同步器的状态被用于访问条件以确定线程能否获得访问权限。在 [Lock](http://tutorials.jenkov.com/java-concurrency/locks.html) 中状态保存在 `boolean` 变量中，表示该 `Lock` 是否被锁定。在 [Bounded Semaphore](http://tutorials.jenkov.com/java-concurrency/semaphores.html#bounded) 中，内部状态存储在一个计数器(`int`)和上界(`int`)中，前者表示当前调用 `takes()` 的线程数量，后者表示可以调用 `takes()` 的线程最大数量。在 [Blocking Queue](http://tutorials.jenkov.com/java-concurrency/blocking-queues.html) 中，状态保存在队列中元素的 `List` 中，如果存在队列长度限制，那么状态就还包括最大队列长度(`int`)。

下面是来自 `Lock` 和 `BoundedSemaphore` 的两个代码片段，其中包含状态代码：

```java
public class Lock{

  //state is kept here
  private boolean isLocked = false; 

  public synchronized void lock()
  throws InterruptedException{
    while(isLocked){
      wait();
    }
    isLocked = true;
  }

  ...
}
public class BoundedSemaphore {

  //state is kept here
      private int signals = 0;
      private int bound   = 0;
      
  public BoundedSemaphore(int upperBound){
    this.bound = upperBound;
  }

  public synchronized void take() throws InterruptedException{
    while(this.signals == bound) wait();
    this.signal++;
    this.notify();
  }
  ...
}
```

## 访问条件

访问条件是确定是否可以允许调用测试和设置状态方法的线程设置状态的条件。访问条件通常基于同步器的 [状态](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html#state)。通常在 `while` 循环中检查访问条件，以防止 [Spurious Wakeups](http://tutorials.jenkov.com/java-concurrency/thread-signaling.html#spuriouswakeups)。评估访问条件时，它要么是 `true` 要么是 `false`。

在 [Lock](http://tutorials.jenkov.com/java-concurrency/locks.html) 中，访问条件只是检查 `isLocked` 成员变量的值。在 [Bounded Semaphore](http://tutorials.jenkov.com/java-concurrency/semaphores.html#bounded) 中，实际上有两种访问条件，具体取决于您是要“获取”还是“释放”该信号量。如果线程尝试获取信号量，则将对 `signals` 变量进行上限检查。如果线程试图释放信号量，则将 `signals` 变量与 0 进行比较。

这是 `Lock` 和 `BoundedSemaphore` 的两个代码段，访问条件用粗体标出。注意如何在 `while` 循环中始终检查条件。

```java
public class Lock{

  private boolean isLocked = false;

  public synchronized void lock()
  throws InterruptedException{
    //access condition
    while(isLocked){
      wait();
    }
    isLocked = true;
  }

  ...
}
public class BoundedSemaphore {
  private int signals = 0;
  private int bound   = 0;

  public BoundedSemaphore(int upperBound){
    this.bound = upperBound;
  }

  public synchronized void take() throws InterruptedException{
    //access condition
    while(this.signals == bound) wait();
    this.signals++;
    this.notify();
  }

  public synchronized void release() throws InterruptedException{
    //access condition
    while(this.signals == 0) wait();
    this.signals--;
    this.notify();
  }
}
```

