#### 4.2.5. 属性中的占位符

使用时，`application.properties` 中的值将通过现有的 `Environment` 进行过滤，因此您可以引用以前定义的值（例如，在 System 属性中定义的）。

```properties
app.name=MyApp
app.description=${app.name} is a Spring Boot application
```

> 你还可以使用此技术创建现有 Spring Boot 属性的"短"变体。参考*如何使用'短'命令行参数*了解更对细节。

#### 4.2.6. 属性加密

Spring Boot 没有提供任何属性值加密的内建支持，不过，它提供了修改 Spring `Evironment` 中包含的属性值所必需的钩子。`EnvironmentPostProcessor` 接口允许你在应用启动之前修改 `Evironment` 。参考 [Customize the Environment or ApplicationContext Before It Starts](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-customize-the-environment-or-application-context) 了解更多细节。

如果你正在寻找保存账号和密码的安全方式， [Spring Cloud Vault](https://cloud.spring.io/spring-cloud-vault/) 项目提供了将外部好化配置存储到 [HashiCorp Vault](https://www.vaultproject.io/) 中的支持。

#### 4.2.7. 使用 YAML 替代属性文件

[YAML](https://yaml.org/) 是 JSON 的超集，因而，是一种描述层级配置数据的方便格式。`SpringApplication` 类自动支持 YAML 作为属性文件的替代，只要你的类路径上存在 [SnakeYAML](https://bitbucket.org/asomov/snakeyaml) 类库。

> 如果你使用启动器，SnakeYAML 则由 `spring-boot-starter` 自动提供。

##### 加载 YAML

Spring 框架提供两种方便的类用于加载 YAML 文件。`YamlPropertiesFactoryBean` 加载 YAML 为 `Properties` ，`YamlMapFactoryBean` 加载 YAML 为 `Map` 。

比如，考虑下面的 YAML 文件：

```yaml
environments:
    dev:
        url: https://dev.example.com
        name: Developer Setup
    prod:
        url: https://another.example.com
        name: My Cool App
```

上面的例子可以被转化为下面的配置：

```properties
environments.dev.url=https://dev.example.com
environments.dev.name=Developer Setup
environments.prod.url=https://another.example.com
environments.prod.name=My Cool App
```

YAML 列表表示为带有 [`index`] 解引用器的属性键。例如，考虑以下 YAML：

```yaml
my:
   servers:
       - dev.example.com
       - another.example.com
```

上面的例子将被转化为下面的属性：

```properties
my.servers[0]=dev.example.com
my.servers[1]=another.example.com
```

要通过使用 Spring Boot 的 `Binder` 实用程序（这是 `@ConfigurationProperties`的作用）进行类似的属性绑定，您需要在目标 bean 中有一个属性，类型为 `java.util.List`（或 `Set`）。同时需要提供一个 setter 或使用一个可变值对其进行初始化。例如，以下示例绑定到前面显示的属性：

```java
@ConfigurationProperties(prefix="my")
public class Config {

    private List<String> servers = new ArrayList<String>();

    public List<String> getServers() {
        return this.servers;
    }
}
```

##### 在 Spring 环境中暴露 YAML 为属性

`YamlPropertySourceLoader` 类可用于在 Spring 环境中将 YAML 作为 `PropertySource` 公开。这样做可以让您使用带有占位符语法的 `@Value` 注解来访问 YAML 属性。

##### 多配置文件的 YAML 文档

您可以使用 `spring.profiles` 键在一个文件中指定多个特定于配置文件的 YAML 文档，以指示何时应用该文档，如以下示例所示：

```yaml
server:
    address: 192.168.1.100
---
spring:
    profiles: development
server:
    address: 127.0.0.1
---
spring:
    profiles: production & eu-central
server:
    address: 192.168.1.120
```

在前面的示例中，如果 `development` 配置文件处于活动状态，则 `server.address` 属性为 `127.0.0.1`。类似地，如果 `production` **和** `eu-central` 配置文件处于活动状态，则 `server.address` 属性为 `192.168.1.120`。如果未启用 `development` ， `production` 和 `eu-central` 配置文件，则该属性的值为 `192.168.1.100`。

> 因此 `spring.profiles` 可以包含一个简单的配置文件名称（例如 `production`）或一个配置文件表达式。配置文件表达式允许表达更复杂的配置文件逻辑，例如 `production＆(eu-central | eu-west)`。有关更多详细信息，请参见 [参考指南](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/core.html#beans-definition-profiles-java)。

如果在启动应用程序上下文时未明确激活任何配置，则会激活默认配置文件。因此，在以下 YAML 中，我们为 `spring.security.user.password` 设置了一个值，该值仅在“默认”配置文件激活时可用：

```yaml
server:
  port: 8000
---
spring:
  profiles: default
  security:
    user:
      password: weak
```

而在以下示例中，始终设置密码是因为该密码未附加到任何配置文件，并且必须根据需要在所有其他配置文件中将其显式重置：

```yaml
server:
  port: 8000
spring:
  security:
    user:
      password: weak
```

使用 `spring.profiles` 元素指定的 Spring 配置可以通过使用 `!` 字符来取反。如果为单个文档指定了否定的配置文件和非否定的配置文件，则至少一个非否定的配置文件必须匹配，并且否定的配置文件不能匹配。

##### YAML Shortcomings

YAML files cannot be loaded by using the `@PropertySource` annotation. So, in the case that you need to load values that way, you need to use a properties file.

Using the multi YAML document syntax in profile-specific YAML files can lead to unexpected behavior. For example, consider the following config in a file:

application-dev.yml

```yaml
server:
  port: 8000
---
spring:
  profiles: "!test"
  security:
    user:
      password: "secret"
```

If you run the application with the argument `--spring.profiles.active=dev` you might expect `security.user.password` to be set to “secret”, but this is not the case.

The nested document will be filtered because the main file is named `application-dev.yml`. It is already considered to be profile-specific, and nested documents will be ignored.

> We recommend that you don’t mix profile-specific YAML files and multiple YAML documents. Stick to using only one of them.

