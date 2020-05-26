# Java 中的读/写锁

相对于上一章节中介绍的 `Lock` 实现，读/写锁是一种更加复杂的锁。假设你的应用读写某些资源，但是读操作显著多于写操作。两个线程同时读取相同的资源不会产生任何问题，因而多个想要读取该资源的线程可以同时获取访问权限进行重叠读取。但是，如果一个线程希望对该资源进行写入，则所有其他读取和写入线程都不能继续进行。为了解决这种只允许一个写入线程和多个读取线程的问题，你需要一个读/写锁。

Java 5 在 `java.util.concurrent` 包中携带了读/写锁实现。即使如此，了解它们实现背后的原理仍然非常有用。

## 读/写锁的 Java 实现

首先，我们来总结一些获取资源读权限和写权限的条件：

| **读访问** | 没有线程正在写入，也没有线程已经请求写入权限。 |
| ---------- | ---------------------------------------------- |
| **写访问** | **没有线程正在读取或者写入。**                 |

如果一个线程想要读取该资源，前提是没有线程正在写入，也没有线程已经请求该资源的写入权限。通过提升写访问请求的优先级，我们假定写请求比读请求更加重要。另外，如果读操作发生更加频繁，而我们并没有提升写请求的优先级，就可能会发生线程饥饿。请求写操作的线程可能会一直阻塞到所有的读线程释放 `ReadWriteLock`。如果新的读线程始终都能够得到读权限，则等待写入的线程可能会无止境处于阻塞等待状态，也就是线程饥饿。因此，仅当没有线程当前已锁定 `ReadWriteLock` 以进行写操作或请求将其锁定以进行写操作时，才可以授予线程读访问权限。

当没有线程在读写资源时，可以授予想要对资源进行写访问权限的线程写权限。多少个线程请求了写访问权限无关紧要，除非您想保证请求写访问的线程之间的公平性，否则无关紧要。

考虑到这些简单的规则，我们可以实现一个 `ReadWriteLock`，如下所示：

```java
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

`ReadWriteLock` 拥有两对 `lock` 和 `unlock` 方法，一对用于读访问，另一对用于写访问。

读访问的规则实现在 `lockRead()` 方法中。所有线程都能获得读访问权限，除非存在一个线程拥有写访问权限，或者一个或者多个线程已经请求了写访问权限。

写访问的规则实现在 `lockWrite()` 方法中。想要写访问权限的线程通过请求写访问权限（`writeRequests++`）开始。然后它将检查它是否实际上可以获取写访问权限。如果没有线程具有对资源的读访问权，也没有线程具有对资源的写访问权，则线程可以获得写访问权限。有多少个线程请求写访问权限无关紧要。

值得注意的是，`unlockRead()` 和 `unlockWrite()` 都调用 `notifyAll()` 而不是 `notify()`。要解释原因，请想象以下情况：

在 `ReadWriteLock` 内部，有等待读取访问的线程和等待写入访问的线程。如果被 `notify()` 唤醒的线程是一个读访问线程，它将被放回等待状态，因为有线程在等待写访问。但是，没有一个等待写访问的线程被唤醒，因此没有其他事情发生。没有线程获得读或写访问权限。通过调用 `noftifyAll()`，所有等待的线程被唤醒，并检查它们是否可以获得所需的访问权限。

调用 `notifyAll()` 还有另一个好处。如果有多个线程正在等待读取访问，而没有一个线程在等待写入访问，并且调用了 `unlockWrite()`，则所有等待读取访问的线程都被立即授予读取访问权限——而不是一个接一个。