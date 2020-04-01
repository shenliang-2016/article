#### 4.28.2. 定位自动配置候选者

Spring Boot 会检查你发布的 jar 中是否存在 `META-INF/spring.factories` 文件。该文件应该在 `EnableAutoConfiguration` 键下列出你的配置类，如下面例子所示：

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.mycorp.libx.autoconfigure.LibXAutoConfiguration,\
com.mycorp.libx.autoconfigure.LibXWebAutoConfiguration
```

> 自动配置必须通过唯一的特殊方式加载。确保它们定义在特定的包空间下，使得它们永远不会成为组件扫描的目标。进一步地，自动配置类不应该开启组件扫描发现附加组件。可以使用特定的 `@Import` 来替代。

如果你的配置需要按照特定顺序应用，你可以使用 [`@AutoConfigureAfter`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/AutoConfigureAfter.java) 或者 [`@AutoConfigureBefore`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/AutoConfigureBefore.java) 注解。比如，如果你提供了特定与 web 的配置，该配置类就需要在 `WebMvcAutoConfiguration` 之后应用。

如果你希望排序某些互相完全不了解的自动配置，你也可以使用 `@AutoConfigureOrder`。该注解提供了与普通的 `@Order` 注解相同的语义，但是未自动配置类提供了专用的顺序。