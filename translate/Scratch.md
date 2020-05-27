# 比较并交换

**Compare and swap**  CAS 比较并交换是一种用来设计并发算法的技术。基本上，CAS 将变量的实际值与一个期望值进行比较，如果相等，则将变量的值交换为一个新值。CAS 可能听起来有些复杂，不过实际上非常易于理解。接下来我们来进一步探讨这个话题。

## CAS 支持的场景

在程序和并发算法中非常常见的一种模式就是"检查然后操作"模式。代码首先检查一个变量的值，然后基于该变量的值执行操作。下面是个简单的例子：

```java
class MyLock {

    private boolean locked = false;

    public boolean lock() {
        if(!locked) {
            locked = true;
            return true;
        }
        return false;
    }
}
```

这段代码如果被用于多线程应用，可能会发生很多错误，不过我们暂时忽略这些问题。

如你所见，`lock()` 方法首先检查 `locked` 成员变量值是否等于 `false` (检查)，如果相等则将其值设置为 `true` (操作)。

如果多个线程访问同一个 `Mylock` 实例，上面的 `lock()` 方法将无法保证正常工作。如果线程 A 检查 `locked` 值并发现它是 `false` ，线程 B 可能同时也检查 `locked` 的值并发现它是 `false` 。或者，实际上线程 B 可以在线程 A 检查 `locked` 值然后发现其值是 `false` 之后，而在线程 A 将 `locked` 设定为 `true` 之前的任何时刻检查 `locked` 值。因此，线程 A 和线程 B 都会看到 `locked` 值为 `false` ，然后基于这个检查结果执行后续操作。

为了能够在多线程应用中正确工作，"检查然后操作"逻辑必须是原子性的。原子性意味着"检查"和"操作"逻辑都必须作为原子性的代码块执行。任何开始执行该原子性代码块的线程都将在不受其他线程干扰的情况下完成代码块的执行。不能有其他线程同时执行该原子性代码块。

这是以前的代码示例的改进版，其中使用 `synchronized` 关键字将 `lock()` 方法转换为一个原子代码块：

```java
class MyLock {

    private boolean locked = false;

    public synchronized boolean lock() {
        if(!locked) {
            locked = true;
            return true;
        }
        return false;
    }
}
```

现在，`lock()` 方法已同步，因此同一时刻只能有一个线程在同一 `MyLock` 实例上执行它。 `lock()` 方法实际上是原子的。

原子的 `lock()` 方法实际上是“比较和交换”的一个例子。 `lock()` 方法将变量 `locked` 与期望值 `false` 进行比较，如果 `locked` 等于该期望值，则将变量的值交换为 `true`。

