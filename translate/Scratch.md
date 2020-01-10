### 4.7. 开发 Web 应用

Spring Boot 非常适合于 Web 应用程序开发。您可以使用嵌入式 Tomcat，Jetty，Undertow 或 Netty 创建独立的 HTTP 服务器。大多数网络应用程序都使用 `spring-boot-starter-web` 模块来快速启动和运行。您也可以选择使用 `spring-boot-starter-webflux` 模块构建反应式 Web 应用程序。

如果尚未开发 Spring Boot Web 应用程序，则可以遵循 *入门*部分中的 ”Hello World！"示例。

#### 4.7.1. Spring Web MVC 框架

[Spring Web MVC framework](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc) (通常简称为 “Spring MVC”) 是一个完整的 MVC web 框架。Spring MVC 允许您创建特殊的 `@Controller` 或 `@RestController` bean 来处理传入的 HTTP 请求。控制器中的方法通过使用 `@RequestMapping` 注解映射到 HTTP。

下面的代码展示了一个返回 JSON 数据的典型 `@RestController` ：

```java
@RestController
@RequestMapping(value="/users")
public class MyRestController {

    @RequestMapping(value="/{user}", method=RequestMethod.GET)
    public User getUser(@PathVariable Long user) {
        // ...
    }

    @RequestMapping(value="/{user}/customers", method=RequestMethod.GET)
    List<Customer> getUserCustomers(@PathVariable Long user) {
        // ...
    }

    @RequestMapping(value="/{user}", method=RequestMethod.DELETE)
    public User deleteUser(@PathVariable Long user) {
        // ...
    }

}
```

Spring MVC 是 Spring 框架核心的一部分，更多细节参考 [reference documentation](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc)。还有一些 Spring MVC 文档位于 [spring.io/guides](https://spring.io/guides)。

##### Spring MVC 自动配置

Spring Boot 为 Spring MVC 提供了自动配置，可与大多数应用程序完美配合。

自动配置在 Spring 的默认设置之上添加了以下功能：

- 包含 `ContentNegotiatingViewResolver` 和 `BeanNameViewResolver` bean。

- 支持提供静态资源，包括对 WebJars 的支持（在[本文档后面介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-static-content)）。

- 自动转换 `Converter`，`GenericConverter` 和 `Formatter` bean。

- 支持 `HttpMessageConverters`（在 [本文档后面介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-message-converters)）。

- 自动注册 `MessageCodesResolver`（在 [本文档后面介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-message-codes)）。

- 静态的 `index.html` 支持。

- 自定义 `Favicon` 支持（在 [文档后续介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-favicon)）。

- 自动使用 `ConfigurableWebBindingInitializer` bean（在 [本文档后面介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-web-binding-initializer)）。

如果您想保留 Spring Boot MVC 功能并想要添加其他 [MVC配置](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc)（拦截器，格式化程序，视图控制器和其他功能），则可以添加自己的类型 `@WebConfiguration` 的类，类型为 `WebMvcConfigurer`，但不包含 `@EnableWebMvc`。如果您希望提供 `RequestMappingHandlerMapping`，`RequestMappingHandlerAdapter` 或 `ExceptionHandlerExceptionResolver` 的自定义实例，则可以声明 `WebMvcRegistrationsAdapter` 实例以提供此类组件。

如果您想完全控制 Spring MVC，则可以添加带有 `@EnableWebMvc` 注解的自己的 `@Configuration`。

##### HttpMessageConverters

Spring MVC uses the `HttpMessageConverter` interface to convert HTTP requests and responses. Sensible defaults are included out of the box. For example, objects can be automatically converted to JSON (by using the Jackson library) or XML (by using the Jackson XML extension, if available, or by using JAXB if the Jackson XML extension is not available). By default, strings are encoded in `UTF-8`.

If you need to add or customize converters, you can use Spring Boot’s `HttpMessageConverters` class, as shown in the following listing:

```java
import org.springframework.boot.autoconfigure.http.HttpMessageConverters;
import org.springframework.context.annotation.*;
import org.springframework.http.converter.*;

@Configuration(proxyBeanMethods = false)
public class MyConfiguration {

    @Bean
    public HttpMessageConverters customConverters() {
        HttpMessageConverter<?> additional = ...
        HttpMessageConverter<?> another = ...
        return new HttpMessageConverters(additional, another);
    }

}
```

Any `HttpMessageConverter` bean that is present in the context is added to the list of converters. You can also override default converters in the same way.

##### Custom JSON Serializers and Deserializers

If you use Jackson to serialize and deserialize JSON data, you might want to write your own `JsonSerializer` and `JsonDeserializer` classes. Custom serializers are usually [registered with Jackson through a module](https://github.com/FasterXML/jackson-docs/wiki/JacksonHowToCustomSerializers), but Spring Boot provides an alternative `@JsonComponent` annotation that makes it easier to directly register Spring Beans.

You can use the `@JsonComponent` annotation directly on `JsonSerializer`, `JsonDeserializer` or `KeyDeserializer` implementations. You can also use it on classes that contain serializers/deserializers as inner classes, as shown in the following example:

```java
import java.io.*;
import com.fasterxml.jackson.core.*;
import com.fasterxml.jackson.databind.*;
import org.springframework.boot.jackson.*;

@JsonComponent
public class Example {

    public static class Serializer extends JsonSerializer<SomeObject> {
        // ...
    }

    public static class Deserializer extends JsonDeserializer<SomeObject> {
        // ...
    }

}
```

All `@JsonComponent` beans in the `ApplicationContext` are automatically registered with Jackson. Because `@JsonComponent` is meta-annotated with `@Component`, the usual component-scanning rules apply.

Spring Boot also provides [`JsonObjectSerializer`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jackson/JsonObjectSerializer.java) and [`JsonObjectDeserializer`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jackson/JsonObjectDeserializer.java) base classes that provide useful alternatives to the standard Jackson versions when serializing objects. See [`JsonObjectSerializer`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/jackson/JsonObjectSerializer.html) and [`JsonObjectDeserializer`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/jackson/JsonObjectDeserializer.html) in the Javadoc for details.

##### MessageCodesResolver

Spring MVC has a strategy for generating error codes for rendering error messages from binding errors: `MessageCodesResolver`. If you set the `spring.mvc.message-codes-resolver-format` property `PREFIX_ERROR_CODE` or `POSTFIX_ERROR_CODE`, Spring Boot creates one for you (see the enumeration in [`DefaultMessageCodesResolver.Format`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/validation/DefaultMessageCodesResolver.Format.html)).