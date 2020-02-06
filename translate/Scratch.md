### 4.20. Quartz 调度器

Spring Boot 为使用 [Quartz Scheduler](https://www.quartz-scheduler.org/) 提供了许多便利，其中包括 `spring-boot-starter-quartz` “Starter”。如果 Quartz 可用，则自动配置 `Scheduler`（通过 `SchedulerFactoryBean` 抽象）。

以下类型的 Bean 将自动被拾取并与 `Scheduler` 相关联：

- `JobDetail` ：定义特定工作。 `JobDetail` 实例可以使用 `JobBuilder` API 构建。
- `Calendar`。
- `Trigger` ：定义特定工作何时被激活。

默认情况下，使用内存中的 `JobStore`。但是，如果应用程序中有可用的 `DataSource` bean，并且如果相应地配置了 `spring.quartz.job-store-type` 属性，则可以配置基于 JDBC 的存储，如以下示例所示：

```properties
spring.quartz.job-store-type=jdbc
```

使用 JDBC 存储时，可以在启动时初始化模式，如以下示例所示：

```properties
spring.quartz.jdbc.initialize-schema=always
```

> 默认情况下，使用 Quartz 库随附的标准脚本检测并初始化数据库。这些脚本删除现有表，并在每次重新启动时删除所有触发器。也可以通过设置 `spring.quartz.jdbc.schema` 属性来提供自定义脚本。

为了让 Quartz 使用应用程序的主 `DataSource` 之外的 `DataSource`，声明一个 `DataSource` bean，并用 `@QuartzDataSource` 标注其 `@Bean` 方法。这样可以确保 `SchedulerFactoryBean` 和 `Schema` 初始化都使用特定于 Quartz 的 `DataSource`。

默认情况下，通过配置创建的作业将不会覆盖从持久性作业存储中读取的已注册作业。为了覆盖现有的工作定义，设置 `spring.quartz.overwrite-existing-jobs` 属性。

可以使用 `spring.quartz` 属性和 `SchedulerFactoryBeanCustomizer` bean来定制 Quartz Scheduler 配置，这允许以编程方式自定义 `SchedulerFactoryBean`。可以使用 `spring.quartz.properties.*` 自定义高级 Quartz 配置属性。

> 特别是，`Executor` bean 与调度程序没有关联，因为 Quartz 通过 `spring.quartz.properties` 提供了一种配置调度程序的方法。如果您需要自定义任务执行器，请考虑实现 `SchedulerFactoryBeanCustomizer`。

作业可以定义设置器以注入数据映射属性。常规 bean 也可以类似的方式注入，如以下示例所示：

```java
public class SampleJob extends QuartzJobBean {

    private MyService myService;

    private String name;

    // Inject "MyService" bean
    public void setMyService(MyService myService) { ... }

    // Inject the "name" job data property
    public void setName(String name) { ... }

    @Override
    protected void executeInternal(JobExecutionContext context)
            throws JobExecutionException {
        ...
    }

}
```