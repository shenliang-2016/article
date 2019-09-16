## 同步

线程主要通过共享对字段的访问和引用字段引用的对象进行通信。这种通信形式非常有效，但可能产生两种错误：*线程干扰*和*内存一致性错误*。防止这些错误所需的工具是 *synchronization*。

但是，同步可能会引入*线程争用*，当两个或多个线程同时尝试访问同一资源时会导致 Java 运行时更慢地执行一个或多个线程，甚至暂停执行。[Starvation and livelock](https://docs.oracle.com/javase/tutorial/essential/concurrency/starvelive.html) 是线程争用的形式。有关详细信息，请参阅 [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 。

本节涵盖以下主题：

- [线程干扰](https://docs.oracle.com/javase/tutorial/essential/concurrency/interfere.html) 描述了当多个线程访问共享数据时如何引入错误。
- [内存一致性错误](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html) 描述由共享内存的不一致视图导致的错误。
- [同步方法](https://docs.oracle.com/javase/tutorial/essential/concurrency/syncmeth.html) 描述了一个简单的习惯用法，可以有效地防止线程干扰和内存一致性错误。
- [隐式锁和同步](https://docs.oracle.com/javase/tutorial/essential/concurrency/locksync.html) 描述了一种更通用的同步习惯用法，并描述了同步是如何基于隐式锁工作的。
- [原子访问](https://docs.oracle.com/javase/tutorial/essential/concurrency/atomic.html) 讨论不能被其他线程干扰的操作的一般概念。

### 线程干扰

考虑下面的 [`Counter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Counter.java) ：

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

`Counter` 的设计是为了每次调用 `increment` 都会将1加到 `c`，每次调用 `decrement` 都会从 `c` 中减去1。但是，如果从多个线程引用 `Counter` 对象，则线程之间的干扰可能会阻止这种情况按预期发生。

当两个操作在不同的线程中运行但是对相同的数据进行操作时会发生干扰*interleave*。这意味着这两个操作由多个步骤组成，并且步骤序列重叠。

对于 `Counter` 实例的操作似乎不可能交错，因为 `c` 上的两个操作都是单个简单的语句。但是，即使是简单的语句也可以由虚拟机转换为多个步骤。我们不会检查虚拟机采取的具体步骤 - 只需知道单个表达式 `c++` 可以分解为三个步骤：

1. 检索 `c` 的当前值。
2. 将检索值增加1。
3. 将递增的值存回 `c`。

表达式 `c--` 可以以相同的方式分解，除了第二步是减少而不是增量。

假设线程 A 调用 `increment` ，在大约同一时间线程 B 调用 `decrement`。如果 `c` 的初始值为 `0`，则它们的交错动作可能遵循以下顺序：

1. 线程A：检索 `c`。

2. 线程B：检索 `c`。

3. 线程A：增加检索值；结果是1。

4. 线程B：减少检索值；结果是-1。

5. 线程A：将结果存储在 `c` 中；`c` 现在是1。

6. 线程B：将结果存储在 `c` 中；`c` 现在是-1。

线程 A 的结果丢失，被线程 B 覆盖。这种特殊的交错只是一种可能性。在不同情况下，可能是线程 B 的结果丢失，或者根本没有错误。因为它们是不可预测的，所以难以检测和修复线程干扰错误。