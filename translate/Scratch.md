#### 7.4.3. `scheduled-tasks` 元素

Spring task 命名空间最强大的功能是支持配置要在 Spring Application Context 中安排的任务。这遵循类似于 Spring 中其他“方法调用者”的方法，例如 JMS 命名空间提供的用于配置消息驱动的 POJO 的方法。基本上，`ref` 属性可以指向任何 Spring 管理的对象，而 `method` 属性提供要在该对象上调用的方法的名称。以下清单显示了一个简单的示例：

```xml
<task:scheduled-tasks scheduler="myScheduler">
    <task:scheduled ref="beanA" method="methodA" fixed-delay="5000"/>
</task:scheduled-tasks>

<task:scheduler id="myScheduler" pool-size="10"/>
```

调度程序由外部元素引用，并且每个单独的任务都包括其触发元数据的配置。在前面的示例中，该元数据定义了一个具有固定延迟的周期性触发器，该延迟指示了每个任务执行完成后要等待的毫秒数。另一个选项是 `fixed-rate`，它表示应该执行该方法的频率，而不管之前执行的时间如何。另外，对于 `fixed-delay` 和 `fixed-rate` 任务，您都可以指定 `initial-delay` 参数，指示首次执行该方法之前要等待的毫秒数。为了获得更多控制，您可以改为提供 `cron` 属性。以下示例显示了这些其他选项：

```xml
<task:scheduled-tasks scheduler="myScheduler">
    <task:scheduled ref="beanA" method="methodA" fixed-delay="5000" initial-delay="1000"/>
    <task:scheduled ref="beanB" method="methodB" fixed-rate="5000"/>
    <task:scheduled ref="beanC" method="methodC" cron="*/5 * * * * MON-FRI"/>
</task:scheduled-tasks>

<task:scheduler id="myScheduler" pool-size="10"/>
```

