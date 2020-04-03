### 5.2. 端点

执行器端点允许你监控你的引用并与之交互。Spring Boot 包含大量内建端点，同时允许你自行添加自己的端点。比如，`health` 端点提供了基本的应用健康信息。

每个端点都可以单独 [开启或者关闭](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-enabling-endpoints)。这可以控制该端点是否会被创建，以及相关的 bean 是否存在于应用上下文中。为了远程访问，端点必须 [通过 JMX 或者 HTTP 暴露](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints)。大部分应用选择了 HTTP，此时，端点的 ID 包含前缀 `/actuator` 映射到一个 URL。比如，默认地，`health` 端点映射到 `/actuator/health`。

下列与技术无关的端点是可用的：

| ID                 | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| `auditevents`      | 暴露当前应用的审计事件信息。需要 `AuditEventRepository` bean。 |
| `beans`            | 展示你的应用中所有 Spring beans 的完整列表。                 |
| `caches`           | 暴露可用的缓存。                                             |
| `conditions`       | 展示配置和自动配置上被评估的条件，以及它们满足与否的原因。   |
| `configprops`      | 展示所有的 `@ConfigurationProperties` 的整理好的列表。       |
| `env`              | 暴露来自 Spring’s `ConfigurableEnvironment` 的属性。         |
| `flyway`           | 显示任何已经被应用的 Flyway database 迁移。需要一个或者多个 `Flyway` beans。 |
| `health`           | 显示应用健康状态信息。                                       |
| `httptrace`        | 显示 HTTP 跟踪信息（默认地，最近 100 次请求-响应交互）。需要 `HttpTraceRepository` bean。 |
| `info`             | 显示任意应用信息。                                           |
| `integrationgraph` | 展示 Spring 集成图。需要 `spring-integration-core` 依赖。    |
| `loggers`          | 展示和修改应用中的日志记录器配置。                           |
| `liquibase`        | 展示任何已经应用的 Liquibase 数据库迁移。需要一个或者多个 `Liquibase` beans。 |
| `metrics`          | 显示当前应用的 ‘metrics’ 信息。                              |
| `mappings`         | 显示整理好的所有 `@RequestMapping` 路径的列表。              |
| `scheduledtasks`   | 显示你的应用中的调度任务。                                   |
| `sessions`         | 允许从 Spring Session 支持的会话存储中检索和删除用户会话。需要使用 Spring Session 的基于 Servlet 的 Web 应用程序。 |
| `shutdown`         | 允许应用优雅地关闭。默认关闭。                               |
| `threaddump`       | 执行线程转储。                                               |

如果你的应用是 web 应用 (Spring MVC, Spring WebFlux, 或者 Jersey)，你还可以使用下面的附加端点：

| ID           | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| `heapdump`   | 返回一个 `hprof` 堆转储文件。                                |
| `jolokia`    | 通过 HTTP暴露 JMX beans  (当 Jolokia 在类路径上时，对 WebFlux 不可用)。需要 `jolokia-core` 依赖。 |
| `logfile`    | 返回日志文件的内容 (如果设置了 `logging.file.name` 或者 `logging.file.path` 属性)。支持使用 HTTP `Range` 请求首部获取日志文件的部分内容。 |
| `prometheus` | 以 Prometheus 服务器可以抓取的格式暴露指标信息。需要依赖于`micrometer-registry-prometheus`。 |

了解更多有关 Actuator’s 端点以及相应的请求响应格式，请参考独立 API 文档 ([HTML](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/actuator-api//html/) 或者 [PDF](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/actuator-api//pdf/spring-boot-actuator-web-api.pdf))。