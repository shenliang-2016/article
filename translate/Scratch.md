# Java Future

Java *Future*，即 `java.util.concurrent.Future`，表示异步计算的结果。创建异步任务后，将返回 Java `Future` 对象。这个 `Future` 对象用作异步任务结果的引用。异步任务完成后，可以通过启动任务时返回的 `Future` 对象访问结果。

Java 的一些内置并发实用程序，例如 [Java ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html)，从其某些方法中返回 Java `Future` 对象。对于 `ExecutorService`，当您提交一个 `Callable` 使其并发（异步）执行时，它将返回一个 `Future`。

## Java Future 接口定义

为了理解 Java `Future` 接口如何工作，下面是简要的接口定义：

```java
public interface Future<V> {
    boolean cancel(boolean mayInterruptIfRunning)
    V       get();
    V       get(long timeout, TimeUnit unit);
    boolean isCancelled();
    boolean isDone();
}
```

接下来将逐个介绍这些方法——不过，如你所见， Java `Future` 接口并没有多么复杂。

## 从 Future 获取结果

如前所述，Java `Future` 表示异步任务的结果。为了获得结果，您可以调用 `Future` 上的两个 `get()` 方法之一。 `get()` 方法都返回一个 `Object`，但是返回类型也可以是范型返回类型（意味着特定类的对象，而不仅仅是 `Object`）。这是一个通过 Java `Future` 的 `get()` 方法获得结果的示例：

```java
Future future = ... // get Future by starting async task

// do something else, until ready to check result via Future

// get result from Future
try {
    Object result = future.get();
} catch (InterruptedException e) {
    e.printStackTrace();
} catch (ExecutionException e) {
    e.printStackTrace();
}
```

如果你在异步任务执行完成之前调用 `get()` 方法，该方法将会阻塞直到结果已经准备好。

有一个 `get()` 方法的版本，它可以在经过一定时间后超时，您可以通过方法参数来指定超时时间。这是调用该 `get()` 版本的示例：

```java
try {
    Object result =
        future.get(1000, TimeUnit.MILLISECONDS);
} catch (InterruptedException e) {

} catch (ExecutionException e) {

} catch (TimeoutException e) {
    // thrown if timeout time interval passes
    // before a result is available.
}
```

上面的示例最多等待 1000 毫秒，以便结果在 `Future`  中可用。如果在 1000 毫秒内没有结果可用，则抛出 `TimeoutException`。

## 通过 Future cancel() 取消任务

您可以通过调用 `Future` `cancel()` 方法来取消由 Java `Future` 实例表示的异步任务。必须实现异步任务执行以支持取消。没有这样的支持，调用 `cancel()` 将无效。这是通过 Java `Future` `cancel()` 方法取消任务的示例：

```java
future.cancel();
```

## 检查任务是否完成

通过调用 `Future` `isDone()` 方法，你可以检查异步任务是否完成（结果可用）。下面是示例：

```java
Future future = ... // Get Future from somewhere

if(future.isDone()) {
    Object result = future.get();
} else {
    // do something else
}
```

## 检查任务是否取消

还可以检查由 Java `Future` 表示的异步任务是否被取消。您可以通过调用 `Future` `isCancelled()` 方法进行检查。这是检查任务是否被取消的示例：

```java
Future future = ... // get Future from somewhere

if(future.isCancelled()) {

} else {

}
```

