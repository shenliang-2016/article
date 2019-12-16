#### 7.2.1. `Trigger` 接口

`Trigger` 接口本质上是受 JSR-236 的启发，该 JSR-236 自 Spring 3.0 起尚未正式实现。`Trigger` 的基本思想是执行时间可以根据过去的执行结果甚至任意条件来决定。如果这些决定确实考虑了先前执行的结果，则该信息在 `TriggerContext` 中可用。`Trigger` 接口本身非常简单，如以下清单所示：

```java
public interface Trigger {

    Date nextExecutionTime(TriggerContext triggerContext);
}
```

`TriggerContext` 是最重要的部分。它封装了所有相关数据，并在将来必要时开放以进行扩展。`TriggerContext` 是一个接口（默认情况下使用 `SimpleTriggerContext` 实现）。下面的清单展示了 `Trigger` 实现的可用方法。

```java
public interface TriggerContext {

    Date lastScheduledExecutionTime();

    Date lastActualExecutionTime();

    Date lastCompletionTime();
}
```

#### 7.2.2. `Trigger` 实现

Spring 提供了 `Trigger` 接口的两种实现。最有趣的是 `CronTrigger`。它启用了基于 cron 表达式的任务调度。例如，以下任务计划在每小时的 15 分钟后运行，但仅在工作日的上午 9 点到下午 5 点之间的“工作时间”内运行：

```java
scheduler.schedule(task, new CronTrigger("0 15 9-17 * * MON-FRI"));
```

另一个实现是 `PeriodicTrigger`，它接受一个固定的周期，一个可选的初始延迟值和一个布尔值，以指示该周期应被解释为固定速率还是固定延迟。由于 `TaskScheduler` 接口已经定义了以固定速率或固定延迟调度任务的方法，因此应尽可能直接使用这些方法。`PeriodicTrigger` 实现的价值在于您可以在依赖于 `Trigger` 抽象的组件中使用它。例如，允许周期性触发器，基于 cron 的触发器，甚至自定义触发器实现可互换使用可能很方便。这样的组件可以利用依赖注入的优势，以便您可以在外部配置此类 `Triggers` ，因此可以轻松地对其进行修改或扩展。

