# Slipped Conditions

## 什么是 Slipped Conditions？

Slipped conditions 含义是，在一个线程检查某个条件到它实际操作该条件期间，该条件已经被其他线程修改了，这样实际上前一个线程的操作就是错误的。下面是个简单的例子：

```java
public class Lock {

    private boolean isLocked = true;

    public void lock(){
      synchronized(this){
        while(isLocked){
          try{
            this.wait();
          } catch(InterruptedException e){
            //do nothing, keep waiting
          }
        }
      }

      synchronized(this){
        isLocked = true;
      }
    }

    public synchronized void unlock(){
      isLocked = false;
      this.notify();
    }

}
```

注意 `lock()` 方法包含两个同步块。第一个块等待，直到 `isLocked` 为假。第二个块将 `isLocked` 设置为 `true`，以锁定其他线程的 `Lock` 实例。

假设 `isLocked` 为假，并且两个线程同时调用 `lock()`。如果进入第一个同步块的第一个线程在第一个同步块之后被抢占，则该线程将检查 `isLocked` 并指出它为假。如果现在允许第二个线程执行，从而进入第一个同步块，那么该线程也将把 `isLocked` 视为 `false`。现在，两个线程都将条件读取为 `false`。然后，两个线程将进入第二个同步块，将 `isLocked` 设置为 `true`，然后继续。

这种情况是 slipped conditions 的一个例子。两个线程都测试条件，然后退出同步块，从而允许其他线程在两个线程中的任何一个更改后续线程的条件之前测试条件。换句话说，从线程检查条件开始到后续线程将其更改之前，条件一直在滑动。

为了避免 slipped conditions ，必须通过执行该操作的线程来自动进行条件的测试和设置，这意味着没有其他线程可以在第一个线程进行的测试和条件设置之间检查条件。

上面示例中的解决方案很简单。只需在 `while` 循环之后，将 `isLocked = true;` 行上移到第一个同步块中即可。如下所示：

```java
public class Lock {

    private boolean isLocked = true;

    public void lock(){
      synchronized(this){
        while(isLocked){
          try{
            this.wait();
          } catch(InterruptedException e){
            //do nothing, keep waiting
          }
        }
        isLocked = true;
      }
    }

    public synchronized void unlock(){
      isLocked = false;
      this.notify();
    }

}
```

现在 `isLocked` 条件的检测和设定都在同一个同步块内部自动完成。