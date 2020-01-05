##### 构造器绑定

上一节中的例子可以被重写为不可变风格，如下所示：

```java
package com.example;

import java.net.InetAddress;
import java.util.List;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.boot.context.properties.ConstructorBinding;
import org.springframework.boot.context.properties.DefaultValue;

@ConstructorBinding
@ConfigurationProperties("acme")
public class AcmeProperties {

    private final boolean enabled;

    private final InetAddress remoteAddress;

    private final Security security;

    public AcmeProperties(boolean enabled, InetAddress remoteAddress, Security security) {
        this.enabled = enabled;
        this.remoteAddress = remoteAddress;
        this.security = security;
    }

    public boolean isEnabled() { ... }

    public InetAddress getRemoteAddress() { ... }

    public Security getSecurity() { ... }

    public static class Security {

        private final String username;

        private final String password;

        private final List<String> roles;

        public Security(String username, String password,
                @DefaultValue("USER") List<String> roles) {
            this.username = username;
            this.password = password;
            this.roles = roles;
        }

        public String getUsername() { ... }

        public String getPassword() { ... }

        public List<String> getRoles() { ... }

    }

}
```

在此设置中，使用 `@ConstructorBinding` 注解指示应使用构造函数绑定。这意味着绑定器将期望找到带有您希望绑定的参数的构造函数。

`@ConstructorBinding` 类的嵌套成员（例如上例中的 `Security`）也将通过其构造函数进行绑定。

可以使用 `@DefaultValue` 指定默认值，并且将应用相同的转换服务将 `String` 值强制转换为缺少属性的目标类型。

> 要使用构造函数绑定，必须使用 `@EnableConfigurationProperties` 或配置属性扫描来启用该类。您不能对通过常规 Spring 机制创建的 bean 使用构造函数绑定（例如，`@Component bean` 的 beans，通过 `@Bean` 方法创建的 bean 或使用 `@Import` 加载的 bean）。

> 如果您的类有多个构造函数，则还可以直接在应绑定的构造函数上使用 `@ConstructorBinding`。

##### 启用 `@ConfigurationProperties` 注解的类型

Spring Boot 提供了绑定 `@ConfigurationProperties` 类型并将其注册为 Bean 的基础架构。您可以逐类启用配置属性，也可以启用与组件扫描类似的方式进行配置属性扫描。

有时，带有 `@ConfigurationProperties` 注解的类可能不适用于扫描，例如，如果您正在开发自己的自动配置，或者想要有条件地启用它们。在这些情况下，请使用 `@EnableConfigurationProperties` 注解指定要处理的类型列表。可以在任何 `@Configuration` 类上完成，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
@EnableConfigurationProperties(AcmeProperties.class)
public class MyConfiguration {
}
```

要使用配置属性扫描，请在您的应用程序中添加 `@ConfigurationPropertiesScan` 注解。通常，它被添加到以 `@SpringBootApplication` 注解的主应用程序类中，但是也可以被添加到任何 `@Configuration` 类中。默认情况下，将从声明注解的类的包中进行扫描。如果要定义要扫描的特定程序包，可以按照以下示例所示进行操作：

```java
@SpringBootApplication
@ConfigurationPropertiesScan({ "com.example.app", "org.acme.another" })
public class MyApplication {
}
```

> 当使用配置属性扫描或通过 `@EnableConfigurationProperties` 注册了 `@ConfigurationProperties` bean时，该 bean 具有常规名称：`<prefix>-<fqn>`，其中，`<prefix>` 是在 `@ConfigurationProperties` 中指定的环境 key 前缀。`<fqn>` 是 Bean 的完全限定名称。如果注解不提供任何前缀，则仅使用 Bean 的完全限定名称。
>
> 上例中的 bean 名称是 `acme-com.example.AcmeProperties`。

我们建议 `@ConfigurationProperties` 只处理环境，尤其不要从上下文中注入其他 bean。对于极端情况，可以使用 setter 注入或框架提供的任何 `*Aware` 接口（例如，如果需要访问 `Environment`，则可以使用 `EnvironmentAware`）。如果仍然想使用构造函数注入其他 bean，则必须使用 `@Component` 注解配置属性 bean，并使用基于 JavaBean 的属性绑定。

##### 使用 `@ConfigurationProperties` 注解的类型

这种配置样式与 `SpringApplication` 外部 YAML 配置特别有效，如以下示例所示：

```yaml
# application.yml

acme:
    remote-address: 192.168.1.1
    security:
        username: admin
        roles:
          - USER
          - ADMIN

# additional configuration as required
```

要使用 `@ConfigurationProperties` bean，可以像使用其他任何 bean 一样注入它们，如以下示例所示：

```java
@Service
public class MyService {

    private final AcmeProperties properties;

    @Autowired
    public MyService(AcmeProperties properties) {
        this.properties = properties;
    }

    //...

    @PostConstruct
    public void openConnection() {
        Server server = new Server(this.properties.getRemoteAddress());
        // ...
    }

}
```

> 使用 `@ConfigurationProperties` 还可以让您生成元数据文件，IDE 可以使用这些元数据文件为您提供关键字自动完成功能。有关详细信息，请参见 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#configuration-metadata)。

