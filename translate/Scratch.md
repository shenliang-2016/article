##### HTTP Client Metrics

Spring Boot Actuator 可以管理 `RestTemplate` 和 `WebClient ` 的检测基础设施。为此，你必须注入相应的构建器并使用它创建实例：

- `RestTemplateBuilder` 用于 `RestTemplate`
- `WebClient.Builder` 用于 `WebClient`

也可以手动应用负责此工具的定制程序，即 `MetricsRestTemplateCustomizer` 和 `MetricsWebClientCustomizer`。

默认情况下，使用名称 `http.client.requests` 生成度量。可以通过设置 `management.metrics.web.client.request.metric-name` 属性来自定义名称。

默认情况下，通过检测的客户端生成的度量标准标记有以下信息：

| Tag          | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| `clientName` | URI 的 Host 部分                                             |
| `method`     | 请求方法 (比如， `GET` 或者 `POST`)                          |
| `outcome`    | 基于响应状态码的请求输出。 1xx 是 `INFORMATIONAL`, 2xx 是 `SUCCESS`, 3xx 是 `REDIRECTION`, 4xx `CLIENT_ERROR`, 而 5xx 是 `SERVER_ERROR`, 否则是 `UNKNOWN` 。 |
| `status`     | 响应的 HTTP 状态码，如果可用 (比如， `200` 或者 `500`)，或者 `IO_ERROR` 如果出现 I/O 问题， 否则是 `CLIENT_ERROR` 。 |
| `uri`        | 应用变量之前的请求 URI 模板，如果可能 (比如， `/api/person/{id}`) |

要根据您选择的客户端自定义标签，可以提供实现 `@RestTemplateExchangeTagsProvider` 或 `WebClientExchangeTagsProvider` 的 `@Bean`。`RestTemplateExchangeTags` 和 `WebClientExchangeTags` 中有便捷的静态函数。