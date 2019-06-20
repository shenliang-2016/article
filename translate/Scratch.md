#### 同步方法

Java编程语言提供了两种基本的同步习惯用法：*synchronized方法*和*synchronized语句*。两者中更复杂的是同步语句，将在下一章节中介绍。本节介绍同步方法。

要使方法同步，只需将`synchronized`关键字添加到其声明：

```java
public class SynchronizedCounter {
    private int c = 0;

    public synchronized void increment() {
        c++;
    }

    public synchronized void decrement() {
        c--;
    }

    public synchronized int value() {
        return c;
    }
}
```

如果`count` 是一个 `SynchronizedCounter`实例，则使得这些方法同步会有两方面影响：

 - 首先，对同一对象的两个同步方法的调用不可能交错。当一个线程正在为对象执行同步方法时，所有其他线程调用同一对象的同步方法阻塞（暂停执行）直到第一个线程完成对象上的执行。
 - 其次，当同步方法退出时，它会自动与同一对象的同步方法的任何后续调用建立*happens-before*关系。 这可以保证对所有线程都可以看到对象状态的更改。

请注意，构造函数无法同步 - 将`synchronized`关键字与构造函数一起使用是一种语法错误。同步构造函数没有意义，因为只有创建对象的线程在构造时才能访问它。

----

**警告：** 构造将在线程之间共享的对象时，要非常小心，保证对象的引用不会过早“泄漏”。例如，假设您要维护一个包含每个类实例的名为`instances`的`List`。您可能想要将以下行添加到构造函数中：

````java
instances.add(this);
````

但是其他线程可以在构造对象完成之前使用`instances`来访问对象。

----

同步方法启用了一种简单的策略来防止线程干扰和内存一致性错误：如果一个对象对多个线程可见，则对该对象变量的所有读取或写入都是通过同步方法完成的。（一个重要的例外：构造对象后无法修改`final`字段，一旦构造了对象，就可以通过非同步方法安全地读取）这种策略是有效的，但是可能会带来 [liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 问题，就像我们稍后将看到的那样。

#### 内在锁和同步

同步是围绕被称为*内部锁*或*监视器锁*的内部实体构建的。（API规范通常将此实体简称为“监视器”。）内部锁在同步的两个方面都发挥作用：强制对对象状态进行独占访问，并建立对可见性至关重要的*happens-before*关系。

每个对象都有一个与之关联的内在锁。按照惯例，需要对对象字段进行独占和一致访问的线程必须在访问对象之前*获取*对象的内部锁，然后在完成它们时*释放*内部锁。一个线程在获得锁定和释放锁定之间被称为*拥有*内在锁。只要一个线程拥有一个内部锁，没有其他线程可以获得相同的锁。另一个线程在尝试获取锁时将阻塞。

当线程释放内部锁时，在该操作与同一锁的任何后续*获取*之间建立*happens-before*关系。

**同步方法中的锁**

当线程调用`synchronized`方法时，它会自动获取该方法对象的内部锁，并在方法返回时释放它。即使返回是由未捕获的异常引起的，也会发生锁定释放。

您可能想知道在调用静态同步方法时会发生什么，因为静态方法与类相关联，而不是与对象相关联。在这种情况下，线程获取与该类关联的`Class`对象的内部锁。因此，对类的静态字段的访问由与该类的任何实例的锁不同的锁控制。

**同步语句**

创建同步代码的另一种方法是使用`synchronized`语句。与`synchronized`方法不同，`synchronized`语句必须指定提供内部锁的对象：

```java
public void addName(String name) {
    synchronized(this) {
        lastName = name;
        nameCount++;
    }
    nameList.add(name);
}
```

在此示例中，`addName`方法需要将更改同步到`lastName`和`nameCount`，但还需要避免同步其他对象方法的调用。（从同步代码调用其他对象的方法可能会产生在 [Liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html) 部分中描述的问题。）如果没有`synchronized`语句，则必须有一个单独的，不同步的方法，其唯一目的是调用`nameList.add`。

同步语句对于通过细粒度同步提高并发性也很有用。例如，假设类`MsLunch`有两个从不一起使用的实例字段`c1`和`c2`。必须同步这些字段的所有更新，但没有理由阻止`c1`的更新与`c2`的更新交错 - 这样做会通过创建不必要的阻塞来降低并发性。我们创建两个对象仅用于提供锁，而不是使用同步方法或以其他方式使用与`this`关联的锁。

```java
public class MsLunch {
    private long c1 = 0;
    private long c2 = 0;
    private Object lock1 = new Object();
    private Object lock2 = new Object();

    public void inc1() {
        synchronized(lock1) {
            c1++;
        }
    }

    public void inc2() {
        synchronized(lock2) {
            c2++;
        }
    }
}
```

谨慎使用此方式。您必须绝对确保对受影响字段的访问交替进行是否安全。

**可重入同步**

回想一下，线程无法获取另一个线程拥有的锁。但是一个线程可以获得它已经拥有的锁。允许线程多次获取相同的锁可启用*可重入同步*。这描述了一种情况，其中同步代码直接或间接地调用也包含同步代码的方法，并且两组代码使用相同的锁。在没有可重入同步的情况下，同步代码必须采取许多额外的预防措施，以避免线程导致自身阻塞。