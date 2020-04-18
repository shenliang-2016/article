##### Spring MVC Metrics

通过自动配置，可以检测由 Spring MVC 处理的请求。当 `management.metrics.web.server.request.autotime.enabled` 为 `true` 时，将对所有请求进行检测。 另外，当设置为 `false` 时，可以通过在请求处理方法中添加 `@Timed` 来启用检测：

```java
@RestController
@Timed // 控制器类，用于对控制器中的每个请求处理程序启用计时。
public class MyController {

    @GetMapping("/api/people")
    @Timed(extraTags = { "region", "us-east-1" }) // 一种启用单个端点的方法。如果您将它放在类中，则不必这样做，但是可以用于进一步为此特定端点自定义计时器。
    @Timed(value = "all.people", longTask = true) // longTask = true 的方法为该方法启用长任务计时器。长任务计时器需要单独的度量标准名称，并且可以与短任务计时器堆叠在一起。
    public List<Person> listPeople() { ... }

}
```

默认情况下，使用名称 `http.server.requests` 生成度量。可以通过设置 `management.metrics.web.server.request.metric-name` 属性来自定义名称。

默认情况下，与 Spring MVC 相关的指标带有以下信息标记：

| Tag         | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `exception` | 处理请求时引发的任何异常的简单类名。                         |
| `method`    | 请求方法 (比如， `GET` 或者 `POST`)                          |
| `outcome`   | 根据响应的状态码请求的结果。1xx 是 `INFORMATIONAL`，2xx 是 `SUCCESS`，3xx 是 `REDIRECTION`，4xx 是 `CLIENT_ERROR`，5xx 是 `SERVER_ERROR` |
| `status`    | 响应的 HTTP 状态码 (比如， `200` 或者 `500`)                 |
| `uri`       | 应用变量之前的请求的 URI 模板，如果可能 (比如， `/api/person/{id}`) |

为了自定义这些标签，提供一个实现了 `WebMvcTagsProvider` 接口的 `@Bean` 类。