### 1.14 注册 `LoadTimeWeaver`

Spring使用`LoadTimeWeaver`在类加载到Java虚拟机（JVM）时动态转换类。

要启用加载时编织，可以将`@EnableLoadTimeWeaving`添加到一个`@Configuration`类中，如以下示例所示：

```java
@Configuration
@EnableLoadTimeWeaving
public class AppConfig {
}
```

或者，对于XML配置，您可以使用`context:load-time-weaver`元素：

```xml
<beans>
    <context:load-time-weaver/>
</beans>
```

一旦为`ApplicationContext`配置，那个`ApplicationContext`中的任何bean都可以实现`LoadTimeWeaverAware`，从而接收对加载时编织器实例的引用。这与 [Spring的JPA支持](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/data-access.html#orm-jpa) 结合使用时特别有用。加载时编织可能是JPA类转换所必需的。有关更多详细信息，请参阅[`LocalContainerEntityManagerFactoryBean`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.html) 文档。有关AspectJ加载时编织的更多信息，请参阅[Spring Framework中使用AspectJ进行加载时编织](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-aj-ltw) 。