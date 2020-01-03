#### 4.1.10. 应用退出

每个 `SpringApplication` 向 JVM 注册一个关闭钩子，以确保 `ApplicationContext` 在退出时正常关闭。所有标准的 Spring 生命周期回调（例如 `DisposableBean` 接口或 `@PreDestroy` 注解）都可以使用。

另外，如果 bean 希望在调用 `SpringApplication.exit()` 时返回特定的退出代码，则可以实现 `org.springframework.boot.ExitCodeGenerator` 接口。然后可以将此退出代码传递给 `System.exit()` 以将其作为状态代码返回，如以下示例所示：

```java
@SpringBootApplication
public class ExitCodeApplication {

    @Bean
    public ExitCodeGenerator exitCodeGenerator() {
        return () -> 42;
    }

    public static void main(String[] args) {
        System.exit(SpringApplication.exit(SpringApplication.run(ExitCodeApplication.class, args)));
    }

}
```

同样，`ExitCodeGenerator` 接口可以通过异常实现。当遇到这样的异常时，Spring Boot 返回由实现的 `getExitCode()` 方法提供的退出代码。

