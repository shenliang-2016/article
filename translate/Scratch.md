# Java Callable

Java `Callable` 接口， `java.util.concurrent.Callable`，表示可以被一个单独的线程执行的一个异步任务。比如，可以将一个 `Callable` 对象提交给 [Java ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) 以便随后异步执行它。

## Java Callable 接口定义

Java `Callable` 接口非常简单。它只包含一个方法 `call()`。下面是该接口的样子：

```java
public interface Callable<V> {

    V call() throws Exception;

}
```

调用 `call()` 方法以执行异步任务。该方法会返回一个结果。如果任务被异步执行，则结果通常将会通过一个 [Java Future](http://tutorials.jenkov.com/java-util-concurrent/java-future.html) 反向传播给任务的创建者。这是将 `Callable` 提交给 `ExecutorService` 进行并发执行的情况。

 `call()` 方法也会抛出 `Exception`，如果任务执行失败。

## 实现 Callable

下面是 `Callable` 接口的一个简单实现：

```java
public class MyCallable implements Callable<String> {

    @Override
    public String call() throws Exception {
        return String.valueOf(System.currentTimeMillis());
    }
}
```

此实现非常简单。它携带设定为 [Java String](http://tutorials.jenkov.com/java/strings.html) 的范型类型。`call()` 方法的结果将返回一个 `String` 。例子中 `call()` 方法实现返回一个字符串表示当前时间的毫秒数。在真实的应用中，任务可能会是更大、更复杂的一系列操作的集合。

IO 操作（例如从磁盘或网络读取或写入磁盘或网络）通常是可以同时执行的任务的理想选择。IO 操作在读取和写入数据块之间通常需要很长的等待时间。通过在单独的线程中执行此类任务，可以避免不必要地阻塞主应用程序线程。

## Callable vs. Runnable

Java `Callable` 接口类似于 Java `Runnable` 接口，因为它们都代表一个任务，该任务打算由一个单独的线程同时执行。

Java `Callable` 与 `Runnable` 的不同之处在于 `Runnable` 接口的 `run()` 方法不返回值，并且它不能抛出已检查的异常（仅 `RuntimeException`）。

另外，`Runnable` 最初是为长时间运行的并发执行而设计的，例如同时运行网络服务器，或监视目录中是否有新文件。 `Callable` 接口更适合一次性任务返回单个结果。