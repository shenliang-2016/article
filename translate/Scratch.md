##### 自定义 Key 生成声明

由于缓存是通用的，因此目标方法很可能具有各种签名，这些签名无法轻易映射到缓存结构顶部。当目标方法具有多个参数时，只有其中一些参数适合缓存（而其余参数仅由方法逻辑使用），这往往会变得很明显。考虑以下示例：

```java
@Cacheable("books")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

乍一看，虽然两个 `boolean` 参数会影响书的查找方式，但它们对缓存没有用处。此外，如果两者中只有一个重要而另一个不重要怎么办？

对于这种情况，可以通过`@Cacheable` 注解指定如何通过其 `key` 属性生成密钥。 您可以使用 [SpEL](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions) 选择感兴趣的参数（或其嵌套属性） ），执行操作甚至调用任意方法，而无需编写任何代码或实现任何接口。相对于 [默认生成器](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-annotations-cacheable-default-key) ，更推荐这种方式。因为随着代码库的增长，方法的签名趋向于完全不同。虽然默认策略可能适用于某些方法，但很少适用于所有方法。

下面的例子展示了各种 SpEL 声明（如果你还不熟悉 SpEL ，参考 [Spring Expression Language](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions)）：

```java
@Cacheable(cacheNames="books", key="#isbn")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)

@Cacheable(cacheNames="books", key="#isbn.rawNumber")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)

@Cacheable(cacheNames="books", key="T(someType).hash(#isbn)")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

前面的代码片段显示了选择某个参数，其属性之一甚至是任意（静态）方法是多么简单。

如果负责生成键的算法过于具体或需要共享，则可以在操作上定义一个自定义的 `keyGenerator`。为此，请指定要使用的 `KeyGenerator` bean实现的名称，如以下示例所示：

```java
@Cacheable(cacheNames="books", keyGenerator="myKeyGenerator")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

> `key` 和 `keyGenerator` 参数是互斥的，同时指定这两个参数的操作将导致异常。

##### 默认缓存解析

缓存抽象使用一个简单的 `CacheResolver`，通过使用配置的 `CacheManager` 来检索在操作级别定义的缓存。

要提供其他默认的缓存解析器，您需要实现 `org.springframework.cache.interceptor.CacheResolver` 接口。

##### 自定义缓存解析

默认的缓存解析非常适合与单个 `CacheManager` 一起使用且对复杂的缓存解析没有要求的应用程序。

对于使用多个缓存管理器的应用程序，可以将 `cacheManager` 设置为用于每个操作，如以下示例所示：

```java
@Cacheable(cacheNames="books", cacheManager="anotherCacheManager") 
public Book findBook(ISBN isbn) {...}
```

您还可以完全按照替换 [密钥生成](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-annotations-cacheable-key) 的方式完全替换 `CacheResolver`。每个缓存操作都需要解析，让实现实际上可以根据运行时参数来解析要使用的缓存。以下示例显示了如何指定 `CacheResolver`：

```java
@Cacheable(cacheResolver="runtimeCacheResolver") 
public Book findBook(ISBN isbn) {...}
```

> 从Spring 4.1开始，缓存注解的 `value` 属性不再是必需的，因为 `CacheResolver` 可以提供该特定信息，而与注解的内容无关。
>
> 与 `key` 和 `keyGenerator` 类似，`cacheManager` 和 `cacheResolver` 参数是互斥的，并且同时指定这两个参数的操作将导致异常。因为自定义 `CacheManager` 被 `CacheResolver` 实现忽略。这可能不是您所期望的。

