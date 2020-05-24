# Thread 信号

线程信号的目的是允许线程彼此之间发送信号。同时，线程信号使得线程可以等待来自其他线程的信号。比如，线程 B 可能等待来自线程 A 的信号，该信号表明数据已经准备好被处理。

## 通过共享对象发送信号

线程之间发送信号的简单方式是将信号值设置到某些共享对象变量中。线程 A 可以在同步块内部将布尔类型的成员变量 `hasDataToProcess` 为 `true` ，线程 B 可以读取该成员变量，同样也是在同步块中。下面的示例展示了一个可以承载一个信号的对象，同时提供了相应的设置和检查方法：

```java
public class MySignal{

  protected boolean hasDataToProcess = false;

  public synchronized boolean hasDataToProcess(){
    return this.hasDataToProcess;
  }

  public synchronized void setHasDataToProcess(boolean hasData){
    this.hasDataToProcess = hasData;  
  }

}
```

线程 A 和 B 必须拥有一个共享的 `MySignal` 示例的引用来承载信号。如果两个线程拥有的是不同对象实例的引用，将无法检测到彼此的信号。需要处理的数据可以存储在与 `MySignal` 实例分开的共享缓冲区内。

