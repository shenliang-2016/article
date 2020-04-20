##### Jersey Server Metrics

当 Micrometer 的`micrometer-jersey2`模块位于类路径上时，自动配置将启用对 Jersey JAX-RS 实现所处理的请求的检测。当 `management.metrics.web.server.request.autotime.enabled` 为 `true` 时，将对所有请求进行检测。另外，当设置为 `false` 时，可以通过在请求处理方法中添加 `@Timed` 来启用检测：

```java
@Component
@Path("/api/people")
@Timed //在资源类上，以对资源中的每个请求处理程序启用计时。
public class Endpoint {
    @GET
    @Timed(extraTags = { "region", "us-east-1" }) //关于启用单个端点的方法。如果您将它放在类中，则不必这样做，但是可以用于进一步为此特定端点自定义计时器。
    @Timed(value = "all.people", longTask = true) //在 longTask = true 的方法上为该方法启用长任务计时器。长任务计时器需要单独的度量标准名称，并且可以与短任务计时器堆叠在一起。
    public List<Person> listPeople() { ... }
}
```

默认情况下，使用名称 `http.server.requests` 生成度量。可以通过设置 `management.metrics.web.server.request.metric-name` 属性来自定义名称。

默认情况下，Jersey 服务器指标带有以下信息：

| Tag         | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `exception` | 处理请求时引发的任何异常的简单类名。                         |
| `method`    | 请求方法 (比如， `GET` 或者 `POST`)                          |
| `outcome`   | 基于响应状态码的亲求输出。 1xx 是 `INFORMATIONAL`, 2xx 是 `SUCCESS`, 3xx 是 `REDIRECTION`, 4xx `CLIENT_ERROR`, 而 5xx 是 `SERVER_ERROR` |
| `status`    | 响应的 HTTP 状态码 (比如， `200` 或者 `500`)                 |
| `uri`       | 应用变量替换之前的请求 URI 模板，如果可能 (比如， `/api/person/{id}`) |

要自定义标签，提供一个实现了 `JerseyTagsProvider` 的 `@Bean` 。