### 7.3. 使用 Groovy Beans DSL 开发应用程序

Spring Framework 4.0 对 `beans{}` “DSL” （从 [Grails](https://grails.org/) 借来）具有本地支持，您可以使用相同的格式将 bean 定义嵌入 Groovy 应用程序脚本中。有时，这是包括外部功能（如中间件声明）的好方法，如以下示例所示：

```groovy
@Configuration(proxyBeanMethods = false)
class Application implements CommandLineRunner {

    @Autowired
    SharedService service

    @Override
    void run(String... args) {
        println service.message
    }

}

import my.company.SharedService

beans {
    service(SharedService) {
        message = "Hello World"
    }
}
```

您可以将类声明与 `beans{}` 混合在同一个文件中，只要它们位于顶层即可；或者，如果愿意，可以将 bean DSL 放在单独的文件中。

### 7.4. 使用 `settings.xml` 配置 CLI 

Spring Boot CLI 使用 Maven 的依赖性解析引擎 Aether 来解决依赖性。 CLI 利用 `~/.m2/settings.xml` 中的 Maven 配置来配置 Aether。CLI 遵循以下配置设置：

- Offline
- Mirrors
- Servers
- Proxies
- Profiles
  - Activation
  - Repositories
- Active profiles

参考 [Maven’s settings documentation](https://maven.apache.org/settings.html) 了解更多信息。

### 7.5. 进一步阅读

您可以使用 GitHub 存储库中的一些 [示例groovy脚本](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/samples) 试用 Spring Boot CLI。 [源代码](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/src/main/java/org/springframework/boot/cli) 中还包含丰富的 javadoc。

如果发现达到了 CLI 工具的极限，则可能需要考虑将应用程序转换为完整的 Gradle 或 Maven 构建的 “Groovy项目”。下一节将介绍 Spring Boot 的 “[构建工具插件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#build-tool-plugins)”  ，可以与 Gradle 或 Maven 一起使用。