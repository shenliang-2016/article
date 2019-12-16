## 7. 任务执行和调度

Spring 框架分别通过 `TaskExecutor` 和 `TaskScheduler` 接口为任务的异步执行和调度提供了抽象。Spring 还提供了那些接口的实现，这些接口在应用程序服务器环境中支持线程池或委托给 `CommonJ`。最终，在公共接口后面使用这些实现可以抽象化 Java SE 5，Java SE 6 和 Java EE 环境之间的差异。

Spring还具有集成类，以支持使用 `Timer`（自 1.3 开始成为 JDK 的一部分）和 Quartz Scheduler（https://www.quartz-scheduler.org/）进行调度。您可以通过使用带有分别对 `Timer` 或 `Trigger` 实例的可选引用的 `FactoryBean` 来设置这两个调度程序。此外，还提供了 Quartz Scheduler 和 `Timer` 的便捷类，可用于调用现有目标对象的方法（类似于常规的 `MethodInvokingFactoryBean` 操作）。

### 7.1. Spring `TaskExecutor` 抽象

Executors 是线程池概念的JDK名称。 Executors 的命名是由于无法保证基础实现实际上是一个池。执行程序可能是单线程的，甚至是同步的。Spring 的抽象隐藏了 Java SE 和 Java EE 环境之间的实现细节。

Spring 的 `TaskExecutor` 接口与 `java.util.concurrent.Executor` 接口相同。实际上，最初，其存在的主要原因是在使用线程池时抽象出对 Java 5 的需求。该接口具有单个方法（ `execute(Runnable task)`），该方法根据线程池的语义和配置接受要执行的任务。

最初创建 `TaskExecutor` 的目的是为其他 Spring 组件提供所需的线程池抽象。诸如 `ApplicationEventMulticaster`，JMS 的 `AbstractMessageListenerContainer` 和 Quartz 集成之类的组件均使用 `TaskExecutor` 抽象来池化线程。但是，如果您的 bean 需要线程池行为，则也可以根据自己的需要使用此抽象。

