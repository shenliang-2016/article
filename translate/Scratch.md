# 竞争条件和临界区

竞争条件是可能发生在临界区内的特殊条件。所谓临界区是指由多个线程执行的代码段，多个线程的不同执行顺序会产生临界区并发执行的不同结果。

当多线程执行临界区的结果何时会有所不同取决于线程的执行顺序时，我们就说该临界区包含竞争条件。术语竞争条件来自这样的比喻：多个线程正在竞争通过临界区，这种竞争的结果影响了临界区执行的结果。

听起来好像有点复杂，所以接下来我会分别详细介绍它们。

## 临界区

在同一应用程序中运行多个线程本身不会导致问题。当多个线程访问相同的资源时，就会出现问题。例如，相同的内存（变量，数组或对象），系统（数据库，Web服务等）或文件。

实际上，仅当一个或多个线程写入这些资源时才会出现问题。只要资源不变，让多个线程读取相同的资源是安全的。

这是临界区的Java代码示例，如果同时由多个线程执行，则该示例可能会失败：

```java
  public class Counter {

     protected long count = 0;

     public void add(long value){
         this.count = this.count + value;
     }
  }
```

设想两个线程，A 和 B，正在执行同一个 `Counter` 类实例上的 `add` 方法。没有任何办法可以确知操作系统如何调度两个线程。`add()` 方法中的代码并不会作为一个原子指令被 JVM 执行。它会作为一系列更小的指令被执行，类似于：

1. 从内存中读取 `this.count` 到寄存器中。
2. 增加值到寄存器。
3. 将寄存器写回内存。

观察当 A 和 B 像下面这样交错执行时会发生什么：

```
       this.count = 0;

   A:  Reads this.count into a register (0)
   B:  Reads this.count into a register (0)
   B:  Adds value 2 to register
   B:  Writes register value (2) back to memory. this.count now equals 2
   A:  Adds value 3 to register
   A:  Writes register value (3) back to memory. this.count now equals 3
```

这两个线程想将值 2 和 3 加到计数器上。因此，两个线程完成执行后，该值应为5。但是，由于两个线程的执行是交错的，因此结果最终会有所不同。

在上面列出的执行序列示例中，两个线程都从内存中读取值 0。然后，将各自的值 2 和 3 加到该值上，并将结果写回到内存中。`this.count`中剩下的值将是最后一个线程写入的值，而不是 5。在上述情况下，它是线程 A 的结果，但也可能是线程 B 的结果。

## 临界区中的竞争条件

前面示例中 `add()` 方法中的代码包含一个临界区。当多个线程执行此临界区时，就会出现竞争条件。

更正式地讲，两个线程争用同一资源的情况（竞争资源的顺序很重要）被称为竞争条件。导致竞争条件的代码段称为临界区。

## 预防竞争条件

为了防止出现竞争条件，您必须确保临界区作为原子指令执行。这意味着一旦一个线程执行了它，其他线程就无法执行它，直到第一个线程离开了临界区。

可以通过对临界区进行适当的线程同步来避免竞争条件。可以使用 [Java代码的同步块](http://tutorials.jenkov.com/java-concurrency/synchronized.html) 实现线程同步。线程同步也可以使用其他同步结构（例如 [locks](http://tutorials.jenkov.com/java-concurrency/locks.html) 或原子变量，例如 [java.util.concurrent.atomic.AtomicInteger](http://tutorials.jenkov.com/java-util-concurrent/atomicinteger.html)。

## 临界区吞吐量

对于多个较小的临界区，将整个临界区作为一个同步代码块是可行的。但是，对于较大的临界区，将其拆分为多个较小的临界区，以允许多个线程并发执行每个较小的临界区，可能是有好处的。这样做可以降低对共享资源的争用，因而提升整个临界区的吞吐量。

下面的简单的代码示例展示了这一点：

```java
public class TwoSums {
    
    private int sum1 = 0;
    private int sum2 = 0;
    
    public void add(int val1, int val2){
        synchronized(this){
            this.sum1 += val1;   
            this.sum2 += val2;
        }
    }
}
```

注意 `add()` 方法如何将值添加到两个不同的 `sum` 成员变量。为了防止竞争条件，求和是在Java同步块内执行的。 使用此实现，同一时刻只有一个线程可以执行求和。

然而，由于两个 sum 变量实际上是相互独立的，你可以将求和逻辑拆分为两个同步块，如下所示：

```java
public class TwoSums {
    
    private int sum1 = 0;
    private int sum2 = 0;

    private Integer sum1Lock = new Integer(1);
    private Integer sum2Lock = new Integer(2);

    public void add(int val1, int val2){
        synchronized(this.sum1Lock){
            this.sum1 += val1;   
        }
        synchronized(this.sum2Lock){
            this.sum2 += val2;
        }
    }
}
```

现在，两个线程可以同时执行`add()`方法。第一个同步块内的一个线程，第二个同步块内的另一个线程。两个同步块在不同的对象上同步，因此两个不同的线程可以独立执行两个块。这样，线程将更少地等待彼此来执行`add()`方法。

当然，这个例子很简单。在现实生活中共享的资源中，临界区的分解可能要复杂得多，并且需要对执行顺序的可能性进行更多分析。