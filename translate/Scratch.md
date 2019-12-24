#### 8.2.7. 使用自定义注解

> 自定义注解和 AspectJ
>
> 该功能仅适用于基于代理的方法，但可以通过使用 AspectJ 进行一些额外的工作来启用。
>
> `spring-aspects` 模块仅为标准注解定义了一个方面。如果定义了自己的注解，则还需要为其定义一个方面。查看作为示例的 `AnnotationCacheAspect` 。

缓存抽象使您可以使用自己的注解来标识触发缓存填充或逐出的方法。作为模板机制，这非常方便，因为它消除了重复缓存注解声明的需求，如果指定了键或条件，或代码库中不允许外部导入（`org.springframework`），则这特别有用。与 [stereotype](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-stereotype-annotations) 注解的其余部分类似，您可以将 `@Cacheable`，`@CachePut`，`@CacheEvict` 和 `@CacheConfig` 用作 [元注解](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-meta-annotations)（即可以注释其他注解的注解）。在以下示例中，我们用自己的自定义注解替换了通用的 `@Cacheable` 声明：

```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.METHOD})
@Cacheable(cacheNames="books", key="#isbn")
public @interface SlowService {
}
```

在前面的示例中，我们定义了自己的 `SlowService` 注解，该注解本身以 `@Cacheable` 注解修饰。现在我们可以替换以下代码：

```java
@Cacheable(cacheNames="books", key="#isbn")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

以下示例显示了自定义注解，我们可以用其替换前面的代码：

```java
@SlowService
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

即使 `@SlowService` 不是 Spring 注解，容器也会在运行时自动获取其声明并理解其含义。请注意，如 [前文](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-annotation-enable) 所述，注解驱动的行为需要被启用。

