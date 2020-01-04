#### 4.2.4. 特定于配置文件的属性

除了 `application.properties` 文件之外，还可以使用以下命名约定来定义特定于配置文件的属性： `application-{profile}.properties`。如果没有设置任何活动配置文件，则 `Environment` 具有一组默认配置文件（默认为 `[default]`）。换句话说，如果没有显式激活任何配置文件，则将加载 `application-default.properties` 中的属性。

特定于配置文件的属性是从与标准 `application.properties` 相同的位置加载的，特定于配置文件的文件总是会覆盖非特定文件，无论特定于配置文件的文件位于打包 jar 的内部还是外部。

如果指定了多个配置文件，则采用后赢策略。例如，由 `spring.profiles.active` 属性指定的配置文件会在通过 `SpringApplication` API 配置的配置文件之后添加，因此具有优先权。

> 如果您在 `spring.config.location` 中指定了任何文件，则不考虑这些文件的特定于配置文件的变体。如果您还想使用特定于配置文件的属性，请使用 `spring.config.location` 中的目录。

