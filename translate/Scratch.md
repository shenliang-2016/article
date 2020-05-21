## 在 Java 内存模型和硬件内存架构之间架起桥梁

如前所述，Java 内存模型和硬件内存架构是不同的。硬件内存架构并不区分线程栈和堆。从硬件层面看，线程栈和堆都在主内存中。部分线程栈和堆有时候可以出现在 CPU 缓存或者 CPU 寄存器中。下图展示了这种分布情况：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-5.png)

当对象和变量可以被存储在各种不同的计算机存储区域中时，可能会发生某些问题。主要的两类问题：

- 线程对共享变量的修改（写入）的可见性。
- 在读取，校验以及写入共享变量时的竞争条件。

接下来分别解释这两类问题。

### 共享对象的可见性

如果两个线程正在共享一个对象，如果没有正确使用 `volatile` 声明或者同步，那么一个线程对共享对象的修改将可能不会被另一个线程看到。

设想共享对象最初存储在主内存中。一个运行在 CPU 上的线程将该共享对象读取到它的 CPU 缓存中。然后对该对象进行了修改。由于 CPU 此时并没有将缓存中的对象写回主内存，所以共享对象的修改之后的版本对运行在其他 CPU 上的线程是不可见的。这样每个线程都各自拥有自己的共享对象副本，每个副本存储在不同的 CPU 缓存中。

下图描述了上述情形。运行在左侧 CPU 上的线程将共享对象拷贝到它的 CPU 缓存中，然后修改其 `count` 变量为2。这个修改对运行在右侧 CPU 上的线程是不可见的，因为对 `count` 的修改尚未被会写到主内存。

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-6.png)

解决此类问题的办法是使用 [Java 的 volatile 关键字](http://tutorials.jenkov.com/java-concurrency/volatile.html)。 `volatile` 关键字能够确保给定的变量直接从主内存中读取，当修改时始终会直接写回主内存。

### 竞争条件

如果两个或者多个线程共享一个对象，其中若干线程修改该共享对象的变量，就可能会发生 [竞争条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) 。

设想这样的情形，如果线程 A 将共享对象中的变量 `count` 读取到它的 CPU 缓存中。运行在另一个 CPU 上的线程 B 也将该变量读取到自己所在 CPU 的缓存中。现在线程 A 对 `count` 加1，线程 B 也对 `count` 加1。现在 `count` 已经被增加过两次，每个 CPU 缓存一次。

如果这两次增加操作顺序发生，变量 `count` 将会增加两次，初始值增加2并写回主内存。

然而，两次增加并发发生，而没有正确地同步。无论哪个线程将它修改过的 `count` 版本写回主内存，最终的结果只会比初始值增加1，两次增加操作无效。

下图展示了上述发生竞争条件的情形：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-7.png)

解决此类问题的办法是使用 [Java synchronized 块](http://tutorials.jenkov.com/java-concurrency/synchronized.html)。同步块保证在任何给定时间点只有一个线程可以进入给定的代码临界区。同步块同时保证所有在同步块内部访问的变量都将直接从主内存读取。同时，当线程退出同步块时，所有被修改过的变量都会立即被写回主内存，无论变量有没有声明为 `volatile` 。

