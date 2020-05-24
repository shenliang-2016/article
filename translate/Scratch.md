## 丢失的信号

万一调用时没有线程在等待，方法 `notify()` 和 `notifyAll()` 不会将方法调用保存到它们中。然后，通知信号就丢失了。因此，如果线程在发出信号的线程调用 `wait()` 之前调用 `notify()` ，则等待的线程将丢失该信号。这可能是问题，也可能不是问题，但是在某些情况下，这可能会导致等待线程永远等待，永远不会醒来，因为错过了唤醒信号。

为了避免信号丢失，它们应该被存储在信号类内部。在 `MyWaitNotify` 示例中，唤醒信号应该存储在 `MyWaitNotify` 实例的一个成员变量中。下面是示例：

```java
public class MyWaitNotify2{

  MonitorObject myMonitorObject = new MonitorObject();
  boolean wasSignalled = false;

  public void doWait(){
    synchronized(myMonitorObject){
      if(!wasSignalled){
        try{
          myMonitorObject.wait();
         } catch(InterruptedException e){...}
      }
      //clear signal and continue running.
      wasSignalled = false;
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      wasSignalled = true;
      myMonitorObject.notify();
    }
  }
}
```

注意，在调用 `notify()` 之前，`doNotify()` 方法现在如何将 `wasSignalled` 变量设置为 `true`。另外，请注意 `doWait()` 方法现在如何在调用 `wait()` 之前检查 `wasSignalled` 变量。实际上，如果在先前的 `doWait()` 调用与本次调用之间未接收到任何信号，则仅调用 `wait()`。

## 虚假唤醒

由于无法解释的原因，即使未调用 `notify()` 和 `notifyAll()` ，线程也有可能被唤醒。这就是所谓的虚假唤醒。没有任何原因的唤醒。

如果在 `MyWaitNofity2` 类的 `doWait()` 方法中发生了虚假唤醒，则等待线程可能会继续处理而没有收到适当的信号！这可能会在您的应用程序中引起严重的问题。

为了防止虚假唤醒，请在 `while` 循环内而不是 `if` 语句内检查 `signal` 成员变量。这样的 `while` 循环也称为自旋锁。唤醒的线程一直旋转，直到旋转锁（`while` 循环）中的条件变为 `false` 为止。这是 `MyWaitNotify2` 的修改版本，展示了此内容：

```java
public class MyWaitNotify3{

  MonitorObject myMonitorObject = new MonitorObject();
  boolean wasSignalled = false;

  public void doWait(){
    synchronized(myMonitorObject){
      while(!wasSignalled){
        try{
          myMonitorObject.wait();
         } catch(InterruptedException e){...}
      }
      //clear signal and continue running.
      wasSignalled = false;
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      wasSignalled = true;
      myMonitorObject.notify();
    }
  }
}
```

请注意，`wait()` 调用现在如何嵌套在 `while` 循环而不是 `if` 语句内。如果等待线程在没有收到信号的情况下唤醒，则 `wasSignalled` 成员仍然为 `false`，而 `while` 循环将再次执行，从而使唤醒的线程返回等待状态。