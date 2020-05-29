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

# ArrayBlockingQueue

`ArrayBlockingQueue` 类实现了 [`BlockingQueue`](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) 接口。参考 [`BlockingQueue`](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) 章节了解更多。

`ArrayBlockingQueue` 是一个有界的，阻塞队列，内部把元素存储在数组中。有界的意思是它不能存储无限数量的元素。队列可以存储的元素数量存在上限。你可以在实例化时刻设置元素数量上界，之后就无法修改。

 `ArrayBlockingQueue` 内部按照 FIFO 顺序存储元素。队列的 `head` 是进入队列时间最长的元素，而 `tail` 就是进入队列时间最短的元素。

下面展示了如何实例化和使用 `ArrayBlockingQueue`：

```java
BlockingQueue queue = new ArrayBlockingQueue(1024);

queue.put("1");

Object object = queue.take();
```

下面是一个使用范型的 `BlockingQueue` 示例，注意如何放入和获取字符串：

```java
BlockingQueue<String> queue = new ArrayBlockingQueue<String>(1024);

queue.put("1");

String string = queue.take();
```

# DelayQueue

`DelayQueue` 类实现了 [`BlockingQueue`](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) 接口。参考 [`BlockingQueue`](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) 更多地了解该接口。

`DelayQueue` 在内部阻塞元素知道某个延迟时间到达。元素必须实现 `java.util.concurrent.Delayed` 接口。下面就是该接口：

```java
public interface Delayed extends Comparable<Delayed< {

 public long getDelay(TimeUnit timeUnit);

}
```

`getDelay()` 方法返回的值应该是元素可以被释放之前的延迟剩余时间。如果返回 0 或者负数，延迟会被认为已经超时。元素会在 `DelayQueue` 上的下一次 `take()` 调用时被释放。

传递给 `getDelay()` 方法的 `TimeUnit` 实例是一个 `Enum` ，表示返回的延迟值的时间单位。`TimeUnit` 枚举可以携带以下值：

```
DAYS
HOURS
MINUTES
SECONDS
MILLISECONDS
MICROSECONDS
NANOSECONDS
```

`Delayed` 接口还扩展了 `java.lang.Comparable` 接口，如你所见，该接口表示 `Delayed` 对象可以相互比较。着可能会在 `DelayQueue` 内部用来对队列中元素进行排序，从而它们可以按照超时时间顺序被释放。

下面是使用 `DelayQueue` 的例子：

```java
public class DelayQueueExample {

    public static void main(String[] args) {
        DelayQueue queue = new DelayQueue();

        Delayed element1 = new DelayedElement();

        queue.put(element1);

        Delayed element2 = queue.take();
    }
}
```

`DelayedElement` 是我创建的 `Delayed` 接口的实现。它不是 `java.util.concurrent` 包的一部分。您必须创建自己的 `Delayed` 接口实现，才能使用 `DelayQueue` 类。

# LinkedBlockingQueue

`LinkedBlockingQueue` 类实现了 [`BlockingQueue`](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) 接口。

`LinkedBlockingQueue` 内部将元素存储在链表结构（链表的节点）中。如果需要，此链表的结构可以选择具有上限。如果未指定上限，则将 `Integer.MAX_VALUE` 用作上限。

`LinkedBlockingQueue` 在内部以 FIFO（先进先出）顺序存储元素。队列的 `head` 是已在队列中最长时间的元素，而队列的 `tail` 是已在队列中最短时间的元素。

下面是  `LinkedBlockingQueue` 实例化和使用的例子：

```java
BlockingQueue<String> unbounded = new LinkedBlockingQueue<String>();
BlockingQueue<String> bounded   = new LinkedBlockingQueue<String>(1024);

bounded.put("Value");

String value = bounded.take();
```

# PriorityBlockingQueue

`PriorityBlockingQueue` 类实现了 [`BlockingQueue`](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) 接口。

`PriorityBlockingQueue` 是一个无界并发队列。它使用的排序规则与 `java.util.PriorityQueue` 类相同。这种队列中不能插入 null。

所有被插入 `PriorityBlockingQueue` 中的元素必须实现 `java.lang.Comparable` 接口。这些元素会根据你的 `Comparable` 实现中确定的优先级进行排序。

注意， `PriorityBlockingQueue` 并没有强制拥有相同优先级（`compare() == 0`）的元素应该具有任何特定行为。

还要注意，如果从 `PriorityBlockingQueue` 中获得 `Iterator`，则 `Iterator` 并不能保证按优先级顺序迭代元素。

这里是使用 `PriorityBlockingQueue` 的例子：

```java
BlockingQueue queue   = new PriorityBlockingQueue();

    //String implements java.lang.Comparable
    queue.put("Value");

    String value = queue.take();
```

# SynchronousQueue

`SynchronousQueue` 类实现了 [`BlockingQueue`](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) 接口。

`SynchronousQueue` 是一个队列，内部只能包含一个元素。阻塞将元素插入队列的线程，直到另一个线程从队列中获取该元素。同样，如果线程尝试获取一个元素而当前队列中不存在任何元素，则该线程将被阻塞，直到别的线程将一个元素插入队列。

将此类称为队列可能有点夸大其词。更像是一个会和点。

# BlockingDeque

`java.util.concurrent` 类中的 `BlockingDeque` 接口表示一个双端队列，该双端队列可以线程安全地将对象实例放入其中或者从中获取实例。在本文中，我将向您展示如何使用此 `BlockingDeque`。

`BlockingDeque` 类是一个`Deque`，它阻塞尝试向双端队列中插入元素或删除元素的线程，如果当前无法向双端队列中插入元素或从队列中删除元素。

`deque` 是“双端队列”的缩写。因此，“双端队列”是一个队列，您可以从两端插入和取出元素。

## BlockingDeque 用途

如果一个线程同时产生和消耗同一队列的元素，则可以使用 `BlockingDeque`。如果生产线程需要在队列的两端插入，而消费线程需要从队列的两端移除，则也可以使用它。下面是一个示意图：

| ![A BlockingDeque - threads can put and take from both ends of the deque.](http://tutorials.jenkov.com/images/java-concurrency-utils/blocking-deque.png) |
| ------------------------------------------------------------ |
| **一个 BlockingDeque - 线程可以从队列两端插入和删除元素。**  |

线程将产生元素并将其插入队列的任一端。如果双端队列当前已满，则插入线程将被阻塞，直到移除线程将一个元素从双端队列中取出。如果双端队列当前为空，则删除线程将被阻塞，直到插入线程将元素插入双端队列为止。

### BlockingDeque 方法

`BlockingDeque` 具有 4 种不同的方法来插入，删除和检查双端队列中的元素。如果无法立即执行所请求的操作，则每组方法的行为都会有所不同。这是方法表：

|             | **Throws Exception** | **Special Value** | **Blocks**     | **Times Out**                      |
| ----------- | -------------------- | ----------------- | -------------- | ---------------------------------- |
| **Insert**  | `addFirst(o)`        | `offerFirst(o)`   | `putFirst(o)`  | `offerFirst(o, timeout, timeunit)` |
| **Remove**  | `removeFirst(o)`     | `pollFirst(o)`    | `takeFirst(o)` | `pollFirst(timeout, timeunit)`     |
| **Examine** | `getFirst(o)`        | `peekFirst(o)`    | ` `            | ` `                                |

|             | **Throws Exception** | **Special Value** | **Blocks**    | **Times Out**                     |
| ----------- | -------------------- | ----------------- | ------------- | --------------------------------- |
| **Insert**  | `addLast(o)`         | `offerLast(o)`    | `putLast(o)`  | `offerLast(o, timeout, timeunit)` |
| **Remove**  | `removeLast(o)`      | `pollLast(o)`     | `takeLast(o)` | `pollLast(timeout, timeunit)`     |
| **Examine** | `getLast(o)`         | `peekLast(o)`     | ` `           | ` `                               |

4 种不同行为如下：

1. **Throws Exception**:
   如果尝试的操作不可能立即执行，则抛出异常。
2. **Special Value**:
   如果尝试的操作不可能立即执行，返回一个特定值（通常是 `true`/`false`）。
3. **Blocks**:
   如果尝试的操作不可能立即执行，方法阻塞知道操作可执行。
4. **Times Out**:
   如果无法立即进行尝试的操作，则该方法调用将一直阻塞直到可以执行，但等待时间不得长于给定的超时。返回一个表示操作是否成功的特殊值（通常为 `true`/`false`）。

## BlockingDeque 扩展了 BlockingQueue

`BlockingDeque` 接口扩展了 `BlockingQueue` 接口。这意味着您可以将 `BlockingDeque` 用作 `BlockingQueue`。如果这样做，各种插入方法会将元素添加到双端队列的末尾，而 `remove` 方法将从双端队列的开头删除这些元素。即，`BlockingQueue` 接口的插入和删除方法。

这是一张表，介绍了 `BlockingQueue` 方法在 `BlockingDeque` 实现中的对应方法：

| **BlockingQueue** | **BlockingDeque** |
| ----------------- | ----------------- |
| add()             | addLast()         |
| offer() x 2       | offerLast() x 2   |
| put()             | putLast()         |
|                   |                   |
| remove()          | removeFirst()     |
| poll() x 2        | pollFirst()       |
| take()            | takeFirst()       |
|                   |                   |
| element()         | getFirst()        |
| peek()            | peekFirst()       |

## BlockingDeque 实现

由于 `BlockingDeque` 是一个接口，你需要通过它的实现使用它。`java.util.concurrent` 包中提供了下面的 `BlockingDeque` 接口实现：

- [LinkedBlockingDeque](http://tutorials.jenkov.com/java-util-concurrent/linkedblockingdeque.html)

## BlockingDeque 代码实例

下面是 `BlockingDeque` 方法使用实例：

```java
BlockingDeque<String> deque = new LinkedBlockingDeque<String>();

deque.addFirst("1");
deque.addLast("2");

String two = deque.takeLast();
String one = deque.takeFirst();
```

# LinkedBlockingDeque

`LinkedBlockingDeque` 类实现了 [`BlockingDeque`](http://tutorials.jenkov.com/java-util-concurrent/blockingdeque.html) 接口。

`Deque` 一词来自“双端队列”一词。因此，`Deque` 是一个队列，您可以从队列的两端插入和删除元素。

`LinkedBlockingDeque` 是一个 `Deque`，如果线程在线程为空时尝试从中取出元素，则该线程将被阻塞，而不管线程试图从哪一端取出元素。

这是实例化和使用 `LinkedBlockingDeque` 的方法：

```java
BlockingDeque<String> deque = new LinkedBlockingDeque<String>();

deque.addFirst("1");
deque.addLast("2");

String two = deque.takeLast();
String one = deque.takeFirst();
```

# ConcurrentMap

# java.util.concurrent.ConcurrentMap

`java.util.concurrent.ConcurrentMap` 接口表示一个 [Map](http://tutorials.jenkov.com/java-collections/map.html)，它能够处理对它的并发访问（插入和获取）。

`ConcurrentMap` 除了从其父接口 [`java.util.Map`](http://tutorials.jenkov.com/java-collections/map.html) 继承的方法外，还具有一些其他原子方法。

## ConcurrentMap 实现

由于 `ConcurrentMap` 是一个接口，你需要通过实现类来使用它。`java.util.concurrent` 包中提供了下面的 `ConcurrentMap` 接口实现：

- ConcurrentHashMap

### ConcurrentHashMap

`ConcurrentHashMap` 与 `java.util.HashTable` 类非常相似，不同的是 `ConcurrentHashMap` 比 `HashTable` 具有更好的并发性。从中读取时，`ConcurrentHashMap` 不会锁定 `Map`。另外，`ConcurrentHashMap` 在写入时不会锁定整个 `Map`。它仅在内部锁定 `Map` 的写入部分。

另一个区别是，如果在迭代时更改了 `ConcurrentHashMap`，则 `ConcurrentHashMap` 不会引发 `ConcurrentModificationException`。但是，`Iterator` 不能被多个线程使用。

查看官方 JavaDoc 以获取有关 `ConcurrentMap` 和 `ConcurrentHashMap` 的更多详细信息。

## ConcurrentMap 示例

下面是 `ConcurrentMap` 接口的示例。该示例使用了 `ConcurrentHashMap` 实现：

```java
ConcurrentMap concurrentMap = new ConcurrentHashMap();

concurrentMap.put("key", "value");

Object value = concurrentMap.get("key");
```

# ConcurrentNavigableMap

`java.util.concurrent.ConcurrentNavigableMap` 类是 [java.util.NavigableMap](http://tutorials.jenkov.com/java-collections/navigablemap.html)，支持并发访问，并且具有为其子图启用的并发访问。“子图”是通过各种方法（例如 `headMap()`，`subMap()` 和 `tailMap()`）返回的图。

与其重新解释在 `NavigableMap` 中的所有方法，不如看一下由 `ConcurrentNavigableMap` 添加的方法。

## headMap()

`headMap(T toKey)` 方法返回一个包含严格小于给定键的键的视图。

如果您对原始图进行更改，这些更改将反映在头部视图中。

这是一个说明使用 `headMap()` 方法的示例。

```java
ConcurrentNavigableMap map = new ConcurrentSkipListMap();

map.put("1", "one");
map.put("2", "two");
map.put("3", "three");

ConcurrentNavigableMap headMap = map.headMap("2");
```

`headMap` 将指向 `ConcurrentNavigableMap`，其中仅包含键 `1`，因为只有此键严格小于 `2`。

有关此方法如何工作以及其重载版本如何工作的更多特定详细信息，请参见 JavaDoc。

## tailMap()

`tailMap(T fromKey)` 方法返回包含大于或等于给定的 `fromKey` 的键的视图。

如果您对原始图进行更改，则这些更改将反映在尾部视图中。

这是一个示例使用 `tailMap()` 方法的示例：

```java
ConcurrentNavigableMap map = new ConcurrentSkipListMap();

map.put("1", "one");
map.put("2", "two");
map.put("3", "three");

ConcurrentNavigableMap tailMap = map.tailMap("2");
```

`tailMap` 将包含键 `2` 和 `3`，因为这两个键大于或等于给定键 `2`。

有关此方法如何工作以及其重载版本如何工作的更多特定详细信息，请参见 JavaDoc。

## subMap()

`subMap()` 方法返回原始图的视图，该视图包含从 `from`（包括）到 `to`（不包括）的作为该方法的参数给出的两个键的所有键。这是一个例子：

```java
ConcurrentNavigableMap map = new ConcurrentSkipListMap();

map.put("1", "one");
map.put("2", "two");
map.put("3", "three");

ConcurrentNavigableMap subMap = map.subMap("2", "3");
```

返回的子图仅包含键 `2`，因为只有此键大于或等于 `2` 且小于 `3`。

## 更多方法

`ConcurrentNavigableMap` 接口包含更多可能有用的方法。 例如：

- descendingKeySet()
- descendingMap()
- navigableKeySet()

有关这些方法的更多信息，请参见官方 JavaDoc。

