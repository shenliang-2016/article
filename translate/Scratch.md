#### 5.2.2. 暴露端点

由于端点可能包含敏感信息，谨慎考虑何时暴露它们。下表展示了内建端点的默认暴露情况：

| ID                 | JMX  | Web  |
| :----------------- | :--- | :--- |
| `auditevents`      | Yes  | No   |
| `beans`            | Yes  | No   |
| `caches`           | Yes  | No   |
| `conditions`       | Yes  | No   |
| `configprops`      | Yes  | No   |
| `env`              | Yes  | No   |
| `flyway`           | Yes  | No   |
| `health`           | Yes  | Yes  |
| `heapdump`         | N/A  | No   |
| `httptrace`        | Yes  | No   |
| `info`             | Yes  | Yes  |
| `integrationgraph` | Yes  | No   |
| `jolokia`          | N/A  | No   |
| `logfile`          | N/A  | No   |
| `loggers`          | Yes  | No   |
| `liquibase`        | Yes  | No   |
| `metrics`          | Yes  | No   |
| `mappings`         | Yes  | No   |
| `prometheus`       | N/A  | No   |
| `scheduledtasks`   | Yes  | No   |
| `sessions`         | Yes  | No   |
| `shutdown`         | Yes  | No   |
| `threaddump`       | Yes  | No   |

为了修改端点的暴露情况，使用下面的特定于技术的 `include` 和 `exclude` 属性：

| Property                                    | Default        |
| :------------------------------------------ | :------------- |
| `management.endpoints.jmx.exposure.exclude` |                |
| `management.endpoints.jmx.exposure.include` | `*`            |
| `management.endpoints.web.exposure.exclude` |                |
| `management.endpoints.web.exposure.include` | `info, health` |

`include` 属性列出了暴露的端点的 IDs。`exclude` 属性列出了不应该暴露的端点。后者的优先级高于前者。两者都可以配置为端点 IDs 列表。

比如，为了停止所有通过 JMX 暴露的端点，仅仅暴露 `health` 和 `info` 端点，使用下面的属性：

```properties
management.endpoints.jmx.exposure.include=health,info
```

`*` 可以用于选择所有端点。比如，为了通过 HTTP 暴露所有端点，除了 `env` 和 `beans` 端点，使用下面的属性：

```properties
management.endpoints.web.exposure.include=*
management.endpoints.web.exposure.exclude=env,beans
```

> `*` 在 YMAL 中有特殊含义，因此需要用双引号标识，以表示选择或者不选所有端点。如下面例子所示：
>
> ````
> management:
>   endpoints:
>     web:
>       exposure:
>         include: "*"
> ````

> 如果你的应用暴露在公开环境中，我们强烈建议你 [为你的端点添加安全设施](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-security)。 

> 如果你想要实现自己的端点暴露策略，你可以注册一个 `EndpointFilter` bean。