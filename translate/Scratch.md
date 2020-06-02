# AtomicBoolean

`AtomicBoolean` 类向你提供了一个 `boolean` 变量，该变量可以原子地读写。同时它还拥有其他一些高级的原子性操作，比如 `compareAndSet()`。`AtomicBoolean` 类位于 `java.util.concurrent.atomic` 包中，完整类名是 `java.util.concurrent.atomic.AtomicBoolean` 。本教程介绍的 `AtomicBoolean` 是 Java 8 版本，不过该类最初是 Java 5 版本加入的。

`AtomicBoolean` 类设计的背后动机在我的 Java 并发教程的 [Compare and Swap](http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html) 部分做了解释。

## 创建 AtomicBoolean

如下创建 `AtomicBoolean` ：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean();
```

这个例子使用值 `false` 创建了一个新的 `AtomicBoolean` 。

如果你需要为 `AtomicBoolean` 实例显式设定初始值，你可以向 `AtomicBoolean` 构造器传递初始值参数：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);
```

## 获取 AtomicBoolean 的值

你可以使用 `get()` 方法获取 `AtomicBoolean` 的值：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);

boolean value = atomicBoolean.get();
```

代码执行之后 `value` 变量将包含 `true`。

## 设定 AtomicBoolean 的值

你可以使用 `set()` 方法设定 `AtomicBoolean` 的值：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);

atomicBoolean.set(false);
```

代码执行之后 `AtomicBoolean` 变量将包含 `false`。

## 替换 AtomicBoolean 的值

你可以使用 `getAndSet()` 方法替换 `AtomicBoolean` 的值。`getAndSet()` 方法返回 `AtomicBoolean` 的当前值，并为其设置一个新值：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);

boolean oldValue = atomicBoolean.getAndSet(false);
```

执行完此代码后，`oldValue` 变量将包含值 `true`，而 `AtomicBoolean` 实例将包含值 `false`。该代码有效地将 `AtomicBoolean` 的当前值 `true` 交换为 `false` 。

## 比较并替换 AtomicBoolean 的值

`compareAndSet()` 方法允许您将 `AtomicBoolean` 的当前值与期望值进行比较，如果当前值等于期望值，则可以在 `AtomicBoolean` 上设置一个新值。`compareAndSet()` 方法是原子的，因此只有一个线程可以同时执行它。因此，`compareAndSet()` 方法可用于实现类似于锁的简单的同步器。

这是一个 `compareAndSet()` 示例：

```java
AtomicBoolean atomicBoolean = new AtomicBoolean(true);

boolean expectedValue = true;
boolean newValue      = false;

boolean wasNewValueSet = atomicBoolean.compareAndSet(
    expectedValue, newValue);
```

本示例将 `AtomicBoolean` 的当前值与 `true` 进行比较，如果两个值相等，则将 `AtomicBoolean` 的新值设置为 `false`。