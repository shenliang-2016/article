# AtomicReferenceArray

`java.util.concurrent.atomic` 包中的 `AtomicReferenceArray` 是对象引用的数组，可以原子方式对其进行更新。`AtomicReferenceArray` 类还支持 [compare-and-swap](http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html) 功能。

## 创建 AtomicReferenceArray

您可以使用两个构造函数之一创建一个 `AtomicReferenceArray`。

第一个构造函数采用 `int` 作为参数。这个 `int` 指定要创建的 `AtomicReferenceArray` 的长度，这意味着它应该有多少个元素。这是一个使用此构造函数创建 `AtomicReferenceArray` 的示例：

```java
AtomicReferenceArray array = new AtomicReferenceArray(10);
```

这个例子创建了一个容量为 10 的 `AtomicReferenceArray` （它有 10 个对象引用作为元素）。

第二个构造函数使用一个 `E[]` 数组作为参数，其中 `E` 是对象引用的类型（类）。使用此构造函数创建的 `AtomicReferenceArray` 将具有与 `array` 参数相同的容量，并且该 `array` 参数中的所有元素都将被复制到 `AtomicReferenceArray` 中。这是一个使用此构造函数创建 `AtomicReferenceArray` 的示例：

```java
Object[] source = new Object[10];

source[5] = "Some string";

AtomicReferenceArray array = new AtomicReferenceArray(source);
```

这个例子首先创建一个 `Object[]` 数组，并为索引为 5 的元素设置一个值。然后，它以 `Object[]` 数组作为参数创建一个 `AtomicReferenceArray`。

您还可以为 `AtomicReferenceArray` 设置范型类型。这是上面的示例，其中泛型类型设置为 `String`：

```java
String[] source = new String[10];

source[5] = "Some string";

AtomicReferenceArray<String> array = 
    new AtomicReferenceArray<String>(source);
```

## get()

`get()` 方法返回给定索引的元素的值。索引作为参数传递给 `get()` 方法。如下所示：

```java
Object element = array.get(5);
```

如果 `AtomicReferenceArray` 拥有范型类型， `get()` 方法返回该类型的对象。比如，如果范型类型是 `String`，然后如下调用 `get()` ：

```java
String element = array.get(5);
```

注意，这里转型为 `String` 是必需的。

## set()

`set()` 方法设置具有特定索引的元素的值。索引和值作为参数传递给 `set()` 方法。这是一个 `set()` 示例：

```java
array.set(5, "another object");
```

第一个参数是要设置的元素的索引。第二个参数是为元素设置的值。如果 `AtomicReferenceArray` 具有泛型类型，则此参数的类型将为该类型。否则，类型为 `Object`。

## compareAndSet()

`AtomicReferenceArray` 的 `compareAndSet()` 方法可以将存储在给定元素中的当前引用与预期引用进行比较，如果引用相同，则将当前引用替换为新引用。这是一个 `compareAndSwap()` 示例：

```java
String string1 = "string1";
String string2 = "string2";
    
String[] source = new String[10];
source[5] = string1;

AtomicReferenceArray<String> array = 
    new AtomicReferenceArray<String>(source);
    

array.compareAndSet(5, string1, string2);
```

此示例首先创建一个 `String` 数组，并将索引为 5 的元素设置为指向 `string1` 的引用。然后，它将索引为 5 的元素的值与 `string1` 引用进行比较，如果它们相同，则将元素的引用设置为 `string2`。如果没有其他线程更改索引为 5 的元素的引用（在上述情况下是不可能的），则设置成功（设置了新引用）。

## 附加方法

`AtomicReferenceArray` 还有其他几种方法可以用于特殊目的。您应该查看 JavaDoc 中的 `AtomicReferenceArray` 类，以了解有关这些方法的更多信息。