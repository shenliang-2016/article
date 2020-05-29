# Exchanger

`java.util.concurrent.Exchanger` 类表示一种两个线程可以在该处交换对象的汇合点。下面是该机制的示意图：

| ![Two threads exchanging objects via an Exchanger.](http://tutorials.jenkov.com/images/java-concurrency-utils/exchanger.png) |
| ------------------------------------------------------------ |
| **两个线程通过 Exchanger 交换对象。**                        |

对象交换通过两个 `exchange()` 方法之一进行。如下所示：

```java
Exchanger exchanger = new Exchanger();

ExchangerRunnable exchangerRunnable1 =
        new ExchangerRunnable(exchanger, "A");

ExchangerRunnable exchangerRunnable2 =
        new ExchangerRunnable(exchanger, "B");

new Thread(exchangerRunnable1).start();
new Thread(exchangerRunnable2).start();
```

下面是 `ExchangerRunnable` 代码：

```java
public class ExchangerRunnable implements Runnable{

    Exchanger exchanger = null;
    Object    object    = null;

    public ExchangerRunnable(Exchanger exchanger, Object object) {
        this.exchanger = exchanger;
        this.object = object;
    }

    public void run() {
        try {
            Object previous = this.object;

            this.object = this.exchanger.exchange(this.object);

            System.out.println(
                    Thread.currentThread().getName() +
                    " exchanged " + previous + " for " + this.object
            );
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

例子输出如下：

```
Thread-0 exchanged A for B
Thread-1 exchanged B for A
```

# Semaphore

`java.util.concurrent.Semaphore` 类是一个 [counting semaphore](http://tutorials.jenkov.com/java-concurrency/semaphores.html#counting)。这就意味着它包含两个主要方法：

- acquire()
- release()

计数信号量以给定数量的"许可"初始化。对于每次对 `acquire()` 的调用，调用线程都会获得许可。对于每次对 `release()` 的调用，都会将许可返回给信号量。因此，最多 N 个线程可以通过 `acquire()` 方法，而无需任何 `release()` 调用，其中 N 是初始化信号量的许可数量。许可只是一个简单的计数器，没什么好看的。

## Semaphore 用途

信号量通常有两种用途：

1. 防止超过 N 个线程同时进入临界区。

2. 在两个线程之间发送信号。

### 守卫临界区

如果使用信号量保护临界区，则尝试进入临界区的线程通常会首先尝试获取许可，进入临界区，然后在此之后再次释放许可。像这样：

```java
Semaphore semaphore = new Semaphore(1);

//critical section
semaphore.acquire();

...

semaphore.release();
```

### 在线程之间发送信号

如果使用信号量在线程之间发送信号，则通常一个线程调用 `acquire()` 方法，另一个线程调用 `release()` 方法。

如果没有可用的许可，则 `acquire()` 调用将阻塞，直到另一个线程释放许可为止。类似地，如果没有更多的许可可以释放到该信号量中，则将阻止 `release()` 调用。

因此可以协调线程。例如，如果在线程 1 将对象插入共享列表后调用了 `acquire()` ，而线程 2 在从该列表中获取对象之前调用了 `release()`，则实际上已经创建了一个阻塞队列。信号量中可用的许可数量将对应于阻塞队列可以容纳的最大元素数量。

## 公平

从“信号量”获取许可的线程的 [公平性](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 不能得到保证。也就是说，不能保证第一个调用 `acquire()` 的线程也是获得许可的第一个线程。如果第一个线程在等待许可时被阻塞，那么在释放许可时检查许可的第二个线程实际上可以在第一个线程之前获得许可。

如果要保证公平性，则 `Semaphore` 类具有一个构造函数，该构造函数接受一个布尔值来告知该信号是否应保证公平性。保证公平会影响性能/并发性，因此除非需要，请不要启用它。

这是在公平模式下创建 `Semaphore` 的方法：

```java
Semaphore semaphore = new Semaphore(1, true);
```

## 更多方法

`java.util.concurrent.Semaphore` 类拥有更多方法，比如：

- `availablePermits()`
- `acquireUninterruptibly()`
- `drainPermits()`
- `hasQueuedThreads()`
- `getQueuedThreads()`
- `tryAcquire()`
- `etc.`

参考 JavaDoc 更多地了解这些方法。