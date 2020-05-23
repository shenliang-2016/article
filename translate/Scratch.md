## volatile 并不总是足够

即使 `volatle` 关键字保证直接从主内存读取所有的 `volatile` 变量，所有对 `volatile` 变量的写入都直接写入主内存，仍然存在某些情况，仅仅将变量声明为 `volatile` 是不够的。

在上文中解释的情况下，只有一个线程 1 对共享变量 `counter` 进行写入，将该变量声明为 `volatile` 就足以保证线程 2 始终都能看到最新写入的值。

事实上，如果写入变量的新值不依赖于变量的先前值，多个线程甚至能够同时写入共享的 `volatile` 变量，仍然能够保证主内存中存储正确的值。换句话说，如果一个写入共享 `volatile` 变量的线程不需要事先读取该变量的值就能确定它的下一个值就可以。

一旦线程需要事先读取 `volatile` 变量的值，然后基于该值产生该变量的新值，则声明为 `volatile` 变量就不再足够保证正确的可见性。`volatile` 变量读取和新值写入操作之间短暂的时间差，制造出一个 [race condition](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) ，其中多个线程可能读取到该 `volatile` 变量的相同的值，产生变量的新值，而在将变量值写回主内存时——覆盖其他线程写入的值。

多个线程同时增加同一个计数器的场景正好就是 `volatile` 变量不足够的例子。下面一节进一步解释这种情况。

设想如果线程 1 读取一个值为 0 的共享 `counter` 变量到它的 CPU 缓存中，对其值加 1 而并没有将修改之后的值写入主内存。线程 2 接下来从主内存读取同一个 `counter` 变量，其值仍为 0 ，到它的 CPU 缓存中。然后线程 2 也对其值加 1 ，也没有将修改后的值写入主内存。如下图所示：

![](http://tutorials.jenkov.com/images/java-concurrency/java-volatile-3.png)

现在，线程 1 和线程 2 实际上不同步。共享的 `counter` 变量的实际值应该为 2 ，但是每个线程在其 CPU 缓存中的变量值为 1 ，而在主内存中该值仍然为 0 。真是一团糟！即使线程最终将共享 `counter` 变量的值写回到主存中，该值也将是错误的。

## volatile 何时足够？

如前所述，如果两个线程都在读取和写入共享变量，那么仅使用 `volatile` 关键字是不够的。在这种情况下，您需要使用 [synchronized](http://tutorials.jenkov.com/java-concurrency/synchronized.html)，以确保变量的读写是原子性的。读取或写入 `volatile` 变量不会阻止线程读取或写入。为此，您必须在临界区周围使用 `synchronized` 关键字。

作为 `synchronized` 块的替代方法，您还可以使用在 [`java.util.concurrent`包](http://tutorials.jenkov.com/java-util-concurrent/index.html) 中找到的许多原子数据类型之一。例如，[`AtomicLong`](http://tutorials.jenkov.com/java-util-concurrent/atomiclong.html) 或 [`AtomicReference`](http://tutorials.jenkov.com/java-util-concurrent/atomicreference.html) 或其他之一。

如果只有一个线程读取和写入 `volatile` 变量的值，而其他线程仅读取该变量，则保证读取线程可以看到写入 `volatile` 变量的最新值。如果不使变量 `volatile` ，则将无法保证。

关键字 `volatile` 可以在 32 位和 64 位变量上工作。

## volatile 性能分析

读取和写入 `volatile` 变量会使该变量被读取或写入主存储器。与访问 CPU 缓存相比，读写主存储器的开销更大。访问 `volatile` 变量还可以防止指令重新排序，这是正常的性能增强技术。因此，仅在确实需要增强变量的可见性时才应使用 `volatile` 变量。

