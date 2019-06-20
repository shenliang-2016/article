### 同步

线程主要通过共享对字段的访问和字段表示的对象引用进行通信。这种通信形式非常有效，但可能会出现两种错误：*线程干扰*和*内存一致性错误*。防止这些错误所需的工具是*同步*。

但是，同步可能会引入*线程争用*，当两个或多个线程同时尝试访问同一资源，并导致Java运行时更慢地执行一个或多个线程，甚至暂停执行时，就会发生这种情况。[饥饿和活锁](https://docs.oracle.com/javase/tutorial/essential/concurrency/starvelive.html) 是线程争用的形式。有关更多信息，请参阅 [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 部分。

本章节包含以下主题：

- [线程干扰](https://docs.oracle.com/javase/tutorial/essential/concurrency/interfere.html) 描述了当多个线程访问共享数据时错误如何产生。
- [内存一致性错误](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html) 描述由共享内存的不一致视图导致的错误。
- [同步方法](https://docs.oracle.com/javase/tutorial/essential/concurrency/syncmeth.html) 描述了一个简单的惯用方法，可以有效解决线程干扰和内存一致性错误。
- [隐式锁和同步](https://docs.oracle.com/javase/tutorial/essential/concurrency/locksync.html) 描述了更通用的同步习惯用法，并描述了基于隐式锁的同步方式。
- [原子访问](https://docs.oracle.com/javase/tutorial/essential/concurrency/atomic.html) 讨论了不会被其它线程干扰的操作的一般概念。

#### 线程干扰

考虑下面的简单的类 [`Counter`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Counter.java)

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

`Counter` 的设计使得每次调用`increment` 都会将`c`加1，每次调用`decrement` 都会从`c`中减去1。但是，如果从多个线程引用`Counter`对象，则线程之间的干扰可能会阻止这种情况按预期发生。

当两个操作在不同的线程中运行但作用于相同的数据时，会发生干扰。这意味着这两个操作由多个步骤组成，并且步骤序列重叠。

对于`Counter`实例的操作似乎不可能发生交错，因为对`c`的两个操作都是单个简单的语句。但是，即使是简单的语句也可以由虚拟机转换为多个步骤。我们不会检查虚拟机采取的具体步骤 - 足以知道单个表达式`c++`可以分解为三个步骤：

1. 获取 `c`的当前值。
2. 将获取的值加1。
3. 将增加之后的值存储到变量 `c` 中。

表达式`c--`可以以相同的方式分解，除了第二步是减少而不是增量。

假设线程A在大约同一时间调用 `increment` ，线程B调用 `decrement`。如果`c`的初始值为0，则它们的交错操作可能遵循以下顺序：

1. 线程A：检索`c`。
2. 线程B：检索`c`。
3. 线程A：增加检索值；结果是1。
4. 线程B：减少检索值；结果是-1。
5. 线程A：将结果存储在`c`中；`c`现在是1。
6. 线程B：将结果存储在`c`中；`c`现在是-1。

线程A的结果丢失，被线程B覆盖。这种特殊的交错只是一种可能性。在不同情况下，可能是线程B的结果丢失，或者根本没有错误。因为它们是不可预测的，所以难以检测和修复线程干扰错误。

#### 内存一致性错误

当不同的线程具有应该是相同数据的不一致视图时，会发生内存一致性错误。内存一致性错误的原因很复杂，超出了本教程的范围。幸运的是，程序员不需要详细了解这些原因。所需要的只是避免它们的策略。

避免内存一致性错误的关键是理解 *happens-before* 关系。这种关系只是简单地保证一个特定语句的内存写入对另一个特定语句可见。要查看此内容，请考虑以下示例。假设定义并初始化了一个简单的`int`字段：

```
int counter = 0;
```

 `counter` 字段在两个线程A和B之间共享。假设线程A递增 `counter` ：

```
counter++;
```

然后，不久之后，线程B打印出 `counter`：

```
System.out.println(counter);
```

如果两个语句已在同一个线程中执行，则可以安全地假设打印出的值为“1”。但是如果这两个语句是在不同的线程中执行的，那么打印出的值可能是“0”，因为不能保证线程A对计数器的更改对于线程B是可见的 - 除非程序员已经在这两个语句之间建立了*happens-before*关系。

有几种行为可以建立*happens-before*关系。其中之一是同步，我们将在以下部分中看到。

我们已经看到了两种建立*happens-before*关系的行为。

 - 当一个语句调用`Thread.start`时，与该语句具有*happens-before*关系的每个语句也与新线程执行的每个语句都有一个*happens-before*关系。 新线程可以看到导致创建新线程的代码的影响。
 - 当一个线程终止并导致另一个线程中的`Thread.join`返回时，终止线程执行的所有语句与成功`join`后的所有语句都有一个*happens-before*关系。现在，执行`join`的线程可以看到线程中代码的效果。

可以创建*happens-before*关系的行为列表，参考 [ `java.util.concurrent` 包的摘要页面。](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html#MemoryVisibility)