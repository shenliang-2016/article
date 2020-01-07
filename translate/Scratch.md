#### 4.3.1. 添加活动 Profiles

`spring.profiles.active` 属性遵循与其他属性相同的排序规则：最高的 `PropertySource` 获胜。这意味着您可以在 `application.properties` 中指定活动 profile，然后使用命令行开关“替换”它们。

有时，将特定于配置文件的属性“添加”到活动 profile 文件而不是替换它们是有用的。`spring.profiles.include` 属性可用于无条件添加活动 profile 文件。`SpringApplication` 入口点还具有 Java API，用于设置其他配置文件（即，在由 `spring.profiles.active` 属性激活的 profile 的上面）。参见 [SpringApplication](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/SpringApplication.html) 中的 `setAdditionalProfiles()` 方法。

例如，当使用开关 `--spring.profiles.active=prod` 运行具有以下属性的应用程序时，也会激活 `proddb` 和 `prodmq` profile 文件：

```yaml
---
my.property: fromyamlfile
---
spring.profiles: prod
spring.profiles.include:
  - proddb
  - prodmq
```

> 请记住，可以在 YAML 文档中定义 `spring.profiles` 属性，以确定何时将该特定文档包括在配置中。请参阅 [根据环境更改配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-change-configuration-depending-on-the-environment ) 了解更多细节。

#### 4.3.2. 编程式设定 Profiles

您可以在应用程序运行之前通过调用 `SpringApplication.setAdditionalProfiles(…)` 来以编程方式设置活动 profile 文件。也可以使用 Spring 的 `ConfigurableEnvironment` 接口来激活 profile 文件。

#### 4.3.3. 特定于 Profile 的配置文件

`application.properties`（或 `application.yml`）和通过 `@ConfigurationProperties` 引用的文件的特定于配置文件的变体都被视为文件并已加载。参见“ [特定于配置文件的属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties) “以获取详细信息。

