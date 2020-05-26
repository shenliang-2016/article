## 锁的可重入

Java 中的同步块是可重入的。这就意味着，如果一个 Java 线程进入一个同步块的代码，也就是获取了该同步块同步于其上的监视器对象的锁，该线程就可以进入同步在同一个监视器对象上的其他同步块代码。如下面例子所示：

```java
public class Reentrant{

  public synchronized outer(){
    inner();
  }

  public synchronized inner(){
    //do something
  }
}
```

注意，`outer()` 和 `inner()` 方法都被声明为同步的，在 Java 中等价于 `synchronized(this)` 块。如果一个线程调用 `outer()` ，则从 `outer()` 内部调用 `inner()` 没有任何问题。因为两个方法(代码块)都是同步在同一个监视器对象（`this`）上。如果一个线程已经持有了监视器对象上的锁，它就同时获取了同步在同一个监视器对象上的所有同步块的访问权限。这种特性被称为可重入。该线程可以任意进入它所持有的锁相关的任何同步代码块。

前面的锁实现不可重入。如下这样重写 `Reentrant` 类，调用 `outer()` 方法的线程将被阻塞在 `inner()` 方法中的 `lock.lock()` 内部。

```java
public class Reentrant2{

  Lock lock = new Lock();

  public outer(){
    lock.lock();
    inner();
    lock.unlock();
  }

  public synchronized inner(){
    lock.lock();
    //do something
    lock.unlock();
  }
}
```

调用 `outer()` 的线程将首先锁定 `Lock` 实例。然后它将调用 `inner()`。在 `inner()` 方法内部线程将重新尝试锁定 `Lock` 实例。这种尝试将会失败(意味着线程将会被阻塞)，因为 `Lock` 实例已经在 `outer()` 方法中被锁定。

当我们查看 `lock()` 实现时，很明显，线程第二次调用 `lock()` 而没有在其间调用 `unlock()` 时被阻塞的原因很明显：

```java
public class Lock{

  boolean isLocked = false;

  public synchronized void lock()
  throws InterruptedException{
    while(isLocked){
      wait();
    }
    isLocked = true;
  }

  ...
}
```

`while` 循环（自旋锁）中的条件决定了是否允许线程退出 `lock()` 方法。当前条件是，无论哪个线程将其锁定，`isLocked` 必须为 `false` 才能被允许。

将 `Lock` 类修改为可重入的，只需要进行稍微修改：

```java
public class Lock{

  boolean isLocked = false;
  Thread  lockedBy = null;
  int     lockedCount = 0;

  public synchronized void lock()
  throws InterruptedException{
    Thread callingThread = Thread.currentThread();
    while(isLocked && lockedBy != callingThread){
      wait();
    }
    isLocked = true;
    lockedCount++;
    lockedBy = callingThread;
  }


  public synchronized void unlock(){
    if(Thread.curentThread() == this.lockedBy){
      lockedCount--;

      if(lockedCount == 0){
        isLocked = false;
        notify();
      }
    }
  }

  ...
}
```

注意 `while` 循环（自旋锁）现在也将锁定 `Lock` 实例的线程纳入考虑范围。如果锁被解锁（`isLocked = false`）或调用线程是锁定 `Lock` 实例的线程，则 `while` 循环将不会执行，并且调用 `lock()` 的线程将被允许退出该方法。

另外，我们需要计算锁被同一线程锁定的次数。否则，一次调用 `unlock()` 将会解锁该锁，即使该锁已被多次锁定。我们不希望在锁定它的线程执行与 `lock()` 调用相同数量的 `unlock()` 调用之前将其解锁。

`Lock` 类现在是可重入的。