## 指令重排序挑战

为了提高程序性能，JVM 和 CPU 可以对指令进行重排序，同时保持指令的语义不变。比如，下面的指令：

```java
int a = 1;
int b = 2;

a++;
b++;
```

这些指令可以被如下重新排序，而不会丢失程序的语义：

```java
int a = 1;
a++;

int b = 2;
b++;
```

不过，当存在 `volatile` 变量时，指令重排序就会带来一些挑战。让我们来重新审视前面使用过的 `MyClass` 例子：

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

一旦 `update()` 方法将一个值写入 `days`，新的写入 `years` 和 `months` 的值也会被同时写入主内存。但是，当 JVM 对指令进行进行重排序之后：

```java
public void update(int years, int months, int days){
    this.days   = days;
    this.months = months;
    this.years  = years;
}
```

`months`  和 `years` 的值在 `days` 变量值变化的时候仍然会被写入主内存，但是此时写入动作发生在对 `months` 和 `years` 赋新值之前。因此，新的值就没有正确地对其他线程可见。也就是重排序之后的指令语义发生了变化。

Java 对此问题有一套解决方案，接下来介绍。

## Java volatile Happens-Before 保证

为了应对指令重排序挑战，Java `volatile` 关键字在可见性保证基础上，又提供了 "happens-before" 保证。该保证含义如下：

- 对其他变量的读取和写入不能被重排序为发生在写入 `volatile` 变量之后，如果该读取和写入本来发生在写入 `volatile` 之前。`volatile` 变量写入操作之前的读写操作保证会发生在 `volatile` 变量写入之前。注意，本来发生在 `volatile` 变量写入操作之后的对其他变量的读取操作还是有可能会被重排序到发生在 `volatile` 变量写入操作之前。而非相反。也就是说，经过指令重排序，后面的移动到前面允许，前面移动到后面不允许。

- 对其他变量的读取和写入不能被重排序为发生在读取 `volatile` 变量之前，如果该读取和写入本来发生在读取 `volatile` 之后。注意，本来发生在 `volatile` 变量读取操作之前的对其他变量的读取操作还是有可能会被重排序到发生在 `volatile` 变量读取操作之后。而非相反。也就是说，经过指令重排序，前面的移动到后面允许，后面的移动到前面不允许。

上述 "happens-before" 保证假定 `volatile` 关键字的可见性保证正在发挥作用。

