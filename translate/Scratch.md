##### 编写自定义健康状况指标

要提供自定义的健康信息，您可以注册实现 [`HealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthIndicator.java) 接口。您需要提供`health()`方法的实现并返回`Health`响应。 `Health` 响应应包含状态，并可以选择包含要显示的其他详细信息。以下代码显示了示例 `HealthIndicator` 的实现：

```java
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Component;

@Component
public class MyHealthIndicator implements HealthIndicator {

    @Override
    public Health health() {
        int errorCode = check(); // perform some specific health check
        if (errorCode != 0) {
            return Health.down().withDetail("Error Code", errorCode).build();
        }
        return Health.up().build();
    }

}
```

> 给定 `HealthIndicator` 的标识符是不带 `HealthIndicator` 后缀（如果存在）的 bean 名称。前面的例子中，健康信息可以通过名为 `my` 的入口得到。

除了 Spring Boot 预定义的 [`Status`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/Status.java) 类型，为 `Health` 返回自定义 `Status` 以表示新的系统状态也是可以的。这种情况下，需要提供相应的 [`StatusAggregator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/StatusAggregator.java) 接口自定义实现。或者该接口的默认实现通过 `management.endpoint.health.status.order` 配置属性进行了配置。

比如，假定携带编码 `FATAL` 的 `Status` 被用于你的 `HealthIndicator` 实现。为了配置优先顺序，将下面的属性添加到你的应用配置中：

```properties
management.endpoint.health.status.order=fatal,down,out-of-service,unknown,up
```

响应中的 HTTP 状态代码反映了总体健康状态（例如，`UP` 映射为 200，而 `OUT_OF_SERVICE` 和 `DOWN` 映射为 503）。如果通过 HTTP 访问运行状况端点，则可能还需要注册自定义状态映射。例如，以下属性将 `FATAL` 映射到 503（服务不可用）：

```properties
management.endpoint.health.status.http-mapping.fatal=503
```

> 如果你需要更多控制，可以定义你自己的 `HttpCodeStatusMapper` bean。

下表展示了内建状态包含的默认状态映射：

| Status         | Mapping                                      |
| :------------- | :------------------------------------------- |
| DOWN           | SERVICE_UNAVAILABLE (503)                    |
| OUT_OF_SERVICE | SERVICE_UNAVAILABLE (503)                    |
| UP             | No mapping by default, so http status is 200 |
| UNKNOWN        | No mapping by default, so http status is 200 |