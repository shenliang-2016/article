# AtomicReference

`AtomicReference` 类提供了一个对象引用变量，可以原子地对其进行读写。原子性的意思是，多个线程试图更改相同的 `AtomicReference`（例如，通过“比较并交换”操作）不会使 `AtomicReference` 最终处于不一致状态。`AtomicReference` 还具有高级的 `compareAndSet()` 方法，该方法可让您将引用与期望值（引用）进行比较，如果它们相等，则在 `AtomicReference` 对象内设置新引用。

## 创建 AtomicReference

你可以如下创建 `AtomicReference` ：

```java
AtomicReference atomicReference = new AtomicReference();
```

如果你需要用初始引用创建 `AtomicReference` ，就这样做：

```java
String initialReference = "the initially referenced string";
AtomicReference atomicReference = new AtomicReference(initialReference);
```

### 创建类型化的 AtomicReference

你可以使用 Java 范型创建类型化的 `AtomicReference`，如下所示：

```java
AtomicReference<String> atomicStringReference =
    new AtomicReference<String>();
```

你还可以为类型化的 `AtomicReference` 设置初始值，如下所示：

```java
String initialReference = "the initially referenced string";
AtomicReference<String> atomicStringReference =
    new AtomicReference<String>(initialReference);
```

## 获取 AtomicReference 引用

你可以使用 `AtomicReference` 的 `get()` 方法获取存储在 `AtomicReference` 中的引用。如果你操作的是无类型的 `AtomicReference` 则 `get()` 方法会返回一个 `Object` 引用。如果你操作的是类型化的 `AtomicReference` 则 `get()` 方法返回一个你在创建  `AtomicReference` 时声明的类型的引用。

首先是一个非类型化的 `AtomicReference` `get()` 示例：

```java
AtomicReference atomicReference = new AtomicReference("first value referenced");

String reference = (String) atomicReference.get();
```

注意，将 `get()` 方法的返回值转型为 `String` 是必要的，因为对非类型化的 `AtomicReference` 该方法返回的是 `Object` 引用。

下面是类型化 `AtomicReference` 示例：

```java
AtomicReference<String> atomicReference = 
     new AtomicReference<String>("first value referenced");

String reference = atomicReference.get();
```

此时就不需要对 `get()` 的返回值进行转型了。

## 设定 AtomicReference 引用

您可以使用 `set()` 方法设置存储在 `AtomicReference` 实例中的引用。在无类型的 `AtomicReference` 实例中，`set()` 方法将 `Object` 引用作为参数。在类型化 `AtomicReference` 中，`set()` 方法采用您在声明 `AtomicReference` 时声明的任何类型作为为其类型参数。

这是一个 `AtomicReference` `set()` 示例：

```java
AtomicReference atomicReference = 
     new AtomicReference();
    
atomicReference.set("New object referenced");
```

对于无类型或有类型的引用，使用 `set()` 方法没有什么区别。您将遇到的唯一真正的区别是，编译器将限制您可以在类型化的 `AtomicReference` 上设置的类型。

## 比较并设定 AtomicReference 引用

`AtomicReference` 类包含一个名为 `compareAndSet()` 的有用方法。`compareAndSet()` 方法可以将存储在 `AtomicReference` 实例中的引用与期望的引用进行比较，如果两个引用相同（在 `equals()` 中不同但在 `==` 中相同） ，则可以在 `AtomicReference` 实例上设置一个新引用。

如果 `compareAndSet()` 在 `AtomicReference` 中设置了新引用，则 `compareAndSet()` 方法将返回 `true`。否则，`compareAndSet()` 返回 `false`。

这是一个 `AtomicReference`  `compareAndSet()` 示例：

```java
String initialReference = "initial value referenced";

AtomicReference<String> atomicStringReference =
    new AtomicReference<String>(initialReference);

String newReference = "new value referenced";
boolean exchanged = atomicStringReference.compareAndSet(initialReference, newReference);
System.out.println("exchanged: " + exchanged);

exchanged = atomicStringReference.compareAndSet(initialReference, newReference);
System.out.println("exchanged: " + exchanged);
```

本示例创建一个带有初始引用的类型化的 `AtomicReference`。然后，它两次调用 `comparesAndSet()`，将存储的引用与初始引用进行比较，如果存储的引用等于初始引用，则设置一个新引用。这两个引用第一次相同，因此在 `AtomicReference` 上设置了一个新引用。第二次存储的引用是刚刚在调用 `compareAndSet()` 之前设置的新引用，因此存储的引用当然不等于初始引用。因此，没有在 `AtomicReference` 上设置新的引用，并且 `compareAndSet()` 方法返回 `false`。