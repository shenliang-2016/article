#### 4.4.7. Logback 扩展

Spring Boot 包含许多 Logback 扩展，可以帮助进行高级配置。您可以在 `logback-spring.xml` 配置文件中使用这些扩展名。

> 由于标准的 `logback.xml` 配置文件加载得太早，因此您不能在其中使用扩展名。您需要使用 `logback-spring.xml` 或定义 `logging.config` 属性。

> 这些扩展不能与 Logback 的 [配置扫描](https://logback.qos.ch/manual/configuration.html#autoScan) 一起使用。如果尝试这样做，则对配置文件进行更改将导致类似于以下记录之一的错误：

```
ERROR in ch.qos.logback.core.joran.spi.Interpreter@4:71 - no applicable action for [springProperty], current ElementPath is [[configuration][springProperty]]
ERROR in ch.qos.logback.core.joran.spi.Interpreter@4:71 - no applicable action for [springProfile], current ElementPath is [[configuration][springProfile]]
```

##### 特定于 Profile 的配置

使用 `<springProfile>` 标签，您可以根据活动的 Spring profiles 文件有选择地包括或排除配置部分。在 `<configuration>` 元素内的任何位置都支持 profile 小节。使用 `name` 属性指定哪个 profile 文件接受配置。标签 `<springProfile>` 可以包含一个简单的 profile 文件名称（例如 `staging`）或一个 profile 文件表达式。profile 文件表达式允许表达更复杂的 profile 文件逻辑，例如 `production＆(eu-central | eu-west)`。有关更多详细信息，请参见 [参考指南](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/core.html#beans-definition-profiles-java)。以下清单显示了三个示例 profile 文件：

```xml
<springProfile name="staging">
    <!-- configuration to be enabled when the "staging" profile is active -->
</springProfile>

<springProfile name="dev | staging">
    <!-- configuration to be enabled when the "dev" or "staging" profiles are active -->
</springProfile>

<springProfile name="!production">
    <!-- configuration to be enabled when the "production" profile is not active -->
</springProfile>
```

##### 环境属性

使用 `<springProperty>` 标签可以暴露 Spring  `Environment` 中的属性，以便在 Logback 中使用。如果您想从 Logback 配置中访问 `application.properties` 文件中的值，则这样做很有用。该标签的工作方式类似于 Logback 的标准 `<property>` 标签。但是，不是指定直接的 `value`，而是指定属性的 `source`（来自 `Environment`）。如果您需要将属性存储在 `local` 范围之外的其他地方，则可以使用 `scope` 属性。如果需要后备值（如果未在`Environment` 中设置该属性），则可以使用 `defaultValue` 属性。以下示例显示如何公开在 Logback 中使用的属性：

```xml
<springProperty scope="context" name="fluentHost" source="myapp.fluentd.host"
        defaultValue="localhost"/>
<appender name="FLUENT" class="ch.qos.logback.more.appenders.DataFluentAppender">
    <remoteHost>${fluentHost}</remoteHost>
    ...
</appender>
```

> 必须在短横线分隔形式下指定 `source`（例如 `my.property-name`）。但是，可以使用宽松的规则将属性添加到 `Environment` 中。

