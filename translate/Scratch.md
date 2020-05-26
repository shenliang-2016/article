## 读/写锁的可重入性

前面的 `ReadWriteLock` 类是非 [可重入的](http://tutorials.jenkov.com/java-concurrency/locks.html#reentrance)。如果一个已经拥有写访问权限的线程再次请求写访问权限，将会阻塞，因为已经存在一个写入者——它自己。进一步地，考虑下列场景：

1. 线程 1 获得读访问权限。

2. 线程 2 请求写操作权限但是会被阻塞，因为已经存在一个读者。

3. 线程 1 重新请求读访问权限（重新进入锁），将会被阻塞，因为已经存在一个写请求。

这种情况下，前文中所述的 `ReadWriteLock` 将会锁死——类似死锁的情况。所有线程的无论是读还是写请求都不会被满足。

要将 `ReadWriteLock` 修改为可重入的，需要稍微修改一下。读者和写者的可重入将被分别处理。

## 读可重入

为了将 `ReadWriteLock` 改造为读者可重入的，我们需要首先建立读者可重入规则：

- 如果线程可以获取读取访问权限（无写入者或写入请求），或者如果它已经具有读取访问权限（无论写入请求如何），则授予该线程读取重入权限。

为了确定某个线程是否已经具有读取访问权限，将对每个授予读取访问权限的线程的引用及其已获得读取锁定的次数保留在 Map 中。在确定是否可以授予读取访问权限时，将检查此 Map 以获取对调用线程的引用。这是 `lockRead()` 和 `unlockRead()` 方法在更改后的样子：

```java
public class ReadWriteLock{

  private Map<Thread, Integer> readingThreads =
      new HashMap<Thread, Integer>();

  private int writers        = 0;
  private int writeRequests  = 0;

  public synchronized void lockRead() throws InterruptedException{
    Thread callingThread = Thread.currentThread();
    while(! canGrantReadAccess(callingThread)){
      wait();                                                                   
    }

    readingThreads.put(callingThread,
       (getAccessCount(callingThread) + 1));
  }


  public synchronized void unlockRead(){
    Thread callingThread = Thread.currentThread();
    int accessCount = getAccessCount(callingThread);
    if(accessCount == 1){ readingThreads.remove(callingThread); }
    else { readingThreads.put(callingThread, (accessCount -1)); }
    notifyAll();
  }


  private boolean canGrantReadAccess(Thread callingThread){
    if(writers > 0)            return false;
    if(isReader(callingThread) return true;
    if(writeRequests > 0)      return false;
    return true;
  }

  private int getReadAccessCount(Thread callingThread){
    Integer accessCount = readingThreads.get(callingThread);
    if(accessCount == null) return 0;
    return accessCount.intValue();
  }

  private boolean isReader(Thread callingThread){
    return readingThreads.get(callingThread) != null;
  }

}
```

如您所见，读重入仅在当前没有线程写入资源时才被授予。此外，如果调用线程已经具有读取访问权限，则此优先级高于所有写入请求。

## 写可重入

仅当线程已经具有写访问权限时，才授予写重入权限。这是 `lockWrite()` 和 `unlockWrite()` 方法在更改之后的样子：

```java
public class ReadWriteLock{

    private Map<Thread, Integer> readingThreads =
        new HashMap<Thread, Integer>();

    private int writeAccesses    = 0;
    private int writeRequests    = 0;
    private Thread writingThread = null;

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

  public synchronized void unlockWrite() throws InterruptedException{
    writeAccesses--;
    if(writeAccesses == 0){
      writingThread = null;
    }
    notifyAll();
  }

  private boolean canGrantWriteAccess(Thread callingThread){
    if(hasReaders())             return false;
    if(writingThread == null)    return true;
    if(!isWriter(callingThread)) return false;
    return true;
  }

  private boolean hasReaders(){
    return readingThreads.size() > 0;
  }

  private boolean isWriter(Thread callingThread){
    return writingThread == callingThread;
  }
}
```

注意，在确定调用线程是否可以进行写访问时，现在如何考虑当前持有写锁的线程。