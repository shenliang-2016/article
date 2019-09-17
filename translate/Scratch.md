## 保护块

线程通常必须协调他们的行为。最常见的协调习语是*保护块*。这样的块开始于在块可以继续之前必须循环判定为真的条件。要正确执行此操作，需要执行许多步骤。

假设，例如 `guardedJoy` 是一种方法，在另一个线程设置了共享变量 `joy` 之前，该方法不得继续。理论上，这种方法可以简单地循环直到满足条件，但是该循环是浪费的，因为它在等待时连续执行。

```java
public void guardedJoy() {
    // Simple loop guard. Wastes
    // processor time. Don't do this!
    while(!joy) {}
    System.out.println("Joy has been achieved!");
}
```

更有效的防护调用 [`Object.wait`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#wait--) 来暂停当前线程。`wait` 的调用不会返回，直到另一个线程发出了某个特殊事件可能发生的通知 - 虽然不一定是该线程正在等待的事件：

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

------

**注意：**始终在测试等待条件的循环内调用 `wait`。不要假设中断是针对您正在等待的特定条件，或者条件仍然是真的。

------

像许多暂停执行的方法一样，`wait` 可以抛出 `InterruptedException`。在这个例子中，我们可以忽略该异常 - 我们只关心 `joy` 的值。

为什么这个版本的 `guardedJoy` 是同步的？假设 `d` 是我们用来调用 `wait` 的对象。当一个线程调用 `d.wait` 时，它必须拥有 `d` 的内部锁 - 否则抛出一个错误。在 `synchronized` 方法中调用 `wait` 是获取内部锁的一种简单方法。

当调用 `wait` 时，线程释放锁并暂停执行。在将来某个时候，另一个线程将获得相同的锁并调用 [`Object.notifyAll`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#notifyAll--) ，通知等待该锁的所有线程发生了重要的事情：

```java
public synchronized notifyJoy() {
    joy = true;
    notifyAll();
}
```

在第二个线程释放锁之后的一段时间，第一个线程重新获取锁并通过从 `wait` 的调用返回来恢复。

------

**注意：**有第二种通知方法 `notify`，它唤醒一个线程。因为 `notify` 不允许你指定被唤醒的线程，所以它仅在大规模并行应用程序中有用 - 也就是说，具有大量线程的程序，都在执行相似的任务。在这样的应用程序中，您不关心哪个线程被唤醒。

------

让我们使用受保护的块来创建 *Producer-Consumer* 应用程序。这种应用程序在两个线程之间共享数据：*producer*，用于创建数据，*consumer*，用于执行某些操作。两个线程使用共享对象进行通信。协调是必不可少的：消费者线程不得在生产者线程交付之前尝试检索数据，并且如果消费者未检索到旧数据，则生产者线程不得尝试传递新数据。

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

生产者线程在 [`Producer`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Producer.java) 中定义，发送一系列相似的消息。字符串“DONE”表示已发送所有消息。为了模拟真实世界应用程序的不可预测性，生产者线程在消息之间暂停随机间隔。

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

在 [`Consumer`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/Consumer.java) 中定义的消费者线程只是检索消息并将其打印出来，直到它检索到 “完成”字符串消息为止。该线程也会暂停随机间隔。

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

------

**注意：**编写 `Drop` 类是为了展示防护块。为了避免重新发明轮子，在尝试编写自己的数据共享对象代码之前，请检查 [Java Collections Framework](https://docs.oracle.com/javase/tutorial/collections/index.html) 中的现有数据结构。有关更多信息，请参阅 [问题和练习](https://docs.oracle.com/javase/tutorial/essential/concurrency/QandE/questions.html) 部分。

------

