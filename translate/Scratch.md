## 不可变对象

如果一个对象的状态在构造后不能改变，则该对象被认为是*不可变的*。最大程度上依赖不可变对象被广泛接受为创建简单，可靠代码的合理策略。

不可变对象在并发应用程序中特别有用。由于它们不能改变状态，因此它们不会被线程干扰破坏或在不一致状态下被观察到。

程序员通常不愿意使用不可变对象，因为他们担心创建新对象的成本而不是更新对象。对象创建的影响经常被高估，并且可以通过与不可变对象相关联的一些效率来抵消。这些包括由于垃圾收集而减少的开销，以及消除保护可变对象免于损坏所需的代码。

以下小节采用其实例可变的类，并从中派生出具有不可变实例的类。通过这样做，它们为这种转换提供了一般规则，并展示了不可变对象的一些优点。

### 同步类示例

[`SynchronizedRGB`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SynchronizedRGB.java) 类定义了表示颜色的对象。每个对象将颜色表示为代表主要颜色值的三个整数和一个给出颜色名称的字符串。

```java
public class SynchronizedRGB {

    // Values must be between 0 and 255.
    private int red;
    private int green;
    private int blue;
    private String name;

    private void check(int red,
                       int green,
                       int blue) {
        if (red < 0 || red > 255
            || green < 0 || green > 255
            || blue < 0 || blue > 255) {
            throw new IllegalArgumentException();
        }
    }

    public SynchronizedRGB(int red,
                           int green,
                           int blue,
                           String name) {
        check(red, green, blue);
        this.red = red;
        this.green = green;
        this.blue = blue;
        this.name = name;
    }

    public void set(int red,
                    int green,
                    int blue,
                    String name) {
        check(red, green, blue);
        synchronized (this) {
            this.red = red;
            this.green = green;
            this.blue = blue;
            this.name = name;
        }
    }

    public synchronized int getRGB() {
        return ((red << 16) | (green << 8) | blue);
    }

    public synchronized String getName() {
        return name;
    }

    public synchronized void invert() {
        red = 255 - red;
        green = 255 - green;
        blue = 255 - blue;
        name = "Inverse of " + name;
    }
}
```

必须小心使用 `SynchronizedRGB` 以避免在不一致的状态下被看到。例如，假设一个线程执行以下代码：

```java
SynchronizedRGB color =
    new SynchronizedRGB(0, 0, 0, "Pitch Black");
...
int myColorInt = color.getRGB();      //Statement 1
String myColorName = color.getName(); //Statement 2
```

如果另一个线程在语句1之后但在语句2之前调用 `color.set`，则 `myColorInt` 的值将不匹配 `myColorName` 的值。为了避免这种结果，必须将两个语句绑定在一起：

```java
synchronized (color) {
    int myColorInt = color.getRGB();
    String myColorName = color.getName();
} 
```

这种不一致只适用于可变对象 - 对于不可变版本的 `SynchronizedRGB`，它不会成为问题。

### 定义不可变对象的策略

以下规则定义了用于创建不可变对象的简单策略。并非所有记录为“不可变”的类都遵循这些规则。这并不一定意味着这些类的创造者是草率的 - 他们可能有充分的理由相信他们的类实例在建造后永远不会改变。但是，这种策略需要复杂的分析，不适合初学者。

1. 不要提供“setter”方法 - 修改字段引用的字段或对象的方法。

2. 使所有字段 `final` 和 `private`。

3. 不允许子类重写方法。最简单的方法是将类声明为 `final`。更复杂的方法是使构造函数 `private` 并在工厂方法中构造实例。

4. 如果实例字段包含对可变对象的引用，则不允许更改这些对象：

   - 不要提供修改可变对象的方法。

   - 不要共享对可变对象的引用。永远不要存储对传递给构造函数的外部可变对象的引用；如有必要，创建副本并存储对副本的引用。同样，必要时创建内部可变对象的副本，以避免在方法中返回原始对象。

将此策略应用于 `SynchronizedRGB` 会导致以下步骤：

1. 本课程中有两个 setter 方法。 第一个，`set`，任意转换对象，并且在类的不可变版本中没有出现。第二个，`invert`，可以通过创建一个新对象而不是修改现有对象来进行调整。
2. 所有字段都已经 `private` 了。他们进一步被声明为 `final` 的。
3. 这个类本身被声明为 `final` 的。

4. 只有一个字段引用一个对象，该对象本身是不可变的。因此，不需要防止改变“包含的”可变对象的状态的保护措施。

这些修改之后，我们得到 [`ImmutableRGB`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/ImmutableRGB.java)：

```java
final public class ImmutableRGB {

    // Values must be between 0 and 255.
    final private int red;
    final private int green;
    final private int blue;
    final private String name;

    private void check(int red,
                       int green,
                       int blue) {
        if (red < 0 || red > 255
            || green < 0 || green > 255
            || blue < 0 || blue > 255) {
            throw new IllegalArgumentException();
        }
    }

    public ImmutableRGB(int red,
                        int green,
                        int blue,
                        String name) {
        check(red, green, blue);
        this.red = red;
        this.green = green;
        this.blue = blue;
        this.name = name;
    }


    public int getRGB() {
        return ((red << 16) | (green << 8) | blue);
    }

    public String getName() {
        return name;
    }

    public ImmutableRGB invert() {
        return new ImmutableRGB(255 - red,
                       255 - green,
                       255 - blue,
                       "Inverse of " + name);
    }
}
```

