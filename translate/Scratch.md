## Java volatile 可见性保证

Java `volatile` 关键字尝试解决可见性问题。通过声明 `counter` 变量为 `volatile` ，所有 `counter` 变量的写入都会被立即写回主内存。同时，所有 `counter` 变量的读取都会直接来自主内存。

声明 `volatile` 变量 `counter` 如下：

```java
public class SharedObject {

    public volatile int counter = 0;

}
```

声明变量为 `volatile` 提供了该变量的写入对其他线程的可见性保证。

上面给出的场景中，一个线程(T1)修改 `counter` ，另一个线程(T2)读取 `counter` 而不修改它，声明 `counter` 为 `volatile` 足以保证 T2 对 `counter` 变量写入的可见性。

但是，如果 T1 和 T2 都在增加 `counter` 变量，那么声明 `counter` 变量 `volatile` 将是不够的。接下来解释。

### 完整 volatile 可见性保证

实际上，Java `volatile` 的可见性保证不仅局限于 `volatile` 变量本身。完整的可见性保证如下：

- 如果线程 A 写入一个 `volatile` 变量，然后线程 B 随后读取相同的 `volatile` 变量，那么在写入 `volatile` 变量之前，线程 A 可见的所有变量，在线程 B 读取 `volatile` 变量之后也将对其可见。
- 如果线程 A 读取了 `volatile` 变量，那么读取 `volatile` 变量时线程 A 可见的所有所有变量也将从主内存中重新读取。

代码示例：

```java
public class MyClass {
    private int years;
    private int months
    private volatile int days;


    public void update(int years, int months, int days){
        this.years  = years;
        this.months = months;
        this.days   = days;
    }
}
```

`udpate()` 方法写入三个变量，其中只有 `days` 是 `volatile` 的。

完整的 `volatile` 可见性保证的含义是，当一个值被写入 `days`，所有对线程可见的变量也都会被写入主内存。也就是说，当一个值被写入 `days`， `years` 和 `months` 的值也会同时被写入主内存。

当读取 `years`， `months` 和 `days` 时，可以这样做：

```java
public class MyClass {
    private int years;
    private int months
    private volatile int days;

    public int totalDays() {
        int total = this.days;
        total += months * 30;
        total += years * 365;
        return total;
    }

    public void update(int years, int months, int days){
        this.years  = years;
        this.months = months;
        this.days   = days;
    }
}
```

注意，`totalDays()` 方法是通过将 `days` 的值读入 `total` 变量开始的。当读取 `days` 的值时， `months` 和 `years` 的值也被从主存储器读入。因此，可以保证按照上述读取顺序看到 `days`，`months` 和 `years` 的最新值。