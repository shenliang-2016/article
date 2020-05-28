# Java Concurrency Utilities - java.util.concurrent

[http://tutorials.jenkov.com/java-util-concurrent/index.html](http://tutorials.jenkov.com/java-util-concurrent/index.html)



Java 5 为 Java 平台添加了一个新的包 `java.util.concurrent`。这个包中携带了一系列的类，可以极大简化并发(多线程)应用的开发。在添加这个包之前，你不得不编写自己的并发工具类。

本教程中，我将带你纵览 `java.util.concurrent` 包中的工具类，介绍如何使用它们。例子中使用的是 Java 6，我不确定这两个版本是否完全一致。

本教程不会解释 Java 并发的核心概念，其背后的原理。如果你对这部分感兴趣，请参考我的 [Java Concurrency tutorial](http://tutorials.jenkov.com/java-concurrency/index.html)。

## 内容目录

下面是本教程涵盖的主题列表。

- [Java BlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html)
- [Java ArrayBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/arrayblockingqueue.html)
- [Java DelayQueue](http://tutorials.jenkov.com/java-util-concurrent/delayqueue.html)
- [Java LinkedBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/linkedblockingqueue.html)
- [Java PriorityBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/priorityblockingqueue.html)
- [Java SynchronousQueue](http://tutorials.jenkov.com/java-util-concurrent/synchronousqueue.html)
- [Java BlockingDeque](http://tutorials.jenkov.com/java-util-concurrent/blockingdeque.html)
- [Java LinkedBlockingDeque](http://tutorials.jenkov.com/java-util-concurrent/linkedblockingdeque.html)
- [Java ConcurrentMap](http://tutorials.jenkov.com/java-util-concurrent/concurrentmap.html)
- [Java ConcurrentNavigableMap](http://tutorials.jenkov.com/java-util-concurrent/concurrentnavigablemap.html)
- [Java CountDownLatch](http://tutorials.jenkov.com/java-util-concurrent/countdownlatch.html)
- [Java CyclicBarrier](http://tutorials.jenkov.com/java-util-concurrent/cyclicbarrier.html)
- [Java Exchanger](http://tutorials.jenkov.com/java-util-concurrent/exchanger.html)
- [Java Semaphore](http://tutorials.jenkov.com/java-util-concurrent/semaphore.html)
- [Java ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html)
- [Java Callable](http://tutorials.jenkov.com/java-util-concurrent/java-callable.html)
- [Java Future](http://tutorials.jenkov.com/java-util-concurrent/java-future.html)
- [Java ThreadPoolExecutor](http://tutorials.jenkov.com/java-util-concurrent/threadpoolexecutor.html)
- [Java ScheduledExecutorService](http://tutorials.jenkov.com/java-util-concurrent/scheduledexecutorservice.html)
- [Java ForkJoinPool](http://tutorials.jenkov.com/java-util-concurrent/java-fork-and-join-forkjoinpool.html)
- [Java Lock](http://tutorials.jenkov.com/java-util-concurrent/lock.html)
- [Java ReadWriteLock](http://tutorials.jenkov.com/java-util-concurrent/readwritelock.html)
- [Java AtomicInteger](http://tutorials.jenkov.com/java-util-concurrent/atomicinteger.html)
- [Java AtomicLong](http://tutorials.jenkov.com/java-util-concurrent/atomiclong.html)
- [Java AtomicReference](http://tutorials.jenkov.com/java-util-concurrent/atomicreference.html)
- [Java AtomicStampedReference](http://tutorials.jenkov.com/java-util-concurrent/atomicstampedreference.html)
- [Java AtomicIntegerArray](http://tutorials.jenkov.com/java-util-concurrent/atomicintegerarray.html)
- [Java AtomicLongArray](http://tutorials.jenkov.com/java-util-concurrent/atomiclongarray.html)
- [Java AtomicReferenceArray](http://tutorials.jenkov.com/java-util-concurrent/atomicreferencearray.html)

## 随时联系我

如果您不同意我在此处写的有关 `java.util.concurrent` 实用程序的任何内容，或者有任何意见，问题等，请随时给我发送电子邮件。可以在 [about](http://jenkov.com/about/index.html) 页面上找到我的电子邮件地址。

# Java BlockingQueue

*Java* *BlockingQueue* 接口 `java.util.concurrent.BlockingQueue`，表示一个队列，向其中添加元素和从中取出元素的操作都是线程安全的。换句话说，多个线程可以同时向其中插入元素并从其中读取元素，而不会发生任何并发问题。

术语"阻塞队列"来自 Java `BlockingQueue` 能够阻塞试图向队列中插入元素或者从队列中读取元素的线程这个事实。比如，如果一个线程试图从队列中读取元素，但队列中已经没有元素，该线程就会被阻塞，直到有元素可以读取。线程是否会阻塞取决于你调用 `BlockingQueue` 上的哪个方法。稍后将详细介绍各个方法的不同。

本文也不会讲解如何实现你自己的 `BlockingQueue` 。如果你感兴趣，可以参考 [Java Concurrency Tutorial](http://tutorials.jenkov.com/java-concurrency/index.html)。

## BlockingQueue 用途

 `BlockingQueue` 通常用于生产者－消费者场景，也就是一个线程生产对象，同时另一个线程消费对象。下面是该场景的示意图：

| ![A BlockingQueue with one thread putting into it, and another thread taking from it.](http://tutorials.jenkov.com/images/java-concurrency-utils/blocking-queue.png) |
| ------------------------------------------------------------ |
| **一个 BlockingQueue ，一个线程添加元素，另一个线程取出元素。** |

生产者线程将持续不断地生产新的对象并插入 `BlockingQueue` 中，直到队列达到它可以容纳的元素的上限。队列是有限的，换句话说。如果阻塞队列大小达到了其上限，生产者线程在试图插入新元素是就会阻塞，直到消费者线程从队列中取出一个对象。

消费者线程持续不断从 `BlockingQueue` 中取出对象进行处理。如果消费者线程试图从空队列中获取对象，就会阻塞，直到生产者线程将新的对象插入队列。

### BlockingQueue 方法

Java `BlockingQueue` 接口有 4 个类方法用来插入元素、删除元素以及检查队列中的元素。每种方法在请求的操作无法立即执行对情况下行为有所不同。下表列出了这些方法：

|             | **Throws Exception** | **Special Value** | **Blocks** | **Times Out**                 |
| ----------- | -------------------- | ----------------- | ---------- | ----------------------------- |
| **Insert**  | `add(o)`             | `offer(o)`        | `put(o)`   | `offer(o, timeout, timeunit)` |
| **Remove**  | `remove(o)`          | `poll()`          | `take()`   | `poll(timeout, timeunit)`     |
| **Examine** | `element()`          | `peek()`          | ` `        | ` `                           |

4 种不同的行为集合含义是：

1. **Throws Exception**:
   如果尝试的操作无法立即执行，则抛出异常。
2. **Special Value**:
   如果尝试的操作不可能立即执行，返回特定的值（通常是 `true` 或者 `false`）。
3. **Blocks**:
   如果尝试的操作不可能立即执行，调用方法的线程阻塞，直到执行变为可能。
4. **Times Out**:
   如果无法立即进行尝试的操作，则该方法调用将一直阻塞直到可以执行，但等待时间不得长于给定的超时时间。返回一个表示操作是否成功的特殊值（通常为 `true` / `false`）。

无法将 `null` 插入 `BlockingQueue`。如果您尝试插入 `null`，则 `BlockingQueue` 将抛出 `NullPointerException`。

也可以访问 `BlockingQueue` 内部的所有元素，而不仅仅是开始和结束的元素。例如，假设您已将一个对象排队等待处理，但是您的应用程序决定取消该对象。然后，您可以调用  `remove(o)` 删除队列中的特定对象。但是，这样做的效率不是很高，因此除非确实需要，否则不应使用这些 `Collection` 方法。

## BlockingQueue 实现

由于 `BlockingQueue` 是一个接口，你需要通过它的实现类使用它。 `java.util.concurrent` 包中已经有了下列的 `BlockingQueue` 接口的实现类：

- [ArrayBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/arrayblockingqueue.html)
- [DelayQueue](http://tutorials.jenkov.com/java-util-concurrent/delayqueue.html)
- [LinkedBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/linkedblockingqueue.html)
- [PriorityBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/priorityblockingqueue.html)
- [SynchronousQueue](http://tutorials.jenkov.com/java-util-concurrent/synchronousqueue.html)

查看每个链接了解每种实现。

## Java BlockingQueue 示例

这里是一个 Java `BlockingQueue` 示例。使用 `BlockingQueue` 的 `ArrayBlockingQueue` 实现。

首先， `BlockingQueueExample` 类启动一个 `Producer` 线程和一个 `Consumer` 线程。该 `Producer` 将字符串插入共享 `BlockingQueue`，而 `Consumer` 将字符串从队列中取出。

```java
public class BlockingQueueExample {

    public static void main(String[] args) throws Exception {

        BlockingQueue queue = new ArrayBlockingQueue(1024);

        Producer producer = new Producer(queue);
        Consumer consumer = new Consumer(queue);

        new Thread(producer).start();
        new Thread(consumer).start();

        Thread.sleep(4000);
    }
}
```

下面是 `Producer` 类。注意它在每次 `put()` 调用之间休眠 1 秒钟。这将导致 `Consumer` 被阻塞，以等待对象被插入队列。

```java
public class Producer implements Runnable{

    protected BlockingQueue queue = null;

    public Producer(BlockingQueue queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            queue.put("1");
            Thread.sleep(1000);
            queue.put("2");
            Thread.sleep(1000);
            queue.put("3");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

下面是 `Consumer` 类。它将对象从队列中取出，并将它们打印到 `System.out`。

```java
public class Consumer implements Runnable{

    protected BlockingQueue queue = null;

    public Consumer(BlockingQueue queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            System.out.println(queue.take());
            System.out.println(queue.take());
            System.out.println(queue.take());
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

