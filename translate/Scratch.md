##### 错误处理

默认情况下，Spring Boot 提供一个 `/error` 映射，以一种明智的方式处理所有错误，并且在 servlet 容器中被注册为“全局”错误页面。对于机器客户端，它将生成一个 JSON 响应，其中包含错误，HTTP 状态和异常消息的详细信息。对于浏览器客户端，有一个“whitelabel”错误视图以 HTML 格式呈现相同的数据（要对其进行自定义，请添加一个可解析为 `error` 的 `view`）。要完全替换默认行为，您可以实现 `ErrorController` 并注册该类型的 bean 定义，或者添加类型为 `ErrorAttributes` 的 bean 以使用现有机制但替换其内容。

> `BasicErrorController` 可用作自定义 `ErrorController` 的基类。如果您要为新的内容类型添加处理程序（默认是专门处理 `text/html` 并为其他所有内容提供后备功能），则此功能特别有用。为此，扩展 `BasicErrorController`，添加一个具有 `produces` 属性的 `@RequestMapping` 注解的公共方法，并创建一个新类型的 bean。

您还可以定义一个带有 `@ControllerAdvice` 注解的类，以自定义 JSON 文档以针对特定的控制器和/或异常类型返回，如以下示例所示：

```java
@ControllerAdvice(basePackageClasses = AcmeController.class)
public class AcmeControllerAdvice extends ResponseEntityExceptionHandler {

    @ExceptionHandler(YourException.class)
    @ResponseBody
    ResponseEntity<?> handleControllerException(HttpServletRequest request, Throwable ex) {
        HttpStatus status = getStatus(request);
        return new ResponseEntity<>(new CustomErrorType(status.value(), ex.getMessage()), status);
    }

    private HttpStatus getStatus(HttpServletRequest request) {
        Integer statusCode = (Integer) request.getAttribute("javax.servlet.error.status_code");
        if (statusCode == null) {
            return HttpStatus.INTERNAL_SERVER_ERROR;
        }
        return HttpStatus.valueOf(statusCode);
    }

}
```

在前面的示例中，如果在与 `AcmeController` 相同的包中定义的控制器抛出了 `YourException`，则使用 `CustomErrorType` POJO 的 JSON 表示形式而不是 `ErrorAttributes` 表示形式。

###### 自定义错误页面

如果要显示给定状态代码的自定义 HTML 错误页面，则可以将文件添加到 `/error` 文件夹中。错误页面可以是静态 HTML（即添加到任何静态资源文件夹下），也可以使用模板来构建。文件名应为确切的状态代码或系列掩码。

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

要使用 `FreeMarker` 模板映射所有 `5xx` 错误，您的文件夹结构如下：

```
src/
 +- main/
     +- java/
     |   + <source code>
     +- resources/
         +- templates/
             +- error/
             |   +- 5xx.ftlh
             +- <other templates>
```

对于更复杂的映射，还可以添加实现 `ErrorViewResolver` 接口的 bean，如以下示例所示：

```java
public class MyErrorViewResolver implements ErrorViewResolver {

    @Override
    public ModelAndView resolveErrorView(HttpServletRequest request,
            HttpStatus status, Map<String, Object> model) {
        // Use the request or status to optionally return a ModelAndView
        return ...
    }

}
```

你也可以使用通用的 Spring MVC 特性，比如 [`@ExceptionHandler` methods](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-exceptionhandlers) 和 [`@ControllerAdvice`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-ann-controller-advice)。`ErrorController` 就会处理任何未处理的异常。

