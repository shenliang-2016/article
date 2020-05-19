# 线程安全和共享资源

可以安全地被多个线程同时调用的代码称为线程安全的。如果一段代码是线程安全的，那么肯定不包含 [竞争条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html)。竞争条件只有在多个线程更新共享资源时才会出现。因此，了解 java 线程执行过程中共享了什么资源是至关重要的。

## 局部变量

局部变量存储在每个线程自己的栈中。这就意味着局部变量绝对不会在线程之间共享。同时还意味着所有局部基本数据类型的变量都是线程安全的。下面是线程安全的基本数据类型的局部变量的例子：

```java
public void someMethod(){

  long threadSafeInt = 0;

  threadSafeInt++;
}
```

## 局部对象引用

对象的局部引用有点不同。这些引用本身并不是共享的。被引用的对象也不是存储在线程自己的局部栈中。所有的对象都存储在共享堆中。

如果一个被局部创建的对象从来没有从创建它的方法中逃逸，它就是线程安全的。事实上，你也可以将它传递给别的方法或者对象，只要这些目标方法或者对象都没有将该对象开放给其他线程使用。

下面是线程安全的局部对象的示例：

```java
public void someMethod(){

  LocalObject localObject = new LocalObject();

  localObject.callMethod();
  method2(localObject);
}

public void method2(LocalObject localObject){
  localObject.setValue("value");
}
```

例子中的 `LocalObject` 实例不会从方法返回，也不会被传递给任何可以从 `someMethod()` 方法外部访问的其他对象。每个执行  `someMethod()`  方法的线程将创建自己的 `LocalObject` 实例并分配给 `localObject` 引用。因此，这里 `localObject` 的使用是线程安全的。

事实上，整个 `someMethod()` 方法都是线程安全的。即使 `LocalObject` 实例被作为参数传递给同一个类或者别的类中其他方法，对它的使用也都是线程安全的。

唯一的例外，如果使用  `LocalObject` 作为参数调用一个方法，以允许从其他线程中访问的方式存储  `LocalObject`  实例。

## 对象成员变量

对象成员变量(域)和对象一起存储在堆中。因此，如果两个线程调用同一个对象实例上的一个方法，该方法会修改对象成员变量，该方法就不是线程安全的。下面是此类方法的例子：

```java
public class NotThreadSafe{
    StringBuilder builder = new StringBuilder();

    public add(String text){
        this.builder.append(text);
    }
}
```

如果两个线程同时调用同一个非线程安全的实例上的 `add()` 方法，将导致竞争条件。比如：

```java
NotThreadSafe sharedInstance = new NotThreadSafe();

new Thread(new MyRunnable(sharedInstance)).start();
new Thread(new MyRunnable(sharedInstance)).start();

public class MyRunnable implements Runnable{
  NotThreadSafe instance = null;

  public MyRunnable(NotThreadSafe instance){
    this.instance = instance;
  }

  public void run(){
    this.instance.add("some text");
  }
}
```

注意，两个 `MyRunnable` 实例如何共享同一个 `NotThreadSafe` 实例。因此，当它们同时调用  `NotThreadSafe`  实例上的 `add()` 方法时，将会导致竞争条件。

然而，如果两个线程同时调用不同实例上的 `add()` 方法时，当然就不会导致竞争条件。下面是这个版本的例子：

```java
new Thread(new MyRunnable(new NotThreadSafe())).start();
new Thread(new MyRunnable(new NotThreadSafe())).start();
```

现在，两个线程都有自己的 `NotThreadSafe` 实例，因而它们调用 `add()` 方法时就不会有任何相互影响。代码不再包含竞争条件。因此，即使是非线程安全的对象，也可以被以不会导致竞争条件的方式使用。

## 线程控制逃逸规则

可以使用线程控制逃逸规则来判断你的代码是否访问了某些线程安全的特定资源：

```
If a resource is created, used and disposed within
the control of the same thread,
and never escapes the control of this thread,
the use of that resource is thread safe.
```

资源可以是任何共享资源，比如对象、数组、文件数据库连接或者网络套接字等等。在 Java 中你并不会显式销毁对象，因此，这里的"销毁"意味着对象的引用丢失或者置空。

即使对象的使用是线程安全的，如果对象指向共享资源，比如文件或者数据库，你的应用作为一个整体可能仍然是非线程安全的。比如，如果线程 1 和线程 2 分别创建它们自己的数据库连接，连接 1 和连接 2 ，每个连接本身的使用是线程安全的。但是对这些连接指向的数据库的使用就未必是线程安全的。比如，如果两个线程都执行入戏逻辑：

```
check if record X exists
if not, insert record X
```

如果两个线程同时执行，同时它们检查的记录 X 恰好又是同一条数据，这就有两个线程都插入成功的风险。过程如下：

```
Thread 1 checks if record X exists. Result = no
Thread 2 checks if record X exists. Result = no
Thread 1 inserts record X
Thread 2 inserts record X
```

在文件或其他共享资源上运行的线程也可能发生这种情况。因此，区分由线程控制的对象是资源还是仅引用资源（就像数据库连接一样）是很重要的。