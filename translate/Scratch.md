### 4.28.  创建你自己的  Auto-configuration

如果你在一个开发共享类库的公司，或者你在使用开源或者社区类库，你可能希望开发自己的自动配置。自动配置类可以打包成为外部 jars 包，从而仍然能够被 Spring Boot 使用。

自动配置可以配置启动器使用，像那些同样提供了自动配置的典型类库那样。我们首先介绍构建自己的自动配置所需要了解的内容，然后介绍 [创建自定义启动器的必需步骤](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-custom-starter) 。

>  这个 [示例项目](https://github.com/snicoll-demos/spring-boot-master-auto-configuration) 可以展示如何一步步创建一个启动器。

#### 4.28.1. 理解自动配置 Beans

在底层，自动配置由标准的 `@Configuration` 类实现。附加的 `@Conditional` 注解用来限制何时应用自动配置。通常，自动配置类使用 `@ConditionalOnClass` 和 `@ConditionalOnMissingBean` 注解。这能够保证该自动配置只是在相关类没有找到，以及当你没有声明自己的 `@Configuration` 类时。

你可以阅读 [`spring-boot-autoconfigure`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure) 的源码来了解 Spring 提供的 `@Configuration` 类 (参考 [`META-INF/spring.factories`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/resources/META-INF/spring.factories) 文件)。