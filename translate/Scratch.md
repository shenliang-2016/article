## 完整可重入 ReadWriteLock

下面是完整可重入的 `ReadWriteLock` 实现。我对访问条件进行了一些重构，以使它们更易于阅读，从而更容易使自己确信它们是正确的。

```java
public class ReadWriteLock{

  private Map<Thread, Integer> readingThreads =
       new HashMap<Thread, Integer>();

   private int writeAccesses    = 0;
   private int writeRequests    = 0;
   private Thread writingThread = null;


  public synchronized void lockRead() throws InterruptedException{
    Thread callingThread = Thread.currentThread();
    while(! canGrantReadAccess(callingThread)){
      wait();
    }

    readingThreads.put(callingThread,
     (getReadAccessCount(callingThread) + 1));
  }

  private boolean canGrantReadAccess(Thread callingThread){
    if( isWriter(callingThread) ) return true;
    if( hasWriter()             ) return false;
    if( isReader(callingThread) ) return true;
    if( hasWriteRequests()      ) return false;
    return true;
  }


  public synchronized void unlockRead(){
    Thread callingThread = Thread.currentThread();
    if(!isReader(callingThread)){
      throw new IllegalMonitorStateException("Calling Thread does not" +
        " hold a read lock on this ReadWriteLock");
    }
    int accessCount = getReadAccessCount(callingThread);
    if(accessCount == 1){ readingThreads.remove(callingThread); }
    else { readingThreads.put(callingThread, (accessCount -1)); }
    notifyAll();
  }

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
    if(!isWriter(Thread.currentThread()){
      throw new IllegalMonitorStateException("Calling Thread does not" +
        " hold the write lock on this ReadWriteLock");
    }
    writeAccesses--;
    if(writeAccesses == 0){
      writingThread = null;
    }
    notifyAll();
  }

  private boolean canGrantWriteAccess(Thread callingThread){
    if(isOnlyReader(callingThread))    return true;
    if(hasReaders())                   return false;
    if(writingThread == null)          return true;
    if(!isWriter(callingThread))       return false;
    return true;
  }


  private int getReadAccessCount(Thread callingThread){
    Integer accessCount = readingThreads.get(callingThread);
    if(accessCount == null) return 0;
    return accessCount.intValue();
  }


  private boolean hasReaders(){
    return readingThreads.size() > 0;
  }

  private boolean isReader(Thread callingThread){
    return readingThreads.get(callingThread) != null;
  }

  private boolean isOnlyReader(Thread callingThread){
    return readingThreads.size() == 1 &&
           readingThreads.get(callingThread) != null;
  }

  private boolean hasWriter(){
    return writingThread != null;
  }

  private boolean isWriter(Thread callingThread){
    return writingThread == callingThread;
  }

  private boolean hasWriteRequests(){
      return this.writeRequests > 0;
  }

}
```

## 从 finally 子句调用 unlock()

当用 `ReadWriteLock` 保护临界区时，临界区可能会抛出异常，从 `finally` 子句内部调用 `readUnlock()` 和 `writeUnlock()` 方法很重要。这样做可以确保 `ReadWriteLock` 始终会被解锁，以便其他线程可以锁定它。这是一个例子：

```java
lock.lockWrite();
try{
  //do critical section code, which may throw exception
} finally {
  lock.unlockWrite();
}
```

这个小结构确保万一临界区中的代码抛出异常，仍然可以将 `ReadWriteLock` 解锁。如果未从 `finally` 子句中调用 `unlockWrite()`，并且临界区引发了异常，则 `ReadWriteLock` 将永远保持写锁定状态，从而导致所有调用 `lockRead()` 或 `lockWrite()` 的线程在该 `ReadWriteLock` 实例上无限期阻塞。再次可以解锁 `ReadWriteLock` 的唯一可能是，如果 `ReadWriteLock` 是可重入的，并且在引发异常时锁定了它的线程，后来成功锁定了它，执行了临界区并调用了 `unlockWrite()` 之后，再次解锁 `ReadWriteLock`。但是，为什么要等到这种情况发生？如果它真的发生了呢？从 `finally` 子句中调用 `unlockWrite()` 是一种更为可靠的解决方案。