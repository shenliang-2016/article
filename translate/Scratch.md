### 8.2. 基于注解的声明式缓存

对于缓存声明，Spring 缓存抽象提供了一系列 Java 注解：

- `@Cacheable`: 触发缓存填充。
- `@CacheEvict`: 触发缓存淘汰。
- `@CachePut`: 不影响方法调度情况下更新缓存。
- `@Caching`: 对应用于一个方法的多个缓存操作重新编组。
- `@CacheConfig`: 在类层面共享某些公用缓存相关的设置。

#### 8.2.1.  `@Cacheable` 注解

如名称所暗示的，你可以使用 `@Cacheable` 注解来标定可以被缓存的方法－也就是说，方法的结果可以被存储在缓存中，因此后续相同参数的方法调用就可以直接返回缓存中的结果，而不需要实际执行方法。最简单的形式中，注解声明之需要讲缓存名称与被注解的方法关联起来，如下面例子所示：

```java
@Cacheable("books")
public Book findBook(ISBN isbn) {...}
```

在前面的代码段中，`findBook` 方法与名为 `books` 的缓存相关联。每次调用该方法时，都会检查缓存以查看调用是否已经执行并且不必重复执行。尽管在大多数情况下，仅声明一个缓存，但注解可指定多个名称，以便使用多个缓存。在这种情况下，在执行方法之前检查每个缓存-如果命中了至少一个缓存，则返回关联的值。

> 即使未实际执行缓存的方法，所有其他不包含该值的缓存也会被更新。

下面的例子在 `findBook` 方法上使用 `@Cacheable` 注解：

```java
@Cacheable({"books", "isbns"})
public Book findBook(ISBN isbn) {...}
```

##### 默认 Key 生成

由于缓存本质上是键值存储，因此每次调用缓存方法都需要转换为适合缓存访问的键。缓存抽象使用基于以下算法的简单 `KeyGenerator`：

- 如果未提供任何参数，则返回 `SimpleKey.EMPTY`。

- 如果仅给出一个参数，则返回该实例。

- 如果给出了一个以上的参数，则返回包含所有参数的 `SimpleKey`。

只要参数具有自然键并实现有效的 `hashCode()` 和 `equals()` 方法，该方法就适用于大多数场景。如果不是这种情况，则需要更改策略。

为了提供不同的默认键生成器，你需要实现 `org.springframework.cache.interceptor.KeyGenerator` 接口。

> 随着 Spring 4.0 的发布，默认的键生成策略发生了变化。Spring 的早期版本使用了键生成策略，该策略对于多个关键参数仅考虑参数的 `hashCode()` 而不考虑 `equals()`。这可能会导致意外的键冲突（有关背景，请参见 [SPR-10237](https://jira.spring.io/browse/SPR-10237)）。新的 `SimpleKeyGenerator` 在这种情况下使用复合键。
>
> 如果您想继续使用以前的键生成策略，则可以配置已弃用的 `org.springframework.cache.interceptor.DefaultKeyGenerator` 类或创建基于哈希的自定义 `KeyGenerator` 实现。

