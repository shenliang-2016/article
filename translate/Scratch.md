#### 4.28.4. 测试你的自动配置

自动配置可能受许多因素影响：用户配置（`@Bean` 定义和 `Environment` 自定义），条件评估（存在特定库）以及其他因素。具体而言，每个测试都应创建定义良好的 `ApplicationContext`，以表示这些自定义项的组合。`ApplicationContextRunner` 提供了一种实现此目标的好方法。

通常将 `ApplicationContextRunner` 定义为测试类的一个字段，以收集基本的通用配置。下面的示例确保始终调用 `UserServiceAutoConfiguration`：

```java
private final ApplicationContextRunner contextRunner = new ApplicationContextRunner()
        .withConfiguration(AutoConfigurations.of(UserServiceAutoConfiguration.class));
```

> 如果必须定义多个自动配置，则无需按与运行应用程序时完全相同的顺序调用它们的声明。

每个测试都可以使用运行器来表示特定的用例。例如，下面的示例调用一个用户配置（`UserConfiguration`），并检查自动配置是否正确退出。调用`run`提供了可与`Assert4J`一起使用的回调上下文。

```java
@Test
void defaultServiceBacksOff() {
    this.contextRunner.withUserConfiguration(UserConfiguration.class).run((context) -> {
        assertThat(context).hasSingleBean(UserService.class);
        assertThat(context).getBean("myUserService").isSameAs(context.getBean(UserService.class));
    });
}

@Configuration(proxyBeanMethods = false)
static class UserConfiguration {

    @Bean
    UserService myUserService() {
        return new UserService("mine");
    }

}
```

同样可能很容易地自定义 `Environment` ，如下面例子所示：

```java
@Test
void serviceNameCanBeConfigured() {
    this.contextRunner.withPropertyValues("user.name=test123").run((context) -> {
        assertThat(context).hasSingleBean(UserService.class);
        assertThat(context.getBean(UserService.class).getName()).isEqualTo("test123");
    });
}
```

运行器也可以用来显示`ConditionEvaluationReport`。该报告可以以 `INFO` 或 `DEBUG` 级别打印。以下示例显示了如何使用`ConditionEvaluationReportLoggingListener`在自动配置测试中打印报告。

```java
@Test
public void autoConfigTest {
    ConditionEvaluationReportLoggingListener initializer = new ConditionEvaluationReportLoggingListener(
            LogLevel.INFO);
    ApplicationContextRunner contextRunner = new ApplicationContextRunner()
            .withInitializer(initializer).run((context) -> {
                    // Do something...
            });
}
```

##### 模拟 Web 上下文

如果您需要测试仅在 Servlet 或 Reactive Web 应用程序上下文中运行的自动配置，请分别使用`WebApplicationContextRunner`或`ReactiveWebApplicationContextRunner`。

##### 覆盖类路径

也可以测试在运行时不存在特定的类和/或程序包时发生的情况。Spring Boot 附带有一个 `FilteredClassLoader`，运行器可以轻松使用。在以下示例中，我们断言，如果不存在 `UserService`，则会自动禁用自动配置：

```java
@Test
void serviceIsIgnoredIfLibraryIsNotPresent() {
    this.contextRunner.withClassLoader(new FilteredClassLoader(UserService.class))
            .run((context) -> assertThat(context).doesNotHaveBean("userService"));
}
```