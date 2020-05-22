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

## 同步块的局限性和替代方案

Java 中的同步块具有一些局限性。比如，一个同步块同一时刻只允许一个线程进入。然而，如果两个线程都只是想要读取共享值，而并不会修改它呢？允许同时读取可能是安全的。作为同步块的替代方案，你可以使用一种名为 [Read / Write Lock](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) 的技术来保护你的代码，这是一种比同步块更加先进的锁语义。Java 实际上已经内置了一个你可以直接使用的 [ReadWriteLock](http://tutorials.jenkov.com/java-util-concurrent/readwritelock.html) 类。

如果你希望若干个线程进入同步块，而不仅仅是一个，该怎么办？你可以使用 [Semaphore](http://tutorials.jenkov.com/java-concurrency/semaphore.html) 实现这种行为。Java 内置了你可以直接使用的 [Java Semaphore](http://tutorials.jenkov.com/java-util-concurrent/semaphore.html) 类。

同步块并不能保证等待进入同步块的线程最终会以何种顺序进入同步块。如果你想要保证这些等待线程能够按照它们最初请求进入同步块的顺序依次进入同步块，该怎么办？你需要实现自己的 [Fairness](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 。

如果你希望一个线程写入共享变量的同时，别的线程还可以同时读取该变量，该如何做？可能你只需要使用 [volatile variable](http://tutorials.jenkov.com/java-concurrency/volatile.html) 而不需要任何同步逻辑。

## 同步块的性能损耗

与进入和退出 Java 中的同步块相关的性能开销很小。随着 Jave 的发展，性能开销下降了，但是仍然要付出很小的代价。

如果您在一个紧密的循环内多次进入和退出同步块，则通常要担心进入和退出同步块的性能开销。

另外，请尽量不要使同步块大于必需的块。换句话说，仅同步真正需要同步的操作——避免阻止其他线程执行不必同步的操作。同步块中只有绝对必要的指令。应该尽可能增加代码的并行性。

## 同步块的可重入

一旦线程已经进入同步块，则称该线程"持有了同步块同步于其上的监视器对象的锁"。如果该线程调用另外的方法，后者又反向调用同步块内部的前者方法，则持有锁的线程可以再次进入该同步块。它不会被阻塞，因为该线程本身正持有锁。除非别的线程持有了锁。分析下面的例子：

```java
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

不必在意上述计算列表元素的方法根本没有任何意义。只需关注 `count()` 方法内的同步块内部如何递归调用 `count()` 方法即可。因此，线程调用 `count()` 最终可能会多次进入同一同步块。这是允许的。

注意：如果你不谨慎设计你的代码，允许一个线程进入多个同步块可能会导致 [嵌套监视器锁定](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html)。

## 集群设置中的同步块

请记住，同步块仅阻止同一 Java VM 中的线程进入该代码块。如果在集群中的多个 Java VM 上运行相同的 Java 应用程序，则每个 Java VM 中的一个线程可能同时进入该同步块。

如果需要跨集群中所有 Java VM 进行同步，则将需要使用其他同步机制，而不仅仅是同步块。

