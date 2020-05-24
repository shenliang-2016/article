## 忙等

需要处理数据的线程 B 正在等待数据准备好被处理。换句话说，它正在等待来自线程 A 的表示 `hasDataToProcess()` 返回 `true` 的信号。这是在线程 B 等待该信号期间运行的循环：

```java
protected MySignal sharedSignal = ...

...

while(!sharedSignal.hasDataToProcess()){
  //do nothing... busy waiting
}
```

注意，该循环将会一直运行直到 `hasDataToProcess()` 返回 `true`。这被称为忙等。线程在等待期间是繁忙的。

## wait(), notify() 和 notifyAll()

忙等策略无法有效利用运行等待线程的计算机的 CPU 资源，除非平均等待时间非常短。相反，如果等待线程可以休眠或者不活动直到接收到所等待的信号，无疑更加聪明。

Java 拥有一种内置的等待机制允许线程在等待信号时变成不活动状态。`java.lang.Object` 类定义了三个方法，`wait()`，`notify()`，以及 `notifyAll()` 来做到这一点。

在任何对象上调用 `wait()` 的线程会变成不活动状态，直到另外的线程在该对象上调用 `notify()` 方法。为了调用这两个方法，调用者线程必须首先获得该对象的锁。换句话说，调用者线程必须在同步块内部调用着两个方法。下面是示例：

```java
public class MonitorObject{
}

public class MyWaitNotify{

  MonitorObject myMonitorObject = new MonitorObject();

  public void doWait(){
    synchronized(myMonitorObject){
      try{
        myMonitorObject.wait();
      } catch(InterruptedException e){...}
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      myMonitorObject.notify();
    }
  }
}
```

等待线程将调用 `doWait()`，唤醒线程将调用 `doNotify()`。当一个线程在一个对象上调用 `notify()`，在该对象上等待的线程之一就会被唤醒并允许执行。而 `notifyAll()` 方法则会给定对象上等待的所有线程。

如你所见，等待线程和唤醒线程都在同步块内部调用 `wait()` 和 `notify()` 方法。这是强制性的。线程不能在尚未获取到对象锁的情况下在该对象上调用 `wait()`，`notify()` 以及 `notifyAll()` 方法。如果强行这么做，将会抛出 `IllegalMonitorStateException` 。

但是，这怎么可能呢？只要等待线程在同步块中执行，它就不会持有对监视器对象（`myMonitorObject`）的锁吗？等待线程是否不会阻止通知线程从 `doNotify()` 中进入同步块？答案是不会。线程调用 `wait()` 后，它将释放它持有的监视器对象的锁。这也允许其他线程调用 `wait()` 或 `notify()`，因为必须从同步块内部调用这些方法。

一旦线程被唤醒，在调用 `notify()` 的线程退出同步块之前，被唤醒的线程都无法退出 `wait()` 调用。换句话说，被调用的线程在它能够退出 `wait()` 调用之前必须重新获得监视器对象的锁，因为该 `wait()` 调用包含在同步块中。如果多个线程通过 `notifyAll()` 被唤醒，则同一时刻只有其中一个线程能够退出 `wait()` 方法，因为在退出 `wait()` 调用之前，每个线程都必须依次获取监视器对象上的锁。