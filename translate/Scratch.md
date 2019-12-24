##### 同步缓存

在多线程环境中，某些操作可能被使用相同的参数并发调用（典型地在启动阶段）。默认地，缓存抽象不会锁定任何东西，同一个值可能被计算很多次，这就与缓存的目标背道而驰。

对这些特殊场景，你可以使用 `sync` 属性来构建底层缓存提供者来锁定缓存数据实体，当同一个值被重复计算时。作为结果，只有一个线程忙于计算需要缓存的值，同时其他线程都会阻塞到缓存中的该数据实体被更新。下面的例子展示了如何使用 `sync` 属性：

```java
@Cacheable(cacheNames="foos", sync=true) 
public Foo executeExpensiveOperation(String id) {...}
```

> 这是一个可选特性，你喜欢的缓存类库可能不支持。核心框架提供的所有的 `CacheManager` 实现都支持该特性。参考你的缓存提供者文档获取更多细节。

##### 条件缓存

有时候，一个方法并不是始终都适合被缓存（比如，可能依赖于给定的参数）。缓存注解通过 `condition` 参数支持该功能，携带一个 `SpEL` 表达式，该表达式可以被解析为 `true` 或者 `false` 。如果是 `true` ，该方法将被缓存。否者，该方法的行为就会如同没有被缓存一样（也就是说，该方法每次都会执行，无论结果是否被缓存或者使用何种参数）。例如，下面的方法只有当 `name` 参数长度小于 32 时才会被缓存：

```java
@Cacheable(cacheNames="book", condition="#name.length() < 32") 
public Book findBook(String name)
```

除了 `condition` 参数，你还可以使用 `unless` 参数来阻止值被添加到缓存中。与 `condition` 不同，`unless` 表达式在方法被调用之后才会被解析。扩展上面的例子，可能我们只想要缓存平装书，如下面例子所示：

```java
@Cacheable(cacheNames="book", condition="#name.length() < 32", unless="#result.hardback") 
public Book findBook(String name)
```

缓存抽象支持 `java.util.Optional` ，如果它的内容存在，就会作为被缓存的值。`#result` 始终指向业务实体，而不是任何支持的包装器，因此，上面的例子可以写成：

```java
@Cacheable(cacheNames="book", condition="#name.length() < 32", unless="#result?.hardback")
public Optional<Book> findBook(String name)
```

注意，`result` 仍然指向 `Book` 而不是 `Optional` 。因为它可能是 `null` ，我们应该使用安全的导航操作。

##### 可用的缓存 SpEL 解析上下文

每个 `SpEL` 表达式都是针对专门的 [`上下文`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions-language-ref) 解析。除了内建参数，框架提供了专门的缓存相关的元数据，比如参数名称。下面的表格描述了可用于上下文的元素，你可以使用它们进行关键或者条件计算：

| Name          | Location           | Description                                                  | Example                                                      |
| :------------ | :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `methodName`  | Root object        | 被调用方法的名称                                             | `#root.methodName`                                           |
| `method`      | Root object        | 被调用的方法                                                 | `#root.method.name`                                          |
| `target`      | Root object        | 被调用的目标对象                                             | `#root.target`                                               |
| `targetClass` | Root object        | 被调用的目标的类型                                           | `#root.targetClass`                                          |
| `args`        | Root object        | 用于调用目标的参数（作为数组）                               | `#root.args[0]`                                              |
| `caches`      | Root object        | 执行当前方法的缓存的集合                                     | `#root.caches[0].name`                                       |
| Argument name | Evaluation context | 任何方法参数的名称。如果名称不可用（可能是由于没有调试信息），则参数名称也可以在 `#a <#arg>` 下使用，其中 `#arg` 代表参数索引（从 `0` 开始）。 | `#iban` or `#a0` (you can also use `#p0` or `#p<#arg>` notation as an alias). |
| `result`      | Evaluation context | 方法调用的结果（要缓存的值）。仅在 `unless` 表达式，`cache put` 表达式（用于计算 `key`）或`cache evict`表达式（`beforeInvocation` 为 `false` 时）中可用。对于支持的包装器（例如 `Optional`），`#result` 是指实际对象，而不是包装器。 | `#result`                                                    |

