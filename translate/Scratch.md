### 7.4.  `task` 命名空间

Spring 3.0 中包含了配置 `TaskExecutor` 和 `TaskScheduler` 实例的命名空间。同时提供一种方便的方式配置将要通过触发器调度的任务。

#### 7.4.1.  `scheduler` 元素

下面的元素创建一个 `ThreadPoolTaskScheduler` 实例，使用指定的线程池大小：

```xml
<task:scheduler id="scheduler" pool-size="10"/>
```

`id` 属性的值被用来作为线程池中的线程名称的前缀。`scheduler` 元素相对简单。如果你没有指定 `pool-size` 属性，默认的线程池就只会有一个线程。该元素没有其它配置选项。

#### 7.4.2.  `executor` 元素

下面的例子创建一个 `ThreadPoolTaskExecutor` 实例：

```xml
<task:executor id="executor" pool-size="10"/>
```

与 [上一部分](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#scheduling-task-namespace-scheduler) 中显示的调度器一样，为 `id` 属性提供的值用作池中线程名称的前缀。就池的大小而言， `executor` 元素比 `scheduler` 元素支持更多的配置选项。一方面，`ThreadPoolTaskExecutor` 的线程池本身更具可配置性。执行器的线程池不仅可以只包含一个线程，而且可以具有不同的核心线程数和最大线程数。如果提供单个值，则执行器具有固定大小的线程池（核心大小和最大大小相同）。但是，`executor` 元素的 `pool-size` 属性也接受 `min-max` 形式的范围。以下示例将最小值设置为 `5`，将最大值设置为 `25`：

```xml
<task:executor
        id="executorWithPoolSizeRange"
        pool-size="5-25"
        queue-capacity="100"/>
```

在前述配置中，还提供了 `queue-capacity` 值。还应根据执行器的队列容量来考虑线程池的配置。有关池大小和队列容量之间关系的完整说明，请参见 [`ThreadPoolExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html)。主要思想是，在提交任务时，如果当前活动线程数小于核心大小，则执行器首先尝试使用空闲线程。如果已达到核心大小，则只要尚未达到线程池最大容量，就将任务添加到队列中。只有当达到队列的最大容量，执行器才创建超出核心大小的新线程。如果同时还达到了线程池最大大小，那么执行器将拒绝该任务。

默认情况下，队列是无界的，但大部分情况下着并不是所需的配置，因为如果在所有池线程繁忙时将足够的任务添加到该队列中，则会导致 `OutOfMemoryErrors`。此外，如果队列是无界的，则最大大小完全无效。由于执行器总是在创建超出核心大小的新线程之前尝试队列，因此队列必须具有有限的容量，线程池才能超出核心大小（这就是为什么固定大小的池是使用无限队列时唯一明智的情况）。

如上所述，考虑拒绝任务的情况。默认情况下，当任务被拒绝时，线程池执行器将抛出 `TaskRejectedException`。但是，拒绝策略实际上是可配置的。使用默认拒绝策略（即 `AbortPolicy` 实现）时会引发异常。对于某些可以在高负载下跳过某些任务的应用程序，您可以配置 `DiscardPolicy` 或 `DiscardOldestPolicy`。对于需要在重负载下限制提交的任务的应用程序来说，另一个不错的选择是 `CallerRunsPolicy`。该策略不会引发异常或放弃任务，而是强制调用提交方法的线程运行任务本身。这样做的想法是，这样的调用者在运行该任务时很忙，无法立即提交其他任务。因此，它提供了一种在保持线程池和队列限制的同时限制传入负载的简单方法。通常，这允许执行者“赶上”它正在处理的任务，从而释放队列、池中或两者中的某些容量。您可以从 `executor` 元素上的 `rejection-policy` 属性的可用值枚举中选择任何一个。

下面的例子展示了一个 `executor` 元素，使用一系列属性指定各种行为：

```xml
<task:executor
        id="executorWithCallerRunsPolicy"
        pool-size="5-25"
        queue-capacity="100"
        rejection-policy="CALLER_RUNS"/>
```

最后，`keep-alive` 设置确定线程在终止之前可以保持空闲状态的时间限制（以秒为单位）。如果当前线程池中的线程数超过核心数，则在等待此时间而不处理任务后，多余的线程将被终止。时间值为零会导致多余的线程在执行任务后立即终止，而不会在任务队列中保留后续工作。以下示例将 `keep-alive` 值设置为两分钟：

```xml
<task:executor
        id="executorWithKeepAlive"
        pool-size="5-25"
        keep-alive="120"/>
```

