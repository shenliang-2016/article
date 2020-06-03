# AtomicLongArray

Java `AtomicLongArray` 类 (`java.util.concurrent.atomic.AtomicLongArray`) 表示一个 `long` 数组。`AtomicLongArray` 中的元素可以原子性地更新。`AtomicLongArray` 也支持 [compare-and-swap](http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html) 功能。

## 创建 AtomicLongArray

你可以使用两个构造器之一创建 `AtomicLongArray` 。

第一个构造器使用 `int` 作为参数。该 `int` 参数指定了创建的 `AtomicLongArray` 的长度，意味着它拥有的空间可以存储多少个元素。如下所示：

```java
AtomicLongArray array = new AtomicLongArray(10);
```

本示例创建一个容量为 10 个 `long` 的 `AtomicLongArray`（它具有 10 个 `long` 元素的空间）。

第二个构造函数采用一个 `long[]` 数组作为参数。使用此构造函数创建的 `AtomicLongArray` 具有与 `array` 参数相同的容量，并且该 `array` 参数中的所有元素都将被复制到 `AtomicLongArray` 中。这是一个使用此构造函数创建 `AtomicLongArray` 的示例：

```java
long[] longs = new long[10];

longs[5] = 123;

AtomicLongArray array = new AtomicLongArray(longs);
```

这个例子首先创建一个 `long[]` 数组，并为索引为 5 的元素设置一个值。然后，它创建一个 `long[]` 数组作为参数的 `AtomicLongArray`。

## get()

您可以使用 `AtomicLongArray` 上的 `get()` 方法来获取给定元素的值。这是调用 `get()` 方法的示例：

```java
long value = array.get(5);
```

## set()

您可以使用 `AtomicLongArray` 上的 `set()` 方法来设置给定元素的值。这是调用 `set()` 方法的示例：

```java
array.set(5, 999);
```

## compareAndSet()

`compareAndSet()` 方法用于将给定元素的值与指定值进行比较，如果两个值相等，则为该元素设置一个新值。这是 `AtomicLongArray` 支持原子比较和交换功能的示例。一次只能有一个线程可以执行 `compareAndSet()` 方法。

调用 `AtomicLongArray` 的 `compareAndSet()` 方法如下：

```java
boolean swapped = array.compareAndSet(5, 999, 123);
```

本示例将索引为 5 的元素与期望值 999 进行比较，如果相等，则为索引为 5 的元素设置新值 123。`compareAndSet()` 方法返回值为 `true` 的布尔值，表示元素设置了一个新值。否则返回为 `false`（如果该元素不等于期望值）。

## addAndGet()

`AtomicLongArray` 还包含一种方法，可用于将值添加到给定元素，并返回该元素的新值。调用 `addAndGet()` 也是一个原子操作（就像对 `AtomicLongArray` 的所有操作一样）。这是调用 `addAndGet()` 的示例：

```java
long newValue = array.addAndGet(5, 3);
```

代码执行之后 `newValue` 变量将包含索引为 5 的元素的值，并增加 3。

## getAndAdd()

`AtomicLongArray` 类还包含一个名为 `getAndAdd()` 的方法。`getAndAdd()` 方法的作用与 `addAndGet()` 方法相同，不同之处在于 `getAndAdd()` 方法在元素添加值之前返回元素的值。这是一个 `getAndAdd()` 示例：

```java
long oldValue = array.getAndAdd(5, 3);
```

执行完此代码后，`oldValue` 变量将包含索引为 5 的元素的旧值，然后再将值 3 添加到其中。

## incrementAndGet()

`incrementAndGet()` 方法将给定元素的值递增（加 1），并返回该元素的新值。这是一个 `incrementAndGet()` 示例：

```java
long newValue = array.incrementAndGet(5);
```

执行此代码后，`newValue` 变量将包含索引为 5 的元素的值，并添加 1。

## getAndIncrement()

`AtomicLongArray` 类还包含一个名为 `getAndIncrement()` 的方法。`getAndIncrement()` 方法的功能与 `incrementAndGet()` 方法的功能相同，不同之处在于 `getAndIncrement()` 方法在元素递增之前返回元素的值。这是一个 `getAndIncrement()` 示例：

```java
long oldValue = array.getAndIncrement(5);
```

执行完此代码后，`oldValue` 变量将包含索引为 5 的元素的旧值，然后将其递增（添加 1）。

## decrementAndGet()

`decrementAndGet()` 方法将给定元素的值递减（减去1），并返回该元素的新值。这是一个 `decrementAndGet()` 的例子：

```java
long newValue = array.decrementAndGet(5);
```

执行完此代码后，`newValue` 变量将包含索引为 5 的元素的值，并减去 1。

## getAndDecrement()

`AtomicLongArray` 类还包含一个名为 `getAndDecrement()` 的方法。`getAndDecrement()` 方法与 `decrementAndGet()` 方法的功能相同，不同之处在于 `getAndDecrement()` 方法在减量之前返回元素的值。这是一个 `getAndDecrement()` 示例：

```java
long oldValue = array.getAndDecrement(5);
```

执行完此代码后，`oldValue` 变量将包含索引为 5 的元素的旧值，然后将其递减（从中减去 1）。

## 附加方法

`AtomicLongArray` 还有其他几种方法可以用于特殊目的。您应该查看 JavaDoc 中的 `AtomicLongArray` 类，以了解有关这些方法的更多信息。

