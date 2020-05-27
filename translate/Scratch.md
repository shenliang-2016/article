## 有界信号量

上面的 `CoutingSemaphore` 没有可以存储的信号数量的上界。我们现在把它修改为规定计数上界的信号量：

```java
public class BoundedSemaphore {
  private int signals = 0;
  private int bound   = 0;

  public BoundedSemaphore(int upperBound){
    this.bound = upperBound;
  }

  public synchronized void take() throws InterruptedException{
    while(this.signals == bound) wait();
    this.signals++;
    this.notify();
  }

  public synchronized void release() throws InterruptedException{
    while(this.signals == 0) wait();
    this.signals--;
    this.notify();
  }
}
```

请注意，如果信号数量等于上限，那么 `take()` 方法现在将阻塞。如果 `BoundedSemaphore` 已达到其信号上限，直到线程调用 `release()` 后，才允许调用 `take()` 的线程传递其信号。

## 将信号量作为锁

将有界信号量用作锁是可能的。只需要将计数上界设定为 1，使用 `take()` 和 `release()` 调用首位临界区。如下所示：

```java
BoundedSemaphore semaphore = new BoundedSemaphore(1);

...

semaphore.take();

try{
  //critical section
} finally {
  semaphore.release();
}
```

与信号用例相比，方法 `take()` 和 `release()` 现在由同一线程调用。因为只允许一个线程获取信号量，所以所有其他调用 `take()` 的线程都将被阻塞，直到调用 `release()` 为止。由于始终总是先调用 `take()`，因此对 `release()` 的调用将永远不会阻塞。

您还可以使用有界信号量来限制代码段中允许的线程数。例如，在上面的示例中，如果将 `BoundedSemaphore` 的计数上界设置为 5，会发生什么情况？一次允许5个线程进入临界区。但是，您必须确保这 5 个线程的线程操作不会冲突，否则应用程序将失败。

从 `finally` 块内部调用 `release()` 方法以确保即使从临界区抛出异常也可以调用该方法。

