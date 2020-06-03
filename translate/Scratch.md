# AtomicStampedReference

`AtomicStampedReference` 类提供了一个对象引用变量，可以原子地对其进行读写。原子的意思是，多个线程尝试更改相同的 `AtomicStampedReference` 将不会使 `AtomicStampedReference` 最终处于不一致状态。

`AtomicStampedReference` 与 [`AtomicReference`](http://tutorials.jenkov.com/java-util-concurrent/atomicreference.html) 的不同在于 `AtomicStampedReference` 在内部保留对象引用和标记。可以通过 `compareAndSet()` 方法使用单个原子比较和交换操作来更新引用和标记。

`AtomicStampedReference` 旨在解决 A-B-A 问题，而仅凭 `AtomicReference` 是无法解决的。稍后将介绍 A-B-A 问题。

## 创建 AtomicStampedReference

如下创建 `AtomicStampedReference` ：

```java
Object initialRef   = null;
int    initialStamp = 0;

AtomicStampedReference atomicStampedReference =
    new AtomicStampedReference(intialRef, initialStamp);
```

### 创建类型化 AtomicStampedReference

你可以使用 [Java generics](http://tutorials.jenkov.com/java-generics/index.html) 创建类型化的 `AtomicStampedReference`。如下所示：

```java
String initialRef   = null;
int    initialStamp = 0;

AtomicStampedReference<String> atomicStampedReference =
    new AtomicStampedReference<String>(
        initialRef, initialStamp
    );
```

在此示例中创建的 Java `AtomicStampedReference` 将仅接受对 `String` 实例的引用。如果您知道将存储在引用中的类型，建议始终使用带有明确的泛型类型的 `AtomicStampedReference`。

## 获取 AtomicStampedReference 引用

您可以使用 `AtomicStampedReference` 的 `getReference()` 方法获取存储在 `AtomicStampedReference` 中的引用。如果您有未类型化的 `AtomicStampedReference`，则 `getReference()` 方法将返回一个 `Object` 引用。如果您输入的是类型化的 `AtomicStampedReference`，则 `getReference()` 返回对创建时在 `AtomicStampedReference` 变量上声明的类型的引用。

这是无类型的 `AtomicStampedReference` `getReference()` 示例：

```java
String initialRef = "first text";

AtomicStampedReference atomicStampedReference = (String)
    new AtomicStampedReference(initialRef, 0);

String reference = atomicStampedReference.getReference();
```

注意，必须将 `getReference()` 返回的引用强制转换为 `String`，因为对非类型化的 `AtomicStampedReference`，`getReference()` 返回一个 `Object` 引用。

这是一个键入的 `AtomicStampedReference` 示例：

```java
String initialRef = "first text";

AtomicStampedReference<String> atomicStampedReference =
    new AtomicStampedReference<String>(
        initialRef, 0
    );

String reference = atomicStampedReference.getReference();
```

注意，不再需要强制转换 `getReference()` 返回的引用，因为编译器知道它将返回一个 `String` 引用。

## 获取 AtomicStampedReference 标记

`AtomicStampedReference` 还包含一个 `getStamp()` 方法，通过它可以获取内部存储的标记。如下所示：

```java
String initialRef = "first text";

AtomicStampedReference<String> atomicStampedReference =
    new AtomicStampedReference<>(initialRef, 0);

int stamp = atomicStampedReference.getStamp();
```

## 原子性获取引用和标记

您可以使用 `get()` 方法在单个原子操作中从 `AtomicStampedReference` 获取引用和戳记。`get()` 方法返回引用作为该方法的返回值。标记被插入到作为参数传递给 `get()` 方法的一个 `int[]` 数组中。如下所示：

```java
String initialRef   = "text";
String initialStamp = 0;

AtomicStampedReference<String> atomicStampedReference =
    new AtomicStampedReference<>(
        initialRef, initialStamp
    );

int[] stampHolder = new int[1];
String ref = atomicStampedReference.get(stampHolder);

System.out.println("ref = " + ref);
System.out.println("stamp = " + stampHolder[0]);
```

对于某些类型的并发算法，能够作为单个原子操作同时获得参考和标记很重要。

## 设置 AtomicStampedReference 引用

您可以使用 `set()` 方法设置存储在 `AtomicStampedReference` 实例中的引用。在无类型的 `AtomicStampedReference` 实例中，`set()` 方法将 `Object` 引用作为第一个参数。在类型化的 `AtomicStampedReference` 实例中，`set()` 方法采用任何类型的参数作为声明 `AtomicStampedReference` 时所声明的类型。

这是一个 `AtomicStampedReference` `set()` 示例：

```java
AtomicStampedReference<String> atomicStampedReference =
     new AtomicStampedReference<>(null, 0);


String newRef = "New object referenced";
int    newStamp = 1;

atomicStampedReference.set(newRef, newStamp);
```

对于无类型或有类型的引用，使用 `set()` 方法没有什么区别。您将遇到的唯一真正的区别是，编译器将限制您可以在类型化的 `AtomicStampedReference` 上设置的类型。

## 比较并设定 AtomicStampedReference 引用

`AtomicStampedReference` 类包含一个有用的名为 `compareAndSet()` 的方法。`compareAndSet()` 方法可以将存储在 `AtomicStampedReference` 实例中的引用与期望的引用进行比较，并将存储的标记与期望的标记进行比较，如果两个引用和标记是相同的（在 `equals()` 中不同，在 `==` 中相同），则可以在 `AtomicStampedReference` 实例上设置新的引用。

如果 `compareAndSet()` 在 `AtomicStampedReference` 中设置了新引用，则 `compareAndSet()` 方法将返回 `true`。否则，`compareAndSet()` 返回 `false`。

这是一个 `AtomicStampedReference` `compareAndSet()` 示例：

```java
String initialRef   = "initial value referenced";
int    initialStamp = 0;

AtomicStampedReference<String> atomicStringReference =
    new AtomicStampedReference<String>(
        initialRef, initialStamp
    );

String newRef   = "new value referenced";
int    newStamp = initialStamp + 1;

boolean exchanged = atomicStringReference
    .compareAndSet(initialRef, newRef, initialStamp, newStamp);
System.out.println("exchanged: " + exchanged);  //true

exchanged = atomicStringReference
    .compareAndSet(initialRef, "new string", newStamp, newStamp + 1);
System.out.println("exchanged: " + exchanged);  //false

exchanged = atomicStringReference
    .compareAndSet(newRef, "new string", initialStamp, newStamp + 1);
System.out.println("exchanged: " + exchanged);  //false

exchanged = atomicStringReference
    .compareAndSet(newRef, "new string", newStamp, newStamp + 1);
System.out.println("exchanged: " + exchanged);  //true
```

这个例子首先创建一个 `AtomicStampedReference`，然后使用 `compareAndSet()` 交换引用和标记。

在第一次调用 `compareAndSet()` 之后，该示例尝试两次交换引用和标记两次，但均未成功。首次将 `initialRef` 作为预期参考传递，但此时内部存储的参考为 `newRef`，因此 `compareAndSet()` 调用失败。第二次将 `initialStamp` 作为期望的标记传递，但是此时内部存储的标记是 `newStamp`，因此 `compareAndSet()` 调用失败。

最终的 `compareAndSet()` 调用将成功，因为期望的引用是 `newRef`，期望的标记是 `newStamp`。

## AtomicStampedReference 与 A-B-A 问题

`AtomicStampedReference` 旨在解决 A-B-A 问题。A-B-A 问题是将引用从指向 A 更改为 B，然后再更改为 A 的情况。

当使用比较和交换操作原子地更改引用，并确保只有一个线程可以将引用从旧引用更改为新引用时，检测 A-B-A 情况是不可能的。

A-B-A 问题可能会在 [非阻塞算法](http://tutorials.jenkov.com/java-concurrency/non-blocking-algorithms.html) 中发生。非阻塞算法通常使用对受保护数据结构正在进行的修改的引用，以向其他线程发信号通知当前正在进行修改。如果线程 1 看到没有正在进行的修改（引用指向 `null`），则另一个线程可以提交修改（引用现在为非 `null`），完成修改并将引用换回指向 `null`，而线程 1 并不会检测到它。在我关于 [非阻塞算法](http://tutorials.jenkov.com/java-concurrency/non-blocking-algorithms.html) 的教程中，更详细地说明了非阻塞算法中 A-B-A 问题的确切发生方式。

通过使用 `AtomicStampedReference` 而不是 `AtomicReference`，可以检测到 A-B-A 情况。线程 1 可以使用 `get()` 从原子上复制引用并在 `AtomicStampedReference` 中标记出来。如果另一个线程将引用从 A 更改为 B，然后又更改回 A，则该标记将发生更改（给出的线程会合理地更新标记-例如将其递增）。

以下代码显示了如何使用 `AtomicStampedReference` 检测 A-B-A 情况：

```java
int[] stampHolder = new int[1];
Object ref = atomicStampedReference.get(stampHolder);

if(ref == null){
    //prepare optimistic modification
}

//if another thread changes the
//reference and stamp here,
//it can be detected

int[] stampHolder2 = new int[1];
Object ref2 = atomicStampedReference.get(stampHolder);

if(ref == ref2 && stampHolder[0] == stampHolder2[0]){
    //no modification since optimistic modification was prepared

} else {
    //retry from scratch.
}
```

