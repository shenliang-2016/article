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

## BlockingQueue Usage

A `BlockingQueue` is typically used to have one thread produce objects, which another thread consumes. Here is a diagram that illustrates this principle:

| ![A BlockingQueue with one thread putting into it, and another thread taking from it.](http://tutorials.jenkov.com/images/java-concurrency-utils/blocking-queue.png) |
| ------------------------------------------------------------ |
| **A BlockingQueue with one thread putting into it, and another thread taking from it.** |

The producing thread will keep producing new objects and insert them into the `BlockingQueue`, until the queue reaches some upper bound on what it can contain. It's limit, in other words. If the blocking queue reaches its upper limit, the producing thread is blocked while trying to insert the new object. It remains blocked until a consuming thread takes an object out of the queue.

The consuming thread keeps taking objects out of the `BlockingQueue` to processes them. If the consuming thread tries to take an object out of an empty queue, the consuming thread is blocked until a producing thread puts an object into the queue.

### BlockingQueue Methods

The Java `BlockingQueue` interface has 4 different sets of methods for inserting, removing and examining the elements in the queue. Each set of methods behaves differently in case the requested operation cannot be carried out immediately. Here is a table of the methods:

|             | **Throws Exception** | **Special Value** | **Blocks** | **Times Out**                 |
| ----------- | -------------------- | ----------------- | ---------- | ----------------------------- |
| **Insert**  | `add(o)`             | `offer(o)`        | `put(o)`   | `offer(o, timeout, timeunit)` |
| **Remove**  | `remove(o)`          | `poll()`          | `take()`   | `poll(timeout, timeunit)`     |
| **Examine** | `element()`          | `peek()`          | ` `        | ` `                           |

The 4 different sets of behaviour means this:

1. **Throws Exception**:
   If the attempted operation is not possible immediately, an exception is thrown.
2. **Special Value**:
   If the attempted operation is not possible immediately, a special value is returned (often true / false).
3. **Blocks**:
   If the attempted operation is not possible immedidately, the method call blocks until it is.
4. **Times Out**:
   If the attempted operation is not possible immedidately, the method call blocks until it is, but waits no longer than the given timeout. Returns a special value telling whether the operation succeeded or not (typically true / false).

It is not possible to insert `null` into a `BlockingQueue`. If you try to insert null, the `BlockingQueue` will throw a `NullPointerException`.

It is also possible to access all the elements inside a `BlockingQueue`, and not just the elements at the start and end. For instance, say you have queued an object for processing, but your application decides to cancel it. You can then call e.g. `remove(o)` to remove a specific object in the queue. However, this is not done very efficiently, so you should not use these `Collection` methods unless you really have to.

## BlockingQueue Implementations

Since `BlockingQueue` is an interface, you need to use one of its implementations to use it. The `java.util.concurrent` package has the following implementations of the `BlockingQueue` interface:

- [ArrayBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/arrayblockingqueue.html)
- [DelayQueue](http://tutorials.jenkov.com/java-util-concurrent/delayqueue.html)
- [LinkedBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/linkedblockingqueue.html)
- [PriorityBlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/priorityblockingqueue.html)
- [SynchronousQueue](http://tutorials.jenkov.com/java-util-concurrent/synchronousqueue.html)

Click the links in the list to read more about each implementation.

## Java BlockingQueue Example

Here is a Java `BlockingQueue` example. The example uses the `ArrayBlockingQueue` implementation of the `BlockingQueue` interface.

First, the `BlockingQueueExample` class which starts a `Producer` and a `Consumer` in separate threads. The `Producer` inserts strings into a shared `BlockingQueue`, and the `Consumer` takes them out.

```
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

Here is the `Producer` class. Notice how it sleeps a second between each `put()` call. This will cause the `Consumer` to block, while waiting for objects in the queue.

```
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

Here is the `Consumer` class. It just takes out the objects from the queue, and prints them to `System.out`.

```
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