### 3.5. Spring Beans 和依赖注入

您可以自由使用任何标准的 Spring Framework 技术来定义 bean 及其注入的依赖关系。为简单起见，我们经常发现使用 `@ComponentScan`（查找您的 bean）和使用 `@Autowired`（进行构造函数注入）效果很好。

如果按照上面的建议构造代码（将应用程序类放在根包中），则可以添加不带任何参数的 `@ComponentScan`。您的所有应用程序组件（`@Component`，`@Service`，`@Repository`，`@Controller` 等）都将自动注册为 Spring Bean。

下面的例子展示了一个 `@Service` bean ，它使用了构造器注入来获取所需的 `RiskAssessor` bean：

```java
package com.example.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class DatabaseAccountService implements AccountService {

    private final RiskAssessor riskAssessor;

    @Autowired
    public DatabaseAccountService(RiskAssessor riskAssessor) {
        this.riskAssessor = riskAssessor;
    }

    // ...

}
```

如果 bean 拥有构造器，你就可以忽略 `@Autowired` ，如下面例子所示：

```java
@Service
public class DatabaseAccountService implements AccountService {

    private final RiskAssessor riskAssessor;

    public DatabaseAccountService(RiskAssessor riskAssessor) {
        this.riskAssessor = riskAssessor;
    }

    // ...

}
```

> 请注意，使用构造函数注入如何将 `riskAssessor` 字段标记为 `final`，指示其随后无法更改。

### 3.6. 使用 @SpringBootApplication 注解

许多 Spring Boot 开发者喜欢他们的应用使用自动配置，组件扫描，并能够在他们的"应用类”中定义额外的配置。单独一个 `@SpringBootApplication` 就可以同时开启这三个特性。也就是：

- `@EnableAutoConfiguration`: 开启 [Spring Boot’s auto-configuration mechanism](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-auto-configuration) 。
- `@ComponentScan`: 在应用所在的包上开启 `@Component` 扫描 (参考 [the best practices](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-structuring-your-code))。
- `@Configuration`: 允许在上下文中注册额外 bean 或者引入额外的配置类。

```java
package com.example.myapplication;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication // same as @Configuration @EnableAutoConfiguration @ComponentScan
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

> `@SpringBootApplication` 还提供了别名来自定义 `@EnableAutoConfiguration` 和 `@ComponentScan` 属性。

> 这些功能都不是强制性的，您可以选择替换任何单个注解来开关用它启用的任何功能。例如，您可能不想在应用程序中使用组件扫描或配置属性扫描：
>
> ````java
> package com.example.myapplication;
> 
> import org.springframework.boot.SpringApplication;
> import org.springframework.context.annotation.ComponentScan
> import org.springframework.context.annotation.Configuration;
> import org.springframework.context.annotation.Import;
> 
> @Configuration(proxyBeanMethods = false)
> @EnableAutoConfiguration
> @Import({ MyConfig.class, MyAnotherConfig.class })
> public class Application {
> 
>     public static void main(String[] args) {
>             SpringApplication.run(Application.class, args);
>     }
> 
> }
> ````
>
> 在此示例中，除了没有自动检测到带有 `@Component` 注解的类和带有 `@ConfigurationProperties` 注解的类并且显式导入了用户定义的 Bean 之外，`Application` 就像其他任何 Spring Boot 应用程序一样（参考 `@Import`）。

