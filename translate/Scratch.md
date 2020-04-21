### 5.7. 审计

一旦启动了 Spring Security，Spring Boot Actuator 将具有一个灵活的审计框架，该框架可以发布事件（默认情况下，“身份验证成功”，“失败”和“拒绝访问”异常）。此功能对于报告和基于身份验证失败实施锁定策略非常有用。

可以通过在应用程序的配置中提供类型为 `AuditEventRepository` 的 Bean 来启用审计。为了方便起见，Spring Boot 提供了一个 `InMemoryAuditEventRepository`。`InMemoryAuditEventRepository` 具有有限的功能，我们建议仅将其用于开发环境。对于生产环境，请考虑创建自己的替代 `AuditEventRepository` 实现。

#### 5.7.1. 自定义审计

要自定义已发布的安全事件，可以提供自己的 `AbstractAuthenticationAuditListener` 和 `AbstractAuthorizationAuditListener` 的实现。

您也可以将审计服务用于自己的业务事件。为此，可以将 `AuditEventRepository` bean 注入到您自己的组件中，然后直接使用它，或者通过 Spring `ApplicationEventPublisher`（通过实现 `ApplicationEventPublisherAware`）发布 `AuditApplicationEvent`。