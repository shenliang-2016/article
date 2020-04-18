##### Spring WebFlux Metrics

自动配置为所有由 WebFlux 控制器和功能处理的请求启用指标基础设施。

默认情况下，度量指标使用名称 `http.server.requests` 生成。你可以通过设定 `management.metrics.web.server.request.metric-name` 属性来自定义名称。

默认地，WebFlux 相关的指标会被以下信息标记：

| Tag         | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `exception` | 处理请求时抛出的任何异常的简单类名。                         |
| `method`    | 请求方法 (比如，`GET` 或者 `POST`)                           |
| `outcome`   | 基于响应状态码的请求输出。 1xx 是 `INFORMATIONAL`， 2xx 是 `SUCCESS`， 3xx 是 `REDIRECTION`， 4xx 是 `CLIENT_ERROR`， 5xx 是 `SERVER_ERROR` |
| `status`    | 响应的 HTTP 状态码 (比如， `200` 或者 `500`)                 |
| `uri`       | 应用变量值之前的请求的 URI 模板，如果可能的话 (比如， `/api/person/{id}`) |

为了自定义标签，提供一个实现了 `WebFluxTagsProvider` 接口的 `@Bean` 类。