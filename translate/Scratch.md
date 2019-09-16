### 内存一致性错误

当不同的线程具有应该是相同数据的不一致视图时，会发生*内存一致性错误*。内存一致性错误的原因很复杂，超出了本教程的范围。幸运的是，程序员不需要详细了解这些原因。所需要的只是避免它们的策略。

避免内存一致性错误的关键是理解 *happen-before* 关系。这种关系只是保证一个特定语句的内存写入对另一个特定语句可见。要查看此内容，请考虑以下示例。假设定义并初始化了一个简单的 `int` 字段：

```
int counter = 0;
```

 `counter` 字段由两个线程共享，A 和 B。假定线程 A 增加 `counter`：

```
counter++;
```

然后，不久之后，线程B打印出 `counter`：

```
System.out.println(counter);
```

如果两个语句已在同一个线程中执行，则可以安全地假设打印出的值为“1”。但是如果这两个语句是在不同的线程中执行的，那么打印出的值可能是“0”，因为不能保证线程 A 对 `counter` 的更改对于线程 B 是可见的 - 除非程序员已经建立了这两个陈述之间的 `happens-before` 关系。

有几种行为可以创造 `happens-before` 关系。其中之一是同步，我们将在以下部分中看到。

我们已经看到了两种创造 `happens-before` 关系的行为。

 - 当一个语句调用 `Thread.start` 时，与该语句有一个 `happens-before` 关系的每个语句也与新线程执行的每个语句都有一个 `happens-before` 关系。新线程可以看到导致创建新线程的代码的影响。
 - 当一个线程终止并导致另一个线程中的 `Thread.join` 返回时，终止线程执行的所有语句与成功连接后的所有语句都有一个 `happens-before` 关系。现在，执行连接的线程可以看到线程中代码的效果。

可以创建 `happens-before` 关系的操作列表参考 [Summary page of the `java.util.concurrent`package](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html#MemoryVisibility) 。

### 同步方法

Java 编程语言提供了两种基本的同步习语：*synchronized methods* 和 *synchronized statements*。下两节将介绍两者中较为复杂的同步语句。本节介绍同步方法。

要使方法同步，只需在其声明中添加 `synchronized` 关键字：

```java
public class SynchronizedCounter {
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

如果 `count` 是 `SynchronizedCounter` 的一个实例，那么使这些方法同步有两个影响：

 - 首先，对同一对象的两个同步方法的调用不可能进行交错。当一个线程正在为对象执行同步方法时，所有其他线程调用同一对象的同步方法阻塞（暂停执行）直到第一个线程完成对象。
 - 其次，当同步方法退出时，它会自动与同一对象的同步方法的*任何后续调用*建立 ` happens-before ` 关系。这可以保证所有线程都可以看到对象状态的更改。

请注意，构造函数无法同步 - 将 `synchronized` 关键字与构造函数一起使用是一种语法错误。同步构造函数没有意义，因为只有创建对象的线程在构造时才能访问它。

------

**警告：** 构造将在线程之间共享的对象时，要非常小心，对对象的引用不会过早“泄漏”。例如，假设您要维护一个包含每个类实例的 `List` 调用实例。您可能想要将以下行添加到构造函数中：

```java
instances.add(this);
```

但是其他线程可以在构造对象完成之前使用 `instances` 来访问对象。

------

同步方法启用了一种简单的策略来防止线程干扰和内存一致性错误：如果一个对象对多个线程可见，则对该对象变量的所有读取或写入都是通过 `synchronized` 方法完成的。（一个重要的例外：`final` 字段，在构造对象后无法修改，可以通过非同步方法安全地读取，一旦构造了对象）这种策略是有效的，但可能会带来 [活性]( https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 的问题，我们将在本课后面看到。

