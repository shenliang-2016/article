#### 8.2.2.  `@CachePut` 注解

当需要在不影响方法执行的情况下更新缓存时，可以使用 `@CachePut` 注解。也就是说，该方法总是被执行，其结果被放入缓存（根据 `@CachePut` 选项）。它支持与 `@Cacheable` 相同的选项，应该用于缓存填充，而不是方法流优化。以下示例使用了 `@CachePut` 注解：

```java
@CachePut(cacheNames="book", key="#isbn")
public Book updateBook(ISBN isbn, BookDescriptor descriptor)
```

> 强烈建议不要在同一方法上使用 `@CachePut` 和 `@Cacheable` 注解，因为它们的行为不同。后者导致通过使用缓存跳过方法执行，而前者则强制执行以便执行缓存更新。这会导致意外的行为，并且，除了特定的极端情况（例如具有互斥条件的注解）外，应避免此类声明。还要注意，这样的条件不应依赖于结果对象（即 `#result` 变量），因为这些条件已预先进行验证以确认排除。

#### 8.2.3.  `@CacheEvict` 注解

缓存抽象不仅允许缓存存储的填充，还允许逐出。此过程对于从缓存中删除陈旧或未使用的数据很有用。与 `@Cacheable` 相反，`@CacheEvict` 区分执行高速缓存逐出的方法（即，用作触发从高速缓存中删除数据的触发器的方法）。与它的同级类似，`@CacheEvict` 需要指定一个或多个受操作影响的缓存，允许自定义缓存和键解析或条件，并指定一个额外的参数（`allEntries`）来指示是否 需要执行缓存范围内的逐出，而不仅仅是条目逐出（基于键）。以下示例将所有 `books` 缓存中的条目逐出：

```java
@CacheEvict(cacheNames="books", allEntries=true) 
public void loadBooks(InputStream batch)
```

当需要清除整个缓存区域时，此选项非常有用。如前面的示例所示，而不是逐出每个条目（这会花费很长时间，因为效率很低），而是一次操作删除所有条目。请注意，该框架会忽略此方案中指定的任何键，因为它不适用（整个高速缓存被驱逐，而不仅仅是一个条目）。

您还可以通过使用 `beforeInvocation` 属性指示驱逐应该发生在方法执行之后还是在方法执行之前（默认是方法执行之后）。前者提供与其余注解相同的语义：方法成功完成后，将对缓存执行操作（在这种情况下为逐出）。 如果该方法未执行（可能已被缓存）或引发了异常，则不会发生驱逐。后者（`beforeInvocation=true`）导致逐出总是在调用该方法之前发生。在不需要将逐出与方法结果联系在一起的情况下，这很有用。

注意，`void` 方法可以与 `@CacheEvict` 一起使用－因为这些方法充当触发器，所以返回值将被忽略（因为它们不与缓存交互）。这不同于 `@Cacheable` 的情况，它会向缓存中添加或更新数据，因此需要结果。

#### 8.2.4.  `@Caching` 注解

有时，需要指定相同类型的多个注解（例如，`@CacheEvict` 或 `@CachePut`），例如，因为不同缓存之间的条件或键表达式不同。`@Caching` 可以在同一方法上使用多个嵌套的 `@Cacheable`，`@CachePut` 和 `@CacheEvict` 注解。以下示例使用了两个 `@CacheEvict` 注解：

```java
@Caching(evict = { @CacheEvict("primary"), @CacheEvict(cacheNames="secondary", key="#p0") })
public Book importBooks(String deposit, Date date)
```

#### 8.2.5.  `@CacheConfig` 注解

到目前为止，我们已经看到缓存操作提供了许多自定义选项，并且您可以为每个操作设置这些选项。但是，如果某些自定义选项适用于该类的所有操作，则配置它们可能很繁琐。 、例如，指定用于类的每个高速缓存操作的高速缓存的名称可以由单个类级定义代替。这就是 `@CacheConfig` 起作用的地方。以下示例使用 `@CacheConfig` 设置缓存的名称：

```java
@CacheConfig("books") 
public class BookRepositoryImpl implements BookRepository {

    @Cacheable
    public Book findBook(ISBN isbn) {...}
}
```

`@CacheConfig` 是一个类级别的注解，它允许共享缓存名称，自定义的 `KeyGenerator`，自定义的 `CacheManager` 和自定义的 `CacheResolver`。将此注解放在类上不会打开任何缓存操作。

操作级别的自定义始终会覆盖在 `@CacheConfig` 上的设置。因此，这为每个高速缓存操作提供了三个定制级别：

- 全局配置，可用于 `CacheManager`，`KeyGenerator`。

- 在类级别，使用 `@CacheConfig`。

- 在操作级别。

