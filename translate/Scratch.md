# Java 同步块

Java 同步块将一个方法或者代码块标记为同步的。Java 同步块同一时刻只能被一个线程执行(取决于你如何使用)。因此，Java 同步块可以被用于避免 [竞争条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html)。本文详细介绍了 Java *synchronized* 关键字的工作原理。

## Java 并发工具类

 `synchronized` 机制是 Java 用于多线程同步访问共享对象的第一种机制。 `synchronized` 机制目前看来并不是非常好用。因此 Java 5 添加了整套的 [concurrency utility classes](http://tutorials.jenkov.com/java-util-concurrent/index.html) 来帮助开发者实现相较与 `synchronized` 更精细的并发控制。

## Java synchronized 关键字

Java 同步块使用 `synchronized` 关键字标记。Java 同步块被同步在某些对象上。所有同步在相同对象上的所有同步块在同一时刻只允许一个线程在它们内部执行。所有其他试图进入同步块的线程都会被阻塞，直到同步块内的线程退出同步块。

 `synchronized` 可以用来标记四种不同类型的代码块：

1. 实例方法
2. 静态方法
3. 实例方法内部的代码块
4. 静态方法内部的代码块

这些代码块被同步在不同对象上。你需要何种同步块需要具体情况具体分析。接下来我们详细介绍每种类型的同步块。

## 同步实例方法

这是一个同步的实例方法：

```java
public class MyCounter {

  private int count = 0;

  public synchronized void add(int value){
      this.count += value;
  }
}
```

注意 `synchronized` 关键字使用在 `add()` 方法声明中。这就告诉 Java 该方法是同步的。

Java 中的同步实例方法被同步在拥有该方法的实例(对象)上。因此，每个实例拥有的同步方法都同步在不同的对象上：拥有该方法的实例。

每个实例上只有一个线程能够在一个同步实例方法内部执行。如果存在多个实例，则同一时刻一个线程只能在每个实例的一个同步实例方法内部执行。每个实例一个线程。

这一点对于同一个对象(实例)中的所有同步实例方法也是使用的。因此，下面例子中，只有一个线程能够在两个同步方法之一内部执行。一个实例只有一个线程：

```java
public class MyCounter {

  private int count = 0;

  public synchronized void add(int value){
      this.count += value;
  }
  public synchronized void subtract(int value){
      this.count -= value;
  }

}
```

## 同步静态方法

类似于实例方法，静态方法也可以使用 `synchronized` 关键字标记为同步的。下面是 Java 同步静态方法的例子：

```java
public static MyStaticCounter{

  private static int count = 0;

  public static synchronized void add(int value){
      count += value;
  }

}
```

这里的 `synchronized` 关键字也是告诉 Java  `add()` 方法是同步的。

同步静态方法是同步在静态方法所在的类的类对象上。由于每个类只会有唯一一个类对象存在于 JVM 中，只会有一个线程能够在同一个类的一个同步静态方法中执行。

如果一个类包含多个同步静态方法，同一时刻只能有一个线程执行这些方法中任何一个。请看下面的例子：

```java
public static MyStaticCounter{

  private static int count = 0;

  public static synchronized void add(int value){
    count += value;
  }

  public static synchronized void subtract(int value){
    count -= value;
  }
}
```

在任何给定时间点只有一个线程可以在 `add()` 和 `subtract()` 其中之一内部执行。如果线程 A 正在执行 `add()`，则线程 B 既不能执行 `add()` 也不能执行 `subtract()` ，直到线程 A 退出 `add()`。

如果静态同步方法位于不同类中，则一个线程可以在每个类的静态同步方法内部执行。每个类一个线程，无论它调用的是哪个静态同步方法。

## 实例方法中的同步块

你并不是必须同步整个方法，有时候仅仅同步方法的一部分逻辑更加合理。Java 的方法内部同步块允许你做到这一点。

下面是一个非同步 Java 方法内部的同步代码块的示例：

```java
  public void add(int value){

    synchronized(this){
       this.count += value;   
    }
  }
```

这个例子使用 Java 同步块结构来将一个代码块标记为同步的。该代码块将类似于同步方法那样被执行。

注意，Java 同步块结构如何选择同步使用的对象。上面例子中使用了 `this` ，也就是 `add` 方法在其上被调用的那个实例。被同步结构选取放在括号中的对象被称为监视器对象。代码块被称为被同步在监视器对象上。一个同步实例方法使用它所属的对象作为监视器对象。

只有一个线程可以在同步于同一个监视器对象的 Java 同步代码块内部运行。

下面两个例子都是同步在它们被调用于其上的实例上。它们在同步方面是等效的：

```java
  public class MyClass {
  
    public synchronized void log1(String msg1, String msg2){
       log.writeln(msg1);
       log.writeln(msg2);
    }

  
    public void log2(String msg1, String msg2){
       synchronized(this){
          log.writeln(msg1);
          log.writeln(msg2);
       }
    }
  }
```

因此，只有一个线程能够执行在例子中的两个同步块之一内部。

如果第二个同步块被同步在一个不同于 `this` 的对象上，则一个线程就可以在同一时刻执行在每个方法内部。

## 静态方法中的同步块

同步块也可以被用在静态方法内部。这里是与前面静态方法示例相同的例子。这些方法都同步在它们所属的类的类对象上：

```java
  public class MyClass {

    public static synchronized void log1(String msg1, String msg2){
       log.writeln(msg1);
       log.writeln(msg2);
    }

  
    public static void log2(String msg1, String msg2){
       synchronized(MyClass.class){
          log.writeln(msg1);
          log.writeln(msg2);  
       }
    }
  }
```

同一时刻只有一个线程能够执行在这两个方法之一内部。

如果第二个同步块被同步在 `MyClass.class` 之外的对象上，则同一时刻一个线程可以执行在每个方法内部。

## Lambda 表达式中的同步块

在 [Java Lambda Expression](http://tutorials.jenkov.com/java/lambda-expressions.html) 和匿名类内部使用同步块也是可能的。

这是一个内部包含同步块的 Java lambda 表达式。注意，该同步块同步在包含该 lambda 表达式的类的类对象上。如果有必要，它也可以同步在其他对象上。不过使用类对象很适合这个例子：

```java
import java.util.function.Consumer;

public class SynchronizedExample {

  public static void main(String[] args) {

    Consumer<String> func = (String param) -> {

      synchronized(SynchronizedExample.class) {

        System.out.println(
            Thread.currentThread().getName() +
                    " step 1: " + param);

        try {
          Thread.sleep( (long) (Math.random() * 1000));
        } catch (InterruptedException e) {
          e.printStackTrace();
        }

        System.out.println(
            Thread.currentThread().getName() +
                    " step 2: " + param);
      }

    };


    Thread thread1 = new Thread(() -> {
        func.accept("Parameter");
    }, "Thread 1");

    Thread thread2 = new Thread(() -> {
        func.accept("Parameter");
    }, "Thread 2");

    thread1.start();
    thread2.start();
  }
}
```

## Java 同步示例

这个例子启动两个线程，它们都会调用同一个计数器实例上的 `add` 方法。此时只有一个线程能够调用同一个实例上的 `add` 方法，因为该方法被同步在它所属的实例上。

```java
  public class Example {

    public static void main(String[] args){
      Counter counter = new Counter();
      Thread  threadA = new CounterThread(counter);
      Thread  threadB = new CounterThread(counter);

      threadA.start();
      threadB.start();
    }
  }
```

下面是例子中用到的类， `Counter` 和 `CounterThread`。

```java
  public class Counter{
     
     long count = 0;
    
     public synchronized void add(long value){
       this.count += value;
     }
  }
  public class CounterThread extends Thread{

     protected Counter counter = null;

     public CounterThread(Counter counter){
        this.counter = counter;
     }

     public void run() {
	for(int i=0; i<10; i++){
           counter.add(i);
        }
     }
  }
```

两个线程被创建。同一个 `Counter` 实例通过构造器被传递给它们。`Counter.add()` 方法被同步到该实例上，因为 `add` 方法是实例方法，而且被标记为同步的。由于此时只有一个线程可以调用 `add()` 方法。另外一个线程将等待直到第一个线程退出 `add()` 方法，然后才能执行该方法。

如果两个线程引用了各自独立的 `Counter` 实例，它们同时调用 `add()` 方法就没有任何问题。调用将会指向不同的对象，因此方法调用也可以在不同的对象（拥有该方法的对象）上同步。方法的调用不会被阻塞。大概是下面这样：

```java
public class Example {

  public static void main(String[] args){
    Counter counterA = new Counter();
    Counter counterB = new Counter();
    Thread  threadA = new CounterThread(counterA);
    Thread  threadB = new CounterThread(counterB);

    threadA.start();
    threadB.start();
  }
}
```

注意，两个线程，线程 A 和线程 B，不再引用相同的 `Counter` 实例。`counterA` 和 `counterB` 上的 `add()` 方法在各自的对象实例上同步。调用 `counterA` 上的 `add()` 当然不会阻塞对 `counterB` 上的 `add()` 的调用。

## 同步和数据可见性

除了使用 `synchronized` 关键字(或者 [Java volatile](http://tutorials.jenkov.com/java-concurrency/volatile.html) 关键字)，无法保证当一个线程修改与其他线程共享的变量的值时，其他的线程能够看到这个修改的值。对于由线程读取到 CPU 寄存器中的变量何时会被"提交"到主内存中，没有任何保证。同样，别的线程何时根据主内存对自己的 CPU 寄存器中的变量进行"刷新"，也没有任何保证。

`synchronized` 关键字改变了这一切。当一个线程进入同步块，它将刷行所有它可见的变量的值。当一个线程退出同步块时，该线程可见的所有变量的变化都会被提交到主内存。类似于 [volatile keyword](http://tutorials.jenkov.com/java-concurrency/volatile.html) 的行为。

## 同步和指令重排序

Java 编译器和 Java 虚拟机被允许对你的代码进行指令重排序以使得它们执行更快，通常是通过允许重排序之后的指令被 CPU 并行执行。

对那些同时被多个线程执行的代码进行指令重排序可能会导致问题。比如，如果一个发生在同步块内部的变量写入被重排序到了同步块之外。

为了解决这种问题，Java `synchronized` 关键字对同步块之前、内部以及之后的指令重排序设置了一些限制。类似于 [volatile 关键字](http://tutorials.jenkov.com/java-concurrency/volatile.html) 设置的限制。

最终结果是，您可以确保您的代码正确运行——不会发生指令重新排序，最终导致该代码的行为不同于您编写的代码所期望的行为。

## 在什么对象上同步

如前所述，同步块必须同步在某些对象上。你可以选择几乎任何对象以同步于其上，但是建议不要在 `String` 对象上同步，或者任何其他基本数据类型的包装对象。因为编译器可能对此进行优化，导致代码中你以为使用的是不同的实例的地方，可能实际上使用的是相同的实例。分析下面的例子：

```java
synchronized("Hey") {
   //do something in here.
}
```

如果你有多个同步块都同步在字面值"Hey"上，编译器可能在背后实际上使用同一个 `String` 对象。结果是，这些同步块就同步在同一个对象上。这可能不是你期望的行为。

使用基本数据类型包装对象时的情况类似。如下面的例子：

```java
synchronized(Integer.valueOf(1)) {
   //do something in here.
}
```

如果你调用 `Integer.valueOf(1)` 很多次，它可能实际上为相同的输入参数值返回同一个包装对象实例。这就意味着，如果你将多个同步块同步在相同的基本数据类型包装对象上，你可能就会面临所有同步块都同步在同一个对象上的风险。这也不是你期望的行为。

为了确保安全，在 `this` 上同步——或者在 `new Object()` 上同步。使用那些不会被编译器、JVM 或者 Java 类库内部缓存或者复用的对象。

## Synchronized Block Limitations and Alternatives

Synchronized blocks in Java have several limitations. For instance, a synchronized block in Java only allows a single thread to enter at a time. However, what if two threads just wanted to read a shared value, and not update it? That might be safe to allow. As alternative to a synchronized block you could guard the code with a [Read / Write Lock](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) which as more advanced locking semantics than a synchronized block. Java actually comes with a built in [ReadWriteLock](http://tutorials.jenkov.com/java-util-concurrent/readwritelock.html) class you can use.

What if you want to allow N threads to enter a synchronized block, and not just one? You could use a [Semaphore](http://tutorials.jenkov.com/java-concurrency/semaphore.html) to achieve that behaviour. Java actually comes with a built-in [Java Semaphore](http://tutorials.jenkov.com/java-util-concurrent/semaphore.html) class you can use.

Synchronized blocks do not guarantee in what order threads waiting to enter them are granted access to the synchronized block. What if you need to guarantee that threads trying to enter a synchronized block get access in the exact sequence they requested access to it? You need to implement [Fairness](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) yourself.

What if you just have one thread writing to a shared variable, and other threads only reading that variable? Then you might be able to just use a [volatile variable](http://tutorials.jenkov.com/java-concurrency/volatile.html) without any synchronization around.

## Synchronized Block Performance Overhead

There is a small performance overhead associated with entering and exiting a synchronized block in Java. As Jave have evolved this performance overhead has gone down, but there is still a small price to pay.

The performance overhead of entering and exiting a synchronized block is mostly something to worry about if you enter and exit a synchronized block lots of times within a tight loop or so.

Also, try not to have larger synchronized blocks than necessary. In other words, only synchronize the operations that are really necessary to synchronize - to avoid blocking other threads from executing operations that do not have to be synchronized. Only the absolutely necessary instructions in synchronized blocks. That should increase parallelism of your code.

## Synchronized Block Reentrance

Once a thread has entered a synchronized block the thread is said to "hold the lock" on the monitoring object the synchronized block is synchronized on. If the thread calls another method which calls back to the first method with the synchronized block inside, the thread holding the lock can reenter the synchronized block. It is not blocked just because a thread (itself) is holding the lock. Only if a differen thread is holding the lock. Look at this example:

```
public class MyClass {
    
  List<String> elements = new ArrayList<String>();
    
  public void count() {
    if(elements.size() == 0) {
        return 0;
    }
    synchronized(this) {
       elements.remove();
       return 1 + count();  
    }
  }
    
}
```

Forget for a moment that the above way of counting the elements of a list makes no sense at all. Just focus on how inside the synchronized block inside the `count()` method calls the `count()` method recursively. Thus, the thread calling count() may eventually enter the same synchronized block multiple times. This is allowed. This is possible.

Keep in mind though, that designs where a thread enters into multiple synchronized blocks may lead to [nested monitor lockout](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html) if you do not design your code carefully.

## Synchronized Blocks in Cluster Setups

Keep in mind that a synchronized block only blocks threads within the same Java VM from entering that code block. If you have the same Java application running on multiple Java VMs - in a cluster - then it is possible for one thread *within each Java VM* to enter that synchronized block at the same time.

If you need synchronization across all Java VMs in a cluster you will need to use other synchronization mechanisms than just a synchronized block.