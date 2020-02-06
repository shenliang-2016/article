### 4.19. Hazelcast
如果 [Hazelcast](https://hazelcast.com/) 位于类路径上，并且找到了合适的配置，则 Spring Boot 会自动配置一个 `HazelcastInstance`，您可以将其注入应用程序中。

如果定义 `com.hazelcast.config.Config` bean，Spring Boot 会使用它。如果您的配置定义了一个实例名称，Spring Boot 会尝试查找现有实例，而不是创建一个新实例。

您还可以指定通过配置使用的 Hazelcast 配置文件，如以下示例所示：
````
spring.hazelcast.config=classpath:config/my-hazelcast.xml
````
否则，Spring Boot 会尝试从默认位置查找 Hazelcast 配置：工作目录中或类路径根目录中的 `hazelcast.xml`，或相同位置中的 `.yaml` 副本。我们还将检查 `hazelcast.config` 系统属性是否已设置。有关更多详细信息，请参见 [Hazelcast文档](https://docs.hazelcast.org/docs/latest/manual/html-single/)。

如果在类路径中存在 `hazelcast-client`，Spring Boot 首先尝试通过检查以下配置选项来创建客户端：
* `com.hazelcast.client.config.ClientConfig` bean的存在。

* 由 `spring.hazelcast.config` 属性定义的配置文件。

* `hazelcast.client.config` 系统属性的存在。

* 工作目录中或类路径根目录中的 `hazelcast-client.xml`。

* 工作目录中或类路径根目录中的 `hazelcast-client.yaml`。

> Spring Boot 还具有 [对 Hazelcast 的显式缓存支持](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#boot-features-caching-provider-hazelcast)。 如果启用了缓存，则 `HazelcastInstance` 将自动包装在 `CacheManager` 实现中。

