#### 7.2.3. `TaskScheduler` 实现

与 Spring 的 `TaskExecutor` 抽象一样，`TaskScheduler` 安排的主要好处是应用程序的调度需求与部署环境分离。在部署到不应由应用程序本身直接创建线程的应用程序服务器环境时，此抽象级别特别重要。对于这种情况，Spring 提供了一个在 WebLogic 或 WebSphere 上委派给 CommonJ `TimerManager` 的 `TimerManagerTaskScheduler`，以及一个在 Java EE 7+ 环境中委派给 JSR-236 `ManagedScheduledExecutorService` 的较新的 `DefaultManagedTaskScheduler`。两者通常都配置有 JNDI 查找。

每当不需要外部线程管理时，一个更简单的选择就是在应用程序中进行本地 `ScheduledExecutorService` 设置，可以通过 Spring 的 `ConcurrentTaskScheduler` 进行适配。为了方便起见，Spring 还提供了一个 `ThreadPoolTaskScheduler`，它在内部委托给 `ScheduledExecutorService` 以按照 `ThreadPoolTaskExecutor` 的方式提供通用的 bean 样式的配置。这些变体也适用于宽松的应用程序服务器环境中的本地嵌入式线程池设置，尤其是在 Tomcat 和 Jetty 上。

