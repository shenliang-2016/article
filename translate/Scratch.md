#### 5.2.8. 健康信息

你可以使用健康信息来检查运行中应用的状态。健康信息通常会被监控软件用来在生产系统发生故障时发出告警。健康信息通过 `health` 端点暴露，取决于 `management.endpoint.health.show-details` 和 `management.endpoint.health.show-components` 属性，这两个属性可以设置为下面的值：

| Name              | Description                                                  |
| :---------------- | :----------------------------------------------------------- |
| `never`           | 永远不展示细节。                                             |
| `when-authorized` | 细节信息只向授权用户展示。授权角色可以通过 `management.endpoint.health.roles` 配置。 |
| `always`          | 细节向所有用户展示。                                         |

默认值是 `never`。当用户属于一个或者多个端点角色时会被认为是授权用户。如果端点没有配置角色（默认情况）所有通过身份认证的用户都被认为是授权用户。角色可以通过 `management.endpoint.health.roles` 属性配置。

> 如果您已经保护了您的应用程序并希望使用 `always`，则您的安全配置必须允许经过身份验证的用户和未经身份验证的用户都可以访问健康状况端点。

健康状况信息收集自 [`HealthContributorRegistry`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthContributorRegistry.java) 的内容 (默认情况下所有定义在你的 `ApplicationContext` 中的 [`HealthContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthContributor.java) 实例)。Spring Boot 包含大量自动配置的 `HealthContributors` ，同时你哈可以编写你自己的。

一个 `HealthContributor` 可以是一个 `HealthIndicator` 或者一个 `CompositeHealthContributor`。`HealthIndicator`  提供实际的健康状况信息，包括 `Status`。`CompositeHealthContributor` 提供其他 `HealthContributors` 的组合。组合在一起，构成一个树形结构从整体上反映系统健康状况。

默认情况下，最终的系统健康状况是由 `StatusAggregator` 派生的，该 `StatusAggregator` 根据状态的有序列表对每个 `HealthIndicator` 中的状态进行排序。排序列表中的第一个状态用作整体运行状况。如果没有 `HealthIndicator` 返回 `StatusAggregator` 已知的状态，则使用 `UNKNOWN` 状态。

> `HealthContributorRegistry` 可以被用于在运行时注册或者注销健康状况指标。