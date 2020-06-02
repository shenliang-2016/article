# AtomicInteger

`AtomicInteger` 类为您提供了一个 `int` 变量，该变量可以原子方式读写，并且还包含高级原子操作，如 `compareAndSet()`。`AtomicInteger` 类位于 `java.util.concurrent.atomic` 包中，因此完整的类名是 `java.util.concurrent.atomic.AtomicInteger`。本文描述了 Java 8 中的 `AtomicInteger` 版本，但第一个版本是添加到 Java 5 中的。

`AtomicInteger` 设计背后的动机在我的并发教程的 [Compare and Swap](http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html) 部分中做了解释。

## 创建 AtomicInteger

如下创建 `AtomicInteger` ：

```java
AtomicInteger atomicInteger = new AtomicInteger();
```

这个例子使用初始值 `0` 创建了一个 `AtomicInteger`。

如果你想要使用初始值创建 `AtomicInteger`，可以这样做：

```java
AtomicInteger atomicInteger = new AtomicInteger(123);
```

此示例将值 `123` 作为参数传递给 `AtomicInteger` 构造函数，该构造函数将 `AtomicInteger` 实例的初始值设置为 `123`。

## 获取 AtomicInteger 的值

你可以通过 `get()` 方法获取 `AtomicInteger` 实例的值。如下所示：

```java
AtomicInteger atomicInteger = new AtomicInteger(123);

int theValue = atomicInteger.get();
```

## 设定 AtomicInteger 的值

你可以通过 `set()` 方法设定 `AtomicInteger` 实例的值。如下所示：

```java
AtomicInteger atomicInteger = new AtomicInteger(123);

atomicInteger.set(234);
```

例子使用初始值 `123` 创建一个 `AtomicInteger` ，下一行代码将其值设定为 `234`。

## 比较并替换 AtomicInteger 的值

`AtomicInteger` 类还具有原子的 `compareAndSet()` 方法。该方法将 `AtomicInteger` 实例的当前值与期望值进行比较，如果两个值相等，则为 `AtomicInteger` 实例设置一个新值。这是一个 `AtomicInteger.compareAndSet()` 示例：

```java
AtomicInteger atomicInteger = new AtomicInteger(123);

int expectedValue = 123;
int newValue      = 234;
atomicInteger.compareAndSet(expectedValue, newValue);
```

此示例首先创建一个初始值为 `123` 的 `AtomicInteger` 实例。然后，它将 `AtomicInteger` 的值与期望值 `123` 进行比较，如果它们相等，则 `AtomicInteger` 的新值将变为 `234`。

## 增加 AtomicInteger 的值

`AtomicInteger` 类包含一些方法，可用于将值添加到 `AtomicInteger` 并返回其值。这些方法是：

- `addAndGet()`
- `getAndAdd()`
- `getAndIncrement()`
- `incrementAndGet()`

第一个方法 `addAndGet()` 将一个数字添加到 `AtomicInteger` 中，并在添加后返回其值。第二种方法 `getAndAdd()` 也向 `AtomicInteger` 添加一个数字，但返回 `AtomicInteger` 在添加之前的值。应该使用这两种方法中的哪一种取决于您的场景。示例如下：

```java
AtomicInteger atomicInteger = new AtomicInteger();


System.out.println(atomicInteger.getAndAdd(10));
System.out.println(atomicInteger.addAndGet(10));
```

本示例将打印出值 `0` 和 `20`。首先，该示例在添加 `10` 之前获取 `AtomicInteger` 的值。其执行加法前的值为 `0`。然后，该示例将 `10` 加到 `AtomicInteger` 中，并获得执行加法后的值。现在的值为 `20`。

您也可以通过这两种方法在 `AtomicInteger` 中添加负数。结果实际上是相减。

方法 `getAndIncrement()` 和 `incrementAndGet()` 的工作方式与 `getAndAdd()` 和 `addAndGet()` 的相同，只是将 `AtomicInteger` 的值加 `1`。

## 减少 AtomicInteger 的值

`AtomicInteger` 类还包含一些原子性的从 `AtomicInteger` 值中减去值的方法。这些方法是：

- `decrementAndGet()`
- `getAndDecrement()`

`decrementAndGet()` 从 `AtomicInteger` 值中减去 `1`，并在减法后返回其值。`getAndDecrement()` 也从 `AtomicInteger` 值中减去 `1`，但返回减法之前 `AtomicInteger` 的值。

