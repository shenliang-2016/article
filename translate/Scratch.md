### 5.3.  通过 HTTP 进行监控和管理

如果您正在开发 Web 应用程序，则 Spring Boot Actuator 会自动配置所有启用的端点以通过 HTTP 公开。默认约定是使用端点的 `id` 和前缀 `/actuator` 作为 URL 路径。例如，`health` 被公开为 `/actuator/health`。

> Spring MVC，Spring WebFlux 和 Jersey 本身支持 Actuator。如果 Jersey 和 Spring MVC 均可用，则将使用 Spring MVC。

#### 5.3.1. 自定义管理端点路径

有时，自定义管理端点的前缀很有用。例如，您的应用程序可能已经将 `/actuator` 用于其他用途。您可以使用 `management.endpoints.web.base-path` 属性来更改管理端点的前缀，如以下示例所示：

```properties
management.endpoints.web.base-path=/manage
```

前面的 `application.properties` 示例将端点由 `/actuator/{id}` 修改为 `/manage/{id}` (比如，`/manage/info`)。

> 除非管理端口已配置为 [通过使用其他 HTTP 端口公开端点](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-customizing-management-server-port)。`management.endpoints.web.base-path` 相对于 `server.servlet.context-path`。如果配置了 `management.server.port`，则 `management.endpoints.web.base-path` 相对于 `management.server.servlet.context-path`。

如果要将端点映射到其他路径，则可以使用 `management.endpoints.web.path-mapping` 属性。

以下示例将 `/actuator/health` 重新映射为 `/healthcheck`：

application.properties

```properties
management.endpoints.web.base-path=/
management.endpoints.web.path-mapping.health=healthcheck
```

