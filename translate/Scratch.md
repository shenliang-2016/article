### 8.3. JCache (JSR-107) 注解

从 4.1 版开始，Spring 的缓存抽象完全支持 JCache 标准注解：`@CacheResult`，`@CachePut`，`@CacheRemove` 和 `@CacheRemoveAll` 以及 `@CacheDefaults`，`@CacheKey` 和 `@CacheValue` 。您甚至可以在不将缓存存储迁移到 JSR-107 的情况下使用这些注解。内部实现使用 Spring 的缓存抽象，并提供符合规范的默认 `CacheResolver` 和 `KeyGenerator` 实现。换句话说，如果您已经在使用 Spring 的缓存抽象，则可以切换到这些标准注解，而无需更改缓存存储（或配置）。

#### 8.3.1. 特性综述

对于那些熟悉 Spring 缓存注解的人，下表描述了 Spring 注解与 JSR-107 对应体之间的主要区别：

| Spring                         | JSR-107           | Remark                                                       |
| :----------------------------- | :---------------- | :----------------------------------------------------------- |
| `@Cacheable`                   | `@CacheResult`    | 相当相似。`@CacheResult` 可以缓存特定的异常并强制执行该方法，而不管缓存的内容如何。 |
| `@CachePut`                    | `@CachePut`       | 当 Spring 使用方法调用的结果更新缓存时，JCache 要求将其作为参数传递给它，并使用 `@CacheValue` 注解。由于存在这种差异，JCache 允许在实际方法调用之前或之后更新缓存。 |
| `@CacheEvict`                  | `@CacheRemove`    | 相当相似。当方法调用导致异常时， `@CacheRemove` 支持条件驱逐。 |
| `@CacheEvict(allEntries=true)` | `@CacheRemoveAll` | 参考 `@CacheRemove`。                                        |
| `@CacheConfig`                 | `@CacheDefaults`  | 让您以类似的方式配置相同的概念。                             |

JCache 的概念是 `javax.cache.annotation.CacheResolver`，与 Spring 的 `CacheResolver` 接口相同，只是 JCache 仅支持单个缓存。默认情况下，一个简单的实现根据注解中声明的名称检索要使用的缓存。应该注意的是，如果注解中未指定缓存名称，则会自动生成一个默认值。有关更多信息，请参见 `@CacheResult#cacheName()` 的 javadoc。

`CacheResolver` 实例由 `CacheResolverFactory` 检索。可以为每个缓存操作自定义工厂，如以下示例所示：

```java
@CacheResult(cacheNames="books", cacheResolverFactory=MyCacheResolverFactory.class) 
public Book findBook(ISBN isbn)
```

> 对于所有引用的类，Spring 尝试查找具有给定类型的 bean。如果存在多个匹配项，则创建一个新实例，并可以使用常规 bean 生命周期回调，例如依赖项注入。

Key 是由 `javax.cache.annotation.CacheKeyGenerator` 生成的，其目的与 Spring 的 `KeyGenerator` 相同。默认情况下，所有方法参数都被考虑在内，除非至少一个参数用 `@CacheKey` 注解修饰。这类似于 Spring 的 [自定义 key 生成声明](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-annotations-cacheable-key) 。例如，以下是相同的操作，一个使用 Spring 的抽象，另一个使用 JCache：

```java
@Cacheable(cacheNames="books", key="#isbn")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)

@CacheResult(cacheName="books")
public Book findBook(@CacheKey ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

您也可以在操作上指定 `CacheKeyResolver`，类似于指定 `CacheResolverFactory` 的方法。

JCache 可以管理带注解的方法引发的异常。这样可以防止更新缓存，但是也可以将异常缓存为失败的指示，而不必再次调用该方法。假设如果 ISBN 的结构无效，则抛出 `InvalidIsbnNotFoundException`。这是一个永久性的失败（使用这样的参数无法检索任何书籍）。以下内容缓存了该异常，以便使用相同的无效 ISBN 进行的进一步调用直接引发该缓存的异常，而不是再次调用该方法：

```java
@CacheResult(cacheName="books", exceptionCacheName="failures"
            cachedExceptions = InvalidIsbnNotFoundException.class)
public Book findBook(ISBN isbn)
```

#### 8.3.2. 启用 JSR-107 支持

除了启用 Spring 的声明性注解支持外，您无需执行任何其他操作即可启用 JSR-107 支持。如果类路径中同时存在 JSR-107 API 和 `spring-context-support` 模块，则 `@EnableCaching` 和 `cache:annotation-driven` 元素都会自动启用 JCache 支持。

> 根据您的使用场景，选择基本上由您来做。您甚至可以通过在某些服务器上使用 JSR-107 API 并在其他服务器上使用 Spring 自己的注解来混合和匹配服务。但是，如果这些服务影响相同的缓存，则应使用一致且相同的 key 生成实现。

