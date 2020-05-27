## 状态变化

一旦线程获得对临界区的访问权，它就必须更改同步器的状态，以（可能）阻止其他线程进入它。换句话说，状态需要反映一个事实，即线程正在临界区内部执行。这将影响其他尝试获得访问权限的线程的访问条件。

在 [Lock](http://tutorials.jenkov.com/java-concurrency/locks.html) 中，状态更改是代码设置 `isLocked = true`。在信号量中，要么是代码 `signals--` 要么是 `signals++`。

这是两个代码片段，其中状态更改代码以粗体显示：

```java
public class Lock{

  private boolean isLocked = false;

  public synchronized void lock()
  throws InterruptedException{
    while(isLocked){
      wait();
    }
    //state change
    isLocked = true;
  }

  public synchronized void unlock(){
    //state change
    isLocked = false;
    notify();
  }
}
public class BoundedSemaphore {
  private int signals = 0;
  private int bound   = 0;

  public BoundedSemaphore(int upperBound){
    this.bound = upperBound;
  }

  public synchronized void take() throws InterruptedException{
    while(this.signals == bound) wait();
    //state change
    this.signals++;
    this.notify();
  }

  public synchronized void release() throws InterruptedException{
    while(this.signals == 0) wait();
    //state change
    this.signals--;
    this.notify();
  }
}
```

## 通知策略

一旦线程更改了同步器的状态，有时可能需要将状态更改通知其他正在等待的线程。也许此状态更改可能会使其他线程的访问条件变为 `true`。

通知策略通常分为三类。

1. 通知所有等待的线程。

2. 随机通知 N 个等待线程中的 1 个。

3. 通知 N 个等待线程中特定的 1 个。

通知所有正在等待的线程非常容易。所有等待线程在同一对象上调用 `wait()`。一旦线程想要通知等待线程，它将在等待线程调用 `wait()` 的对象上调用 `notifyAll()`。

随机通知一个等待线程也很容易。通知线程只需在等待线程已调用 `wait()` 的对象上调用 `notify()` 即可。调用 `notify` 不能保证将通知哪个等待线程。因此，术语就是“随机等待线程”。

有时您可能需要通知特定的线程而不是随机的等待线程。例如，如果您需要保证以特定的顺序通知正在等待的线程，则可以是它们调用同步器的顺序，也可以是某些优先顺序。为了达到这个目的，每个等待线程必须在其自己的单独对象上调用 `wait()`。当通知线程要通知特定的等待线程时，它将在该特定线程已调用 `wait()` 的对象上调用 `notify()`。可以在 [饥饿与公平](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 中找到一个示例。

以下是带有粗体标记的通知策略（通知 1 个随机等待线程）的代码段：

```java
public class Lock{

  private boolean isLocked = false;

  public synchronized void lock()
  throws InterruptedException{
    while(isLocked){
      //wait strategy - related to notification strategy
      wait();
    }
    isLocked = true;
  }

  public synchronized void unlock(){
    isLocked = false;
    notify(); //notification strategy
  }
}
```