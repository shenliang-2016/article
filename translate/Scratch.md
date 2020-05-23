## volatile 并不总是足够

即使 `volatle` 关键字保证直接从主内存读取所有的 `volatile` 变量，所有对 `volatile` 变量的写入都直接写入主内存，仍然存在某些情况，仅仅将变量声明为 `volatile` 是不够的。

在上文中解释的情况下，只有一个线程 1 对共享变量 `counter` 进行写入，将该变量声明为 `volatile` 就足以保证线程 2 始终都能看到最新写入的值。

事实上，如果写入变量的新值不依赖于变量的先前值，多个线程甚至能够同时写入共享的 `volatile` 变量，仍然能够保证主内存中存储正确的值。

In fact, multiple threads could even be writing to a shared `volatile` variable, and still have the correct value stored in main memory, if the new value written to the variable does not depend on its previous value. In other words, if a thread writing a value to the shared `volatile` variable does not first need to read its value to figure out its next value.

As soon as a thread needs to first read the value of a `volatile` variable, and based on that value generate a new value for the shared `volatile` variable, a `volatile` variable is no longer enough to guarantee correct visibility. The short time gap in between the reading of the `volatile` variable and the writing of its new value, creates an [race condition](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) where multiple threads might read the same value of the `volatile` variable, generate a new value for the variable, and when writing the value back to main memory - overwrite each other's values.

The situation where multiple threads are incrementing the same counter is exactly such a situation where a `volatile` variable is not enough. The following sections explain this case in more detail.

Imagine if Thread 1 reads a shared `counter` variable with the value 0 into its CPU cache, increment it to 1 and not write the changed value back into main memory. Thread 2 could then read the same `counter` variable from main memory where the value of the variable is still 0, into its own CPU cache. Thread 2 could then also increment the counter to 1, and also not write it back to main memory. This situation is illustrated in the diagram below:

![](http://tutorials.jenkov.com/images/java-concurrency/java-volatile-3.png)

Thread 1 and Thread 2 are now practically out of sync. The real value of the shared `counter` variable should have been 2, but each of the threads has the value 1 for the variable in their CPU caches, and in main memory the value is still 0. It is a mess! Even if the threads eventually write their value for the shared `counter` variable back to main memory, the value will be wrong.

## volatile 何时足够？

As I have mentioned earlier, if two threads are both reading and writing to a shared variable, then using the `volatile` keyword for that is not enough. You need to use a [synchronized](http://tutorials.jenkov.com/java-concurrency/synchronized.html) in that case to guarantee that the reading and writing of the variable is atomic. Reading or writing a volatile variable does not block threads reading or writing. For this to happen you must use the `synchronized` keyword around critical sections.

As an alternative to a `synchronized` block you could also use one of the many atomic data types found in the [`java.util.concurrent` package](http://tutorials.jenkov.com/java-util-concurrent/index.html). For instance, the [`AtomicLong`](http://tutorials.jenkov.com/java-util-concurrent/atomiclong.html) or [`AtomicReference`](http://tutorials.jenkov.com/java-util-concurrent/atomicreference.html) or one of the others.

In case only one thread reads and writes the value of a volatile variable and other threads only read the variable, then the reading threads are guaranteed to see the latest value written to the volatile variable. Without making the variable volatile, this would not be guaranteed.

The `volatile` keyword is guaranteed to work on 32 bit and 64 variables.

## volatile 性能分析

Reading and writing of volatile variables causes the variable to be read or written to main memory. Reading from and writing to main memory is more expensive than accessing the CPU cache. Accessing volatile variables also prevent instruction reordering which is a normal performance enhancement technique. Thus, you should only use volatile variables when you really need to enforce visibility of variables.