##### 健康组

有时候将健康指标组织成组可能会有用，这样便于用于不同目的。比如，如果你将应用部署到 Kubernetes，您可能需要一套不同的健康指标来进行“活力”和“就绪”检查。

要创建一个健康指标组，您可以使用 `management.endpoint.health.group.<name>` 属性，并指定一个健康指标 ID 列表以 `include` 或 `exclude`。例如，要创建仅包含数据库指示符的组，可以定义以下内容：

```properties
management.endpoint.health.group.custom.include=db
```

然后，您可以点击 `localhost:8080/actuator/health/custom` 来检查结果。

默认情况下，组将继承与系统运行状况相同的 `StatusAggregator` 和 `HttpCodeStatusMapper` 设置，但是，也可以在每个组的基础上进行定义。如果需要，也可以覆盖 `show-details` 和 `roles` 属性：

```properties
management.endpoint.health.group.custom.show-details=when-authorized
management.endpoint.health.group.custom.roles=admin
management.endpoint.health.group.custom.status.order=fatal,up
management.endpoint.health.group.custom.status.http-mapping.fatal=500
```

> 你可以使用 `@Qualifier("groupname")` 如果你需要注册自定义 `StatusAggregator` 或者 `HttpCodeStatusMapper` beans 以和该组一起使用。

