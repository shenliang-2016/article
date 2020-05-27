## Test 和 Set 方法

同步器通常有两种类型的方法，其中 `test-and-set` 是第一种类型的方法（ [set](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html#set) 是另一个）。测试并设置意味着调用此方法的线程会根据访问条件**测试**同步器的内部状态。如果满足条件，则线程**设置**同步器的内部状态以反映该线程已获得访问权限。

状态转换通常会导致其他尝试获取访问权限的线程的访问条件变为假，但可能并非总是如此。例如，在 [读写锁](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) 中，获得读取访问权限的线程会将读写锁定的状态更新为反映这一点，但是只要没有线程请求写访问权限，其他请求读访问权限的线程也将被授予访问权限。

必须以原子方式执行测试并设置操作，这意味着在测试和状态设置之间不允许在测试设置方法中执行其他线程。

测试并设置方法的程序流程通常类似于以下内容：

1. 必要时在测试前设置状态

2. 根据访问条件测试状态

3. 如果不符合访问条件，请等待

4. 如果满足访问条件，则设置状态，并在必要时通知等待线程

下面展示的 [ReadWriteLock](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) 类的 `lockWrite()` 方法是测试并设置方法的示例。调用 `lockWrite()` 的线程首先在测试之前设置状态（`writeRequests++`）。然后，在 `canGrantWriteAccess()` 方法中根据访问条件测试内部状态。如果测试成功，则退出该方法之前，将再次设置内部状态。请注意，此方法不会通知等待线程。

```java
public class ReadWriteLock{
    private Map<Thread, Integer> readingThreads =
        new HashMap<Thread, Integer>();

    private int writeAccesses    = 0;
    private int writeRequests    = 0;
    private Thread writingThread = null;

    ...

    
        public synchronized void lockWrite() throws InterruptedException{
        writeRequests++;
        Thread callingThread = Thread.currentThread();
        while(! canGrantWriteAccess(callingThread)){
        wait();
        }
        writeRequests--;
        writeAccesses++;
        writingThread = callingThread;
        }
    

    ...
}
```

下面的 `BoundedSemaphore` 类拥有两个测试并设置方法： `take()` 和
`release()`。两个方法都测试并设置内部状态。

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

## Set 方法

`set` 方法是同步器通常包含的第二种方法。`set` 方法仅设置同步器的内部状态，而无需先对其进行测试。`set` 方法的一个典型示例是 `Lock` 类的 `unlock()` 方法。持有锁的线程可以始终将其解锁，而无需测试 `Lock` 是否已解锁。

`set` 方法的程序流通常遵循以下原则：

1. 设置内部状态

2. 通知等待线程

这是一个示例 `unlock()` 方法：

```java
public class Lock{

  private boolean isLocked = false;
  
      public synchronized void unlock(){
      isLocked = false;
      notify();
      }
  
}
```

