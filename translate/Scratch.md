# Java 内存模型

Java 内存模型指定了 Java 虚拟机如何使用计算机的内存(RAM)。Java 虚拟机可以看作是整个计算机的模型，因而自然包含一个内存模型——也就是所谓的 Java 内存模型。

如果想要设计具有精确行为的并发程序，理解 Java 内存模型是非常重要的。Java 内存模型指定了不同的线程在何时以何种方法可以看到由其他线程写入共享变量的值，以及在必要时如何同步访问共享变量。

最初的 Java 内存模型性能不好，因而在 Java 1.5 中进行了改进。改进后的 Java 内存模型在 Java 1.8 中仍然使用。

## 内部 Java 内存模型

JVM 内部使用的 Java 内存模型将内存划分为线程栈和堆。下图展示了 Java 内存模型的逻辑表达形式：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-1.png)

Java 虚拟机中运行的每个线程都拥有自己的线程栈。线程栈包含线程已经调用的方法直到当前执行到的代码位置的信息。我将这种信息称为"调用栈"。随着线程执行代码，调用栈不断变化。

线程栈还包含正在执行的每个方法（调用栈上的所有方法）的所有局部变量。线程只能访问自己的线程栈。由线程创建的局部变量对除了创建它的线程之外的所有线程都是不可见的。即使两个线程正在执行完全相同的代码，两个线程仍然会在各自的线程栈中创建代码中的局部变量。因此，每个线程都拥有每个局部变量的自身版本。

所有的基本数据类型 ( `boolean`, `byte`, `short`, `char`, `int`, `long`, `float`, `double`) 的局部变量都完全存储在线程栈上，因而对其他线程不可见。线程可以将一个基本数据类型的变量传递给另一个线程，但是并不能共享自己的基本数据类型的局部变量。

堆包含你的 Java 应用中创建的所有对象，不关心创建对象的线程。包括基本数据类型的对象版本 (比如， `Byte`, `Integer`, `Long` 等等)。对象被创建并分配给局部变量，或者作为另一个对象的成员变量被创建，都没关系，这些对象都存储在堆中。

下图展示了存储在线程栈中的调用栈和局部变量，以及存储在堆中的对象：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-2.png)

局部变量也可能是基本数据类型，这种情况下完全存储在线程栈中。

局部变量也可以是对象的引用。这种情况下该引用(局部变量)存储在线程栈上，但是对象本身存储在堆上。

一个对象可能包含方法，而这些方法可能包含局部变量。即使这些方法所属的对象存储在堆中，这些局部变量也存储在线程栈中。

对象的成员变量与对象本身一起存储在堆中。当成员变量是原始类型时，以及它是对对象的引用时，都是如此。静态类变量也与类定义一起存储在堆中。

引用对象的所有线程都可以访问堆上的对象。当线程可以访问对象时，它也可以访问该对象的成员变量。如果两个线程同时在同一个对象上调用方法，则它们都将有权访问该对象的成员变量，但是每个线程将拥有自己的局部变量副本。

下图展示了上述要点：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-3.png)

两个线程具有一组局部变量。局部变量之一（`Local Variable 2`）指向堆上的共享对象（对象3）。这两个线程分别具有对同一对象的不同引用。它们的引用是局部变量，因此存储在每个线程的线程栈中（在每个线程上）。但是，两个不同的引用指向堆上的同一对象。

请注意，共享对象（对象3）如何引用对象2和对象4作为成员变量（如从对象3到对象2和对象4的箭头所示）。通过对象3中的这些成员变量引用，两个线程可以访问对象2和对象4。

该图还显示了一个局部变量，该局部变量指向堆上的两个不同对象。在这种情况下，引用指向两个不同的对象（对象1和对象5），而不是同一对象。理论上，如果两个线程都引用了两个对象，则两个线程都可以访问对象1和对象5。但是在上图中，每个线程仅具有对两个对象之一的引用。

那么，什么样的 Java 代码能够产生上面的内存分布图？如下的代码即可：

```java
public class MyRunnable implements Runnable() {

    public void run() {
        methodOne();
    }

    public void methodOne() {
        int localVariable1 = 45;

        MySharedObject localVariable2 =
            MySharedObject.sharedInstance;

        //... do more with local variables.

        methodTwo();
    }

    public void methodTwo() {
        Integer localVariable1 = new Integer(99);

        //... do more with local variable.
    }
}
public class MySharedObject {

    //static variable pointing to instance of MySharedObject

    public static final MySharedObject sharedInstance =
        new MySharedObject();


    //member variables pointing to two objects on the heap

    public Integer object2 = new Integer(22);
    public Integer object4 = new Integer(44);

    public long member1 = 12345;
    public long member1 = 67890;
}
```

如果两个线程都正在执行 `run()` 方法，则前面的图将会产生。`run()` 方法调用 `methodOne()` ，而 `methodOne()` 调用 `methodTwo()`。

`methodOne()` 声明一个基本数据类型的局部变量 ( `int` 类型的`localVariable1` ) 和一个对象引用类型的局部变量 (`localVariable2`)。

每个执行 `methodOne()` 的线程都将在各自的线程栈上创建自己的 `localVariable1` 和 `localVariable2` 的副本。 `localVariable1` 变量将是彻底相互独立的，各自存活在自己的线程栈中。一个线程无法看到别的线程对它自己的 `localVariable1` 的副本所作的修改。

每个执行 `methodOne()` 的线程也会创建自己的 `localVariable2` 副本。但是，`localVariable2` 的两个不同副本最终都指向堆上的同一对象。该代码将 `localVariable2` 设置为指向静态变量引用的对象。静态变量只有一个副本，并且此副本存储在堆中。因此，`localVariable2` 的两个副本最终都指向静态变量指向的 `MySharedObject` 的同一实例。`MySharedObject` 实例也存储在堆中。它对应于上图中的对象3。

注意 `MySharedObject` 类也包含两个成员变量。成员变量本身与对象一起存储在堆中。这两个成员变量指向另外两个 `Integer` 对象。这些 `Integer` 对象对应于上图中的对象2和对象4。

还要注意 `methodTwo()` 如何创建一个名为 `localVariable1` 的局部变量。该局部变量是对 `Integer` 对象的对象引用。 该方法将 `localVariable1` 引用设置为指向新的 `Integer` 实例。执行 `methodTwo()` 的每个线程的 `localVariable1` 引用将存储在一个副本中。实例化的两个 `Integer` 对象将存储在堆中，但是由于该方法每次执行时都会创建一个新的 `Integer` 对象，因此执行此方法的两个线程将创建单独的 `Integer` 实例。在 `methodTwo()` 内部创建的 `Integer` 对象对应于上图中的对象1和对象5。

还要注意类型为 `long` 的 `MySharedObject` 类中的两个成员变量，这是原始类型。由于这些变量是成员变量，因此它们仍与对象一起存储在堆中。仅局部变量存储在线程堆栈上。

## 硬件内存架构

现代硬件内存体系结构与内部 Java 内存模型有所不同。同样重要的是，还要了解硬件内存架构，并了解 Java 内存模型如何与之协同工作。本节描述了常见的硬件内存体系结构，下一节将描述 Java 内存模型如何与之协同工作。

下面是最简化的现代计算机硬件架构示意图：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-4.png)

现代计算机通常其中装有2个或更多CPU。其中一些CPU也可能具有多个内核。关键是，在具有2个或更多CPU的现代计算机上，可能同时运行多个线程。每个CPU都可以在任何给定时间运行一个线程。这意味着，如果Java应用程序是多线程的，则每个CPU可能在Java应用程序中同时（并发）运行一个线程。

每个CPU包含一组寄存器，这些寄存器本质上是CPU内存。 CPU在这些寄存器上执行操作的速度比对主存储器中的变量执行操作的速度快得多。这是因为CPU可以比访问主存储器更快地访问这些寄存器。

每个CPU可能还具有一个CPU高速缓存存储层。实际上，大多数现代CPU都具有一定大小的缓存层。 CPU可以比其主存储器更快地访问其高速缓存，但是通常不如它可以访问其内部寄存器的速度快。因此，CPU高速缓存内存介于内部寄存器和主内存的速度之间。某些CPU可能具有多个高速缓存层（第1级和第2级），但是了解Java内存模型如何与内存交互并不重要。重要的是要知道CPU可以具有某种高速缓存层。

计算机还包含一个主存储区（RAM）。所有CPU都可以访问主存储器。主存储区通常比CPU的缓存大得多。

通常，当CPU需要访问主存储器时，它将部分主存储器读入其CPU缓存中。它甚至可以将缓存的一部分读入其内部寄存器，然后对其执行操作。当CPU需要将结果写回主存储器时，它将把值从其内部寄存器刷新到高速缓存，并在某个时候将值刷新回主存储器。

当CPU需要将其他内容存储在高速缓存中时，通常会将高速缓存中存储的值刷新回主存储器。 CPU高速缓存可以一次将数据写入其部分内存，并一次刷新其部分内存。它不必每次更新都读取/写入完整的缓存。通常，缓存在称为“缓存行”的较小存储块中更新。可以将一个或多个高速缓存行读入高速缓存存储器，并且可以将一个或多个高速缓存行再次刷新回主存储器。

## Bridging The Gap Between The Java Memory Model And The Hardware Memory Architecture

As already mentioned, the Java memory model and the hardware memory architecture are different. The hardware memory architecture does not distinguish between thread stacks and heap. On the hardware, both the thread stack and the heap are located in main memory. Parts of the thread stacks and heap may sometimes be present in CPU caches and in internal CPU registers. This is illustrated in this diagram:

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-5.png)

When objects and variables can be stored in various different memory areas in the computer, certain problems may occur. The two main problems are:

- Visibility of thread updates (writes) to shared variables.
- Race conditions when reading, checking and writing shared variables.

Both of these problems will be explained in the following sections.

### Visibility of Shared Objects

If two or more threads are sharing an object, without the proper use of either `volatile` declarations or synchronization, updates to the shared object made by one thread may not be visible to other threads.

Imagine that the shared object is initially stored in main memory. A thread running on CPU one then reads the shared object into its CPU cache. There it makes a change to the shared object. As long as the CPU cache has not been flushed back to main memory, the changed version of the shared object is not visible to threads running on other CPUs. This way each thread may end up with its own copy of the shared object, each copy sitting in a different CPU cache.

The following diagram illustrates the sketched situation. One thread running on the left CPU copies the shared object into its CPU cache, and changes its `count` variable to 2. This change is not visible to other threads running on the right CPU, because the update to `count` has not been flushed back to main memory yet.

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-6.png)

To solve this problem you can use [Java's volatile keyword](http://tutorials.jenkov.com/java-concurrency/volatile.html). The `volatile` keyword can make sure that a given variable is read directly from main memory, and always written back to main memory when updated.

### Race Conditions

If two or more threads share an object, and more than one thread updates variables in that shared object, [race conditions](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) may occur.

Imagine if thread A reads the variable `count` of a shared object into its CPU cache. Imagine too, that thread B does the same, but into a different CPU cache. Now thread A adds one to `count`, and thread B does the same. Now `var1` has been incremented two times, once in each CPU cache.

If these increments had been carried out sequentially, the variable `count` would be been incremented twice and had the original value + 2 written back to main memory.

However, the two increments have been carried out concurrently without proper synchronization. Regardless of which of thread A and B that writes its updated version of `count` back to main memory, the updated value will only be 1 higher than the original value, despite the two increments.

This diagram illustrates an occurrence of the problem with race conditions as described above:

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-7.png)

To solve this problem you can use a [Java synchronized block](http://tutorials.jenkov.com/java-concurrency/synchronized.html). A synchronized block guarantees that only one thread can enter a given critical section of the code at any given time. Synchronized blocks also guarantee that all variables accessed inside the synchronized block will be read in from main memory, and when the thread exits the synchronized block, all updated variables will be flushed back to main memory again, regardless of whether the variable is declared volatile or not.