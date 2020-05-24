## 等待同一个信号的多个线程

如果您有多个等待的线程，则 `while` 循环也是一个不错的解决方案，这些线程都使用 `notifyAll()` 唤醒了，但是只允许其中一个继续。一次只有一个线程将能够获得监视器对象的锁，这意味着只有一个线程可以退出 `wait()` 调用并清除 `wasSignalled` 标志。一旦此线程退出 `doWait()` 方法中的同步块，其他线程便可以退出 `wait()` 调用并检查 `while` 循环内的 `wasSignalled` 成员变量。但是，第一个被唤醒的线程会清除此标志，因此其余唤醒的线程将返回等待状态，直到下一个信号到达为止。

## 不要在常量字符串或全局对象上调用 wait()

上文中 `MyWaitNotify` 示例类，该示例类使用常量字符串（“”）作为监视器对象。该示例的如下：

```java
public class MyWaitNotify{

  String myMonitorObject = "";
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

在空字符串或任何其他常量字符串上调用 `wait()` 和 `notify()` 的问题是，JVM/编译器在内部将常量字符串转换为同一对象。这意味着，即使您有两个不同的 `MyWaitNotify` 实例，它们都引用相同的空字符串实例。这也意味着在第一个 `MyWaitNotify` 实例上调用 `doWait()` 的线程可能会被在第二个 `MyWaitNotify` 实例上的 `doNotify()` 调用唤醒。

这种情况如下图所示：



请记住，即使 4 个线程在同一个共享字符串实例上调用 `wait()` 和 `notify()` ，来自 `doWait()` 和 `doNotify()` 调用的信号也分别存储在两个 `MyWaitNotify` 实例中。在 `MyWaitNotify1` 上进行 `doNotify()` 调用可能会唤醒在 `MyWaitNotify2` 上等待的线程，但是该信号只会存储在 `MyWaitNotify1` 中。

起初，这似乎不是一个大问题。毕竟，如果在第二个 `MyWaitNotify` 实例上调用 `doNotify()`，那么真正发生的一切就是错误地唤醒了线程 A 和 B。唤醒的线程（A 或 B）将在 `while` 循环中检查其信号，然后返回等待状态，因为并未在第一个 `MyWaitNotify` 实例上调用 `doNotify()`，而这些线程在其上等待。这种情况等同于引起虚假唤醒。线程 A 或 B 在未发出信号的情况下唤醒。但是代码可以处理此问题，因此线程可以返回等待状态。

问题是，由于 `doNotify()` 调用仅仅调用 `notify()` 而不是 `notifyAll()`，即使 4 个线程正在同一个字符串（空字符串）实例上等待，只有一个线程会被唤醒。因此，如果线程 A 或者 B 其中之一被唤醒，而实际上信号是发个线程 C 或者 D 的，被唤醒的线程(A 或者 B)将会检查它的信号，发现并没有接收到信号，然后回到等待状态。线程 C 和线程 D 都没有被唤醒以检查它们实际上接收到的信号，这样信号就丢失了。这种情况相当于前文所述的信号丢失问题。线程 C 和 D 都被发送了信号，但是都没能对信号进行响应。

如果 `doNotify()` 方法调用了 `notifyAll()` 而不是 `notify()`，则所有等待线程都被唤醒并依次检查信号。线程 A 和 B 将回到等待状态，但是 C 或 D 中的一个将注意到该信号并留下 `doWait()` 方法调用。C 和 D 中的另一个将返回等待状态，因为发现信号的线程会在退出 `doWait()` 的过程中将其清除。

然后，您可能很想总是调用 `notifyAll()` 而不是 `notify()`，但这在性能上是一个坏主意。当只有一个线程可以响应信号时，没有理由唤醒所有等待的线程。

因此：不要将全局对象，字符串常量等用于 `wait()/notify()`机制。使用对应于使用该对象的结构的唯一的对象。例如，每个 `MyWaitNotify3`（前面部分中的示例）实例都有自己的 `MonitorObject` 实例，而不是将空字符串用于 `wait()/notify()` 调用。

