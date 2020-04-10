#### 5.2.9. 应用信息

应用信息暴露收集自所有定义在你的 `ApplicationContext` 中的 [`InfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/InfoContributor.java) beans 的各种信息。Spring Boot 包含大量自动配置的 `InfoContributor` beans，你也可以编写自己的。

##### 自动配置的信息贡献者

下面的 `InfoContributor` beans 在合适的时候由 Spring Boot 自动配置：

| Name                                                         | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`EnvironmentInfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/EnvironmentInfoContributor.java) | 暴露所有来自 `Environment` 的位于 `info` 键下的键。          |
| [`GitInfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/GitInfoContributor.java) | 暴露 git 信息，如果 `git.properties` 文件可用。              |
| [`BuildInfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/BuildInfoContributor.java) | Exposes build information if a `META-INF/build-info.properties` file is available. |

> It is possible to disable them all by setting the `management.info.defaults.enabled` property.