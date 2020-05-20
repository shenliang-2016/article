# 线程安全和不可变性

[竞争条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) 只有在多个线程同时访问相同的资源，而其中一个或者多个线程写入该资源时才会发生。如果多个线程都只是读取资源，则竞争条件就不会发生。

可以确保线程共享的对象永远不会被任何线程修改的办法是使用不可变的共享对象，这样也就可以实现线程安全。如下面例子所示：

```java
public class ImmutableValue{

  private int value = 0;

  public ImmutableValue(int value){
    this.value = value;
  }

  public int getValue(){
    return this.value;
  }
}
```

注意如何在构造函数中传递 `ImmutableValue` 实例的值。还请注意，没有 setter 方法。一旦创建了 `ImmutableValue` 实例，您将无法更改其值，这是一成不变的。但是，您可以使用 `getValue()` 方法读取它。

如果您需要在 `ImmutableValue` 实例上执行操作，可以通过返回一个新实例并返回该操作产生的值来执行此操作。这是增加操作的示例：

```java
public class ImmutableValue{

  private int value = 0;

  public ImmutableValue(int value){
    this.value = value;
  }

  public int getValue(){
    return this.value;
  }

  
      public ImmutableValue add(int valueToAdd){
      return new ImmutableValue(this.value + valueToAdd);
      }
  
}
```

注意 `add()` 方法返回一个新的 `ImmutableValue` 实例，携带加法操作的结果，而不是将原来的值加上参数值。

## 引用不是线程安全的！

记住这一点非常重要：即使对象是不可变的，因而是线程安全的，指向该对象的引用却可能是非线程安全的。考虑下面的例子：

```java
public class Calculator{
  private ImmutableValue currentValue = null;

  public ImmutableValue getValue(){
    return currentValue;
  }

  public void setValue(ImmutableValue newValue){
    this.currentValue = newValue;
  }

  public void add(int newValue){
    this.currentValue = this.currentValue.add(newValue);
  }
}
```

`Calculator` 类包含对 `ImmutableValue` 实例的引用。注意，如何通过 `setValue()` 和 `add()` 方法都可以更改该引用。因此，即使 `Calculator` 类在内部使用不可变对象，它本身也不是不可变的，因此不是线程安全的。换句话说：`ImmutableValue` 类是线程安全的，但**使用**不是。尝试通过不变性实现线程安全时，请牢记这一点。

为了使 `Calculator` 类线程安全，您可以声明 `getValue()`，`setValue()` 和 `add()` 方法为 `synchronized`。这样就可以了。

