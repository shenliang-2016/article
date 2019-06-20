#### 暂停执行与睡眠

`Thread.sleep`导致当前线程暂停执行指定的时间段。这是使处理器时间可用于应用程序的其他线程或可能在计算机系统上运行的其他应用程序的有效方法。`sleep`方法也可用于调度，如下面的示例所示，并等待具有被理解为具有时间要求的职责的另一个线程，如稍后部分中的`SimpleThreads`示例。

存在两个重载版本的`sleep`：一个指定睡眠时间为毫秒，另一个指定睡眠时间为纳秒。但是，这些睡眠时间并不能保证精确，因为它们受到底层操作系统提供的基础设施的限制。此外，睡眠周期可以通过中断终止，我们将在后面的部分中看到。在任何情况下，您都不能假设调用`sleep`会在指定的时间段内暂停该线程。

 [`SleepMessages`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SleepMessages.java) 示例使用`sleep`以四秒为间隔打印消息：

```java
public class SleepMessages {
    public static void main(String args[])
        throws InterruptedException {
        String importantInfo[] = {
            "Mares eat oats",
            "Does eat oats",
            "Little lambs eat ivy",
            "A kid will eat ivy too"
        };

        for (int i = 0;
             i < importantInfo.length;
             i++) {
            //Pause for 4 seconds
            Thread.sleep(4000);
            //Print a message
            System.out.println(importantInfo[i]);
        }
    }
}
```

请注意，`main`声明它会抛出`InterruptedException`。这是一个异常，当当前线程处于`sleep`状态时，另一个线程在中断当前线程时抛出。由于此应用程序尚未定义另一个导致中断的线程，因此无需捕获`InterruptedException`。

#### 中断

*中断*是一个给线程的指示，告诉它应该停止正在做的事情并做其他事情。由程序员决定线程如何响应中断，但线程终止是很常见的。这是本课程中强调的用法。

线程通过调用`Thread`对象上的 [`interrupt`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#interrupt--) 来发送中断，以便线程被中断。为使中断机制正常工作，被中断的线程必须支持自己的中断。

**支持中断**

线程如何支持自己的中断？这取决于它目前正在做什么。如果线程经常调用抛出`InterruptedException`的方法，它只会在捕获该异常后从`run`方法返回。例如，假设`SleepMessages`示例中的核心消息循环位于线程的`Runnable`对象的`run`方法中。然后可以按如下方式修改它以支持中断：

```java
for (int i = 0; i < importantInfo.length; i++) {
    // Pause for 4 seconds
    try {
        Thread.sleep(4000);
    } catch (InterruptedException e) {
        // We've been interrupted: no more messages.
        return;
    }
    // Print a message
    System.out.println(importantInfo[i]);
}
```

许多抛出`InterruptedException`的方法（例如`sleep`）被设计为取消当前操作并在收到中断时立即返回。

如果一个线程长时间没有调用抛出`InterruptedException`的方法怎么办？它必须定期调用`Thread.interrupted`，如果收到中断，则返回`true`。 例如：

```java
for (int i = 0; i < inputs.length; i++) {
    heavyCrunch(inputs[i]);
    if (Thread.interrupted()) {
        // We've been interrupted: no more crunching.
        return;
    }
}
```

在这个简单的例子中，代码只是测试中断并退出线程（如果已收到）。在更复杂的应用程序中，抛出`InterruptedException`可能更有意义：

```java
if (Thread.interrupted()) {
    throw new InterruptedException();
}
```

这允许中断处理代码集中在`catch`子句中。

**中断状态标识**

中断机制使用称为*中断状态*的内部标志来实现。调用`Thread.interrupt`设置此标志。当线程通过调用静态方法`Thread.interrupted`来检查中断时，将清除中断状态。非静态`isInterrupted`方法，由一个线程用于查询另一个线程的中断状态，不会更改中断状态标志。

按照惯例，任何通过抛出`InterruptedException`退出的方法都会在执行此操作时清除中断状态。但是，通过另一个线程调用`interrupt`，总是可以立即再次设置中断状态。

