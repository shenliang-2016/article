### 守卫块

线程通常必须协调他们的行为。最常见的协调习语是*guarded block*。这样的块开始于在块可以继续之前轮询必须为真的条件。要正确执行此操作，需要执行许多步骤。

假设，例如`guardedJoy`是一种方法，在另一个线程设置了共享变量`joy`之前，该方法不能继续。理论上，这种方法可以简单地循环直到满足条件，但是该循环是浪费的，因为它在等待时连续执行。

```java
public void guardedJoy() {
    // Simple loop guard. Wastes
    // processor time. Don't do this!
    while(!joy) {}
    System.out.println("Joy has been achieved!");
}
```

更有效的防护是调用 [`Object.wait`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#wait--) 来挂起当前线程。在另一个线程发出可能发生某些特殊事件的通知之前，`wait`的调用不会返回 - 尽管不一定是此线程正在等待的事件：

```java
public synchronized void guardedJoy() {
    // This guard only loops once for each special event, which may not
    // be the event we're waiting for.
    while(!joy) {
        try {
            wait();
        } catch (InterruptedException e) {}
    }
    System.out.println("Joy and efficiency have been achieved!");
}
```

----

**注意：** 始终在测试等待条件的循环内调用`wait`。不要假设中断是针对您正在等待的特定条件，或者该条件仍然是真的。

----

像许多暂停执行的方法一样，`wait`会抛出`InterruptedException`。在这个例子中，我们可以忽略该异常 - 我们只关心`joy`的值。

为什么这个版本的`guardedJoy`是同步的？假设`d`是我们用来调用`wait`的对象，当一个线程调用`d.wait`时，它必须拥有`d`的内部锁 - 否则抛出错误。在`synchronized`方法中调用`wait`是获取内部锁的一种简单方法。

当调用`wait`时，线程释放锁并暂停执行。在将来的某个时间，另一个线程将获取相同的锁并调用 [`Object.notifyAll`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#notifyAll--) ，通知等待该锁的所有线程发生了重要的事情：

```java
public synchronized notifyJoy() {
    joy = true;
    notifyAll();
}
```

在第二个线程释放锁之后的一段时间，第一个线程重新获取锁并通过从 `wait` 调用返回来恢复。

----

**注意：** 有第二个通知方法`notify`，它唤醒单个线程。因为`notify`不允许您指定被唤醒的线程，所以它仅在大规模并行应用程序中有用 - 即具有大量线程的程序，所有程序都执行类似的杂务。在这样的应用程序中，您不关心哪个线程被唤醒。

----

让我们使用保护块来创建`Producer-Consumer`应用程序。这种应用程序在两个线程之间共享数据：*生成器*，创建数据，以及使用数据的*消费者*。两个线程使用共享对象进行通信。协调是必不可少的：消费者线程不得在生产者线程交付之前尝试检索数据，并且如果消费者未检索到旧数据，则生产者线程不得尝试传递新数据。

在此示例中，数据是一系列文本消息，通过 [`Drop`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Drop.java) 类型的对象共享：

```java
public class Drop {
    // Message sent from producer
    // to consumer.
    private String message;
    // True if consumer should wait
    // for producer to send message,
    // false if producer should wait for
    // consumer to retrieve message.
    private boolean empty = true;

    public synchronized String take() {
        // Wait until message is
        // available.
        while (empty) {
            try {
                wait();
            } catch (InterruptedException e) {}
        }
        // Toggle status.
        empty = true;
        // Notify producer that
        // status has changed.
        notifyAll();
        return message;
    }

    public synchronized void put(String message) {
        // Wait until message has
        // been retrieved.
        while (!empty) {
            try { 
                wait();
            } catch (InterruptedException e) {}
        }
        // Toggle status.
        empty = false;
        // Store message.
        this.message = message;
        // Notify consumer that status
        // has changed.
        notifyAll();
    }
}
```

 [`Producer`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Producer.java) 中定义的生产者线程发送一系列相似的消息。字符串“DONE”表示已发送所有消息。为了模拟真实世界应用程序的不可预测性，生产者线程在消息之间暂停随机时间间隔。

```java
import java.util.Random;

public class Producer implements Runnable {
    private Drop drop;

    public Producer(Drop drop) {
        this.drop = drop;
    }

    public void run() {
        String importantInfo[] = {
            "Mares eat oats",
            "Does eat oats",
            "Little lambs eat ivy",
            "A kid will eat ivy too"
        };
        Random random = new Random();

        for (int i = 0;
             i < importantInfo.length;
             i++) {
            drop.put(importantInfo[i]);
            try {
                Thread.sleep(random.nextInt(5000));
            } catch (InterruptedException e) {}
        }
        drop.put("DONE");
    }
}
```

在 [`Consumer`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Consumer.java) 中定义的消费者线程只是检索消息并将其打印出来，直到它检索到“DONE”字符串。该线程也会暂停随机时间间隔。

```java
import java.util.Random;

public class Consumer implements Runnable {
    private Drop drop;

    public Consumer(Drop drop) {
        this.drop = drop;
    }

    public void run() {
        Random random = new Random();
        for (String message = drop.take();
             ! message.equals("DONE");
             message = drop.take()) {
            System.out.format("MESSAGE RECEIVED: %s%n", message);
            try {
                Thread.sleep(random.nextInt(5000));
            } catch (InterruptedException e) {}
        }
    }
}
```

最后，这是在 [`ProducerConsumerExample`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/ProducerConsumerExample.java) 中定义的主线程，它启动生产者和消费者线程。

```java
public class ProducerConsumerExample {
    public static void main(String[] args) {
        Drop drop = new Drop();
        (new Thread(new Producer(drop))).start();
        (new Thread(new Consumer(drop))).start();
    }
}
```

----

**注意：** `Drop`类的编写是为了演示保护块。为避免重新发明轮子，请在尝试编写自己的数据共享对象之前检查J [Java Collections Framework](https://docs.oracle.com/javase/tutorial/collections/index.html) 中的现有数据结构。

----

### 不可变对象

如果一个对象的状态在构造后不能改变，则该对象被认为是不可变的。最大程度上依赖不可变对象被广泛接受为创建简单，可靠代码的合理策略。

不可变对象在并发应用程序中特别有用。由于它们不能改变状态，因此它们不会被线程干扰破坏或在不一致状态下被观察到。

程序员通常不愿意使用不可变对象，因为他们担心创建新对象的成本而不是更新对象。对象创建的影响经常被高估，并且可以通过与不可变对象相关联的一些效率来抵消。这些包括由于垃圾收集而减少的开销，以及消除保护可变对象免于损坏所需的代码。

以下小节采用其实例可变的类，并从中派生出具有不可变实例的类。通过这样做，它们为这种转换提供了一般规则，并展示了不可变对象的一些优点。