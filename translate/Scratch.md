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

##### Exposing YAML as Properties in the Spring Environment

The `YamlPropertySourceLoader` class can be used to expose YAML as a `PropertySource` in the Spring `Environment`. Doing so lets you use the `@Value` annotation with placeholders syntax to access YAML properties.

##### Multi-profile YAML Documents

You can specify multiple profile-specific YAML documents in a single file by using a `spring.profiles` key to indicate when the document applies, as shown in the following example:

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

In the preceding example, if the `development` profile is active, the `server.address` property is `127.0.0.1`. Similarly, if the `production` **and** `eu-central` profiles are active, the `server.address` property is `192.168.1.120`. If the `development`, `production` and `eu-central` profiles are **not** enabled, then the value for the property is `192.168.1.100`.

> `spring.profiles` can therefore contain a simple profile name (for example `production`) or a profile expression. A profile expression allows for more complicated profile logic to be expressed, for example `production & (eu-central | eu-west)`. Check the [reference guide](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/core.html#beans-definition-profiles-java) for more details.

If none are explicitly active when the application context starts, the default profiles are activated. So, in the following YAML, we set a value for `spring.security.user.password` that is available **only** in the "default" profile:

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

Whereas, in the following example, the password is always set because it is not attached to any profile, and it would have to be explicitly reset in all other profiles as necessary:

```yaml
server:
  port: 8000
spring:
  security:
    user:
      password: weak
```

Spring profiles designated by using the `spring.profiles` element may optionally be negated by using the `!` character. If both negated and non-negated profiles are specified for a single document, at least one non-negated profile must match, and no negated profiles may match.

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

