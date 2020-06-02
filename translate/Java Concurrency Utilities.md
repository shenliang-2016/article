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

# ConcurrentMap

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

# CountDownLatch

`java.util.concurrent.CountDownLatch` 是一种并发结构，它允许一个或多个线程等待一组给定的操作完成。

用给定的计数初始化 `CountDownLatch`。通过调用 `CountDown()` 方法，该计数减少。等待该计数达到零的线程可以调用 `await()` 方法之一。调用 `await()` 会阻塞线程，直到计数达到零为止。

以下是一个简单的示例。`Decrementer` 在 `CountDownLatch` 上调用 `countDown()` 3 次之后，等待的 `Waiter` 从 `await()` 调用中释放。

```java
CountDownLatch latch = new CountDownLatch(3);

Waiter      waiter      = new Waiter(latch);
Decrementer decrementer = new Decrementer(latch);

new Thread(waiter)     .start();
new Thread(decrementer).start();

Thread.sleep(4000);
public class Waiter implements Runnable{

    CountDownLatch latch = null;

    public Waiter(CountDownLatch latch) {
        this.latch = latch;
    }

    public void run() {
        try {
            latch.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Waiter Released");
    }
}
public class Decrementer implements Runnable {

    CountDownLatch latch = null;

    public Decrementer(CountDownLatch latch) {
        this.latch = latch;
    }

    public void run() {

        try {
            Thread.sleep(1000);
            this.latch.countDown();

            Thread.sleep(1000);
            this.latch.countDown();

            Thread.sleep(1000);
            this.latch.countDown();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

# CyclicBarrier

`java.util.concurrent.CyclicBarrier` 类是一种同步机制，可以使用某种算法同步线程处理。换句话说，它可以看作是所有线程都必须在该处等待的栅栏，所有的线程都不能继续执行，直到所有的线程都到达该处。下面是工作原理示意图：

| ![Two threads waiting for each other at CyclicBarriers.](http://tutorials.jenkov.com/images/java-concurrency-utils/cyclic-barrier.png) |
| ------------------------------------------------------------ |
| **两个线程在循环屏障处等待彼此。**                           |

线程通过在 `CyclicBarrier` 上调用 `await()` 方法彼此等待。一旦 N 个线程在 `CyclicBarrier` 处等待，所有的线程就都会被释放并继续运行。

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

# Java ExecutorService

Java *ExecutorService* 接口，`java.util.concurrent.ExecutorService`，表示一种一步执行机制，该机制能够在后台并发执行多个任务。本文中我将解释如何创建 `ExecutorService`，如何向其提交待执行的任务，如果检查那些任务的执行结果，以及如何在你需要的时候如何关闭 `ExecutorService` 。

## 任务委托

下图展示了线程将一个任务委托给 Java `ExecutorService` 以便异步执行：

| ![A thread delegating a task to an ExecutorService for asynchronous execution.](http://tutorials.jenkov.com/images/java-concurrency-utils/executor-service.png) |
| ------------------------------------------------------------ |
| **线程将一个任务委托给 Java `ExecutorService` 以便异步执行** |

一旦线程将任务委托给了 `ExecutorService` ，该线程就会继续它自己的执行，而不受那个委托出去的任务的影响。`ExecutorService` 会并发执行任务，独立于提交该任务的线程。

## Java ExecutorService 示例

在我们继续深入了解 `ExecutorService` 之前，先看一个简单的例子：

```java
ExecutorService executorService = Executors.newFixedThreadPool(10);

executorService.execute(new Runnable() {
    public void run() {
        System.out.println("Asynchronous task");
    }
});

executorService.shutdown();
```

首先，通过使用 `Executors` `newFixedThreadPool()` 工厂方法创建 `ExecutorService` 。例子中创建了包含了 10 个用于执行任务的线程的线程池。

然后， `Runnable` 接口的一个匿名实现被传递给 `execute()` 方法。这就导致该  `Runnable` 将会被 `ExecutorService` 中的其中一个线程执行。

在本教程中，您将看到更多有关如何使用 `ExecutorService` 的示例。这个例子只是让您快速了解如何使用 `ExecutorService` 在后台执行任务。

## Java ExecutorService 实现

Java `ExecutorService` 与 [线程池](http://tutorials.jenkov.com/java-concurrency/thread-pools.html) 非常相似。实际上，存在于 `java.util.concurrent` 包中的 `ExecutorService` 接口的实现就是线程池实现。如果您想了解如何在内部实现 `ExecutorService` 接口，请阅读上述教程。

由于 `ExecutorService` 是一个接口，因此您需要对其实现进行使用。`ExecutorService` 在 `java.util.concurrent` 包中具有以下实现：

- [ThreadPoolExecutor](http://tutorials.jenkov.com/java-util-concurrent/threadpoolexecutor.html)
- [ScheduledThreadPoolExecutor](http://tutorials.jenkov.com/java-util-concurrent/scheduledexecutorservice.html)

## 创建 ExecutorService

如何创建 `ExecutorService` 取决于你使用的实现。不过，你也可以使用 `Executors` 工厂类创建 `ExecutorService` 实例。下面是几个创建 `ExecutorService` 的例子：

```java
ExecutorService executorService1 = Executors.newSingleThreadExecutor();

ExecutorService executorService2 = Executors.newFixedThreadPool(10);

ExecutorService executorService3 = Executors.newScheduledThreadPool(10);
```

## ExecutorService 使用

有几种不同的方法可以将任务委托给 `ExecutorService` 执行：

- execute(Runnable)
- submit(Runnable)
- submit(Callable)
- invokeAny(...)
- invokeAll(...)

接下来分别介绍这些方法。

### Execute Runnable

Java `ExecutorService` `execute(Runnable)` 方法接收一个 `java.lang.Runnable` 对象，并异步执行它。下面是使用 `ExecutorService` 执行 `Runnable` 的例子：

```java
ExecutorService executorService = Executors.newSingleThreadExecutor();

executorService.execute(new Runnable() {
    public void run() {
        System.out.println("Asynchronous task");
    }
});

executorService.shutdown();
```

没有办法获取被执行的 `Runnable` 的执行结果。如果需要，你将需要使用 `Callable` 来实现这一点。

### Submit Runnable

Java `ExecutorService` `submit(Runnable)` 方法同样接收一个 `Runnable` 实现，但是返回一个 `Future` 对象。这个 `Future` 对象可以被用来确定该 `Runnable` 是否已经执行完成。

下面是 Java `ExecutorService` `submit()` 示例：

```java
Future future = executorService.submit(new Runnable() {
    public void run() {
        System.out.println("Asynchronous task");
    }
});

future.get();  //returns null if the task has finished correctly.
```

该 `submit()` 方法返回一个 [Java Future](http://tutorials.jenkov.com/java-util-concurrent/java-future.html) 对象，该对象可以用来确认该 `Runnable` 何时执行完成。

### Submit Callable

Java `ExecutorService` `submit(Callable)` 方法类似于 `submit(Runnable)` 方法，除了它接收的参数是 [Java Callable](http://tutorials.jenkov.com/java-util-concurrent/java-callable.html) 而不是 `Runnable`。稍后我将介绍 `Callable` 与 `Runnable` 之间的精确差别。

该 `Callable` 的结果能够通过 `submit(Callable)`  方法返回的 [Java Future](http://tutorials.jenkov.com/java-util-concurrent/java-future.html) 对象获取。下面是 `ExecutorService` `Callable` 示例：

```java
Future future = executorService.submit(new Callable(){
    public Object call() throws Exception {
        System.out.println("Asynchronous Callable");
        return "Callable Result";
    }
});

System.out.println("future.get() = " + future.get());
```

上面的例子将输出：

```
Asynchronous Callable
future.get() = Callable Result
```

### invokeAny()

`invokeAny()` 方法接收一个 `Callable` ，或者 `Callable` 的子接口对象集合。调用此方法不会返回 `Future`，但是返回其中一个 `Callable` 对象的结果。无法保证你将会得到哪个 `Callable` 对象的结果，只能说是执行完成当中的一个。

如果其中一个任务完成（或者抛出异常），则其他的 `Callable` 将会被取消。

这是一个示例：

```java
ExecutorService executorService = Executors.newSingleThreadExecutor();

Set<Callable<String>> callables = new HashSet<Callable<String>>();

callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 1";
    }
});
callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 2";
    }
});
callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 3";
    }
});

String result = executorService.invokeAny(callables);

System.out.println("result = " + result);

executorService.shutdown();
```

此代码示例将打印出给定集合中 `Callable` 之一返回的对象。我试过几次，结果会发生变化。有时是“Task 1”，有时是“Task 2”。

### invokeAll()

`invokeAll()` 方法调用作为参数传递的集合中传递给它的所有 `Callable` 对象。`invokeAll()` 返回一个 `Future` 对象的列表，通过它可以获取每个 `Callable` 的执行结果。

请记住，任务可能由于异常而终止，因此它可能没有“成功”。 `Future` 并没有办法区别这种不同的结果。

这是一个代码示例：

```java
ExecutorService executorService = Executors.newSingleThreadExecutor();

Set<Callable<String>> callables = new HashSet<Callable<String>>();

callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 1";
    }
});
callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 2";
    }
});
callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 3";
    }
});

List<Future<String>> futures = executorService.invokeAll(callables);

for(Future<String> future : futures){
    System.out.println("future.get = " + future.get());
}

executorService.shutdown();
```

### Runnable vs. Callable

`Runnable` 接口与 `Callable` 接口非常相似。这两个接口都表示可以由线程或 `ExecutorService` 并发执行的任务。这两个接口都只有一个方法。不过，`Callable` 和 `Runnable` 接口之间只有一个小区别。当您看到接口声明时，将更容易看到 `Runnable` 和 `Callable` 接口之间的区别。

首先是 `Runnable` 接口声明：

```java
public interface Runnable {
    public void run();
}
```

这里是 `Callable` 接口声明：

```java
public interface Callable{
    public Object call() throws Exception;
}
```

`Runnable` 的 `run()` 方法和 `Callable` 的 `call()` 方法之间的主要区别是 `call()` 方法可以从方法调用中返回 `Object`。`call()` 和 `run()` 之间的另一个区别是 `call()` 可以引发异常，而 `run()` 不能（除非未经检查的异常- `RuntimeException` 的子类）。

如果需要向 Java `ExecutorService` 提交任务，并且需要任务的结果，则需要使任务实现 `Callable` 接口。否则，您的任务可以只实现 `Runnable` 接口。

### 取消任务

您可以通过在提交任务时返回的 `Future` 上调用 `cancel()` 方法来取消提交给 Java `ExecutorService` 的任务（`Runnable` 或 `Callable`）。仅当任务尚未开始执行时才可以取消任务。这是通过调用 `Future.cancel()` 方法取消任务的示例：

```java
future.cancel();
```

## ExecutorService 关闭

使用完 Java`ExecutorService` 后，应将其关闭，这样线程就不会继续运行。如果您的应用程序是通过 `main()` 方法启动的，而主线程退出了应用程序，那么如果您的应用程序中有活动的 `ExexutorService`，则该应用程序将继续运行。该 `ExecutorService` 中的活动线程可阻止 JVM 关闭。

### shutdown()

要终止 `ExecutorService` 内部的线程，请调用其 `Shutdown()` 方法。`ExecutorService` 不会立即关闭，但是将不再接受新任务，并且一旦所有线程都完成了当前任务，`ExecutorService` 就会关闭。执行所有在调用 `Shutdown()` 之前提交给 `ExecutorService` 的任务。这是执行 Java `ExecutorService shutdown` 的示例：

```java
executorService.shutdown();
```

### shutdownNow()

如果您想立即关闭 `ExecutorService`，可以调用 `shutdownNow()` 方法。这将尝试立即停止所有正在执行的任务，并跳过所有已提交但未处理的任务。不能保证执行任务。也许他们停下来，也许执行到最后。这是尽力而为的尝试。这是调用 `ExecutorService``shutdownNow` 的示例：

```java
executorService.shutdownNow();
```

### awaitTermination()

`ExecutorService的awaitTermination()` 方法将阻塞调用它的线程，直到 `ExecutorService` 完全关闭或发生给定的超时为止。通常在调用 `shutdown()` 或 `shutdownNow()` 之后调用 `awaitTermination()` 方法。这是调用 `ExecutorService``awaitTermination()` 的示例：

```java
executorService.shutdown();

executorService.awaitTermination();
```

# Java Callable

Java `Callable` 接口， `java.util.concurrent.Callable`，表示可以被一个单独的线程执行的一个异步任务。比如，可以将一个 `Callable` 对象提交给 [Java ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) 以便随后异步执行它。

## Java Callable 接口定义

Java `Callable` 接口非常简单。它只包含一个方法 `call()`。下面是该接口的样子：

```java
public interface Callable<V> {

    V call() throws Exception;

}
```

调用 `call()` 方法以执行异步任务。该方法会返回一个结果。如果任务被异步执行，则结果通常将会通过一个 [Java Future](http://tutorials.jenkov.com/java-util-concurrent/java-future.html) 反向传播给任务的创建者。这是将 `Callable` 提交给 `ExecutorService` 进行并发执行的情况。

 `call()` 方法也会抛出 `Exception`，如果任务执行失败。

## 实现 Callable

下面是 `Callable` 接口的一个简单实现：

```java
public class MyCallable implements Callable<String> {

    @Override
    public String call() throws Exception {
        return String.valueOf(System.currentTimeMillis());
    }
}
```

此实现非常简单。它携带设定为 [Java String](http://tutorials.jenkov.com/java/strings.html) 的范型类型。`call()` 方法的结果将返回一个 `String` 。例子中 `call()` 方法实现返回一个字符串表示当前时间的毫秒数。在真实的应用中，任务可能会是更大、更复杂的一系列操作的集合。

IO 操作（例如从磁盘或网络读取或写入磁盘或网络）通常是可以同时执行的任务的理想选择。IO 操作在读取和写入数据块之间通常需要很长的等待时间。通过在单独的线程中执行此类任务，可以避免不必要地阻塞主应用程序线程。

## Callable vs. Runnable

Java `Callable` 接口类似于 Java `Runnable` 接口，因为它们都代表一个任务，该任务打算由一个单独的线程同时执行。

Java `Callable` 与 `Runnable` 的不同之处在于 `Runnable` 接口的 `run()` 方法不返回值，并且它不能抛出已检查的异常（仅 `RuntimeException`）。

另外，`Runnable` 最初是为长时间运行的并发执行而设计的，例如同时运行网络服务器，或监视目录中是否有新文件。 `Callable` 接口更适合一次性任务返回单个结果。

# Java Future

Java *Future*，即 `java.util.concurrent.Future`，表示异步计算的结果。创建异步任务后，将返回 Java `Future` 对象。这个 `Future` 对象用作异步任务结果的引用。异步任务完成后，可以通过启动任务时返回的 `Future` 对象访问结果。

Java 的一些内置并发实用程序，例如 [Java ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html)，从其某些方法中返回 Java `Future` 对象。对于 `ExecutorService`，当您提交一个 `Callable` 使其并发（异步）执行时，它将返回一个 `Future`。

## Java Future 接口定义

为了理解 Java `Future` 接口如何工作，下面是简要的接口定义：

```java
public interface Future<V> {
    boolean cancel(boolean mayInterruptIfRunning)
    V       get();
    V       get(long timeout, TimeUnit unit);
    boolean isCancelled();
    boolean isDone();
}
```

接下来将逐个介绍这些方法——不过，如你所见， Java `Future` 接口并没有多么复杂。

## 从 Future 获取结果

如前所述，Java `Future` 表示异步任务的结果。为了获得结果，您可以调用 `Future` 上的两个 `get()` 方法之一。 `get()` 方法都返回一个 `Object`，但是返回类型也可以是范型返回类型（意味着特定类的对象，而不仅仅是 `Object`）。这是一个通过 Java `Future` 的 `get()` 方法获得结果的示例：

```java
Future future = ... // get Future by starting async task

// do something else, until ready to check result via Future

// get result from Future
try {
    Object result = future.get();
} catch (InterruptedException e) {
    e.printStackTrace();
} catch (ExecutionException e) {
    e.printStackTrace();
}
```

如果你在异步任务执行完成之前调用 `get()` 方法，该方法将会阻塞直到结果已经准备好。

有一个 `get()` 方法的版本，它可以在经过一定时间后超时，您可以通过方法参数来指定超时时间。这是调用该 `get()` 版本的示例：

```java
try {
    Object result =
        future.get(1000, TimeUnit.MILLISECONDS);
} catch (InterruptedException e) {

} catch (ExecutionException e) {

} catch (TimeoutException e) {
    // thrown if timeout time interval passes
    // before a result is available.
}
```

上面的示例最多等待 1000 毫秒，以便结果在 `Future`  中可用。如果在 1000 毫秒内没有结果可用，则抛出 `TimeoutException`。

## 通过 Future cancel() 取消任务

您可以通过调用 `Future` `cancel()` 方法来取消由 Java `Future` 实例表示的异步任务。必须实现异步任务执行以支持取消。没有这样的支持，调用 `cancel()` 将无效。这是通过 Java `Future` `cancel()` 方法取消任务的示例：

```java
future.cancel();
```

## 检查任务是否完成

通过调用 `Future` `isDone()` 方法，你可以检查异步任务是否完成（结果可用）。下面是示例：

```java
Future future = ... // Get Future from somewhere

if(future.isDone()) {
    Object result = future.get();
} else {
    // do something else
}
```

## 检查任务是否取消

还可以检查由 Java `Future` 表示的异步任务是否被取消。您可以通过调用 `Future` `isCancelled()` 方法进行检查。这是检查任务是否被取消的示例：

```java
Future future = ... // get Future from somewhere

if(future.isCancelled()) {

} else {

}
```

# ThreadPoolExecutor

`java.util.concurrent.ThreadPoolExecutor` 是 [`ExecutorService`](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) 接口的一个实现。 `ThreadPoolExecutor` 使用它内部池化的多个线程中的一个执行给定的任务（`Callable` 或者 `Runnable`）。

包含在 `ThreadPoolExecutor` 内部的线程池可以包含大量的线程。线程池中的线程数量由以下参数确定：

- `corePoolSize`
- `maximumPoolSize`

如果在将任务委派给线程池时在线程池中创建的线程数少于 `corePoolSize`，则即使该池中存在空闲线程，也会创建一个新线程。

如果内部任务队列已满，并且正在运行 `corePoolSize` 个线程或更多线程，但正在运行的线程数少于 `maximumPoolSize`，那么将创建一个新线程来执行任务。

下面是 `ThreadPoolExecutor` 原理示意图：

| ![A ThreadPoolExecutor.](http://tutorials.jenkov.com/images/java-concurrency-utils/thread-pool-executor.png) |
| ------------------------------------------------------------ |
| **一个 ThreadPoolExecutor**                                  |

## 创建 ThreadPoolExecutor

 `ThreadPoolExecutor` 有好几种可用的构造方法。比如：

```java
int  corePoolSize  =    5;
int  maxPoolSize   =   10;
long keepAliveTime = 5000;

ExecutorService threadPoolExecutor =
        new ThreadPoolExecutor(
                corePoolSize,
                maxPoolSize,
                keepAliveTime,
                TimeUnit.MILLISECONDS,
                new LinkedBlockingQueue<Runnable>()
                );
```

但是，除非您需要为 `ThreadPoolExecutor` 明确指定所有这些参数，否则通常使用 `java.util.concurrent.Executors` 类中的工厂方法之一更容易，如 [ExecutorService](http ：//tutorials.jenkov.com/java-util-concurrent/executorservice.html) 中所述。

# ScheduledExecutorService

 `java.util.concurrent.ScheduledExecutorService` 是一个 [`ExecutorService`](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) ，可以调度任务在一段延迟时间之后执行，或者按照固定时间间隔重复执行任务。任务将由工作者线程异步执行，而不是由将任务分派给 `ScheduledExecutorService` 的线程执行。

## ScheduledExecutorService 示例

这是一个简单的 `ScheduledExecutorService` 示例：

```java
ScheduledExecutorService scheduledExecutorService =
        Executors.newScheduledThreadPool(5);

ScheduledFuture scheduledFuture =
    scheduledExecutorService.schedule(new Callable() {
        public Object call() throws Exception {
            System.out.println("Executed!");
            return "Called!";
        }
    },
    5,
    TimeUnit.SECONDS);
```

首先创建一个带有 5 个线程的 `ScheduledExecutorService`。然后，创建 `Callable` 接口的匿名实现，并将其传递给 `schedule()` 方法。最后两个参数指定 `Callable` 应在 5 秒钟后执行。

## ScheduledExecutorService 实现

由于 `ScheduledExecutorService` 是一个接口，你需要使用位于 `java.util.concurrent` 包中的接口实现。 `ScheduledExecutorService` 的一个实现如下：

- ScheduledThreadPoolExecutor

## 创建 ScheduledExecutorService

如何创建 `ScheduledExecutorService` 取决于你使用的实现。不过，你也可以使用 `Executors` 工厂类创建 `ScheduledExecutorService` 实例。示例如下：

```java
ScheduledExecutorService scheduledExecutorService = Executors.newScheduledThreadPool(5);
```

## ScheduledExecutorService 使用

一旦创建了 `ScheduledExecutorService` 就可以通过调用它的方法来使用它：

- schedule (Callable task, long delay, TimeUnit timeunit)
- schedule (Runnable task, long delay, TimeUnit timeunit)
- scheduleAtFixedRate (Runnable, long initialDelay, long period, TimeUnit timeunit)
- scheduleWithFixedDelay (Runnable, long initialDelay, long period, TimeUnit timeunit)

下面简要介绍这些方法。

### schedule (Callable task, long delay, TimeUnit timeunit)

此方法在给定的延迟后安排给定的 `Callable` 执行。

该方法返回一个 `ScheduledFuture`，可用于在开始执行之前取消任务，或在执行后获取结果。

这是一个例子：

```java
ScheduledExecutorService scheduledExecutorService =
        Executors.newScheduledThreadPool(5);

ScheduledFuture scheduledFuture =
    scheduledExecutorService.schedule(new Callable() {
        public Object call() throws Exception {
            System.out.println("Executed!");
            return "Called!";
        }
    },
    5,
    TimeUnit.SECONDS);

System.out.println("result = " + scheduledFuture.get());

scheduledExecutorService.shutdown();
```

这个例子输出

```
Executed!
result = Called!
```

### schedule (Runnable task, long delay, TimeUnit timeunit)

该方法的工作方式类似于以 `Callable` 作为参数的方法版本，除了 `Runnable` 无法返回值之外。因此 `ScheduledFuture.get()` 方法在任务完成时返回 `null`。

### scheduleAtFixedRate (Runnable, long initialDelay, long period, TimeUnit timeunit)

此方法调度要定期执行的任务。该任务在 `initialDelay` 之后第一次执行，然后在每次 `period` 到期时重复执行。

如果给定任务的任何执行均引发异常，则该任务将不再执行。如果没有抛出异常，则该任务将继续执行，直到关闭 `ScheduledExecutorService` 为止。

如果任务执行的时间比调度执行时间间更长，则下一次执行将在当前执行完成后开始。被调度的任务一次不会同时由多个线程执行。

### scheduleWithFixedDelay (Runnable, long initialDelay, long period, TimeUnit timeunit)

该方法非常类似于 `scheduleAtFixedRate()`，除了 `period` 的解释不同。

在 `scheduleAtFixedRate()` 方法中，`period` 被解释为上一次执行开始到下一次执行开始之间的时间间隔。

但是，在此方法中，`period` 被解释为上一次执行的“结束”到下一次开始的时间间隔。因此，延迟是在完成执行之间，而不是在执行开始之间。

## ScheduledExecutorService 关闭

就像 `ExecutorService` 一样，`ScheduledExecutorService` 在使用完毕后也需要关闭。如果没有，即使所有其他线程都已关闭，它也将保持 JVM 运行。

您可以使用从 `ExecutorService` 接口继承的 `Shutdown()` 或 `ShutdownNow()` 方法来关闭 `ScheduledExecutorService`。有关更多信息，请参见 [ExecutorService Shutdown](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html#executorservice-shutdown) 部分。

# 使用 ForkJoinPool 的 Java Fork 和 Join 

 Java 7 添加了 `ForkJoinPool` 。 `ForkJoinPool` 类似于 [Java ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) ，除了一个不同点。`ForkJoinPool` 使得将任务分解为若干个粒度更小的任务并同样提交给 `ForkJoinPool` 执行变的容易。只要可以拆分任务，任务就可以继续将其工作拆分为较小的子任务。听起来可能有点抽象，所以在此 fork 和 join 教程中，我将解释 `ForkJoinPool` 的工作方式以及拆分任务的工作方式。

## Fork 和 Join 解释

在介绍 `ForkJoinPool` 之前，我先解释一下普遍意义上的 fork 和 join 工作原理。

fork 和 join 原理包括两个步骤，这些步骤以递归方式执行。这两个步骤是 fork 步骤和 join 步骤。

### Fork

使用 fork 和 join 原理的任务可以将自身分解为多干个可以并发执行的子任务。如下图所示：

![](http://tutorials.jenkov.com/images/java-concurrency-utils/java-fork-and-join-1.png)

通过将任务分解为若干个子任务，每个子任务都可以在不同的 CPU 上，或者同一个 CPU 上不同线程中并行执行。

如果给定任务的工作足够大，则任务只能将自身拆分为子任务。将任务拆分为子任务会产生开销，因此对于少量工作，此开销可能会大于同时执行子任务所实现的加速。

何时适合将任务分解到子任务中的合理时限也称为阈值。不同的任务合理的阈值各不相同。这在很大程度上取决于所完成的工作。

### Join

当一个任务已经被分解为若干子任务，则该任务会等待所有子任务全部执行完成。

一旦所有的子任务都执行完成，任务将会将所有的子结果合并为一个结果。如下图所示：

![](http://tutorials.jenkov.com/images/java-concurrency-utils/java-fork-and-join-2.png)

当然，并非所有类型的任务都可能返回结果。如果任务未返回结果，则任务仅等待其子任务完成。这样就不会进行结果合并。

## ForkJoinPool

`ForkJoinPool` 是一种特殊的线程池，被设计为完美适配 fork-and-join 任务分解。 `ForkJoinPool` 位于 `java.util.concurrent` 包中，完整类名 `java.util.concurrent.ForkJoinPool`。

### 创建 ForkJoinPool

你可以使用构造器创建 `ForkJoinPool`。你可以将所有的并行度作为 `ForkJoinPool` 构造函数的参数，并行度表示要在传递给 `ForkJoinPool` 的任务同时使用多少个线程或 CPU。这是一个 `ForkJoinPool` 创建示例：

```java
ForkJoinPool forkJoinPool = new ForkJoinPool(4);
```

本示例创建一个并行度水平为 4 的 `ForkJoinPool` 。

### 向 ForkJoinPool 提交任务

您将任务提交给 `ForkJoinPool` 的方式类似于将任务提交给 `ExecutorService` 的方式。您可以提交两种类型的任务。一个不返回任何结果的任务（一个“action”），一个返回结果的任务（一个“task”）。这两种任务由 `RecursiveAction` 和 `RecursiveTask` 类表示。如何使用这两项任务以及如何提交这些任务将在以下各节中介绍。

## RecursiveAction

`RecursiveAction` 是一种不返回任何值的任务。它只是执行某些工作，比如，将数据写入磁盘然后退出。

`RecursiveAction` 可能仍然需要将它的工作分解为多哥分片，以便可以使用各自独立的线程或者 CPU 执行。

你可以通过实现子类来实现 `RecursiveAction` 。下面是 `RecursiveAction` 的例子：

```java
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.RecursiveAction;

public class MyRecursiveAction extends RecursiveAction {

    private long workLoad = 0;

    public MyRecursiveAction(long workLoad) {
        this.workLoad = workLoad;
    }

    @Override
    protected void compute() {

        //if work is above threshold, break tasks up into smaller tasks
        if(this.workLoad > 16) {
            System.out.println("Splitting workLoad : " + this.workLoad);

            List<MyRecursiveAction> subtasks =
                new ArrayList<MyRecursiveAction>();

            subtasks.addAll(createSubtasks());

            for(RecursiveAction subtask : subtasks){
                subtask.fork();
            }

        } else {
            System.out.println("Doing workLoad myself: " + this.workLoad);
        }
    }

    private List<MyRecursiveAction> createSubtasks() {
        List<MyRecursiveAction> subtasks =
            new ArrayList<MyRecursiveAction>();

        MyRecursiveAction subtask1 = new MyRecursiveAction(this.workLoad / 2);
        MyRecursiveAction subtask2 = new MyRecursiveAction(this.workLoad / 2);

        subtasks.add(subtask1);
        subtasks.add(subtask2);

        return subtasks;
    }

}
```

这个例子非常简化。`MyRecursiveAction` 只是将虚构的 `workLoad` 作为其构造函数的参数。如果 `workLoad` 高于某个阈值，则将工作拆分为多个子任务，这些子任务也调度执行（通过子任务的 `.fork()` 方法）。如果 `workLoad` 低于某个阈值，则该工作由 `MyRecursiveAction` 本身执行。

您可以像这样安排 `MyRecursiveAction` 执行：

```java
MyRecursiveAction myRecursiveAction = new MyRecursiveAction(24);

forkJoinPool.invoke(myRecursiveAction);
```

## RecursiveTask

 `RecursiveTask` 是一种返回结果的任务。它可以将任务分解为若干更小的任务，执行完成之后将所有小任务的结果合并为集合式结果。这种分解合并可能发生在多个层面。下面是一个 `RecursiveTask` 示例：

```java
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.RecursiveTask;
    
    
public class MyRecursiveTask extends RecursiveTask<Long> {

    private long workLoad = 0;

    public MyRecursiveTask(long workLoad) {
        this.workLoad = workLoad;
    }

    protected Long compute() {

        //if work is above threshold, break tasks up into smaller tasks
        if(this.workLoad > 16) {
            System.out.println("Splitting workLoad : " + this.workLoad);

            List<MyRecursiveTask> subtasks =
                new ArrayList<MyRecursiveTask>();
            subtasks.addAll(createSubtasks());

            for(MyRecursiveTask subtask : subtasks){
                subtask.fork();
            }

            long result = 0;
            for(MyRecursiveTask subtask : subtasks) {
                result += subtask.join();
            }
            return result;

        } else {
            System.out.println("Doing workLoad myself: " + this.workLoad);
            return workLoad * 3;
        }
    }

    private List<MyRecursiveTask> createSubtasks() {
        List<MyRecursiveTask> subtasks =
        new ArrayList<MyRecursiveTask>();

        MyRecursiveTask subtask1 = new MyRecursiveTask(this.workLoad / 2);
        MyRecursiveTask subtask2 = new MyRecursiveTask(this.workLoad / 2);

        subtasks.add(subtask1);
        subtasks.add(subtask2);

        return subtasks;
    }
}
```

这个例子类似于 `RecursiveAction` 示例，唯一不同是它返回一个结果。 `MyRecursiveTask` 扩展了 `RecursiveTask<Long>` ，这就意味着任务返回的结果是一个 `Long` 。

 `MyRecursiveTask` 示例也将任务分解为子任务，然后通过使用子任务的 `fork()` 方法调度执行。

另外，此示例然后通过调用每个子任务的 `join()` 方法接收每个子任务返回的结果。子任务结果将合并为更大的结果，然后将其返回。这种子任务结果的合并可能会针对多个递归级别进行递归发生。

您可以像这样调度 `RecursiveTask`：

```java
MyRecursiveTask myRecursiveTask = new MyRecursiveTask(128);

long mergedResult = forkJoinPool.invoke(myRecursiveTask);

System.out.println("mergedResult = " + mergedResult);    
```

注意如何通过调用 `ForkJoinPool.invoke()` 方法获取最终结果。

## ForkJoinPool 用户体验

似乎并不是每个人都对 Java 7 中的新 `ForkJoinPool` 感到同样满意。在搜索有关 `ForkJoinPool` 的经验和意见时，我遇到了以下批评：

[A Java Fork-Join Calamity](http://coopsoft.com/ar/CalamityArticle.html)

如果你打算在你的项目中使用 `ForkJoinPool` ，这就值得一读。

# Lock

`java.util.concurrent.locks.Lock` 是一种线程同步机制，类似于 `synchronized` 块。不过，`Lock` 相比于同步块更加灵活和复杂。

顺便说一下，在我的 [Java Concurrency tutorial](http://tutorials.jenkov.com/java-concurrency/index.html) 中描述了如何实现你自己的锁，参考 [Locks](http://tutorials.jenkov.com/java-concurrency/locks.html) 了解更多细节。

## Java Lock 示例

由于 `Lock` 是一个接口，你需要在应用中使用它的某个实现。下面是个简单的例子：

```java
Lock lock = new ReentrantLock();

lock.lock();

//critical section

lock.unlock();
```

首先创建一个 `Lock`。然后调用它的 `lock()` 方法。现在，`Lock` 实例已被锁定。任何其他调用 `lock()` 的线程都将被阻塞，直到锁定该锁的线程调用 `unlock()`。最后调用 `unlock()`，则 `Lock` 现在被解锁，以便其他线程可以锁定它。

## Java Lock 实现

`java.util.concurrent.locks` 包中包含以下 `Lock` 接口实现：

- ReentrantLock

## Locks 与同步块的主要差异

`Lock` 与同步块之间的主要差异：

- 同步块无法保证等待进入的同步块的线程最终的访问顺序。
- 您不能将任何参数传递给同步块。因此，无法对同步块设置超时。
- 同步块必须完整包含在单个方法中。 `Lock` 的 `lock()` 和 `unlock()` 调用可以分开存在于不同的方法中。

## Lock 方法

 `Lock` 接口拥有以下重要方法：

- lock()
- lockInterruptibly()
- tryLock()
- tryLock(long timeout, TimeUnit timeUnit)
- unlock()

如果可能的话，`lock()` 方法会锁定 `Lock` 实例。如果 `Lock` 实例已经被锁定，则调用 `lock()` 的线程将被阻塞，直到 `Lock` 实例被解锁。

除非调用该方法的线程已被中断，否则 `lockInruptible()` 方法将锁定 `Lock`。另外，如果某个线程被阻塞，等待通过此方法锁定 `Lock`，如果该线程被中断，则退出此方法调用。

`tryLock()` 方法尝试立即锁定 `Lock` 实例。如果锁定成功，则返回 `true`，如果已经锁定 `Lock`，则返回 `false`。此方法永远不会阻塞。

`tryLock(long timeout, TimeUnit timeUnit)` 的工作方式与 `tryLock()` 方法类似，只是它在放弃给定的锁之前尝试等待给定的超时时间。

`unlock()` 方法解锁 `Lock` 实例。通常。`Lock` 实现仅允许锁定了 `Lock` 的线程调用此方法。其他调用此方法的线程可能会导致未经检查的异常（`RuntimeException`）。

# ReadWriteLock

`java.util.concurrent.locks.ReadWriteLock` 是一种高级线程锁定机制。同一时刻，它允许多个线程读取某个资源，但只能有一个线程写入该资源。

基本想法是，多个线程可以从共享资源读取而不会引起并发错误。并发错误首先发生在对共享资源的读写同时发生，或者并发发生多个写入时。

在本文中，我仅介绍 Java 的内置 `ReadWriteLock`。如果您想阅读更多有关实现 `ReadWriteLock` 的理论，请参考我的 Java 并发教程中 [Read Write Locks](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) 部分。

## ReadWriteLock 锁定规则

允许线程锁定 `ReadWriteLock` 以读取或写入受保护资源的规则如下：

| **Read Lock**  | 如果没有线程锁定`ReadWriteLock`进行写操作，并且没有线程请求写锁（但尚未获得写锁）。因此，多个线程可以锁定该锁以进行读取。 |
| -------------- | ------------------------------------------------------------ |
| **Write Lock** | **如果没有线程正在读取或写入。因此，一次只能有一个线程可以锁定该锁以进行写入。** |

## ReadWriteLock 实现

`ReadWriteLock` 是一个接口，因此，你需要使用它的一个实现。

`java.util.concurrent.locks` 包含下列 `ReadWriteLock` 实现：

- ReentrantReadWriteLock

## ReadWriteLock 代码示例

下面的例子展示了如何创建 `ReadWriteLock` 以及如何为了读取或者写入而锁定它：

```java
ReadWriteLock readWriteLock = new ReentrantReadWriteLock();


readWriteLock.readLock().lock();

    // multiple readers can enter this section
    // if not locked for writing, and not writers waiting
    // to lock for writing.

readWriteLock.readLock().unlock();


readWriteLock.writeLock().lock();

    // only one writer can enter this section,
    // and only if no threads are currently reading.

readWriteLock.writeLock().unlock();
```

注意 `ReadWriteLock` 实际上如何在内部维护两个 `Lock` 实例，分别负责守卫读操纵和写操作。

# AtomicBoolean

`AtomicBoolean` 类向你提供了一个 `boolean` 变量，该变量可以原子地读写。同时它还拥有其他一些高级的原子性操作，比如 `compareAndSet()`。`AtomicBoolean` 类位于 `java.util.concurrent.atomic` 包中，完整类名是 `java.util.concurrent.atomic.AtomicBoolean` 。本教程介绍的 `AtomicBoolean` 是 Java 8 版本，不过该类最初是 Java 5 版本加入的。

`AtomicBoolean` 类设计的背后动机在我的 Java 并发教程的 [Compare and Swap](http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html) 部分做了解释。

## 创建 AtomicBoolean

如下创建 `AtomicBoolean` ：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean();
```

这个例子使用值 `false` 创建了一个新的 `AtomicBoolean` 。

如果你需要为 `AtomicBoolean` 实例显式设定初始值，你可以向 `AtomicBoolean` 构造器传递初始值参数：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);
```

## 获取 AtomicBoolean 的值

你可以使用 `get()` 方法获取 `AtomicBoolean` 的值：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);

boolean value = atomicBoolean.get();
```

代码执行之后 `value` 变量将包含 `true`。

## 设定 AtomicBoolean 的值

你可以使用 `set()` 方法设定 `AtomicBoolean` 的值：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);

atomicBoolean.set(false);
```

代码执行之后 `AtomicBoolean` 变量将包含 `false`。

## 替换 AtomicBoolean 的值

你可以使用 `getAndSet()` 方法替换 `AtomicBoolean` 的值。`getAndSet()` 方法返回 `AtomicBoolean` 的当前值，并为其设置一个新值：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);

boolean oldValue = atomicBoolean.getAndSet(false);
```

执行完此代码后，`oldValue` 变量将包含值 `true`，而 `AtomicBoolean` 实例将包含值 `false`。该代码有效地将 `AtomicBoolean` 的当前值 `true` 交换为 `false` 。

## 比较并替换 AtomicBoolean 的值

`compareAndSet()` 方法允许您将 `AtomicBoolean` 的当前值与期望值进行比较，如果当前值等于期望值，则可以在 `AtomicBoolean` 上设置一个新值。`compareAndSet()` 方法是原子的，因此只有一个线程可以同时执行它。因此，`compareAndSet()` 方法可用于实现类似于锁的简单的同步器。

这是一个 `compareAndSet()` 示例：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);

boolean expectedValue = true;
boolean newValue      = false;

boolean wasNewValueSet = atomicBoolean.compareAndSet(
    expectedValue, newValue);
```

本示例将 `AtomicBoolean` 的当前值与 `true` 进行比较，如果两个值相等，则将 `AtomicBoolean` 的新值设置为 `false`。

# AtomicInteger

`AtomicInteger` 类为您提供了一个 `int` 变量，该变量可以原子方式读写，并且还包含高级原子操作，如 `compareAndSet()`。`AtomicInteger` 类位于 `java.util.concurrent.atomic` 包中，因此完整的类名是 `java.util.concurrent.atomic.AtomicInteger`。本文描述了 Java 8 中的 `AtomicInteger` 版本，但第一个版本是添加到 Java 5 中的。

`AtomicInteger` 设计背后的动机在我的并发教程的 [Compare and Swap](http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html) 部分中做了解释。

## 创建 AtomicInteger

如下创建 `AtomicInteger` ：

```java
AtomicInteger atomicInteger = new AtomicInteger();
```

这个例子使用初始值 `0` 创建了一个 `AtomicInteger`。

如果你想要使用初始值创建 `AtomicInteger`，可以这样做：

```java
AtomicInteger atomicInteger = new AtomicInteger(123);
```

此示例将值 `123` 作为参数传递给 `AtomicInteger` 构造函数，该构造函数将 `AtomicInteger` 实例的初始值设置为 `123`。

## 获取 AtomicInteger 的值

你可以通过 `get()` 方法获取 `AtomicInteger` 实例的值。如下所示：

```java
AtomicInteger atomicInteger = new AtomicInteger(123);

int theValue = atomicInteger.get();
```

## 设定 AtomicInteger 的值

你可以通过 `set()` 方法设定 `AtomicInteger` 实例的值。如下所示：

```java
AtomicInteger atomicInteger = new AtomicInteger(123);

atomicInteger.set(234);
```

例子使用初始值 `123` 创建一个 `AtomicInteger` ，下一行代码将其值设定为 `234`。

## 比较并替换 AtomicInteger 的值

`AtomicInteger` 类还具有原子的 `compareAndSet()` 方法。该方法将 `AtomicInteger` 实例的当前值与期望值进行比较，如果两个值相等，则为 `AtomicInteger` 实例设置一个新值。这是一个 `AtomicInteger.compareAndSet()` 示例：

```java
AtomicInteger atomicInteger = new AtomicInteger(123);

int expectedValue = 123;
int newValue      = 234;
atomicInteger.compareAndSet(expectedValue, newValue);
```

此示例首先创建一个初始值为 `123` 的 `AtomicInteger` 实例。然后，它将 `AtomicInteger` 的值与期望值 `123` 进行比较，如果它们相等，则 `AtomicInteger` 的新值将变为 `234`。

## 增加 AtomicInteger 的值

`AtomicInteger` 类包含一些方法，可用于将值添加到 `AtomicInteger` 并返回其值。这些方法是：

- `addAndGet()`
- `getAndAdd()`
- `getAndIncrement()`
- `incrementAndGet()`

第一个方法 `addAndGet()` 将一个数字添加到 `AtomicInteger` 中，并在添加后返回其值。第二种方法 `getAndAdd()` 也向 `AtomicInteger` 添加一个数字，但返回 `AtomicInteger` 在添加之前的值。应该使用这两种方法中的哪一种取决于您的场景。示例如下：

```java
AtomicInteger atomicInteger = new AtomicInteger();


System.out.println(atomicInteger.getAndAdd(10));
System.out.println(atomicInteger.addAndGet(10));
```

本示例将打印出值 `0` 和 `20`。首先，该示例在添加 `10` 之前获取 `AtomicInteger` 的值。其执行加法前的值为 `0`。然后，该示例将 `10` 加到 `AtomicInteger` 中，并获得执行加法后的值。现在的值为 `20`。

您也可以通过这两种方法在 `AtomicInteger` 中添加负数。结果实际上是相减。

方法 `getAndIncrement()` 和 `incrementAndGet()` 的工作方式与 `getAndAdd()` 和 `addAndGet()` 的相同，只是将 `AtomicInteger` 的值加 `1`。

## 减少 AtomicInteger 的值

`AtomicInteger` 类还包含一些原子性的从 `AtomicInteger` 值中减去值的方法。这些方法是：

- `decrementAndGet()`
- `getAndDecrement()`

`decrementAndGet()` 从 `AtomicInteger` 值中减去 `1`，并在减法后返回其值。`getAndDecrement()` 也从 `AtomicInteger` 值中减去 `1`，但返回减法之前 `AtomicInteger` 的值。

