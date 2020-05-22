# Java Volatile 关键字

Java `volatile` 关键字用于将 Java 变量标记为"被存储在主内存中"。更精确的含义，每次都从计算机的主内存中读取 `volatile` 变量，而不是从 CPU 缓存中。同时，每次对 `volatile` 变量的写入都会直接写入主内存，而不仅仅写入 CPU 缓存。

实际上，Java 5 以来，`volatile` 关键字不仅仅提供了从主内存读写 `volatile` 变量的保证，接下来将详细介绍其他功能。

## 变量可见性问题

Java `volatile` 关键字保证对共享变量的修改在线程之间的可见性。听起来可能有点抽象，让我们来解释一下。

早多线程应用中，多个线程操作非 `volatile` 变量，为了提高性能，每个线程都会从主内存将变量拷贝到自己的 CPU 缓存中。如果你的计算机有多个 CPU，每个线程可能都运行在不同的 CPU 上。这就意味着，每个线程都会将变量拷贝到各自不同的 CPU 缓存中。如下图所示：

![](http://tutorials.jenkov.com/images/java-concurrency/java-volatile-1.png)

使用非 `volatile` 变量，无法保证 JVM 何时会从主内存读取数据到 CPU 缓存中，何时将 CPU 缓存中的数据写回主内存。下面我将介绍这种情况可能导致的若干问题。

设想这种情况，两个或者更多线程需要访问一个包含计数器变量的共享对象，声明如下：

```java
public class SharedObject {

    public int counter = 0;

}
```

同时假想，只有线程 1 增加 `counter` 变量，不过线程 1 和线程 2 可能不时读取 `counter` 变量。

如果 `counter` 变量没有声明为 `volatile` ，就无法保证该变量的值会被从 CPU 缓存写回主内存。这就意味着，CPU 缓存中的 `counter` 变量的值可能与主内存中的不同。如下所示：

![](http://tutorials.jenkov.com/images/java-concurrency/java-volatile-2.png)

这种由于其他线程没有将变量的缓存写回主内存而导致的线程无法看到变量的最新值的问题，被称为"可见性"问题。一个线程的更新结果对别的线程不可见。