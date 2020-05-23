# Java ThreadLocal

 *Java* *ThreadLocal* 类使得你可以创建只允许同一个线程读写的变量。因此，即使两个线程执行相同的代码，同时该代码拥有同一个 `ThreadLocal` 变量的引用，这两个线程还是无法看到彼此的 `ThreadLocal` 变量。因此，Java   ThreadLocal 类提供了一种简单的方式保证代码的 [线程安全](http://tutorials.jenkov.com/java-concurrency/thread-safety.html) 。

## 创建 ThreadLocal

你可以像创建任何其他 Java 对象那样创建 `ThreadLocal` 实例——通过 `new` 操作符。示例如下：

```java
private ThreadLocal threadLocal = new ThreadLocal();
```

每个线程只需要这样做一次。现在多个线程可以读取和设置该 `ThreadLocal` 中的值，同时每个线程都只能看到它自己设置的值。

## 设置 ThreadLocal 值

一旦 `ThreadLocal` 被创建出来你就可以设置需要存储在其中的值，使用它的 `set()` 方法。

```java
threadLocal.set("A thread local value");
```

## 获取 ThreadLocal 值

你可以读取存储在 `ThreadLocal` 中的值，使用它的 `get()` 方法。如下所示：

```java
String threadLocalValue = (String) threadLocal.get();
```

## 删除 ThreadLocal 值

删除设置在 ThreadLocal 变量中的值是可能的。你可以调用 `ThreadLocal` 的 `remove()` 方法。如下所示：

```java
threadLocal.remove();
```

## 范型 ThreadLocal

你可以使用范型类型创建 `ThreadLocal`。使用范型类型时，只有范型类型对象可以被设置为 `ThreadLocal` 值。另外，你必须对 `get()` 方法返回的值进行类型转换。如下面例子所示：

```java
private ThreadLocal<String> myThreadLocal = new ThreadLocal<String>();
```

现在你只能在 `ThreadLocal` 实例中存储字符串。另外，你不需要对获取自 `ThreadLocal` 的值进行类型转换：

```java
myThreadLocal.set("Hello ThreadLocal");

String threadLocalValue = myThreadLocal.get();
```

