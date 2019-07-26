#### 5.4.1 启用 @AspectJ 支持

为了在 Spring 配置中使用 @AspectJ 切面，你需要启用 Spring 支持以配置 Spring AOP 基于 @AspectJ 切面并自动代理 beans 基于它们是否被那些切面增强。通过自动代理，我们的意思是，如果 Spring 确定一个 bean 被一个或者多个切面增强，它就会自动为该 bean 产生一个代理来拦截方法调用并确保增强按需执行。

可以使用XML或Java样式配置启用@AspectJ支持。在任何一种情况下，您还需要确保AspectJ的`aspectjweaver.jar`库位于应用程序的类路径中（版本1.8或更高版本）。该库位于AspectJ发行版的`lib`目录或 Maven Central 存储库中。

##### 通过 Java 配置启用 @AspectJ 支持

要使用Java`@Configuration`启用@AspectJ支持，请添加`@EnableAspectJAutoProxy`注解，如以下示例所示：

```java
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {

}
```

##### 通过 XML 配置启用 @AspectJ 支持

要使用基于XML的配置启用@AspectJ支持，请使用`aop:aspectj-autoproxy`元素，如以下示例所示：

```xml
<aop:aspectj-autoproxy/>
```

这假设您使用 [基于XML模式的配置](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#xsd-schemas) 中描述的模式支持。有关如何导入 `aop`命名空间中标签的信息，请参阅 [the AOP schema](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#xsd-schemas-aop) 。

#### 5.4.2 声明切面

