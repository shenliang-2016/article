# 非阻塞算法

并发语境中的非阻塞算法是允许线程访问共享状态（或以其他方式进行协作或通信）而不会阻塞所涉及线程的算法。更笼统地说，如果一个线程的挂起不能导致该算法中涉及的其他线程的挂起，则该算法被称为非阻塞。

为了更好地理解阻塞和非阻塞并发算法之间的区别，我将首先解释阻塞算法，然后介绍非阻塞算法。

## 阻塞并发算法

阻塞并发算法是以下一种算法：

- A：执行线程请求的操作——或者
- B：阻塞线程，直到可以安全地执行操作为止

许多类型的算法和并发数据结构都是阻塞式的。例如，[java.util.concurrent.BlockingQueue](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) 接口的不同实现都是阻塞数据结构。如果线程尝试将元素插入到 `BlockingQueue` 且队列中没有空间，则插入线程将被阻塞（挂起），直到 `BlockingQueue` 具有用于新元素的空间。

下图说明了保护共享数据结构的阻塞算法的行为：

![](http://tutorials.jenkov.com/images/java-concurrency/non-blocking-algorithms-1.png)

## 非阻塞并发算法

非阻塞并发算法是以下一种算法：

- A：执行线程请求的操作——或者
- B：通知请求线程无法执行该操作

Java 也包含几个非阻塞数据结构。[AtomicBoolean](http://tutorials.jenkov.com/java-util-concurrent/atomicboolean.html)， [的AtomicInteger](http://tutorials.jenkov.com/java-util-concurrent/atomicinteger.html)，[AtomicLong](http://tutorials.jenkov.com/java-util-concurrent/atomiclong.html) 和 [AtomicReference](http://tutorials.jenkov.com/java-util-concurrent/atomicreference.html) 是非阻塞的数据结构的例子。

下图说明了保护共享数据结构的非阻塞算法的行为：

![](http://tutorials.jenkov.com/images/java-concurrency/non-blocking-algorithms-2.png)

## 非阻塞与阻塞算法

阻塞算法和非阻塞算法之间的主要区别在于行为的第二步，如以上两节所述。换句话说，区别在于当无法执行请求的操作时，阻塞算法和非阻塞算法将执行以下操作：

阻塞算法将阻塞线程，直到可以执行请求的操作为止。非阻塞算法会通知请求该操作的线程该操作无法执行。

使用阻塞算法，线程可能会被阻塞，直到可以执行请求的操作为止。通常，另一个线程的操作将使第一个线程可以执行请求的操作。如果由于某种原因其他线程被挂起（阻塞）在应用程序中的其他位置，从而无法执行使第一个线程请求的操作成为可能的动作，则第一个线程将无限期保持阻塞状态，或者直到另一个线程最终执行必要的行动。

例如，如果一个线程试图将一个元素插入到一个满 `BlockingQueue` 中，则该线程将阻塞，直到另一个线程从 `BlockingQueue` 中获取了一个元素。如果由于某种原因本应从 `BlockingQueue` 中获取元素的线程在应用程序中的其他位置被阻塞（挂起），则尝试插入新元素的线程将无限期保持阻塞状态，或者直到获取元素的线程最终从 `BlockingQueue` 中获取元素。

## 非阻塞并发数据结构

在多线程系统中，线程通常通过某种数据结构进行通信。这样的数据结构可以是任何类型，从简单的变量到更高级的数据结构（例如队列，映射，堆栈等）。为了促进多个线程正确并发地访问数据结构，必须通过某种*并发算法*来保护数据结构。保护算法使数据结构成为*并发数据结构*。

如果保护并发数据结构的算法使用阻塞（使用线程挂起），则称其为 *阻塞算法*。因此，该数据结构被称为*阻塞并发数据结构*。

如果保护并发数据结构的算法不使用阻塞，则称其为*非阻塞算法*。因此，该数据结构被称为*非阻塞并发数据结构*。

每个并发数据结构旨在支持某种通信方法。因此，可以使用哪种并发数据结构取决于您的通信需求。在以下各节中，我将介绍一些非阻塞的并发数据结构，并说明在什么情况下可以使用它们。对这些非阻塞数据结构如何工作的解释应该使您对如何设计和实现非阻塞数据结构有一个了解。

## volatile 变量

[Java volatile变量](http://tutorials.jenkov.com/java-concurrency/volatile.html) 是始终直接从主内存读取的变量。当将新值分配给易失性变量时，该值总是立即写入主存储器。这样可以保证 volatile 变量的最新值始终对在其他 CPU 上运行的其他线程可见。其他线程每次都会从主内存中读取 volatile 的值，而不是从线程正在运行的 CPU 的缓存中读取。

易变变量是非阻塞的。将值写入易失性变量是原子操作，它不能被打断。但是，对易失性变量执行的读写更新序列不是原子的。因此，如果由多个线程执行，则此代码仍可能导致 [争用条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html)：

```java
volatile myVar = 0; 

... 
int temp = myVar; 
temp ++; 
myVar = temp;
```

首先，将 volatile 变量 `myVar` 的值从主存储器读取到 `temp` 变量中。然后将 `temp` 变量加 1。然后将 `temp` 变量的值分配给 volatile `myVar` 变量，这意味着它将被写回到主存储器。

如果两个线程执行此代码，并且两个线程都读取 `myVar` 的值，将其值加 1 并将其写回主内存，则可能有出错的风险。最终结果可能不是将 2 添加到 `myVar` 变量中，而只会添加 1（例如，两个线程）读取值 19，增加到 20，然后写回 20）。

您可能认为您不会像上面那样编写代码，但是实际上上面的代码等效于此：

```java
myVar ++;
```

执行时，将 `myVar` 的值读入 CPU 寄存器或本地 CPU 缓存中，将其相加，然后将来自 CPU 寄存器或 CPU 缓存的值写回到主存储器中。

### 单个写者场景

在某些情况下，只有一个线程写入共享变量，而多个线程读取该变量的值。当只有一个线程正在更新变量时，无论有多少线程正在读取变量，都不会发生竞争条件。因此，只要您只有一个共享变量的写者，就可以使用易失性变量。

当多个线程对共享变量执行读-更新-写操作序列时，就会发生争用条件。如果只有一个线程执行读-更新-写操作序列，而所有其他线程仅执行读操作，则没有竞争条件。

这是一个不使用同步但仍处于并发状态的单写者计数器：

```
public class SingleWriterCounter {

    private volatile long count = 0;

    /**
     * Only one thread may ever call this method,
     * or it will lead to race conditions.
     */
    public void inc() {
        this.count++;
    }


    /**
     * Many reading threads may call this method
     * @return
     */
    public long count() {
        return this.count;
    }
}
```

只要只有一个线程调用，多个线程就可以访问该计数器的相同实例，而只有一个线程可以调用 `inc()`。我的意思不是同一时刻只有一个线程可以调用 `inc()` 。我的意思是，只有相同的单个线程才被允许调用 `inc()`。多个线程可以调用 `count()`。这不会引起任何竞争条件。

下图说明了线程如何访问 volatile `count` 变量：

![](http://tutorials.jenkov.com/images/java-concurrency/non-blocking-algorithms-3.png)

### 基于易变变量的更高级的数据结构

可以创建使用易失性变量组合的数据结构，其中每个易失性变量仅由单个线程写入，并由多个线程读取。每个 volatile 变量可以由不同的线程（但只能是一个线程）写入。使用这样的数据结构，多个线程可能能够使用易失性变量以非阻塞的方式相互发送信息。

这是一个简单的 double writer 计数器类：

```
public class DoubleWriterCounter {

    private volatile long countA = 0;
    private volatile long countB = 0;

    /**
     * Only one (and the same from thereon) thread may ever call this method,
     * or it will lead to race conditions.
     */
    public void incA() { this.countA++;  }


    /**
     * Only one (and the same from thereon) thread may ever call this method,
     * or it will lead to race conditions.
     */
    public void incB() { this.countB++;  }


    /**
     * Many reading threads may call this method
     */
    public long countA() { return this.countA; }


    /**
     * Many reading threads may call this method
     */
    public long countB() { return this.countB; }
}
```

如您所见，`DoubleWriterCounter` 现在包含两个 volatile 变量，以及两对增加和读取方法。只有一个线程可以调用 `incA()`，也只能有一个线程调用 `incB()`。但是不同的线程可以调用 `incA()` 和 `incB()`。允许多个线程调用 `countA()` 和 `countB()`。这不会引起竞争条件。

`DoubleWriterCounter` 可用于诸如两个线程的通信。这两个计数可以表示产生的任务和消耗的任务。该图显示了两个线程通过类似于上面的数据结构进行通信：

![](http://tutorials.jenkov.com/images/java-concurrency/non-blocking-algorithms-4.png)

精明的读者将认识到您可以通过使用两个 `SingleWriterCounter` 实例来达到 `DoubleWriterCounter` 的效果。如果需要，您甚至可以使用更多的线程和 `SingleWriterCounter` 实例。