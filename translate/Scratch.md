# Java ExecutorService

Java *ExecutorService* 接口，`java.util.concurrent.ExecutorService`，表示一种一步执行机制，该机制能够在后台并发执行多个任务。本文中我将解释如何创建 `ExecutorService`，如何向其提交待执行的任务，如果检查那些任务的执行结果，以及如何在你需要的时候如何关闭 `ExecutorService` 。

## 任务委托

下图展示了线程将一个任务委托给 Java `ExecutorService` 以便异步执行：

| ![A thread delegating a task to an ExecutorService for asynchronous execution.](http://tutorials.jenkov.com/images/java-concurrency-utils/executor-service.png) |
| ------------------------------------------------------------ |
| **线程将一个任务委托给 Java `ExecutorService` 以便异步执行** |

一旦线程将任务委托给了 `ExecutorService` ，该线程就会继续它自己的执行，而不受那个委托出去的任务的影响。`ExecutorService` 会并发执行任务，独立于提交该任务的线程。

## Java ExecutorService 示例

在我们继续深入了解 `ExecutorService` 之前，先看一个简单的例子：

```java
ExecutorService executorService = Executors.newFixedThreadPool(10);

executorService.execute(new Runnable() {
    public void run() {
        System.out.println("Asynchronous task");
    }
});

executorService.shutdown();
```

首先，通过使用 `Executors` `newFixedThreadPool()` 工厂方法创建 `ExecutorService` 。例子中创建了包含了 10 个用于执行任务的线程的线程池。

然后， `Runnable` 接口的一个匿名实现被传递给 `execute()` 方法。这就导致该  `Runnable` 将会被 `ExecutorService` 中的其中一个线程执行。

在本教程中，您将看到更多有关如何使用 `ExecutorService` 的示例。这个例子只是让您快速了解如何使用 `ExecutorService` 在后台执行任务。

## Java ExecutorService 实现

Java `ExecutorService` 与 [线程池](http://tutorials.jenkov.com/java-concurrency/thread-pools.html) 非常相似。实际上，存在于 `java.util.concurrent` 包中的 `ExecutorService` 接口的实现就是线程池实现。如果您想了解如何在内部实现 `ExecutorService` 接口，请阅读上述教程。

由于 `ExecutorService` 是一个接口，因此您需要对其实现进行使用。`ExecutorService` 在 `java.util.concurrent` 包中具有以下实现：

- [ThreadPoolExecutor](http://tutorials.jenkov.com/java-util-concurrent/threadpoolexecutor.html)
- [ScheduledThreadPoolExecutor](http://tutorials.jenkov.com/java-util-concurrent/scheduledexecutorservice.html)

## 创建 ExecutorService

如何创建 `ExecutorService` 取决于你使用的实现。不过，你也可以使用 `Executors` 工厂类创建 `ExecutorService` 实例。下面是几个创建 `ExecutorService` 的例子：

```java
ExecutorService executorService1 = Executors.newSingleThreadExecutor();

ExecutorService executorService2 = Executors.newFixedThreadPool(10);

ExecutorService executorService3 = Executors.newScheduledThreadPool(10);
```

## ExecutorService 使用

有几种不同的方法可以将任务委托给 `ExecutorService` 执行：

- execute(Runnable)
- submit(Runnable)
- submit(Callable)
- invokeAny(...)
- invokeAll(...)

接下来分别介绍这些方法。

### Execute Runnable

Java `ExecutorService` `execute(Runnable)` 方法接收一个 `java.lang.Runnable` 对象，并异步执行它。下面是使用 `ExecutorService` 执行 `Runnable` 的例子：

```java
ExecutorService executorService = Executors.newSingleThreadExecutor();

executorService.execute(new Runnable() {
    public void run() {
        System.out.println("Asynchronous task");
    }
});

executorService.shutdown();
```

没有办法获取被执行的 `Runnable` 的执行结果。如果需要，你将需要使用 `Callable` 来实现这一点。

### Submit Runnable

Java `ExecutorService` `submit(Runnable)` 方法同样接收一个 `Runnable` 实现，但是返回一个 `Future` 对象。这个 `Future` 对象可以被用来确定该 `Runnable` 是否已经执行完成。

下面是 Java `ExecutorService` `submit()` 示例：

```java
Future future = executorService.submit(new Runnable() {
    public void run() {
        System.out.println("Asynchronous task");
    }
});

future.get();  //returns null if the task has finished correctly.
```

该 `submit()` 方法返回一个 [Java Future](http://tutorials.jenkov.com/java-util-concurrent/java-future.html) 对象，该对象可以用来确认该 `Runnable` 何时执行完成。

### Submit Callable

Java `ExecutorService` `submit(Callable)` 方法类似于 `submit(Runnable)` 方法，除了它接收的参数是 [Java Callable](http://tutorials.jenkov.com/java-util-concurrent/java-callable.html) 而不是 `Runnable`。稍后我将介绍 `Callable` 与 `Runnable` 之间的精确差别。

该 `Callable` 的结果能够通过 `submit(Callable)`  方法返回的 [Java Future](http://tutorials.jenkov.com/java-util-concurrent/java-future.html) 对象获取。下面是 `ExecutorService` `Callable` 示例：

```java
Future future = executorService.submit(new Callable(){
    public Object call() throws Exception {
        System.out.println("Asynchronous Callable");
        return "Callable Result";
    }
});

System.out.println("future.get() = " + future.get());
```

上面的例子将输出：

```
Asynchronous Callable
future.get() = Callable Result
```

### invokeAny()

`invokeAny()` 方法接收一个 `Callable` ，或者 `Callable` 的子接口对象集合。调用此方法不会返回 `Future`，但是返回其中一个 `Callable` 对象的结果。无法保证你将会得到哪个 `Callable` 对象的结果，只能说是执行完成当中的一个。

如果其中一个任务完成（或者抛出异常），则其他的 `Callable` 将会被取消。

这是一个示例：

```java
ExecutorService executorService = Executors.newSingleThreadExecutor();

Set<Callable<String>> callables = new HashSet<Callable<String>>();

callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 1";
    }
});
callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 2";
    }
});
callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 3";
    }
});

String result = executorService.invokeAny(callables);

System.out.println("result = " + result);

executorService.shutdown();
```

此代码示例将打印出给定集合中 `Callable` 之一返回的对象。我试过几次，结果会发生变化。有时是“Task 1”，有时是“Task 2”。

### invokeAll()

`invokeAll()` 方法调用作为参数传递的集合中传递给它的所有 `Callable` 对象。`invokeAll()` 返回一个 `Future` 对象的列表，通过它可以获取每个 `Callable` 的执行结果。

请记住，任务可能由于异常而终止，因此它可能没有“成功”。 `Future` 并没有办法区别这种不同的结果。

这是一个代码示例：

```java
ExecutorService executorService = Executors.newSingleThreadExecutor();

Set<Callable<String>> callables = new HashSet<Callable<String>>();

callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 1";
    }
});
callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 2";
    }
});
callables.add(new Callable<String>() {
    public String call() throws Exception {
        return "Task 3";
    }
});

List<Future<String>> futures = executorService.invokeAll(callables);

for(Future<String> future : futures){
    System.out.println("future.get = " + future.get());
}

executorService.shutdown();
```

### Runnable vs. Callable

`Runnable` 接口与 `Callable` 接口非常相似。这两个接口都表示可以由线程或 `ExecutorService` 并发执行的任务。这两个接口都只有一个方法。不过，`Callable` 和 `Runnable` 接口之间只有一个小区别。当您看到接口声明时，将更容易看到 `Runnable` 和 `Callable` 接口之间的区别。

首先是 `Runnable` 接口声明：

```java
public interface Runnable {
    public void run();
}
```

这里是 `Callable` 接口声明：

```java
public interface Callable{
    public Object call() throws Exception;
}
```

`Runnable` 的 `run()` 方法和 `Callable` 的 `call()` 方法之间的主要区别是 `call()` 方法可以从方法调用中返回 `Object`。`call()` 和 `run()` 之间的另一个区别是 `call()` 可以引发异常，而 `run()` 不能（除非未经检查的异常- `RuntimeException` 的子类）。

如果需要向 Java `ExecutorService` 提交任务，并且需要任务的结果，则需要使任务实现 `Callable` 接口。否则，您的任务可以只实现 `Runnable` 接口。

### 取消任务

您可以通过在提交任务时返回的 `Future` 上调用 `cancel()` 方法来取消提交给 Java `ExecutorService` 的任务（`Runnable` 或 `Callable`）。仅当任务尚未开始执行时才可以取消任务。这是通过调用 `Future.cancel()` 方法取消任务的示例：

```java
future.cancel();
```

## ExecutorService 关闭

使用完 Java`ExecutorService` 后，应将其关闭，这样线程就不会继续运行。如果您的应用程序是通过 `main()` 方法启动的，而主线程退出了应用程序，那么如果您的应用程序中有活动的 `ExexutorService`，则该应用程序将继续运行。该 `ExecutorService` 中的活动线程可阻止 JVM 关闭。

### shutdown()

要终止 `ExecutorService` 内部的线程，请调用其 `Shutdown()` 方法。`ExecutorService` 不会立即关闭，但是将不再接受新任务，并且一旦所有线程都完成了当前任务，`ExecutorService` 就会关闭。执行所有在调用 `Shutdown()` 之前提交给 `ExecutorService` 的任务。这是执行 Java `ExecutorService shutdown` 的示例：

```java
executorService.shutdown();
```

### shutdownNow()

如果您想立即关闭 `ExecutorService`，可以调用 `shutdownNow()` 方法。这将尝试立即停止所有正在执行的任务，并跳过所有已提交但未处理的任务。不能保证执行任务。也许他们停下来，也许执行到最后。这是尽力而为的尝试。这是调用 `ExecutorService``shutdownNow` 的示例：

```java
executorService.shutdownNow();
```

### awaitTermination()

`ExecutorService的awaitTermination()` 方法将阻塞调用它的线程，直到 `ExecutorService` 完全关闭或发生给定的超时为止。通常在调用 `shutdown()` 或 `shutdownNow()` 之后调用 `awaitTermination()` 方法。这是调用 `ExecutorService``awaitTermination()` 的示例：

```java
executorService.shutdown();

executorService.awaitTermination();
```

