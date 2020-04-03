#### 5.2.1. 开启端点

默认情况下，除 `shutdown` 外的所有端点均处于启用状态。要配置端点的启用，请使用其`management.endpoint..enabled`属性。以下示例启用了`shutdown`端点：

```properties
management.endpoint.shutdown.enabled=true
```

如果您宁愿选择默认关闭所有端点而手动个别开启，请将 `management.endpoints.enabled-by-default` 属性设置为 `false`，并使用各个端点 `enabled` 属性进行开启。以下示例启用`info`端点并禁用所有其他端点：

```properties
management.endpoints.enabled-by-default=false
management.endpoint.info.enabled=true
```

> 被关闭的端点会从应用上下文中彻底删除。如果你只希望在该端点暴露的具体技术实现层面进行控制，使用 [`include` 和 `exclude` 属性](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints) 代替。