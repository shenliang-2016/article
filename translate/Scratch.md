## ThreadLocal 初始值

可以为 Java `ThreadLocal` 设置一个初始值，该值将在首次调用 `get()` 时使用——在以新值调用 `set()` 之前。您可以通过两种方式为 `ThreadLocal` 指定初始值：

- 创建 `ThreadLocal` 子类并覆写 `initialValue()` 方法。
- 使用 `Supplier` 接口的实现创建 `ThreadLocal` 。

接下来详细介绍两种方法。

### 覆写 initialValue()

第一种为 Java `ThreadLocal` 变量指定初始值的方法是创建一个 `ThreadLocal` 子类并覆盖 `initialValue()` 方法。最简单的创建 `ThreadLocal` 子类的方法就是简单地创建一个匿名子类，就在你创建该 `ThreadLocal` 变量的位置。下面是创建一个 `ThreadLocal` 的匿名子类并覆盖 `initialValue()` 方法的例子：

```java
private ThreadLocal myThreadLocal = new ThreadLocal<String>() {
    @Override protected String initialValue() {
        return String.valueOf(System.currentTimeMillis());
    }
};    
```

注意，不同的线程会看到不同的初始值。每个线程将创建自己的初始值。只有当你从 `initialValue()` 方法返回同一个对象时，所有线程才能看到相同的对象。然而，使用 `ThreadLocal` 的根本目的就是避免不同的线程看到相同的变量对象实例。

### 提供 Supplier 实现

第二种为 Java `ThreadLocal` 变量指定初始值的方法是使用静态工厂方法 `withInitial(Supplier)` 传递一个 `Supplier` 接口实现作为参数。该 `Supplier` 实现提供 `ThreadLocal` 的初始值。示例如下：

```
ThreadLocal<String> threadLocal = ThreadLocal.withInitial(new Supplier<String>() {
    @Override
    public String get() {
        return String.valueOf(System.currentTimeMillis());
    }
});
```

由于 `Supplier` 是一个 [函数式接口](http://tutorials.jenkov.com/java-functional-programming/functional-interfaces.html) ，它可以使用 [Java Lambda Expression](http://tutorials.jenkov.com/java/lambda-expressions.html) 实现。下面示例展示了如何使用 lambda 表达式提供 `Supplier` 实现给 `withInitial()` ：

```java
ThreadLocal threadLocal = ThreadLocal.withInitial(
        () -> { return String.valueOf(System.currentTimeMillis()); } );
```

如你所见，这样会简短一些。不过还能继续变短，使用最紧凑语法的 lambada 表达式：

```java
ThreadLocal threadLocal3 = ThreadLocal.withInitial(
        () -> String.valueOf(System.currentTimeMillis()) );
```

