#### 8.2.6. 启用缓存注解

重要的是要注意，仅仅声明缓存注解不会自动触发其动作－就像 Spring 中的许多事情一样，必须声明性地启用该功能（这意味着如果您怀疑缓存是罪魁祸首，则可以通过删除仅一个配置行来禁用它，而不是代码中的所有注解）。

要启用缓存注解，请将注解 `@EnableCaching` 添加到您的 `@Configuration` 类之一：

```java
@Configuration
@EnableCaching
public class AppConfig {
}
```

另外，对于 XML 配置，可以使用 `cache:annotation-driven` 元素：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:cache="http://www.springframework.org/schema/cache"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/cache https://www.springframework.org/schema/cache/spring-cache.xsd">

        <cache:annotation-driven/>
</beans>
```

通过 `cache:annotation-driven` 元素和 `@EnableCaching` 注解，您都可以指定各种选项，这些选项影响通过 AOP 将缓存行为添加到应用程序的方式。该配置与 [`@Transactional`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-annotation-driven-settings) 类似。

> 处理缓存注解的默认增强模式是 `proxy`，它仅允许通过代理来拦截调用。同一类内的本地调用无法以这种方式被拦截。对于更高级的拦截模式，请考虑结合编译时或加载时编织切换到 `aspectj` 模式。

> 有关实现 `CachingConfigurer` 需要的高级自定义（使用 Java 配置）的更多细节，参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) 。

| XML Attribute        | Annotation Attribute                                         | Default                                                      | Description                                                  |
| :------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `cache-manager`      | N/A (see the [`CachingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) javadoc) | `cacheManager`                                               | 要使用的缓存管理器的名称。默认的 `CacheResolver` 是在后台使用此缓存管理器初始化的（如果未设置，则初始化为 ` cacheManager`）。为了更精细地管理缓存粒度，请考虑设置 `cache-resolver` 属性。 |
| `cache-resolver`     | N/A (see the [`CachingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) javadoc) | A `SimpleCacheResolver` using the configured `cacheManager`. | 用来解析后备缓存的 `CacheResolver` 的 bean 名称。此属性不是必需的，仅需指定为 `cache-manager` 属性的替代方法。 |
| `key-generator`      | N/A (see the [`CachingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) javadoc) | `SimpleKeyGenerator`                                         | 要使用的定制 key 生成器的名称。                              |
| `error-handler`      | N/A (see the [`CachingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) javadoc) | `SimpleCacheErrorHandler`                                    | 要使用的自定义缓存错误处理程序的名称。默认情况下，在与缓存相关的操作期间抛出的所有异常都将返回给客户端。 |
| `mode`               | `mode`                                                       | `proxy`                                                      | 默认模式（`proxy`）使用 Spring 的 AOP 框架处理带注解的 bean（要遵循的代理语义，如前所述，仅适用于通过代理传入的方法调用）。相反，替代模式（`aspectj`）使用 Spring 的 AspectJ 缓存切面来编织受影响的类，修改目标类字节码以应用于任何类型的方法调用。AspectJ 编织需要在类路径中启用 `spring-aspects.jar`，并启用加载时编织（或编译时编织）。（有关如何操作的详细信息，请参见 [Spring配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-aj-ltw-spring) 了解如何设置加载时编织。） |
| `proxy-target-class` | `proxyTargetClass`                                           | `false`                                                      | 仅适用于代理模式。控制为使用 `@Cacheable` 或 `@CacheEvict`  注解修饰的类创建哪种类型的缓存代理。如果将 `proxy-target-class` 属性设置为 `true` ，则会创建基于类的代理。如果 `proxy-target-class` 为 `false` 或省略该属性，则创建基于标准 JDK 接口的代理。 （有关不同代理类型的详细检查，请参阅 [代理机制](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-proxying) ） |
| `order`              | `order`                                                      | Ordered.LOWEST_PRECEDENCE                                    | 定义应用于用 `@Cacheable` 或 `@CacheEvict` 注解修释的 bean 的缓存增强的顺序。（有关 AOP 增强排序有关的规则的更多信息，请参阅 [Advice Ordering](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop -ataspectj-advice-ordering) 。没有指定的顺序意味着 AOP 子系统确定增强的顺序。 |

> `<cache：annotation-driven />` 仅在定义了它的相同应用程序上下文中的 bean 上查找 `@Cacheable/@CachePut/@CacheEvict/@Caching`。这意味着，如果将 `<cache:annotation-driven/>` 放在 `WebApplicationContext` 中以作为 `DispatcherServlet`，它将仅在控制器中检查 bean，而不在服务中进行检查。有关更多信息，请参见 [MVC部分](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-servlet) 。

> 方法可见性和缓存注解
>
> 使用代理时，应仅将缓存注解应用于具有公共可见性的方法。如果使用这些注解对受保护的，私有的或程序包可见的方法进行修饰，则不会引发错误，但是带注解的方法不会显示已配置的缓存设置。如果您需要注解非公共方法，请考虑使用 AspectJ（请参阅本节的其余部分），因为它会更改字节码本身。

> Spring 建议您仅使用 `@Cache*` 注解对具体类（以及具体类的方法）进行修饰，而不是对接口进行修饰。您当然可以在接口（或接口方法）上放置 `@Cache*` 注解，但这仅在您使用基于接口的代理时才可以使用。Java 注解不是从接口继承的事实意味着，如果您使用基于类的代理（`proxy-target-class="true"`）或基于编织的方面（`mode="aspectj"`），则代理和编织基础结构无法识别缓存设置，并且该对象也不会包装在缓存代理中。

> 在代理模式（默认）下，仅拦截通过代理传入的外部方法调用。这意味着即使调用的方法标记有 `@Cacheable`，自调用（实际上是目标对象中的方法调用目标对象的另一种方法）也不会导致运行时实际缓存。在这种情况下，请考虑使用 `aspectj` 模式。另外，必须完全初始化代理以提供预期的行为，因此您不应在初始化代码（即 `@PostConstruct`）中依赖此功能。

