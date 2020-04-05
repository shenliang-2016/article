###### Path

谓词的路径由端点的 ID 和暴露的端点的根路径决定。默认的根路径是 `/actuator`。比如，ID 为 `sessions` 的端点将使用 `/actuator/sessions` 作为它的谓词中的路径。

通过使用 `@Selector` 注解修饰操作方法的一个或多个参数，可以进一步自定义路径。将这样的参数作为路径变量添加到路径谓词。调用端点操作时，变量的值将传递到操作方法中。如果要捕获所有剩余的路径元素，则可以在最后一个参数上添加 `@Selector(Match=ALL_REMAINING)` ，并将其设置为与 `String[]` 兼容的转换类型。

###### HTTP 方法

谓词的 HTTP 方法取决于操作类型，如下所示：

| Operation          | HTTP method |
| :----------------- | :---------- |
| `@ReadOperation`   | `GET`       |
| `@WriteOperation`  | `POST`      |
| `@DeleteOperation` | `DELETE`    |

###### Consumes

对于使用请求体的 `@WriteOperation` (HTTP `POST`)，谓词的 consumes 子句是 `application/vnd.spring-boot.actuator.v2+json, application/json`。对于其他操作，consumes 子句是空。

###### Produces

谓词的 produces 子句由 `@DeleteOperation`, `@ReadOperation`, 和 `@WriteOperation` 注解的 `produces` 属性确定。该属性是可选的，如果没有使用，则 produces 子句被自动确定。

如果操作方法返回 `void` 或者 `Void` 则 produces 子句是空。如果操作防范返回 `org.springframework.core.io.Resource`，produces 子句是 `application/octet-stream`。所有其他操作， produces 子句是 `application/vnd.spring-boot.actuator.v2+json, application/json`。

###### Web 端点响应状态

端点操作的响应状态默认取决于操作类型（读、写、或者删除），以及，如果存在，操作返回值。

一个 `@ReadOperation` 返回一个值，则响应状态将是 200 (OK)。如果它没有返回值，响应状态将是 404 (Not Found)。

如果一个 `@WriteOperation` 或者 `@DeleteOperation` 返回一个值，响应状态将是 200 (OK)。如果没有返回值，响应状态将是 204 (No Content)。

如果一个操作被无参数调用，或者调用参数无法转换为需要的类型，操作方法就不会被调用，并且响应状态将是 400 (Bad Request)。

###### Web Endpoint 范围请求

HTTP 范围请求可以用于请求部分 HTTP 资源。当使用 Spring MVC 或者 Spring Web Flux 时，返回 `org.springframework.core.io.Resource` 的操作自动支持范围请求。

> 使用 Jersey 时不支持范围请求。

###### Web 端点安全

在 Web 端点或特定于 Web 的端点扩展上的操作可以接收当前的 `java.security.Principal` 或 `org.springframework.boot.actuate.endpoint.SecurityContext` 作为方法参数。前者通常与 `@Nullable` 结合使用，以为经过身份验证和未经身份验证的用户提供不同的行为。后者通常用于使用其 `isUserInRole(String)` 方法执行授权检查。