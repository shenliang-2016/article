### 8.4. 基于 XML 的声明式缓存

如果无法使用注解（可能是由于无法访问源代码或没有外部代码），则可以使用 XML 进行声明式缓存。因此，您可以从外部指定目标方法和缓存指令，而不是注解用于缓存的方法（类似于声明式事务管理 [advice](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-first-example) ）。上一节中的示例可以转换为以下示例：

```xml
<!-- the service we want to make cacheable -->
<bean id="bookService" class="x.y.service.DefaultBookService"/>

<!-- cache definitions -->
<cache:advice id="cacheAdvice" cache-manager="cacheManager">
    <cache:caching cache="books">
        <cache:cacheable method="findBook" key="#isbn"/>
        <cache:cache-evict method="loadBooks" all-entries="true"/>
    </cache:caching>
</cache:advice>

<!-- apply the cacheable behavior to all BookService interfaces -->
<aop:config>
    <aop:advisor advice-ref="cacheAdvice" pointcut="execution(* x.y.BookService.*(..))"/>
</aop:config>

<!-- cache manager definition omitted -->
```

在前面的配置中，`bookService` 被设置为可缓存的。要应用的缓存语义封装在 `cache:advice` 定义中，这将导致使用 `findBooks` 方法将数据放入缓存，并使用 `loadBooks` 方法将数据逐出。两种定义都针对 `books` 缓存。

`aop:config` 定义通过使用 AspectJ 切入点表达式将缓存建议应用于程序中的适当点（有关更多信息，请参见[使用 Spring 进行面向方面的编程](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) ）。在前面的示例中，考虑了 `BookService` 中的所有方法，并将缓存增强应用于它们。

声明式 XML 缓存支持所有基于注解的模型，因此在两者之间切换应该相当容易。此外，两者都可以在同一应用程序内使用。基于 XML 的方法不会涉及目标代码。但是，它本质上比较冗长。当处理具有用于缓存的重载方法的类时，确定正确的方法确实需要付出额外的努力，因为 `method` 参数不是很好的判别器。在这些情况下，您可以使用 AspectJ 切入点来挑选目标方法并应用适当的缓存功能。但是，通过 XML，更容易应用程序包或组或接口范围的缓存（同样由于 AspectJ 切入点的缘故）和创建类似模板的定义（如我们在前面的示例中那样，通过 `cache:definitions` 的 `cache` 属性）。

### 8.5. 配置缓存存储

缓存抽象提供了几个存储集成选项。要使用它们，您需要声明一个适当的 `CacheManager`（一个控制和管理 `Cache` 实例的实体，可用于检索这些实例以进行存储）。

#### 8.5.1. 基于 JDK `ConcurrentMap` 的缓存

The JDK-based `Cache` implementation resides under `org.springframework.cache.concurrent` package. It lets you use `ConcurrentHashMap` as a backing `Cache` store. The following example shows how to configure two caches:

```xml
<!-- simple cache manager -->
<bean id="cacheManager" class="org.springframework.cache.support.SimpleCacheManager">
    <property name="caches">
        <set>
            <bean class="org.springframework.cache.concurrent.ConcurrentMapCacheFactoryBean" p:name="default"/>
            <bean class="org.springframework.cache.concurrent.ConcurrentMapCacheFactoryBean" p:name="books"/>
        </set>
    </property>
</bean>
```

上面的代码片段使用 `SimpleCacheManager` 为两个嵌套的名为 `default` 和 `books` 的 `ConcurrentMapCache` 实例创建 `CacheManager`。请注意，名称是直接为每个缓存配置的。

由于缓存是由应用程序创建的，因此绑定到其生命周期，使其适合于基本应用场景，测试或简单的应用程序。缓存可以很好地扩展并且非常快，但是它不提供任何管理，持久性功能或驱逐契约。

#### 8.5.2. 基于 Ehcache 的缓存

> Ehcache 3.x 完全符合 JSR-107，并且不需要专用支持。

Ehcache 2.x 实现位于 `org.springframework.cache.ehcache` 包中。同样，要使用它，您需要声明适当的 `CacheManager`。以下示例显示了如何执行此操作：

```xml
<bean id="cacheManager"
        class="org.springframework.cache.ehcache.EhCacheCacheManager" p:cache-manager-ref="ehcache"/>

<!-- EhCache library setup -->
<bean id="ehcache"
        class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean" p:config-location="ehcache.xml"/>
```

这个设置在 Spring IoC 内部引导 ehcache 库（通过 `ehcache` bean），然后将其连接到专用的 `CacheManager` 实现中。注意，整个特定于 Ehcache 的配置是从 `ehcache.xml` 中读取的。

#### 8.5.3. Caffeine 缓存

Caffeine 是 Java 8 对 Guava 缓存的重写，其实现位于 `org.springframework.cache.caffeine` 包中，并提供对 Caffeine 多个功能的访问。

以下示例配置了一个 `CacheManager`，可根据需要创建缓存：

```xml
<bean id="cacheManager"
        class="org.springframework.cache.caffeine.CaffeineCacheManager"/>
```

您还可以显式提供要使用的缓存。在这种情况下，只有那些缓存被管理器认为是可用的。以下示例显示了如何执行此操作：

```xml
<bean id="cacheManager" class="org.springframework.cache.caffeine.CaffeineCacheManager">
    <property name="caches">
        <set>
            <value>default</value>
            <value>books</value>
        </set>
    </property>
</bean>
```

Caffeine `CacheManager` 也支持自定义 `Caffeine` 和 `CacheLoader`。更多信息，参见 [Caffeine 文档](https://github.com/ben-manes/caffeine/wiki) 。

#### 8.5.4. 基于 GemFire 的缓存

GemFire 是面向内存，磁盘支持，弹性可伸缩，连续可用，活动（具有内置的基于模式的订阅通知），全局复制的数据库，并提供功能齐全的边缘缓存。有关如何将 GemFire 用作 `CacheManager`（以及更多）的更多信息，请参见 [Spring Data GemFire 参考文档](https://docs.spring.io/spring-gemfire/docs/current/reference/html/ ) 。

#### 8.5.5. JSR-107 缓存

Spring 的缓存抽象也可以使用符合 JSR-107 的缓存。JCache 实现位于 `org.springframework.cache.jcache` 包中。

同样，要使用它，您需要声明适当的 `CacheManager`。以下示例显示了如何执行此操作：

```xml
<bean id="cacheManager"
        class="org.springframework.cache.jcache.JCacheCacheManager"
        p:cache-manager-ref="jCacheManager"/>

<!-- JSR-107 cache manager setup  -->
<bean id="jCacheManager" .../>
```

#### 8.5.6. 在没有后备存储的情况下处理缓存

有时，在切换环境或进行测试时，您可能具有缓存声明而未配置实际的后备缓存。由于这是无效的配置，因此在运行时会抛出异常，因为缓存基础设施无法找到合适的存储。在这种情况下，可以连接一个简单的伪缓存，该缓存不执行任何缓存操作，而不是删除缓存声明（这可能很乏味），也就是说，它强制每次执行缓存的方法。以下示例显示了如何执行此操作：

```xml
<bean id="cacheManager" class="org.springframework.cache.support.CompositeCacheManager">
    <property name="cacheManagers">
        <list>
            <ref bean="jdkCache"/>
            <ref bean="gemfireCache"/>
        </list>
    </property>
    <property name="fallbackToNoOpCache" value="true"/>
</bean>
```

前面的 `CompositeCacheManager` 链接了多个 `CacheManager` 实例，并通过 `fallbackToNoOpCache` 标志为未配置的缓存管理器处理的所有定义添加无操作缓存。也就是说，在 `jdkCache` 或 `gemfireCache`（在示例中之前配置）中都找不到的每个缓存定义都由无操作缓存处理，该缓存不存储任何信息，导致每次执行目标方法。

### 8.6. 插入不同的后端缓存

显然，有很多缓存产品可以用作后备存储。要插入它们，您需要提供一个 `CacheManager` 和一个 `Cache` 实现，因为不幸的是，没有可用的标准可供我们使用。这听起来可能比实际要难，因为在实践中，这些类通常是简单的 [adapters](https://en.wikipedia.org/wiki/Adapter_pattern) ，它们将缓存抽象框架映射到存储 API 的顶部， 就像 `ehcache` 类一样。大多数 `CacheManager` 类都可以使用 `org.springframework.cache.support` 包中的类（例如 `AbstractCacheManager`，它负责样板代码，仅保留实际的映射）。我们希望，及时提供与 Spring 集成的库可以弥补这一小小的配置空白。

### 8.7. 如何设置 TTL / TTI /驱逐策略/ XXX 功能？

直接通过您的缓存提供程序。缓存抽象是一种抽象，而不是缓存实现。您使用的解决方案可能支持其他解决方案不支持的各种数据策略和不同的拓扑（例如，JDK `ConcurrentHashMap` －暴露在缓存抽象中将是无用的，因为没有后备支持）。此类功能应通过后备缓存（配置时）或通过其本地 API 直接控制。

