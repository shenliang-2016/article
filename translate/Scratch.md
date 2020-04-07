##### 反应式健康指标

对于反应式应用，比如使用 Spring WebFlux 的应用， `ReactiveHealthContributor` 提供了一种非阻塞式的获取应用健康状况信息的协议。类似于传统的 `HealthContributor`，健康状况信息收集自 [`ReactiveHealthContributorRegistry`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthContributorRegistry.java) (默认是你的 `ApplicationContext` 中定义的所有 [`HealthContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthContributor.java) 和 [`ReactiveHealthContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthContributor.java) 实例) 的内容。不检查反应式 API 的常规`HealthContributors`在弹性调度程序上执行。

> 在反应式应用程序中，应使用 `ReactiveHealthContributorRegistry` 在运行时注册和注销健康指标。如果需要注册常规的 `HealthContributor`，则应使用`ReactiveHealthContributor#adapt`对其进行包装。

为了从反应式 API 提供自定义健康信息，你可以注册实现 [`ReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthIndicator.java) 接口的 Spring beans。下面的代码展示了一个简单的 `ReactiveHealthIndicator` 实现：

```java
@Component
public class MyReactiveHealthIndicator implements ReactiveHealthIndicator {

    @Override
    public Mono<Health> health() {
        return doHealthCheck() //perform some specific health check that returns a Mono<Health>
            .onErrorResume(ex -> Mono.just(new Health.Builder().down(ex).build()));
    }

}
```

> 为了自动处理错误，考虑从 `AbstractReactiveHealthIndicator` 扩展。