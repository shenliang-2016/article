#### 并发集合

`java.util.concurrent`包中包含许多Java Collections Framework的附加内容。很容易通过提供的集合接口进行分类：

- [`BlockingQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BlockingQueue.html) 定义先进先出数据结构，当您尝试添加元素到满队列或从空队列中检索时，该数据结构会阻塞或超时。
- [`ConcurrentMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentMap.html) 是`java.util.Map`的子接口，它定义了有用的原子操作。仅当键存在时，这些操作才会删除或替换键值对，或仅在键不存在时才添加键值对。这些操作原子化有助于避免同步。`ConcurrentMap`的标准通用实现是 [`ConcurrentHashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html) ，它是 [`HashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) 的并发模拟。
- [`ConcurrentNavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentNavigableMap.html) 是`ConcurrentMap`的子接口，支持近似匹配。`ConcurrentNavigableMap`的标准通用实现是 [`ConcurrentSkipListMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentSkipListMap.html) ，它是 [`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) 的并发模拟。

所有这些集合通过定义将对象添加到集合的操作与访问或删除该对象的后续操作之间的*happens-before*关系来帮助避免[内存一致性错误](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html) 。

#### 原子变量

[`java.util.concurrent.atomic`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/package-summary.html) 包定义了支持单个变量的原子操作的类。所有类都有`get`和`set`方法，类似于对`volatile`变量的读写操作。也就是说，一个`set`与相关变量的任何后续`get`具有*happens-before*关系。原子`compareAndSet`方法也具有这些内存一致性功能，适用于整数原子变量的简单原子算法也是如此。

要查看如何使用此包，让我们返回我们最初用于演示线程干扰的 [`Counter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Counter.java) 类：

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

使计数器免受线程干扰的一种方法是使其方法同步，如在 [`SynchronizedCounter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SynchronizedCounter.java) 中：

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

对于这个简单的类，同步是可接受的解决方案。但对于更复杂的类，我们可能希望避免不必要的同步对活动的影响。使用`AtomicInteger`替换`int`字段允许我们在不使用同步的情况下防止线程干扰，如在 [`AtomicCounter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/AtomicCounter.java) 中：

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

#### 并发随机数

在JDK 7中，[`java.util.concurrent`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html) 包含一个类 [`ThreadLocalRandom`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadLocalRandom.html) ，用于期望使用来自多个线程或`ForkJoinTasks`的随机数的应用程序。

对于并发访问，使用`ThreadLocalRandom`而不是`Math.random()`可以减少争用，并最终提高性能。

您需要做的就是调用`ThreadLocalRandom.current()`，然后调用其中一个方法来检索随机数。 这是一个例子：

```java
int r = ThreadLocalRandom.current() .nextInt(4, 77);
```

### 扩展阅读

- *Concurrent Programming in Java: Design Principles and Pattern (2nd Edition)* by Doug Lea. A comprehensive work by a leading expert, who's also the architect of the Java platform's concurrency framework.
- *Java Concurrency in Practice* by Brian Goetz, Tim Peierls, Joshua Bloch, Joseph Bowbeer, David Holmes, and Doug Lea. A practical guide designed to be accessible to the novice.
- *Effective Java Programming Language Guide (2nd Edition)* by Joshua Bloch. Though this is a general programming guide, its chapter on threads contains essential "best practices" for concurrent programming.
- *Concurrency: State Models & Java Programs (2nd Edition)*, by Jeff Magee and Jeff Kramer. An introduction to concurrent programming through a combination of modeling and practical examples.
- *Java Concurrent Animated:* Animations that show usage of concurrency features.

