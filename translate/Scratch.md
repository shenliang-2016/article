## 创建 CyclicBarrier

创建 `CyclicBarrier` 时可以指定希望多少线程在其上等待，才能够释放它们。如下所示：

```java
CyclicBarrier barrier = new CyclicBarrier(2);
```

## 在 CyclicBarrier 处等待

线程在 `CyclicBarrier` 处等待：

```java
barrier.await();
```

您还可以为等待的线程指定超时。当超时时间过去后，即使不是所有的 N 个线程都在 `CyclicBarrier` 上等待，该线程也会被释放。这是您指定超时的方法：

```java
barrier.await(10, TimeUnit.SECONDS);
```

等待线程在 `CyclicBarrier` 处等待，直到：

- 最后一个线程到达(调用 `await()`)
- 被其他线程打断(其他线程调用该线程的 `interrupt()` 方法)
- 其他等待线程被打断
- 其他等待线程等待时间超过超时时间
- `CyclicBarrier.reset()` 方法被某些外部线程调用

## CyclicBarrier Action

`CyclicBarrier` 支持屏障操作，这是一个 `Runnable`，在最后一个线程到达时执行。您将 `Runnable` 屏障操作传递给 `CyclicBarrier` 构造函数，如下所示：

```java
Runnable      barrierAction = ... ;
CyclicBarrier barrier       = new CyclicBarrier(2, barrierAction);
```

## CyclicBarrier 示例

下面是使用 `CyclicBarrier` 的示例：

```java
Runnable barrier1Action = new Runnable() {
    public void run() {
        System.out.println("BarrierAction 1 executed ");
    }
};
Runnable barrier2Action = new Runnable() {
    public void run() {
        System.out.println("BarrierAction 2 executed ");
    }
};

CyclicBarrier barrier1 = new CyclicBarrier(2, barrier1Action);
CyclicBarrier barrier2 = new CyclicBarrier(2, barrier2Action);

CyclicBarrierRunnable barrierRunnable1 =
        new CyclicBarrierRunnable(barrier1, barrier2);

CyclicBarrierRunnable barrierRunnable2 =
        new CyclicBarrierRunnable(barrier1, barrier2);

new Thread(barrierRunnable1).start();
new Thread(barrierRunnable2).start();
```

下面是 `CyclicBarrierRunnable` 类：

```java
public class CyclicBarrierRunnable implements Runnable{

    CyclicBarrier barrier1 = null;
    CyclicBarrier barrier2 = null;

    public CyclicBarrierRunnable(
            CyclicBarrier barrier1,
            CyclicBarrier barrier2) {

        this.barrier1 = barrier1;
        this.barrier2 = barrier2;
    }

    public void run() {
        try {
            Thread.sleep(1000);
            System.out.println(Thread.currentThread().getName() +
                                " waiting at barrier 1");
            this.barrier1.await();

            Thread.sleep(1000);
            System.out.println(Thread.currentThread().getName() +
                                " waiting at barrier 2");
            this.barrier2.await();

            System.out.println(Thread.currentThread().getName() +
                                " done!");

        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (BrokenBarrierException e) {
            e.printStackTrace();
        }
    }
}
```

这是执行上述代码的控制台输出。请注意，线程执行写入控制台的顺序可能因执行而异。有时 `Thread-0` 首先打印，有时 `Thread-1` 首先打印，等等。

```
Thread-0 waiting at barrier 1
Thread-1 waiting at barrier 1
BarrierAction 1 executed
Thread-1 waiting at barrier 2
Thread-0 waiting at barrier 2
BarrierAction 2 executed
Thread-0 done!
Thread-1 done!
```

