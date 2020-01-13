##### Spring WebFlux 自动配置

Spring Boot 为 Spring WebFlux 提供的自动配置可以很好地应用于大部分的应用。

自动配置在 Spring 默认基础上添加爱了以下特性：

- 为 `HttpMessageReader` 和 `HttpMessageWriter` 实例配置编解码器（在 [本文档后面](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-webflux-httpcodecs) 介绍）。
- 支持提供静态资源，包括对 WebJars 的支持（在 [本文档后面](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-static-content) 介绍）。

如果您想保留 Spring Boot WebFlux 功能并想要添加其他 [WebFlux配置](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#webflux-config)，您可以添加自己的类型为 `WebFluxConfigurer` 的 `@Configuration` 类，而不需要添加 `@EnableWebFlux` 。

如果您想完全控制 Spring WebFlux，则可以添加带有 `@EnableWebFlux` 注解的自己的 `@Configuration`。

##### 带有 HttpMessageReaders 和 HttpMessageWriters 的 HTTP 编解码器

Spring WebFlux 使用 `HttpMessageReader` 和 `HttpMessageWriter` 接口来转换 HTTP 请求和响应。通过查看类路径中可用的库，将它们配置为 `CodecConfigurer` 以具有合理的默认值。

Spring Boot 为编解码器 `spring.codec.*` 提供了专用的配置属性。它还通过使用 `CodecCustomizer` 实例来应用进一步的自定义。例如，将 `spring.jackson.*` 配置键应用于 Jackson 编解码器。

如果您需要添加或自定义编解码器，则可以创建自定义 `CodecCustomizer` 组件，如以下示例所示：

```java
import org.springframework.boot.web.codec.CodecCustomizer;

@Configuration(proxyBeanMethods = false)
public class MyConfiguration {

    @Bean
    public CodecCustomizer myCodecCustomizer() {
        return codecConfigurer -> {
            // ...
        };
    }

}
```

您还可以利用 [Boot的自定义JSON序列化器和反序列化器](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-json-components)。

 