#### 5.4.5 引入

引入（在AspectJ中称为类型间声明）使切面能够声明被增强对象实现给定接口，并代表这些对象提供该接口的实现。

您可以使用`@DeclareParents`注解进行引入。此注解用于声明匹配类型具有新父类（给定名称名称）。例如，给定名为`UsageTracked`的接口和名为`DefaultUsageTracked`的接口的实现，以下切面声明服务接口的所有实现者也实现`UsageTracked`接口（例如，通过JMX公开统计信息）：

```java
@Aspect
public class UsageTracking {

    @DeclareParents(value="com.xzy.myapp.service.*+", defaultImpl=DefaultUsageTracked.class)
    public static UsageTracked mixin;

    @Before("com.xyz.myapp.SystemArchitecture.businessService() && this(usageTracked)")
    public void recordUsage(UsageTracked usageTracked) {
        usageTracked.incrementUseCount();
    }

}
```

要实现的接口由注解字段的类型确定。`@DeclareParents`注解的`value`属性是 AspectJ 类型模式。任何匹配类型的 bean 都实现`UsageTracked`接口。请注意，在前面示例的前置增强中，服务 bean 可以直接用作`UsageTracked`接口的实现。如果以编程方式访问 bean，您将编写以下内容：

```java
UsageTracked usageTracked = (UsageTracked) context.getBean("myService");
```