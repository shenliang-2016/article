#### 4.1.9. 使用 ApplicationRunner 或者 CommandLineRunner

如果需要在 `SpringApplication` 启动后运行一些特定的代码，则可以实现 `ApplicationRunner` 或 `CommandLineRunner` 接口。两个接口都以相同的方式工作，并提供一个单一的 `run` 方法，该方法在 `SpringApplication.run(…)` 完成之前被调用。

`CommandLineRunner` 接口以简单的字符串数组提供对应用程序参数的访问，而 `ApplicationRunner` 使用前面讨论的 `ApplicationArguments` 接口。以下示例显示了带有 `Run` 方法的 `CommandLineRunner`：

```java
import org.springframework.boot.*;
import org.springframework.stereotype.*;

@Component
public class MyBean implements CommandLineRunner {

    public void run(String... args) {
        // Do something...
    }

}
```

如果定义了几个必须按特定顺序调用的 `CommandLineRunner` 或 `ApplicationRunner` Bean，则可以另外实现 `org.springframework.core.Ordered` 接口或使用 `org.springframework.core.annotation.Order` 注解。

