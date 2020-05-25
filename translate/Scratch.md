# 嵌套监视器锁定

## 嵌套监视器锁定如何发生

嵌套监视器锁定类似于死锁。发生过程如下：

```
Thread 1 synchronizes on A
Thread 1 synchronizes on B (while synchronized on A)
Thread 1 decides to wait for a signal from another thread before continuing
Thread 1 calls B.wait() thereby releasing the lock on B, but not A.

Thread 2 needs to lock both A and B (in that sequence)
        to send Thread 1 the signal.
Thread 2 cannot lock A, since Thread 1 still holds the lock on A.
Thread 2 remain blocked indefinately waiting for Thread1
        to release the lock on A

Thread 1 remain blocked indefinately waiting for the signal from
        Thread 2, thereby
        never releasing the lock on A, that must be released to make
        it possible for Thread 2 to send the signal to Thread 1, etc.
```

听起来更像只是在理论上才会出现，但是看看下面的原生 `Lock` 实现：

```java
//lock implementation with nested monitor lockout problem

public class Lock{
  protected MonitorObject monitorObject = new MonitorObject();
  protected boolean isLocked = false;

  public void lock() throws InterruptedException{
    synchronized(this){
      while(isLocked){
        synchronized(this.monitorObject){
            this.monitorObject.wait();
        }
      }
      isLocked = true;
    }
  }

  public void unlock(){
    synchronized(this){
      this.isLocked = false;
      synchronized(this.monitorObject){
        this.monitorObject.notify();
      }
    }
  }
}
```

请注意， `lock()` 方法首先在 `this` 上同步，然后在 `monitorObject` 成员上同步。如果 `isLocked` 为假，则没有问题。线程不调用 `monitorObject.wait()`。如果 `isLocked` 为 `true`，则调用 `lock()` 的线程将停在 `monitorObject.wait()` 调用中。

这样做的问题是，对 `monitorObject.wait()` 的调用仅释放了 `monitorObject` 成员上的同步监视器，而不是与 `this` 关联的同步监视器。换句话说，刚停在等待状态的线程仍将同步锁保持在 `this` 上。

当首先锁定 `Lock` 的线程尝试通过调用 `unlock()` 对其进行解锁时，试图在 `unlock()` 方法中进入 `synchronized(this)` 块将被阻塞，它将一直保持阻塞状态，直到在 `lock()` 中等待的线程离开 `synchronized(this)` 块为止。但是等待 `lock()` 方法的线程不会离开该块，直到将 `isLocked` 设置为 `false`，并执行 `monitorObject.notify()`，就像在 `unlock()` 中那样。

简而言之，等待 `lock()` 的线程需要执行 `unlock()` 调用才能成功执行，以退出 `lock()` 和其中的同步块。但是，直到在 `lock()` 中等待的线程离开外部同步块之前，没有线程可以真正执行 `unlock()`。

结果是任何调用 `lock()` 或 `unlock()` 的线程都会被无限期地阻塞，这被称为嵌套监视器锁定。