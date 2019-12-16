#### 7.1.2. 使用 `TaskExecutor`

Spring 的 `TaskExecutor` 实现被作为简单的 JavaBean 使用。在以下示例中，我们定义了一个 bean，使用 `ThreadPoolTaskExecutor` 来异步打印出一组消息：

```java
import org.springframework.core.task.TaskExecutor;

public class TaskExecutorExample {

    private class MessagePrinterTask implements Runnable {

        private String message;

        public MessagePrinterTask(String message) {
            this.message = message;
        }

        public void run() {
            System.out.println(message);
        }
    }

    private TaskExecutor taskExecutor;

    public TaskExecutorExample(TaskExecutor taskExecutor) {
        this.taskExecutor = taskExecutor;
    }

    public void printMessages() {
        for(int i = 0; i < 25; i++) {
            taskExecutor.execute(new MessagePrinterTask("Message" + i));
        }
    }
}
```

如你所见，你只是将你自己的 `Runnable` 添加到队列中，而不是从线程池获取线程并自己执行它。然后 `TaskExecutor` 使用它内部的规则决定任务何时执行。

为了配置 `TaskExecutor` 使用的规则，我们暴露简单的 bean 属性：

```xml
<bean id="taskExecutor" class="org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor">
    <property name="corePoolSize" value="5"/>
    <property name="maxPoolSize" value="10"/>
    <property name="queueCapacity" value="25"/>
</bean>

<bean id="taskExecutorExample" class="TaskExecutorExample">
    <constructor-arg ref="taskExecutor"/>
</bean>
```

### 7.2. Spring `TaskScheduler` 抽象

除了对 `TaskExecutor` 的抽象外，Spring 3.0 还引入了 `TaskScheduler`，其中提供了多种方法来安排任务在将来某个时刻运行。以下清单显示 `TaskScheduler` 接口定义：

```java
public interface TaskScheduler {

    ScheduledFuture schedule(Runnable task, Trigger trigger);

    ScheduledFuture schedule(Runnable task, Instant startTime);

    ScheduledFuture schedule(Runnable task, Date startTime);

    ScheduledFuture scheduleAtFixedRate(Runnable task, Instant startTime, Duration period);

    ScheduledFuture scheduleAtFixedRate(Runnable task, Date startTime, long period);

    ScheduledFuture scheduleAtFixedRate(Runnable task, Duration period);

    ScheduledFuture scheduleAtFixedRate(Runnable task, long period);

    ScheduledFuture scheduleWithFixedDelay(Runnable task, Instant startTime, Duration delay);

    ScheduledFuture scheduleWithFixedDelay(Runnable task, Date startTime, long delay);

    ScheduledFuture scheduleWithFixedDelay(Runnable task, Duration delay);

    ScheduledFuture scheduleWithFixedDelay(Runnable task, long delay);
}
```

最简单的方法是一个名为 `schedule` 的方法，该方法仅需要一个 `Runnable` 和一个 `Date`。这将导致任务在指定时间后运行一次。所有其他方法都可以安排任务重复运行。固定速率和固定延迟方法是用于简单，定期执行的，但是接受 `Trigger` 的方法则更加灵活。

