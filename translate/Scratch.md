## 作为原子操作的比较并交换

现代 CPU 内置了对原子比较和交换操作的支持。在 Java 5 中，您可以通过 `java.util.concurrent.atomic` 包中的一些新的原子类访问 CPU 中的这些功能。

这是一个示例，展示了如何使用 `AtomicBoolean` 类来实现前面所示的 `lock()` 方法：

```java
public static class MyLock {
    private AtomicBoolean locked = new AtomicBoolean(false);

    public boolean lock() {
        return locked.compareAndSet(false, true);
    }

}
```

注意，`locked` 变量不再是 `boolean` 而是 `AtomicBoolean`。此类具有 `compareAndSet()` 函数，该函数会将 `AtomicBoolean` 实例的值与期望值进行比较，如果等于期望值，则将其交换为新值。在这种情况下，它将 `locked` 的值与 `false` 进行比较，如果它是 `false` ，则将 `AtomicBoolean` 的新值设置为 `true`。

如果交换了值，则 `compareAndSet()` 方法返回 `true`，否则返回 `false`。

使用 Java 5+ 附带的比较和交换功能而不是自己实现的优点是，Java 5+ 内置的比较和交换功能使您可以利用应用程序所运行的 CPU 的基础比较和交换功能。这使您的比较和交换代码更快。