# AtomicLong

`AtomicLong` 类提供了一个 `long` 变量，可以原子性地读取和写入，同时还包含高级的原子操作，比如 `compareAndSet()`。`AtomicLong` 类位于 `java.util.concurrent.atomic` 包中，完整类名是 `java.util.concurrent.atomic.AtomicLong`。本文描述的是 Java 8 中的版本，不过最初的版本是在 Java 5 中添加的。

`AtomicLong` 设计背后的动机在我的并发教程的 [Compare and Swap](http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html) 部分中做了解释。

## 创建 AtomicLong

如下创建 `AtomicLong` ：

```java
AtomicLong atomicLong = new AtomicLong();
```

使用初始值 `0` 创建 `AtomicLong` 。

如果你想要使用初始值创建 `AtomicLong` ，可以这样做：

```java
AtomicLong atomicLong = new AtomicLong(123);
```

上面的例子将 `123` 作为参数传递给 `AtomicLong` 的构造器，这将新的 `AtomicLong` 实例的初始值设定为 `123` 。

## 获取 AtomicLong 的值

你可以通过 `get()` 方法得到 `AtomicLong` 实例的值。如下所示：

```java
AtomicLong atomicLong = new AtomicLong(123);

long theValue = atomicLong.get();
```

## 设置 AtomicLong 的值

你可以通过 `set()` 方法设定 `AtomicLong` 实例的值。如下所示：

```java
AtomicLong atomicLong = new AtomicLong(123);

atomicLong.set(234);
```

例子使用初始值 `123` 创建 `AtomicLong` 实例，下一行代码设定其值为 `234`。

## 比较并设定 AtomicLong 的值

`AtomicLong` 类还有一个原子性 `compareAndSet()` 方法。该方法比较 `AtomicLong` 实例的当前值与期望值，如果两者相等，则为 `AtomicLong` 实例设置新值。下面是 `AtomicLong.compareAndSet()` 的示例：

```java
AtomicLong atomicLong = new AtomicLong(123);

long expectedValue = 123;
long newValue      = 234;
atomicLong.compareAndSet(expectedValue, newValue);
```

本示例首先创建一个初始值为 `123` 的 `AtomicLong` 实例。然后，它将 `AtomicLong` 的值与期望值 `123` 进行比较，如果它们相等，则 `AtomicLong` 的新值将变为 `234`。

## 增加 AtomicLong 的值

`AtomicLong` 类包含一些可以增加 `AtomicLong` 的值并返回其值的方法。如下：

- `addAndGet()`
- `getAndAdd()`
- `getAndIncrement()`
- `incrementAndGet()`

第一个方法 `addAndGet()` 将一个数字添加到 `AtomicLong` 中，并在添加后返回其值。第二种方法 `getAndAdd()` 也向 `AtomicLong` 添加了一个数字，但是返回了 `AtomicLong` 在添加之前的值。您应该使用这两种方法中的哪一种取决于您的场景。这是示例：

```java
AtomicLong atomicLong = new AtomicLong();


System.out.println(atomicLong.getAndAdd(10));
System.out.println(atomicLong.addAndGet(10));
```

本示例将打印出值 `0` 和 `20`。首先，示例在增加 `10` 之前获得 `AtomicLong` 的值。其加法前的值为 `0`。然后，该示例将 `10` 加到 `AtomicLong` 中，并获得加法后的值。现在的值为 `20`。

您也可以通过这两种方法在 `AtomicLong` 中添加负数。结果实际上是相减。

`getAndIncrement()` 和 `incrementAndGet()` 方法的工作方式与 `getAndAdd()` 和 `addAndGet()` 的工作原理相同，只是将 `AtomicLong` 的值加 `1`。

## 减少 AtomicLong 的值

`AtomicLong` 类还包含一些原子性减少其值的方法。如下：

- `decrementAndGet()`
- `getAndDecrement()`

`decrementAndGet()` 从 `AtomicLong` 值中减去 `1`，并在减去后返回其值。`getAndDecrement()` 也从 `AtomicLong` 值中减去 `1`，但返回减法前 `AtomicLong` 的值。

