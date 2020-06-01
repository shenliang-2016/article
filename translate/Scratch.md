# ScheduledExecutorService

 `java.util.concurrent.ScheduledExecutorService` 是一个 [`ExecutorService`](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) ，可以调度任务在一段延迟时间之后执行，或者按照固定时间间隔重复执行任务。任务将由工作者线程异步执行，而不是由将任务分派给 `ScheduledExecutorService` 的线程执行。

## ScheduledExecutorService 示例

这是一个简单的 `ScheduledExecutorService` 示例：

```java
ScheduledExecutorService scheduledExecutorService =
        Executors.newScheduledThreadPool(5);

ScheduledFuture scheduledFuture =
    scheduledExecutorService.schedule(new Callable() {
        public Object call() throws Exception {
            System.out.println("Executed!");
            return "Called!";
        }
    },
    5,
    TimeUnit.SECONDS);
```

首先创建一个带有 5 个线程的 `ScheduledExecutorService`。然后，创建 `Callable` 接口的匿名实现，并将其传递给 `schedule()` 方法。最后两个参数指定 `Callable` 应在 5 秒钟后执行。

## ScheduledExecutorService 实现

由于 `ScheduledExecutorService` 是一个接口，你需要使用位于 `java.util.concurrent` 包中的接口实现。 `ScheduledExecutorService` 的一个实现如下：

- ScheduledThreadPoolExecutor

## 创建 ScheduledExecutorService

如何创建 `ScheduledExecutorService` 取决于你使用的实现。不过，你也可以使用 `Executors` 工厂类创建 `ScheduledExecutorService` 实例。示例如下：

```java
ScheduledExecutorService scheduledExecutorService = Executors.newScheduledThreadPool(5);
```

## ScheduledExecutorService 使用

一旦创建了 `ScheduledExecutorService` 就可以通过调用它的方法来使用它：

- schedule (Callable task, long delay, TimeUnit timeunit)
- schedule (Runnable task, long delay, TimeUnit timeunit)
- scheduleAtFixedRate (Runnable, long initialDelay, long period, TimeUnit timeunit)
- scheduleWithFixedDelay (Runnable, long initialDelay, long period, TimeUnit timeunit)

下面简要介绍这些方法。

### schedule (Callable task, long delay, TimeUnit timeunit)

此方法在给定的延迟后安排给定的 `Callable` 执行。

该方法返回一个 `ScheduledFuture`，可用于在开始执行之前取消任务，或在执行后获取结果。

这是一个例子：

```java
ScheduledExecutorService scheduledExecutorService =
        Executors.newScheduledThreadPool(5);

ScheduledFuture scheduledFuture =
    scheduledExecutorService.schedule(new Callable() {
        public Object call() throws Exception {
            System.out.println("Executed!");
            return "Called!";
        }
    },
    5,
    TimeUnit.SECONDS);

System.out.println("result = " + scheduledFuture.get());

scheduledExecutorService.shutdown();
```

这个例子输出

```
Executed!
result = Called!
```

### schedule (Runnable task, long delay, TimeUnit timeunit)

该方法的工作方式类似于以 `Callable` 作为参数的方法版本，除了 `Runnable` 无法返回值之外。因此 `ScheduledFuture.get()` 方法在任务完成时返回 `null`。

### scheduleAtFixedRate (Runnable, long initialDelay, long period, TimeUnit timeunit)

此方法调度要定期执行的任务。该任务在 `initialDelay` 之后第一次执行，然后在每次 `period` 到期时重复执行。

如果给定任务的任何执行均引发异常，则该任务将不再执行。如果没有抛出异常，则该任务将继续执行，直到关闭 `ScheduledExecutorService` 为止。

如果任务执行的时间比调度执行时间间更长，则下一次执行将在当前执行完成后开始。被调度的任务一次不会同时由多个线程执行。

### scheduleWithFixedDelay (Runnable, long initialDelay, long period, TimeUnit timeunit)

该方法非常类似于 `scheduleAtFixedRate()`，除了 `period` 的解释不同。

在 `scheduleAtFixedRate()` 方法中，`period` 被解释为上一次执行开始到下一次执行开始之间的时间间隔。

但是，在此方法中，`period` 被解释为上一次执行的“结束”到下一次开始的时间间隔。因此，延迟是在完成执行之间，而不是在执行开始之间。

## ScheduledExecutorService 关闭

就像 `ExecutorService` 一样，`ScheduledExecutorService` 在使用完毕后也需要关闭。如果没有，即使所有其他线程都已关闭，它也将保持 JVM 运行。

您可以使用从 `ExecutorService` 接口继承的 `Shutdown()` 或 `ShutdownNow()` 方法来关闭 `ScheduledExecutorService`。有关更多信息，请参见 [ExecutorService Shutdown](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html#executorservice-shutdown) 部分。