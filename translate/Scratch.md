#### 7.1.1. `TaskExecutor` 类型

Spring 包含若干预置的 `TaskExecutor` 实现。大多数情况下，你应该不需要自己来实现。Spring 提供如下变体：

- `SyncTaskExecutor`: 此实现不回异步执行调用。每个调用都发生在调用线程中。主要用在不需要多线程的场景，比如简单的测试用例。
- `SimpleAsyncTaskExecutor`: 此实现不会复用任何线程。它为每次调用启动一个新的线程。不过，它支持有限制的并发，超过并发度限制的调用将被阻塞直到运行中的线程结束以空出并发额度。如果你需要真正的线程池，参考此列表后面的 `ThreadPoolTaskExecutor` 。
- `ConcurrentTaskExecutor`: 此实现是 `java.util.concurrent.Executor` 实例的适配器。还有一个替代（`ThreadPoolTaskExecutor`），将 `Executor` 配置参数作为 bean 属性公开。很少需要直接使用 `ConcurrentTaskExecutor`。但是，如果 `ThreadPoolTaskExecutor` 不够灵活，无法满足您的需求，则可以选择 `ConcurrentTaskExecutor` 。
- `ThreadPoolTaskExecutor`: 此实现是最常用的。它公开了用于配置 `java.util.concurrent.ThreadPoolExecutor` 的 bean 属性，并将其包装在 `TaskExecutor` 中。如果您需要适配其他类型的 `java.util.concurrent.Executor`，我们建议您改用 `ConcurrentTaskExecutor`。
- `WorkManagerTaskExecutor`: 此实现使用 CommonJ `WorkManager` 作为其支持服务提供者，并且是在 Spring 应用程序上下文中在 WebLogic 或 WebSphere 上设置基于 CommonJ 的线程池集成的中心便利类。
- `DefaultManagedTaskExecutor`: 此实现在兼容 JSR-236 的运行时环境（例如 Java EE 7+ 应用程序服务器）中使用 JNDI 获得的 `ManagedExecutorService`，为此替换了 CommonJ `WorkManager`。

