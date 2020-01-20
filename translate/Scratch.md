### 4.12. 缓存

Spring 框架支持透明地向应用程序添加缓存。从本质上讲，抽象将缓存应用于方法，从而根据缓存中可用的信息减少执行次数。缓存逻辑是对应用透明的，不会对调用者造成任何干扰。只要通过 `@EnableCaching` 注解启用了缓存支持，Spring Boot 就会自动配置缓存基础架构。

> 参考 Spring 框架文档的 [relevant section](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#cache) 获取更多细节。

简而言之，将缓存添加到服务的操作就像将相关注解添加到其方法一样容易，如以下示例所示：

```java
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Component;

@Component
public class MathService {

    @Cacheable("piDecimals")
    public int computePiDecimal(int i) {
        // ...
    }

}
```

本示例说明了在潜在的代价高昂操作上使用缓存的方法。在调用 `computePiDecimal` 之前，抽象将在 `piDecimals` 缓存中查找与 `i` 参数匹配的条目。如果找到条目，则缓存中的内容会立即返回给调用方，并且不会调用该方法。否则，将调用该方法，并在返回值之前更新缓存。

> 您还可以透明地使用标准 JSR-107（JCache）注解（例如，`@CacheResult`）。但是，我们强烈建议您不要混合使用 Spring Cache 和 JCache 注解。

如果您不添加任何特定的缓存库，Spring Boot 会自动配置一个 [简单提供程序](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-simple) ，在内存中使用并发映射。需要缓存时（例如上例中的 `piDecimals`），此提供程序将为您创建它。实际上，不建议将简单的提供程序用于生产用途，但是它对于入门并确保您了解功能非常有用。确定要使用的缓存提供程序后，请确保阅读其文档，以了解如何配置应用程序使用的缓存。几乎所有提供程序都要求您显式配置在应用程序中使用的每个缓存。一些提供了一种方法来定制由 `spring.cache.cache-names` 属性定义的默认缓存。

> 也可以透明地 [更新](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#cache-annotations-put) 或 [淘汰](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#cache-annotations-evict) 来自缓存的数据。

