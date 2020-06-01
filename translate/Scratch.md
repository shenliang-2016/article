# ThreadPoolExecutor

`java.util.concurrent.ThreadPoolExecutor` 是 [`ExecutorService`](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) 接口的一个实现。 `ThreadPoolExecutor` 使用它内部池化的多个线程中的一个执行给定的任务（`Callable` 或者 `Runnable`）。

包含在 `ThreadPoolExecutor` 内部的线程池可以包含大量的线程。线程池中的线程数量由以下参数确定：

- `corePoolSize`
- `maximumPoolSize`

如果在将任务委派给线程池时在线程池中创建的线程数少于 `corePoolSize`，则即使该池中存在空闲线程，也会创建一个新线程。

如果内部任务队列已满，并且正在运行 `corePoolSize` 个线程或更多线程，但正在运行的线程数少于 `maximumPoolSize`，那么将创建一个新线程来执行任务。

下面是 `ThreadPoolExecutor` 原理示意图：

| ![A ThreadPoolExecutor.](http://tutorials.jenkov.com/images/java-concurrency-utils/thread-pool-executor.png) |
| ------------------------------------------------------------ |
| **一个 ThreadPoolExecutor**                                  |

## 创建 ThreadPoolExecutor

 `ThreadPoolExecutor` 有好几种可用的构造方法。比如：

```java
int  corePoolSize  =    5;
int  maxPoolSize   =   10;
long keepAliveTime = 5000;

ExecutorService threadPoolExecutor =
        new ThreadPoolExecutor(
                corePoolSize,
                maxPoolSize,
                keepAliveTime,
                TimeUnit.MILLISECONDS,
                new LinkedBlockingQueue<Runnable>()
                );
```

但是，除非您需要为 `ThreadPoolExecutor` 明确指定所有这些参数，否则通常使用 `java.util.concurrent.Executors` 类中的工厂方法之一更容易，如 [ExecutorService](http ：//tutorials.jenkov.com/java-util-concurrent/executorservice.html) 中所述。

