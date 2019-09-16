# 并发

计算机用户理所当然地认为他们的系统一次可以做多件事。他们假设他们可以继续在文字处理器中工作，而其他应用程序则下载文件，管理打印队列和流式传输音频。即使是单个应用程序通常也希望一次完成多个任务。例如，流式音频应用程序必须同时从网络读取数字音频，解压缩，管理播放和更新其显示。文字处理器应始终准备好响应键盘和鼠标事件，无论重新格式化文本或更新显示有多繁忙。可以执行此类操作的软件称为并发软件。

Java 平台的设计初衷是为了支持并发编程，在 Java 编程语言和 Java 类库中提供基本的并发支持。从 5.0 版开始，Java 平台还包含高级并发 API。本课程介绍了平台的基本并发支持，并总结了 `java.util.concurrent` 包中的一些高级 API。

## 进程和线程

在并发编程中，有两个基本的执行单元：*processes*和*threads*。在 Java 编程语言中，并发编程主要涉及线程。但是，进程也很重要。

计算机系统通常具有许多活动进程和线程。即使在只有一个执行核心的系统中也是如此，因此在任何给定时刻只有一个线程实际执行。通过称为时间切片的 OS 功能，在进程和线程之间共享单个核的处理时间。

对于具有多个处理器或具有多个执行核心的处理器的计算机系统来说，它变得越来越普遍。这极大地增强了系统并发执行进程和线程的能力 - 但即使在没有多个处理器或执行核心的简单系统上也可以实现并发。

**进程**

进程具有自包含的执行环境。进程通常具有完整的私有基本运行时资源集；特别是，每个进程都有自己的内存空间。

流程通常被视为程序或应用程序的同义词。但是，用户看到的单个应用程序实际上可能是一组协作进程。为了促进进程之间的通信，大多数操作系统都支持*进程间通信*（IPC）资源，例如管道和套接字。IPC 不仅用于同一系统上的进程之间的通信，而且还用于不同系统上的进程。

Java 虚拟机的大多数实现都作为单个进程运行。Java 应用程序可以使用 [`ProcessBuilder`](https://docs.oracle.com/javase/8/docs/api/java/lang/ProcessBuilder.html) 对象创建其他进程。多进程应用程序超出了本课程的范围。

**线程**

线程有时被称为*轻量级进程*。进程和线程都提供执行环境，但创建新线程所需的资源比创建新进程要少。

线程存在于进程中 - 每个进程至少有一个进程。线程共享进程的资源，包括内存和打开文件。这使得有效但可能有问题的通信成为可能。

多线程执行是 Java 平台的基本特性。每个应用程序至少有一个线程 - 或几个，如果你把“系统”线程计算在内，它们执行内存管理和信号处理等操作。但是从应用程序员的角度来看，你只从一个线程开始，称为*主线程*。该线程具有创建其他线程的能力，我们将在下一节中进行演示。

## 线程对象

每个线程都与 [`Thread`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html) 类的实例相关联。使用 `Thread` 对象创建并发应用程序有两种基本策略。

* 要直接控制线程创建和管理，只需在每次应用程序需要启动异步任务时实例化 `Thread`。
* 要从应用程序的其余部分抽象线程管理，请将应用程序的任务传递给执行程序。

本节介绍 `Thread` 对象的使用。执行器与 [其他高级并发对象](https://docs.oracle.com/javase/tutorial/essential/concurrency/highlevel.html) 一起讨论。

### 定义并启动线程

创建 `Thread` 实例的应用程序必须提供将在该线程中运行的代码。有两种方法可以做到这一点：

- *提供一个Runnable对象。* [`Runnable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html) 接口定义了一个单独的方法 `run`， 意味着包含在线程中执行的代码。 `Runnable` 对象被传递给 `Thread` 构造函数，如 [`HelloRunnable`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/HelloRunnable.java) 示例：

  ```java
  public class HelloRunnable implements Runnable {
  
      public void run() {
          System.out.println("Hello from a thread!");
      }
  
      public static void main(String args[]) {
          (new Thread(new HelloRunnable())).start();
      }
  
  }
  ```

- *Subclass Thread。* `Thread` 类本身实现 `Runnable`，尽管它的 `run` 方法什么都不做。应用程序可以子类化 `Thread`，提供自己的 `run` 实现，如 [`HelloThread`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/HelloThread.java) 例：

  ```java
  public class HelloThread extends Thread {
  
      public void run() {
          System.out.println("Hello from a thread!");
      }
  
      public static void main(String args[]) {
          (new HelloThread()).start();
      }
  
  }
  ```

请注意，两个示例都调用 `Thread.start` 以启动新线程。

你应该使用哪些习语？使用 `Runnable` 对象的第一个习语是更通用的，因为 `Runnable` 对象可以子类化除了 `Thread` 之外的类。第二个习惯用法在简单的应用程序中更容易使用，但受限于你的任务类必须是 `Thread` 的后代。本课重点介绍第一种方法，它将 `Runnable` 任务与执行任务的 `Thread` 对象分开。这种方法不仅更灵活，而且适用于后面介绍的高级线程管理 API。

`Thread` 类定义了许多对线程管理有用的方法。这些包括 `static` 方法，它们提供有关调用方法的线程的信息或影响其状态。从管理线程和 `Thread` 对象所涉及的其他线程调用其他方法。我们将在以下部分中研究其中一些方法。

### 使用 `sleep` 暂停执行

`Thread.sleep` 导致当前线程暂停执行指定的时间段。这是使处理器时间可用于应用程序的其他线程或可能在计算机系统上运行的其他应用程序的有效方法。 `sleep` 方法也可用于调步，如下面的示例所示，并等待具有被理解为具有时间要求的职责的另一个线程，如后面部分中的 `SimpleThreads` 示例。

提供了两个重载版本的`sleep`：一个指定睡眠时间为毫秒，另一个指定睡眠时间为纳秒。但是，这些睡眠时间并不能保证精确，因为它们受到底层操作系统提供的设施的限制。此外，睡眠周期可以通过中断终止，我们将在后面的部分中看到。在任何情况下，您都不能假设调用 `sleep` 将在指定的时间段内暂停该线程。

 [`SleepMessages`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SleepMessages.java) 示例使用 `sleep` 来按照四秒时间间隔打印消息：

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

请注意，`main` 声明它 `throws InterruptedException`。 当 `sleep` 处于活动状态时，当另一个线程中断当前线程时，则 `sleep` 抛出一个异常。由于此应用程序尚未定义另一个导致中断的线程，因此无需捕获 `InterruptedException`。

### 中断

*interrupt* 表示线程应该停止它正在做的事情并做其他事情。由程序员决定线程如何响应中断，但线程终止是很常见的。这是本课程中强调的用法。

线程通过在要被打断的线程 `Thread` 对象上调用 [`interrupt`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#interrupt--) 来发送中断。为使中断机制正常工作，被中断的线程必须支持自己的中断。

**支持中断**

线程如何支持自己的中断？这取决于它目前正在做什么。如果线程经常调用抛出 `InterruptedException` 的方法，它只会在捕获该异常后从 `run` 方法返回。例如，假设 `SleepMessages` 示例中的中心消息循环位于线程的 `Runnable` 对象的 `run` 方法中。然后可以按如下方式修改它以支持中断：

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

抛出 `InterruptedException` 的许多方法，例如 `sleep`，被设计为取消当前操作并在收到中断时立即返回。

如果一个线程长时间没有调用抛出 `InterruptedException` 的方法怎么办？那么它必须定期调用 `Thread.interrupted`，如果收到中断则返回 `true`。例如：

```java
for (int i = 0; i < inputs.length; i++) {
    heavyCrunch(inputs[i]);
    if (Thread.interrupted()) {
        // We've been interrupted: no more crunching.
        return;
    }
}
```

在这个简单的例子中，代码只是测试中断并退出线程（如果已收到）。在更复杂的应用程序中，抛出 `InterruptedException` 可能更有意义：

```java
if (Thread.interrupted()) {
    throw new InterruptedException();
}
```

这允许中断处理代码集中在 `catch` 子句中。

**中断状态标识**

中断机制使用称为*中断状态*的内部标志实现。调用 `Thread.interrupt` 设置此标志。当线程通过调用静态方法 `Thread.interrupted` 检查中断时，中断状态被清除。非静态 `isInterrupted` 方法，一个线程用来查询另一个线程的中断状态，不会改变中断状态标志。

按照惯例，任何通过抛出 `InterruptedException` 退出的方法都会在执行此操作时清除中断状态。但是，通过另一个调用 `interrupt` 的线程，总是可以立即再次设置中断状态。

### Joins

`join` 方法允许一个线程等待另一个线程的完成。如果 `t` 是一个线程正在执行的 `Thread` 对象，

```
t.join();
```

导致当前线程暂停执行，直到`t`的线程终止。 `join` 的重载允许程序员指定等待期。但是，与 `sleep` 一样，`join`依赖于操作系统的计时，所以你不应该假设 `join`  将等到你指定的时间。

就像 `sleep` 一样，`join` 通过退出 `InterruptedException` 来响应中断。

### 简单的线程例子

以下示例汇总了本节的一些概念。[`SimpleThreads`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/SimpleThreads.java) 由两个线程组成。第一个是每个 Java 应用程序都有的主线程。主线程从 `Runnable` 对象 `MessageLoop` 创建一个新线程，并等待它完成。如果 `MessageLoop` 线程需要很长时间才能完成，主线程会中断它。

`MessageLoop` 线程打印出一系列消息。如果在打印完所有消息之前被中断，则 `MessageLoop` 线程将打印一条消息并退出。

```java
public class SimpleThreads {

    // Display a message, preceded by
    // the name of the current thread
    static void threadMessage(String message) {
        String threadName =
            Thread.currentThread().getName();
        System.out.format("%s: %s%n",
                          threadName,
                          message);
    }

    private static class MessageLoop
        implements Runnable {
        public void run() {
            String importantInfo[] = {
                "Mares eat oats",
                "Does eat oats",
                "Little lambs eat ivy",
                "A kid will eat ivy too"
            };
            try {
                for (int i = 0;
                     i < importantInfo.length;
                     i++) {
                    // Pause for 4 seconds
                    Thread.sleep(4000);
                    // Print a message
                    threadMessage(importantInfo[i]);
                }
            } catch (InterruptedException e) {
                threadMessage("I wasn't done!");
            }
        }
    }

    public static void main(String args[])
        throws InterruptedException {

        // Delay, in milliseconds before
        // we interrupt MessageLoop
        // thread (default one hour).
        long patience = 1000 * 60 * 60;

        // If command line argument
        // present, gives patience
        // in seconds.
        if (args.length > 0) {
            try {
                patience = Long.parseLong(args[0]) * 1000;
            } catch (NumberFormatException e) {
                System.err.println("Argument must be an integer.");
                System.exit(1);
            }
        }

        threadMessage("Starting MessageLoop thread");
        long startTime = System.currentTimeMillis();
        Thread t = new Thread(new MessageLoop());
        t.start();

        threadMessage("Waiting for MessageLoop thread to finish");
        // loop until MessageLoop
        // thread exits
        while (t.isAlive()) {
            threadMessage("Still waiting...");
            // Wait maximum of 1 second
            // for MessageLoop thread
            // to finish.
            t.join(1000);
            if (((System.currentTimeMillis() - startTime) > patience)
                  && t.isAlive()) {
                threadMessage("Tired of waiting!");
                t.interrupt();
                // Shouldn't be long now
                // -- wait indefinitely
                t.join();
            }
        }
        threadMessage("Finally!");
    }
}
```

