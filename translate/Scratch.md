### 7.5. 使用 Quartz 调度器

Quartz 使用 `Trigger`，`Job` 以及 `JobDetail` 对象来实现各种任务的调度。要了解 Quartz 背后的基本概念，请参考 https://www.quartz-scheduler.org/ 。方便起见，Spring 提供了两个类来简化在基于 Spring 的引用中的 Quartz 使用。

#### 7.5.1. 使用 `JobDetailFactoryBean`

Quart `JobDetail` 对象包含运行一项任务所需的所有信息。Spring 提供了 `JobDetailFactoryBean` ，它为 XML 形式的配置提供了 bean 风格的属性。考虑下面的例子：

```xml
<bean name="exampleJob" class="org.springframework.scheduling.quartz.JobDetailFactoryBean">
    <property name="jobClass" value="example.ExampleJob"/>
    <property name="jobDataAsMap">
        <map>
            <entry key="timeout" value="5"/>
        </map>
    </property>
</bean>
```

任务细节配置包含运行任务（`ExampleJob`）所需的所有信息。超时在任务数据映射中指定。任务数据映射在 `JobExectionContext` （在任务执行期间会传递给你）中可用，但是 `JobDetail` 同样也从用于配置任务实例的任务数据映射中获取它的属性。因此，下面的例子中，`ExampleJob` 包含名为 `timeout` 的 bean 属性，`JobDetail` 自动应用该属性值：

```java
package example;

public class ExampleJob extends QuartzJobBean {

    private int timeout;

    /**
     * Setter called after the ExampleJob is instantiated
     * with the value from the JobDetailFactoryBean (5)
     */
    public void setTimeout(int timeout) {
        this.timeout = timeout;
    }

    protected void executeInternal(JobExecutionContext ctx) throws JobExecutionException {
        // do the actual work
    }

}
```

从任务数据映射中获取的额外属性对你来说同样可用。

> 通过使用 `name` 和 `group` 属性，你可以相应修改任务的名称和组。默认情况下，任务名称对应于 `JobDetailFactoryBean` bean 名称（上面例子中的 `exampleJob`）。

#### 7.5.2. 使用 `MethodInvokingJobDetailFactoryBean`

通常你很少需要调用特定对象上的方法。通过使用 `MethodInvokingJobDetailFactoryBean` ，你可以做到这一点，如下面例子所示：

```xml
<bean id="jobDetail" class="org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean">
    <property name="targetObject" ref="exampleBusinessObject"/>
    <property name="targetMethod" value="doIt"/>
</bean>
```

前面的示例导致在 `exampleBusinessObject` 方法上调用 `doIt` 方法，如以下示例所示：

```java
public class ExampleBusinessObject {

    // properties and collaborators

    public void doIt() {
        // do the actual work
    }
}
```

````xml
<bean id="exampleBusinessObject" class="examples.ExampleBusinessObject"/>
````

通过使用 `MethodInvokingJobDetailFactoryBean`，您无需创建仅调用方法的单行作业。您只需要创建实际的业务对象并连接具体对象即可。

默认情况下，Quartz Jobs 是无状态的，从而导致作业相互干扰的可能性。如果为相同的 `JobDetail` 指定两个触发器，则有可能在第一个作业完成之前启动第二个作业。如果 `JobDetail` 类实现了 `Stateful` 接口，则不会发生这种情况。在第一个作业完成之前，第二个作业不会开始。要使由 `MethodInvokingJobDetailFactoryBean` 产生的作业是非并行的，请将 `concurrent` 标记设置为 `false`，如以下示例所示：

```xml
<bean id="jobDetail" class="org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean">
    <property name="targetObject" ref="exampleBusinessObject"/>
    <property name="targetMethod" value="doIt"/>
    <property name="concurrent" value="false"/>
</bean>
```

> 默认情况下，作业将以并发方式运行。

#### 7.5.3. 通过使用触发器和 `SchedulerFactoryBean` 连接作业

我们已经创建了工作详细信息和工作。我们还回顾了便捷 bean，该 bean 使您可以在特定对象上调用方法。当然，我们仍然需要自己调度工作。这是通过使用触发器和一个 `SchedulerFactoryBean` 来完成的。Quartz 中提供了几种触发器，Spring 提供了两个具有方便的默认值的 Quartz `FactoryBean` 实现：`CronTriggerFactoryBean` 和 `SimpleTriggerFactoryBean`。

触发器需要调度。Spring提供了一个 `SchedulerFactoryBean`，它公开了要设置为属性的触发器。  `SchedulerFactoryBean` 通过这些触发器调度实际的作业。

以下清单同时使用了 `SimpleTriggerFactoryBean` 和 `CronTriggerFactoryBean`：

```xml
<bean id="simpleTrigger" class="org.springframework.scheduling.quartz.SimpleTriggerFactoryBean">
    <!-- see the example of method invoking job above -->
    <property name="jobDetail" ref="jobDetail"/>
    <!-- 10 seconds -->
    <property name="startDelay" value="10000"/>
    <!-- repeat every 50 seconds -->
    <property name="repeatInterval" value="50000"/>
</bean>

<bean id="cronTrigger" class="org.springframework.scheduling.quartz.CronTriggerFactoryBean">
    <property name="jobDetail" ref="exampleJob"/>
    <!-- run every morning at 6 AM -->
    <property name="cronExpression" value="0 0 6 * * ?"/>
</bean>
```

前面的示例设置了两个触发器，一个触发器每隔 50 秒运行一次，启动延迟为 10 秒，另一个触发器每天清晨 6 点运行。要完成所有工作，我们需要设置 `SchedulerFactoryBean`，如以下示例所示：

```xml
<bean class="org.springframework.scheduling.quartz.SchedulerFactoryBean">
    <property name="triggers">
        <list>
            <ref bean="cronTrigger"/>
            <ref bean="simpleTrigger"/>
        </list>
    </property>
</bean>
```

更多的属性可用于 `SchedulerFactoryBean`，例如工作明细所使用的日历，用于自定义 Quartz 的属性等。请参阅 [`SchedulerFactoryBean`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/scheduling/quartz/SchedulerFactoryBean.html) Javadoc了解更多信息 。

