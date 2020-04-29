### 7.3. 使用 Groovy Beans DSL 开发应用程序

Spring Framework 4.0 has native support for a `beans{}` “DSL” (borrowed from [Grails](https://grails.org/)), and you can embed bean definitions in your Groovy application scripts by using the same format. This is sometimes a good way to include external features like middleware declarations, as shown in the following example:

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

You can mix class declarations with `beans{}` in the same file as long as they stay at the top level, or, if you prefer, you can put the beans DSL in a separate file.

### 7.4. Configuring the CLI with `settings.xml`

The Spring Boot CLI uses Aether, Maven’s dependency resolution engine, to resolve dependencies. The CLI makes use of the Maven configuration found in `~/.m2/settings.xml` to configure Aether. The following configuration settings are honored by the CLI:

- Offline
- Mirrors
- Servers
- Proxies
- Profiles
  - Activation
  - Repositories
- Active profiles

See [Maven’s settings documentation](https://maven.apache.org/settings.html) for further information.

### 7.5. What to Read Next

There are some [sample groovy scripts](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/samples) available from the GitHub repository that you can use to try out the Spring Boot CLI. There is also extensive Javadoc throughout the [source code](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/src/main/java/org/springframework/boot/cli).

If you find that you reach the limit of the CLI tool, you probably want to look at converting your application to a full Gradle or Maven built “Groovy project”. The next section covers Spring Boot’s "[Build tool plugins](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#build-tool-plugins)", which you can use with Gradle or Maven.