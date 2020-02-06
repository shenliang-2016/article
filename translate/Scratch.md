### 4.21. 任务执行和调度

在上下文中没有 `Executor` bean 的情况下，Spring Boot 会自动配置具有合理默认值的 `ThreadPoolTaskExecutor`，这些默认值可以自动与异步任务执行（`@EnableAsync`）和 Spring MVC 异步请求处理相关联。

> 如果您在上下文中定义了一个自定义的 `Executor`，则常规任务执行（即 `@ EnableAsync`）将透明地使用它，但由于需要 `AsyncTaskExecutor` 实现（名为 `applicationTaskExecutor`），因此不会配置 Spring MVC 支持。根据您的目标安排，您可以将 `Executor` 更改为 `ThreadPoolTaskExecutor` 或定义包装自定义 `Executor` 的 `ThreadPoolTaskExecutor` 和 `AsyncConfigurer` 自动配置的 `TaskExecutorBuilder` 可以轻松创建实例，复制默认情况下自动配置的功能。

线程池使用 8 个核心线程，这些线程可以根据负载增长和收缩。可以使用 `spring.task.execution` 名称空间对这些默认设置进行微调，如以下示例所示：

```properties
spring.task.execution.pool.max-size=16
spring.task.execution.pool.queue-capacity=100
spring.task.execution.pool.keep-alive=10s
```

这会将线程池更改为使用有界队列，以便在队列已满（100 个任务）时，线程池最多增加到 16 个线程。线程的空闲时间为 10 秒（而不是默认情况下的 60 秒）时，回收线程会使池的收缩更加激进。

如果需要与计划任务执行相关联，也可以自动配置 `ThreadPoolTaskScheduler`（`@EnableScheduling`）。线程池默认使用一个线程，并且可以使用 `spring.task.scheduling` 名称空间对这些设置进行微调。

如果需要创建自定义执行程序或调度程序，则可以在上下文中同时使用 `TaskExecutorBuilder` bean和 `TaskSchedulerBuilder` bean。

