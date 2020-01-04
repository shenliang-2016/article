#### 4.2.3. 应用属性文件

`SpringApplication` 从以下位置的 `application.properties` 文件中加载属性，并将它们添加到 Spring `Environment` 中：

1. 当前路径的 `/config` 子路径
2. 当前路径
3. 类路径的 `/config` 包
4. 类路径根目录

该列表按优先级排序（在列表较高位置定义的属性会覆盖在较低位置定义的属性）。

> 你也可以 [使用 YAML (`.yml`) 文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-yaml) 作为 `.properties` 文件的替代。

如果您不喜欢 `application.properties` 作为配置文件名，则可以通过指定 `spring.config.name` 环境属性来切换到另一个文件名。您还可以通过使用 `spring.config.location` 环境属性（这是目录位置或文件路径的逗号分隔列表）来引用显式位置。下面的示例演示如何指定其他文件名：

```
$ java -jar myproject.jar --spring.config.name=myproject
```

下面的例子展示了如何指定两个位置：

```
$ java -jar myproject.jar --spring.config.location=classpath:/default.properties,classpath:/override.properties
```

