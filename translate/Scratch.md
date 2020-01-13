##### 错误处理

Spring Boot 提供了一个 WebExceptionHandler，以一种明智的方式处理所有错误。它在处理顺序中的位置紧靠 WebFlux 提供的处理程序之前，该处理程序被认为是最后一个。对于机器客户端，它将生成一个 JSON 响应，其中包含错误，HTTP 状态和异常消息的详细信息。对于浏览器客户端，有一个 "whitelabel” 错误处理程序，以 HTML 格式呈现相同的数据。您还可以提供自己的 HTML 模板来显示错误（请参见 [下一节](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-webflux-error-handling-custom-error-pages)）。

定制此功能的第一步通常涉及使用现有机制，但替换或增加错误内容。为此，您可以添加类型为 `ErrorAttributes` 的 bean。

要更改错误处理行为，可以实现 `ErrorWebExceptionHandler` 并注册该类型的 bean 定义。由于 `WebExceptionHandler` 的级别很低，因此 Spring Boot 还提供了一个便捷的 `AbstractErrorWebExceptionHandler`，可让您以 WebFlux 功能性的方式处理错误，如以下示例所示：

```java
public class CustomErrorWebExceptionHandler extends AbstractErrorWebExceptionHandler {

    // Define constructor here

    @Override
    protected RouterFunction<ServerResponse> getRoutingFunction(ErrorAttributes errorAttributes) {

        return RouterFunctions
                .route(aPredicate, aHandler)
                .andRoute(anotherPredicate, anotherHandler);
    }

}
```

为了获得更完整的视图，您还可以直接将 `DefaultErrorWebExceptionHandler` 子类化，并覆盖特定的方法。

###### 自定义错误页面

如果要显示给定状态代码的自定义 HTML 错误页面，则可以将文件添加到 `/error` 文件夹中。错误页面可以是静态 HTML（即添加到任何静态资源文件夹下），也可以使用模板构建。文件名应为确切的状态代码或系列掩码。

例如，要将 `404` 映射到静态 HTML 文件，您的文件夹结构如下：

```
src/
 +- main/
     +- java/
     |   + <source code>
     +- resources/
         +- public/
             +- error/
             |   +- 404.html
             +- <other public assets>
```

要使用 Moustache 模板映射所有 `5xx` 错误，您的文件夹结构如下：

```
src/
 +- main/
     +- java/
     |   + <source code>
     +- resources/
         +- templates/
             +- error/
             |   +- 5xx.mustache
             +- <other templates>
```

