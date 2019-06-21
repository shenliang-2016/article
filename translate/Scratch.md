### 高级同步对象

到目前为止，本课程重点关注从一开始就是Java平台一部分的低级API。这些API适用于非常基本的任务，但更高级的任务需要更高级别的构建块。对于充分利用当今多处理器和多核系统的大规模并发应用程序来说尤其如此。

在本节中，我们将介绍Java平台5.0版中引入的一些高级并发功能。大多数这些功能都在新的`java.util.concurrent`包中实现。Java Collections Framework中还有新的并发数据结构。

- [锁对象](https://docs.oracle.com/javase/tutorial/essential/concurrency/newlocks.html) 支持锁定习惯用语并简化许多并发程序。
- [执行器](https://docs.oracle.com/javase/tutorial/essential/concurrency/executors.html) 定义用于启动和管理线程的高级API。`java.util.concurrent`提供的执行器实现提供适用于大规模应用程序的线程池管理。
- [并发集合](https://docs.oracle.com/javase/tutorial/essential/concurrency/collections.html) 使管理大量数据更容易，并可以大大减少同步需求。
- [原子变量](https://docs.oracle.com/javase/tutorial/essential/concurrency/atomicvars.html) 具有最小化同步和帮助避免内存一致性错误的功能。
- [`ThreadLocalRandom`](https://docs.oracle.com/javase/tutorial/essential/concurrency/threadlocalrandom.html) (in JDK 7) 提供从多个线程有效生成伪随机数功能。

#### 锁对象

同步代码依赖于简单的可重入锁。这种锁易于使用，但有许多限制。[`java.util.concurrent.locks`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/package-summary.html) 包支持更复杂的锁定习语。我们不会详细介绍这个包，而是将重点放在其最基本的接口 [`Lock`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/Lock.html) 上。

`Lock`对象非常类似于同步代码使用的隐式锁。与隐式锁一样，一次只有一个线程可以拥有一个`Lock`对象。锁对象还通过其关联的 [`Condition`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/Condition.html) 对象支持 `wait/notify` 机制。

`Lock`对象优于隐式锁的最大优点是它们能够退出获取锁的尝试。如果锁定立即不可用或超时（如果指定），则`tryLock`方法退出。如果另一个线程在获取锁之前发送中断，则`lockInterruptibly`方法将退出。

让我们使用`Lock`对象来解决我们在 [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 中看到的死锁问题。当朋友即将鞠躬时，Alphonse 和 Gaston 已经训练自己能够注意到对方何时也会鞠躬。我们通过要求`Friend`对象必须在继续执行鞠躬之前获取两个参与者的锁来对此进行建模。以下是改进模型`Safelock`的源代码。为了证明这个习语的多样性，我们假设 Alphonse 和 Gaston 如此迷恋他们新发现的安全鞠躬能力，他们不停相互鞠躬：

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

#### 执行器

在前面的所有示例中，由新的线程（由其`Runnable`对象定义）和线程本身（由`Thread`对象定义）完成的任务之间存在紧密的联系。这适用于小型应用程序，但在大型应用程序中，将线程管理和创建与应用程序的其余部分分开是有意义的。封装这些函数的对象称为执行器。以下小节详细描述了执行器。

- [执行器接口](https://docs.oracle.com/javase/tutorial/essential/concurrency/exinter.html) 定义三个执行器对象类型。
- [线程池](https://docs.oracle.com/javase/tutorial/essential/concurrency/pools.html) 是最常见的执行器实现类型。
- [Fork/Join](https://docs.oracle.com/javase/tutorial/essential/concurrency/forkjoin.html) 是一个利用多个处理器的框架（JDK 7中的新增功能）。

##### 执行器接口

`java.util.concurrent` 包定义了三个执行器接口：

- `Executor`，支持启动新任务的简单接口。
- `ExecutorService` ，`Executor` 的子接口，添加了生命周期管理的特性，管理单个任务和执行器本身。
- `ScheduledExecutorService` ，`ExecutorService` 的子接口，支持 `Futrue` 和/或任务的周期性执行。

通常，引用执行器对象的变量被声明为这三种接口类型之一，而不是执行器类类型。

**`Executor` 接口**

[`Executor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html) 接口提供单个方法`execute`，旨在成为常见线程创建习惯用语的替代方法。如果`r`是`Runnable`对象，并且`e`是`Executor`对象，则可以替换

The [`Executor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html) interface provides a single method, `execute`, designed to be a drop-in replacement for a common thread-creation idiom. If `r` is a `Runnable` object, and `e` is an `Executor` object you can replace

```java
(new Thread(r)).start();
```

为

```java
e.execute(r);
```

但是， `execute` 的定义不太具体。低级习语创建一个新线程并立即启动它。根据`Executor`实现，`execute`可以执行相同的操作，但更有可能使用现有的工作线程来运行`r`，或者将`r`放在队列中以等待工作线程变为可用。（我们将在 [线程池](https://docs.oracle.com/javase/tutorial/essential/concurrency/pools.html) 部分中描述工作线程。）

`java.util.concurrent`中的执行器实现旨在充分利用更高级的`ExecutorService`和`ScheduledExecutorService`接口，尽管它们也可以与基本`Executor`接口一起使用。

**`ExecutorService` 接口**

[`ExecutorService`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html) 接口使用类似但更通用的 `submit` 方法补充 `execute` 。与`execute`一样，`submit`接受`Runnable`对象，但也接受 [`Callable`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Callable.html) 对象，这些对象允许任务返回一个值。`submit`方法返回一个`Future`对象，该对象用于检索`Callable`返回值并管理`Callable`和`Runnable`任务的状态。

`ExecutorService`还提供了提交大量`Callable`对象的方法。最后，`ExecutorService`提供了许多用于管理执行器关闭的方法。为了支持立即关闭，任务应该正确处理 [中断](https://docs.oracle.com/javase/tutorial/essential/concurrency/interrupt.html)  。

**`ScheduledExecutorService` 接口**

[`ScheduledExecutorService`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledExecutorService.html) i接口使用`schedule`补充其父`ExecutorService`的方法，该方法在指定的延迟后执行`Runnable`或`Callable`任务。此外，接口定义了`scheduleAtFixedRate`和`scheduleWithFixedDelay`，它们以定义的间隔重复执行指定的任务。

##### 线程池

`java.util.concurrent`中的大多数执行器实现都使用由工作线程组成的线程池。这种线程与它执行的`Runnable`和`Callable`任务分开存在，通常用于执行多个任务。

使用工作线程可以最大限度地减少由于线程创建而产生线程对象使用大量内存，而在大型应用程序中，分配和释放许多线程对象会产生大量的内存管理开销。

一种常见类型的线程池是固定大小线程池。这种类型的池始终具有指定数量的线程运行；如果某个线程仍在使用时以某种方式终止，它将自动替换为新线程。任务通过内部队列提交到线程池中，只要有多个活动任务而不是线程，该队列就会保存额外的任务。

固定大小线程池的一个重要优点是使用它的应用程序可以优雅地降级。要理解这一点，请考虑一个Web服务器应用程序，其中每个HTTP请求都由一个单独的线程处理。如果应用程序只是为每个新的HTTP请求创建一个新线程，并且系统接收的请求数超过它可以立即处理的数量，那么当所有这些线程的开销超过系统容量时，应用程序将突然停止响应所有请求。使用固定大小的线程池，由于可以创建的线程数量有限制，应用程序不会像请求进入时那样快速地为HTTP请求提供服务，但它将在系统可以维持的时间内尽快为它们提供服务。

创建使用固定大小线程池的执行器的一种简单方法是在 [`java.util.concurrent.Executors`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html) 中调用[`newFixedThreadPool`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newFixedThreadPool-int-) 工厂方法。此类还提供以下工厂方法：

 -  [`newCachedThreadPool`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newCachedThreadPool-int-) 方法使用可扩展线程池创建执行器。此执行器适用于启动许多短期任务的应用程序。
 -  [`newSingleThreadExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html#newSingleThreadExecutor-int-) 方法创建一次执行单个任务的执行器。
 -  几个工厂方法是上述执行器的`ScheduledExecutorService`版本。

如果上述工厂方法提供的执行器都不满足您的需要，则构造 [`java.util.concurrent.ThreadPoolExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html) 或者 [`java.util.concurrent.ScheduledThreadPoolExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledThreadPoolExecutor.html) 的实例将为您提供其他选项。

