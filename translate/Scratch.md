### 4.6. JSON

Spring Boot 提供了三种 JSON 映射类库支持：

- Gson
- Jackson
- JSON-B

Jackson 是首选默认的类库。

#### 4.6.1. Jackson

提供了 Jackson 的自动配置功能，并且 Jackson 是 `spring-boot-starter-json` 的一部分。当 Jackson 在类路径上时，将自动配置 `ObjectMapper` bean。提供了几个配置属性用于 [自定义 `ObjectMapper` 的配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-customize-the-jackson-objectmapper)。

#### 4.6.2. Gson

提供了 Gson 的自动配置。当 Gson 在类路径上时，将自动配置 `Gson` bean。提供了几个 `spring.gson.*` 配置属性来定制配置。为了获得更多控制权，可以使用一个或多个 `GsonBuilderCustomizer` bean。

#### 4.6.3. JSON-B

提供了 JSON-B 的自动配置。当 JSON-B API 和实现位于类路径上时，将自动配置 `Jsonb` bean。首选的 JSON-B 实现是提供依赖管理的 Apache Johnzon。

