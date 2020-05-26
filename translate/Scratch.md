# Java 中的读/写锁

相对于上一章节中介绍的 `Lock` 实现，读/写锁是一种更加复杂的锁。假设你的应用读写某些资源，但是读操作显著多于写操作。两个线程同时读取相同的资源不会产生任何问题，因而多个想要读取该资源的线程可以同时获取访问权限进行重叠读取。但是，如果一个线程希望对该资源进行写入，则所有其他读取和写入线程都不能继续进行。为了解决这种只允许一个写入线程和多个读取线程的问题，你需要一个读/写锁。

Java 5 在 `java.util.concurrent` 包中携带了读/写锁实现。即使如此，了解它们实现背后的原理仍然非常有用。

## Read / Write Lock Java Implementation

First let's summarize the conditions for getting read and write access to the resource:

| **Read Access**  | If no threads are writing, and no threads have requested write access. |
| ---------------- | ------------------------------------------------------------ |
| **Write Access** | **If no threads are reading or writing.**                    |

If a thread wants to read the resource, it is okay as long as no threads are writing to it, and no threads have requested write access to the resource. By up-prioritizing write-access requests we assume that write requests are more important than read-requests. Besides, if reads are what happens most often, and we did not up-prioritize writes, [starvation](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) could occur. Threads requesting write access would be blocked until all readers had unlocked the `ReadWriteLock`. If new threads were constantly granted read access the thread waiting for write access would remain blocked indefinately, resulting in [starvation](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html). Therefore a thread can only be granted read access if no thread has currently locked the `ReadWriteLock` for writing, or requested it locked for writing.

A thread that wants write access to the resource can be granted so when no threads are reading nor writing to the resource. It doesn't matter how many threads have requested write access or in what sequence, unless you want to guarantee fairness between threads requesting write access.

With these simple rules in mind we can implement a `ReadWriteLock` as shown below:

```
public class ReadWriteLock{

  private int readers       = 0;
  private int writers       = 0;
  private int writeRequests = 0;

  public synchronized void lockRead() throws InterruptedException{
    while(writers > 0 || writeRequests > 0){
      wait();
    }
    readers++;
  }

  public synchronized void unlockRead(){
    readers--;
    notifyAll();
  }

  public synchronized void lockWrite() throws InterruptedException{
    writeRequests++;

    while(readers > 0 || writers > 0){
      wait();
    }
    writeRequests--;
    writers++;
  }

  public synchronized void unlockWrite() throws InterruptedException{
    writers--;
    notifyAll();
  }
}
```

The `ReadWriteLock` has two lock methods and two unlock methods. One lock and unlock method for read access and one lock and unlock for write access.

The rules for read access are implemented in the `lockRead()` method. All threads get read access unless there is a thread with write access, or one or more threads have requested write access.

The rules for write access are implemented in the `lockWrite()` method. A thread that wants write access starts out by requesting write access (`writeRequests++`). Then it will check if it can actually get write access. A thread can get write access if there are no threads with read access to the resource, and no threads with write access to the resource. How many threads have requested write access doesn't matter.

It is worth noting that both `unlockRead()` and `unlockWrite()` calls `notifyAll()` rather than `notify()`. To explain why that is, imagine the following situation:

Inside the ReadWriteLock there are threads waiting for read access, and threads waiting for write access. If a thread awakened by `notify()` was a read access thread, it would be put back to waiting because there are threads waiting for write access. However, none of the threads awaiting write access are awakened, so nothing more happens. No threads gain neither read nor write access. By calling `noftifyAll()` all waiting threads are awakened and check if they can get the desired access.

Calling `notifyAll()` also has another advantage. If multiple threads are waiting for read access and none for write access, and `unlockWrite()` is called, all threads waiting for read access are granted read access at once - not one by one.