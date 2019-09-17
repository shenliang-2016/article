## 高级并发对象

到目前为止，本课程重点关注从一开始就是 Java 平台一部分的低级 API。这些 API 适用于非常基本的任务。但更高级的任务需要更高级别的构建块。对于充分利用当今多处理器和多核系统的大规模并发应用程序尤其如此。

在本节中，我们将介绍 Java 平台 5.0 版中引入的一些高级并发功能。大多数这些功能都是在新的 `java.util.concurrent` 包中实现的。 Java Collections Framework 中还有新的并发数据结构。

- [锁对象](https://docs.oracle.com/javase/tutorial/essential/concurrency/newlocks.html) 支持可以简化并发应用的锁定习语。
- [Executors](https://docs.oracle.com/javase/tutorial/essential/concurrency/executors.html) 定义用于启动和管理线程的高级 API。 `java.util.concurrent` 提供的执行器实现提供了适用于大规模应用程序的线程池管理。
- [并发集合](https://docs.oracle.com/javase/tutorial/essential/concurrency/collections.html) 使管理大量数据更容易，并可以大大减少同步的需要。
- [原子变量](https://docs.oracle.com/javase/tutorial/essential/concurrency/atomicvars.html) 具有最小化同步和帮助避免内存一致性错误的功能。
- [`ThreadLocalRandom`](https://docs.oracle.com/javase/tutorial/essential/concurrency/threadlocalrandom.html) (in JDK 7) 提供从多个线程有效生成伪随机数。

### 锁对象

同步代码依赖于简单的可重入锁。这种锁易于使用，但有许多限制。 [`java.util.concurrent.locks`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/package-summary.html) 包支持更复杂的锁定习语。我们不会详细介绍这个包，而是将重点放在它最基本的接口上， [`Lock`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/Lock.html) 。

`Lock` 对象的工作方式与同步代码使用的隐式锁非常相似。与隐式锁一样，一次只有一个线程可以拥有一个 `Lock` 对象。`Lock` 对象也通过相关的 [`Condition`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/Condition.html) 对象支持 `wait/notify` 机制。

`Lock` 对象优于隐式锁的最大优点是它们能够退出获取锁的尝试。如果锁不能立即可用或在超时到期之前（如果指定），则 `tryLock` 方法退出。如果另一个线程在获取锁之前发送中断，则 `lockInterruptibly` 方法会退出。

让我们使用 `Lock` 对象来解决我们在 [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 中看到的死锁问题。当朋友即将鞠躬时，Alphonse 和 Gaston 已经训练自己注意到了。我们通过要求我们的 `Friend` 对象必须在继续鞠躬之前获取*两个*参与者的锁来模拟这种改进。以下是改进模型的源代码，[`Safelock`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Safelock.java) 。为了证明这个习语的多样性，我们假设 Alphonse 和 Gaston 如此迷恋他们新发现的安全鞠躬能力，他们不能停止相互鞠躬：

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
import java.util.Random;

public class Safelock {
    static class Friend {
        private final String name;
        private final Lock lock = new ReentrantLock();

        public Friend(String name) {
            this.name = name;
        }

        public String getName() {
            return this.name;
        }

        public boolean impendingBow(Friend bower) {
            Boolean myLock = false;
            Boolean yourLock = false;
            try {
                myLock = lock.tryLock();
                yourLock = bower.lock.tryLock();
            } finally {
                if (! (myLock && yourLock)) {
                    if (myLock) {
                        lock.unlock();
                    }
                    if (yourLock) {
                        bower.lock.unlock();
                    }
                }
            }
            return myLock && yourLock;
        }
            
        public void bow(Friend bower) {
            if (impendingBow(bower)) {
                try {
                    System.out.format("%s: %s has"
                        + " bowed to me!%n", 
                        this.name, bower.getName());
                    bower.bowBack(this);
                } finally {
                    lock.unlock();
                    bower.lock.unlock();
                }
            } else {
                System.out.format("%s: %s started"
                    + " to bow to me, but saw that"
                    + " I was already bowing to"
                    + " him.%n",
                    this.name, bower.getName());
            }
        }

        public void bowBack(Friend bower) {
            System.out.format("%s: %s has" +
                " bowed back to me!%n",
                this.name, bower.getName());
        }
    }

    static class BowLoop implements Runnable {
        private Friend bower;
        private Friend bowee;

        public BowLoop(Friend bower, Friend bowee) {
            this.bower = bower;
            this.bowee = bowee;
        }
    
        public void run() {
            Random random = new Random();
            for (;;) {
                try {
                    Thread.sleep(random.nextInt(10));
                } catch (InterruptedException e) {}
                bowee.bow(bower);
            }
        }
    }
            

    public static void main(String[] args) {
        final Friend alphonse =
            new Friend("Alphonse");
        final Friend gaston =
            new Friend("Gaston");
        new Thread(new BowLoop(alphonse, gaston)).start();
        new Thread(new BowLoop(gaston, alphonse)).start();
    }
}
```

### Executors

在前面的所有例子中，由一个新的线程（由其 `Runnable` 对象定义）完成的任务和线程本身（由 `Thread` 对象定义）之间存在紧密的联系。这适用于小型应用程序，但在大型应用程序中，将线程管理和创建与应用程序的其余部分分开是有意义的。封装这些函数的对象称为 *executors*。以下小节详细描述了执行器。

- [Executor 接口](https://docs.oracle.com/javase/tutorial/essential/concurrency/exinter.html) 定义三个执行器对象类型。
- [Thread Pools](https://docs.oracle.com/javase/tutorial/essential/concurrency/pools.html) 最通用的执行器实现。
- [Fork/Join](https://docs.oracle.com/javase/tutorial/essential/concurrency/forkjoin.html) 是一个利用多个处理器的框架（JDK 7中的新增功能）。

#### Executor 接口

`java.util.concurrent `包定义了三个执行器接口：

 - `Executor`，一个支持启动新任务的简单接口。
 - `ExecutorService`，`Executor` 的子接口，它添加了有助于管理生命周期的功能，包括单个任务和执行器本身。
 - `ScheduledExecutorService` 是 `ExecutorService` 的子接口，支持 future 和/或定期执行任务。

通常，引用执行器对象的变量被声明为这三种接口类型之一，而不是执行器类类型。

**`Executor` 接口**

[`Executor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html) 接口提供了一个方法， `execute`，被设计为普通的线程创建习语的替代品。如果 `r` 是一个 `Runnable` 对象，而 `e` 是一个 `Executor` 对象，你可以替换

```
(new Thread(r)).start();
```

为

```
e.execute(r);
```

但是，`execute `的定义不太具体。低级习语创建一个新线程并立即启动它。根据 `Executor` 实现，`execute` 可以做同样的事情，但更有可能使用现有的工作线程来运行 `r`，或者将 `r` 放在队列中等待工作线程成为可用。（我们将在 [Thread Pools](https://docs.oracle.com/javase/tutorial/essential/concurrency/pools.html) 一节中描述工作线程。）

`java.util.concurrent` 中的执行器实现旨在充分利用更高级的 `ExecutorService` 和 `ScheduledExecutorService` 接口，尽管它们也可以与基本的 `Executor` 接口一起使用。

**`ExecutorService` 接口**

[`ExecutorService`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html) 接口用类似但更通用的 `submit` 补充 `execute`。像 `execute`，`submit` 接受 `Runnable` 对象，但也接受 [`Callable`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Callable.html ) 对象，允许任务返回值。`submit` 方法返回一个 [`Future`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Future.html) 对象，用于检索 `Callable` 返回值并管理 `Callable` 和 `Runnable` 任务的状态。

`ExecutorService` 还提供了提交大型 `Callable` 对象集合的方法。最后，`ExecutorService` 提供了许多管理执行器关闭的方法。为了支持立即关闭，任务应正确处理 [中断](https://docs.oracle.com/javase/tutorial/essential/concurrency/interrupt.html) 。

**`ScheduledExecutorService` 接口**

[`ScheduledExecutorService`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledExecutorService.html) 接口使用 `schedule` 补充其父 `ExecutorService` 的方法，在指定的延迟后执行 `Runnable` 或 `Callable` 任务。此外，接口定义 `scheduleAtFixedRate` 和 `scheduleWithFixedDelay`，它以定义的间隔重复执行指定的任务。

#### ThreadPools

`java.util.concurrent` 中的大多数执行器实现都使用 *thread pools*，它由 *worker threads* 组成。这种线程与它执行的 `Runnable` 和 `Callable` 任务分开存在，通常用于执行多个任务。

使用工作线程可以最大限度地减少由于线程创建而产生线程对象使用大量内存，而在大型应用程序中，分配和释放许多线程对象会产生大量的内存管理开销。

一种常见类型的线程池是*固定线程池*。这种类型的池始终具有指定数量的线程运行；如果某个线程在仍在使用时以某种方式终止，它将自动替换为新线程。任务通过内部队列提交到池中，只要有多个活动任务而不是线程，该队列就会保存额外的任务。

固定线程池的一个重要优点是使用它的应用程序*优雅地降级*。要理解这一点，请考虑一个 Web 服务器应用程序，其中每个 HTTP 请求都由一个单独的线程处理。如果应用程序只为每个新的 HTTP 请求创建一个新线程，并且系统接收的请求数超过它可以立即处理的数量，那么当所有这些线程的开销超过系统容量时，应用程序将突然停止响应*所有*请求。使用线程池时，由于可以创建的线程数量有限制，应用程序不会像它们进入时那样快速地为 HTTP 请求提供服务，但它将在系统可以维持的时间内尽快为它们提供服务。

创建使用固定线程池的执行器的一种简单方法是调用 [`java.util.concurrent.Executors`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html) 中的  [`newFixedThreadPool`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newFixedThreadPool-int-) 工厂方法。该类还提供以下工厂方法：

 -  [`newCachedThreadPool`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newCachedThreadPool-int-) 方法创建一个带有可扩展线程池的执行器。此执行器适用于启动许多短期任务的应用程序。
 -  [`newSingleThreadExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newSingleThreadExecutor-int-) 方法创建执行单个任务的执行程序一次。
 - 几个工厂方法是上述执行器的 `ScheduledExecutorService` 版本。

如果上述工厂方法提供的执行器都不满足您的需要，则构造 [`java.util.concurrent.ThreadPoolExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html) 或 [`java.util.concurrent.ScheduledThreadPoolExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledThreadPoolExecutor.html) 的实例将给你额外的选择。

#### Fork/Join

fork/join 框架是 `ExecutorService` 接口的一个实现，可以帮助您利用多个处理器。它专为可以递归分解成小块的工作而设计。目标是使用所有可用的处理能力来提高应用程序的性能。

与任何 `ExecutorService` 实现一样，fork/join 框架将任务分配给线程池中的工作线程。fork/join框架是不同的，因为它使用 *work-stealing* 算法。完成任务的工作线程可以从仍然忙碌的其他线程中窃取任务。

fork/join 框架的中心是 [`ForkJoinPool`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinPool.html) 类，它是 `AbstractExecutorService` 类。 `ForkJoinPool`实现了核心工作窃取算法，可以执行 [`ForkJoinTask`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinTask.html) 进程。

**基础用法**

使用 fork/join 框架的第一步是编写执行一部分工作的代码。您的代码应类似于以下伪代码：

```
if (my portion of the work is small enough)
  do the work directly
else
  split my work into two pieces
  invoke the two pieces and wait for the results
```

将此代码包装在 `ForkJoinTask` 子类中，通常使用其更专业的类型之一，[`RecursiveTask`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/RecursiveTask.html) （可以返回结果）或[`RecursiveAction`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/RecursiveAction.html) 。

在你的 `ForkJoinTask` 子类准备好之后，创建表示要完成的所有工作的对象，并将其传递给 `ForkJoinPool` 实例的 `invoke()` 方法。

**图像模糊示例**

为了帮助您了解 fork/join 框架的工作原理，请考虑以下示例。假设您想模糊图像。原始 *source* 图像由整数数组表示，其中每个整数包含单个像素的颜色值。模糊*目标*图像也由与源相同大小的整数数组表示。

通过一次一个像素地处理源阵列来完成模糊。每个像素的平均周围像素（红色，绿色和蓝色分量被平均），结果放在目标数组中。由于图像是大型数组，因此此过程可能需要很长时间。通过使用 fork/join 框架实现算法，您可以利用多处理器系统上的并发处理。这是一个可能的实现：

```java
public class ForkBlur extends RecursiveAction {
    private int[] mSource;
    private int mStart;
    private int mLength;
    private int[] mDestination;
  
    // Processing window size; should be odd.
    private int mBlurWidth = 15;
  
    public ForkBlur(int[] src, int start, int length, int[] dst) {
        mSource = src;
        mStart = start;
        mLength = length;
        mDestination = dst;
    }

    protected void computeDirectly() {
        int sidePixels = (mBlurWidth - 1) / 2;
        for (int index = mStart; index < mStart + mLength; index++) {
            // Calculate average.
            float rt = 0, gt = 0, bt = 0;
            for (int mi = -sidePixels; mi <= sidePixels; mi++) {
                int mindex = Math.min(Math.max(mi + index, 0),
                                    mSource.length - 1);
                int pixel = mSource[mindex];
                rt += (float)((pixel & 0x00ff0000) >> 16)
                      / mBlurWidth;
                gt += (float)((pixel & 0x0000ff00) >>  8)
                      / mBlurWidth;
                bt += (float)((pixel & 0x000000ff) >>  0)
                      / mBlurWidth;
            }
          
            // Reassemble destination pixel.
            int dpixel = (0xff000000     ) |
                   (((int)rt) << 16) |
                   (((int)gt) <<  8) |
                   (((int)bt) <<  0);
            mDestination[index] = dpixel;
        }
    }
  
  ...
```

现在你实现了抽象的 `compute()` 方法，它可以直接执行模糊或将它分成两个较小的任务。简单的数组长度阈值有助于确定是执行还是拆分工作。

```java
protected static int sThreshold = 100000;

protected void compute() {
    if (mLength < sThreshold) {
        computeDirectly();
        return;
    }
    
    int split = mLength / 2;
    
    invokeAll(new ForkBlur(mSource, mStart, split, mDestination),
              new ForkBlur(mSource, mStart + split, mLength - split,
                           mDestination));
}
```

如果前面的方法在 `RecursiveAction` 类的子类中，那么将任务设置为在 `ForkJoinPool` 中运行是很简单的，并涉及以下步骤：

1. 创建一个代表要完成的所有工作的任务。

1. ```java
   // source image pixels are in src
   // destination image pixels are in dst
   ForkBlur fb = new ForkBlur(src, 0, src.length, dst);
   ```

2. 创建将运行任务的 `ForkJoinPool`。

   ```java
   ForkJoinPool pool = new ForkJoinPool();
   ```

3. 运行任务。

   ```java
   pool.invoke(fb);
   ```

有关完整源代码（包括一些创建目标文件的额外代码），请参阅 [`ForkBlur`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/ForkBlur.java) 示例。

**标准实现**

除了使用 fork/join 框架来实现在多处理器系统上同时执行的任务的自定义算法（例如上一节中的 `ForkBlur.java` 示例），Java SE 中有一些通常有用的功能已经实现使用 fork/join框架。在 Java SE 8 中引入的一个这样的实现由 [`java.util.Arrays`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html) 使用，用于它的 `parallelSort()` 方法。这些方法类似于 `sort()`，但通过 fork/join 框架利用并发性。在多处理器系统上运行时，大型数组的并行排序比顺序排序更快。但是，这些方法如何利用 fork/join 框架超出了 Java Tutorials 的范围。有关此信息，请参阅 Java API 文档。

fork/join 框架的另一个实现由 `java.util.streams` 包中的方法使用，该包是计划用于 [Project Lambda](http://openjdk.java.net/projects/lambda/) 的一部分，包含在 Java SE 8 发布版中。有关更多信息，请参阅 [Lambda表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) 部分。

### 并发集合

`java.util.concurrent` 包中包含许多对 Java Collections Framework 的增强内容。这些最容易通过提供的集合接口进行分类：

- [`BlockingQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BlockingQueue.html) 定义先进先出数据结构，当您尝试添加到满队列或从空队列中检索时，该数据结构会阻塞或超时。
- [`ConcurrentMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentMap.html) 是 [`java.util.Map`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) 的子接口，定义有用的原子操作。仅当键存在时，这些操作才会删除或替换键值对，或仅在键不存在时才添加键值对。使这些操作原子化有助于避免同步。 `ConcurrentMap` 的标准的通用实现是 [`ConcurrentHashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html)，它是 [`HashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) 的并发模拟。
- [`ConcurrentNavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentNavigableMap.html) 是`ConcurrentMap`的子接口，支持近似匹配。 `ConcurrentNavigableMap` 的标准通用实现是 [`ConcurrentSkipListMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentSkipListMap.html) ，这是 [`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) 的并发模拟。

所有这些集合通过定义将对象添加到集合的操作与后续访问或删除该对象的操作之间的先发生关系来帮助避免 [内存一致性错误](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html) 。

### 原子变量

[`java.util.concurrent.atomic`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/package-summary.html) 包定义了支持的类单变量的原子操作。所有类都有 `get` 和 `set` 方法，类似于 `volatile` 变量的读写操作。也就是说，`set` 与同一变量上的任何后续 `get` 有一个先发生关系。原子 `compareAndSet` 方法也具有这些内存一致性功能，适用于整数原子变量的简单原子算法也是如此。

要查看如何使用这个包，让我们回到我们最初用于演示线程干扰的 [`Counter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Counter.java) 类：

```java
class Counter {
    private int c = 0;

    public void increment() {
        c++;
    }

    public void decrement() {
        c--;
    }

    public int value() {
        return c;
    }

}
```

使 `Counter` 免受线程干扰的一种方法是使其方法同步，如 [`SynchronizedCounter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SynchronizedCounter.java) ：

```java
class SynchronizedCounter {
    private int c = 0;

    public synchronized void increment() {
        c++;
    }

    public synchronized void decrement() {
        c--;
    }

    public synchronized int value() {
        return c;
    }

}
```

对于这个简单的类，同步是可接受的解决方案。但对于更复杂的类，我们可能希望避免不必要的同步对活动的影响。用 `AtomicInteger` 替换 `int` 字段允许我们在不诉诸同步的情况下防止线程干扰，如 [`AtomicCounter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/AtomicCounter.java)：

```java
import java.util.concurrent.atomic.AtomicInteger;

class AtomicCounter {
    private AtomicInteger c = new AtomicInteger(0);

    public void increment() {
        c.incrementAndGet();
    }

    public void decrement() {
        c.decrementAndGet();
    }

    public int value() {
        return c.get();
    }

}
```

### 并发随机数

在JDK 7中，[`java.util.concurrent`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html) 包含一个便利类，[ `ThreadLocalRandom`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadLocalRandom.html) ，适用于期望使用来自多个线程的随机数或 `ForkJoinTask` 的应用程序。

对于并发访问，使用 `ThreadLocalRandom` 而不是 `Math.random()` 可以减少争用，并最终提高性能。

您需要做的就是调用 `ThreadLocalRandom.current()`，然后调用其中一个方法来检索随机数。这是一个例子：

```java
int r = ThreadLocalRandom.current() .nextInt(4, 77);
```

## 扩展阅读

- *Concurrent Programming in Java: Design Principles and Pattern (2nd Edition)* by Doug Lea. 由领先专家提供的全面工作，他也是Java平台并发框架的架构师。
- *Java Concurrency in Practice* by Brian Goetz, Tim Peierls, Joshua Bloch, Joseph Bowbeer, David Holmes, and Doug Lea. 旨在为新手提供的实用指南。
- *Effective Java Programming Language Guide (2nd Edition)* by Joshua Bloch. 虽然这是一个通用的编程指南，但它的线程章节包含并发编程的基本“最佳实践”。
- *Concurrency: State Models & Java Programs (2nd Edition)*, by Jeff Magee and Jeff Kramer. 通过建模和实际示例的组合介绍并发编程。
- *Java Concurrent Animated:* 显示并发功能使用情况的动画。