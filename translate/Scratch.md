### `Thread`对象

每个线程都与`Thread`类的实例相关联。使用`Thread`对象创建并发应用程序有两种基本策略。

- 要直接控制线程创建和管理，只需在每次应用程序需要启动异步任务时实例化`Thread`。
- 要从应用程序的其余部分抽象线程管理，请将应用程序的任务传递给*执行器*。

本节介绍`Thread`对象的使用。执行器与其他 [高级并发对象](https://docs.oracle.com/javase/tutorial/essential/concurrency/highlevel.html) 共同讨论。

#### 创建和启动线程

创建`Thread`实例的应用程序必须提供将在该线程中运行的代码。有两种方法可以做到这一点：

- *提供一个Runnable对象* [`Runnable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html) 接口定义了一个单独的方法`run`， 意味着包含在线程中执行的代码。 `Runnable`对象传递给`Thread`constructor，如 [`HelloRunnable`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/HelloRunnable.java) 示例：

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

- *Thread 的子类* `Thread`类本身实现`Runnable`，尽管它的`run`方法什么都不做。应用程序可以子类化`Thread`，提供自己的`run`实现，如 [`HelloRunnable`](https://docs.oracle.com/javase/tutorial/essential/concurrency/examples/HelloRunnable.java) 示例。

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

请注意，两个示例都调用`Thread.start`以启动新线程。

你应该使用哪个方法？使用`Runnable`对象是更通用的，因为`Runnable`对象可以子类化除了`Thread`之外的类。第二个习惯用法在简单的应用程序中更容易使用，但受限于你的任务类必须是`Thread`的子类。本课重点介绍第一种方法，它将`Runnable`任务与执行任务的`Thread`对象分开。这种方法不仅更灵活，而且适用于后面介绍的高级线程管理API。

`Thread`类定义了许多对线程管理有用的方法。这些包括`static`方法，它们提供有关调用方法的线程的信息或影响其状态。从管理线程和`Thread`对象所涉及的其他线程调用其他方法。我们将在以下部分中研究其中一些方法。

