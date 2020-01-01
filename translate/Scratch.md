#### 3.8.3. LiveReload

`spring-boot-devtools` 模块包含一个内置的 LiveReload 服务器，可以在资源发生变化时用来触发浏览器刷新。来自 [livereload.com](http://livereload.com/extensions/) 的 LiveReload 浏览器插件对 Chrome、Firefox 和 Safari 浏览器开放使用。

如果你不想在应用运行时启动 LiveReload 服务器，你可以将 `spring.devtools.livereload.enabled` 属性设置为 `false`。

> 你可以每次运行一个 LiveReload 服务器。在启动你的应用之前，确保没有其它的 LiveReload 服务器在运行。如果你从 IDE 启动多个应用实例，只有第一个拥有 LiveReload 支持。

#### 3.8.4. 全局设定

你可以通过将以下任意文件添加到 `$HOME/.config/spring-boot` 文件夹下来进行开发者工作的全局配置：

1. `spring-boot-devtools.properties`
2. `spring-boot-devtools.yaml`
3. `spring-boot-devtools.yml`

所有添加到这些文件中的属性都会被应用于你的机器上所有使用开发者工具的 Spring Boot 应用。比如，为了配置重启始终使用 [trigger file](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart-triggerfile)，你可以添加如下属性：

**~/.config/spring-boot/spring-boot-devtools.properties**

```properties
spring.devtools.restart.trigger-file=.reloadtrigger
```

> 如果开发者工具配置文件没有在 `$HOME/.config/spring-boot` 路径下找到，则会在 `$HOME` 根目录下搜索存在的 `.spring-boot-devtools.properties` 文件。这就允许你在不支持 `$HOME/.config/spring-boot` 配置文件路径的老版本 Spring Boot 应用之间共享开发者工具全局配置。

> 在上述文件中激活的配置文件不会影响 [特定于配置文件的配置文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties) 的加载。

#### 3.8.5. 远程应用

Spring Boot 开发人员工具不仅限于本地开发。远程运行应用程序时，您还可以使用多种功能。启用远程支持是可选的，因为启用它可能会带来安全风险。仅当在受信任的网络上运行或使用 SSL 保护时，才应启用它。如果这两个选项都不可用，则不应使用 DevTools 的远程支持。永远不要在生产部署上启用支持。

要启用它，您需要确保重新打包的档案中包含 `devtools`，如以下清单所示：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <excludeDevtools>false</excludeDevtools>
            </configuration>
        </plugin>
    </plugins>
</build>
```

然后您需要设置 `spring.devtools.remote.secret` 属性。像任何重要的密码或机密一样，该值应唯一且强壮，以免被猜测或强行使用。

远程 devtools 支持分为两部分：接受连接的服务器端端点和在 IDE 中运行的客户端应用程序。设置 `spring.devtools.remote.secret` 属性后，服务器组件自动启用。客户端组件必须手动启动。

##### 运行远程客户端应用

远程客户端应用程序旨在在您的 IDE 中运行。您需要使用与您连接到的远程项目相同的类路径来运行 `org.springframework.boot.devtools.RemoteSpringApplication`。该应用程序的唯一必需参数是它连接到的远程 URL。

例如，如果您使用的是 Eclipse 或 STS，并且有一个名为 `my-app` 的项目已部署到 Cloud Foundry，则可以执行以下操作：

- 从“运行”菜单中选择“运行配置...”。

- 创建一个新的 Java 应用程序“启动配置”。

- 选择 `my-app` 项目。

- 使用 `org.springframework.boot.devtools.RemoteSpringApplication` 作为主类。

- 将 `https://myapp.cfapps.io` （或任何远程URL）添加到“程序参数”。

正在运行的远程客户端可能类似于以下清单：

```
  .   ____          _                                              __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _          ___               _      \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` |        | _ \___ _ __  ___| |_ ___ \ \ \ \
 \\/  ___)| |_)| | | | | || (_| []::::::[]   / -_) '  \/ _ \  _/ -_) ) ) ) )
  '  |____| .__|_| |_|_| |_\__, |        |_|_\___|_|_|_\___/\__\___|/ / / /
 =========|_|==============|___/===================================/_/_/_/
 :: Spring Boot Remote :: 2.2.2.RELEASE

2015-06-10 18:25:06.632  INFO 14938 --- [           main] o.s.b.devtools.RemoteSpringApplication   : Starting RemoteSpringApplication on pwmbp with PID 14938 (/Users/pwebb/projects/spring-boot/code/spring-boot-project/spring-boot-devtools/target/classes started by pwebb in /Users/pwebb/projects/spring-boot/code)
2015-06-10 18:25:06.671  INFO 14938 --- [           main] s.c.a.AnnotationConfigApplicationContext : Refreshing org.springframework.context.annotation.AnnotationConfigApplicationContext@2a17b7b6: startup date [Wed Jun 10 18:25:06 PDT 2015]; root of context hierarchy
2015-06-10 18:25:07.043  WARN 14938 --- [           main] o.s.b.d.r.c.RemoteClientConfiguration    : The connection to http://localhost:8080 is insecure. You should use a URL starting with 'https://'.
2015-06-10 18:25:07.074  INFO 14938 --- [           main] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2015-06-10 18:25:07.130  INFO 14938 --- [           main] o.s.b.devtools.RemoteSpringApplication   : Started RemoteSpringApplication in 0.74 seconds (JVM running for 1.105)
```

> 因为远程客户端使用与真实应用程序相同的类路径，所以它可以直接读取应用程序属性。这就是读取 `spring.devtools.remote.secret` 属性并将其传递给服务器进行身份验证的方式。

> 建议始终使用 `https://` 作为连接协议，以便对流量进行加密并且确保密码不能被截获。

> 如果您需要使用代理访问远程应用程序，请配置 `spring.devtools.remote.proxy.host` 和 `spring.devtools.remote.proxy.port` 属性。

##### 远程更新

远程客户端以与 [本地重新启动](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart)  相同的方式监视应用程序类路径的更改。任何更新的资源都会推送到远程应用程序，并且（*如果需要*）会触发重新启动。如果您迭代使用本地没有的云服务的功能，这将很有帮助。通常，远程更新和重新启动比完整的重建和部署周期快得多。

> 仅在远程客户端正在运行时监视文件。如果在启动远程客户端之前更改文件，则不会将其推送到远程服务器。

##### 配置文件系统监视器

[FileSystemWatcher](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-devtools/src/main/java/org/springframework/boot/devtools/filewatch/FileSystemWatcher.java) 的工作方式是按一定时间间隔轮询类更改，然后等待预定义的静默期以确保没有更多更改。然后将更改上传到远程应用程序。在更改较慢的开发环境中，可能会发生静默期不够的情况，并且类中的更改可能会分为几批。第一批类更改上传后，服务器将重新启动。由于服务器正在重新启动，因此下一批不能发送到应用程序。

这通常通过 `RemoteSpringApplication` 日志中的警告来证明，该警告关于无法上载某些类以及随后的重试。但是，这也可能导致应用程序代码不一致，并且在上传第一批更改后无法重新启动。

如果您经常观察到此类问题，请尝试将 `spring.devtools.restart.poll-interval` 和 `spring.devtools.restart.quiet-period` 参数增加到适合您的开发环境的值：

```properties
spring.devtools.restart.poll-interval=2s
spring.devtools.restart.quiet-period=1s
```

现在每 2 秒轮询一次受监视的 `classpath` 文件夹以进行更改，并保持 1 秒钟的静默时间以确保没有其他类更改。

### 3.9. Packaging Your Application for Production

Executable jars can be used for production deployment. As they are self-contained, they are also ideally suited for cloud-based deployment.

For additional “production ready” features, such as health, auditing, and metric REST or JMX end-points, consider adding `spring-boot-actuator`. See *Spring Boot Actuator: Production-ready Features* for details.

### 3.10. What to Read Next

You should now understand how you can use Spring Boot and some best practices that you should follow. You can now go on to learn about specific *Spring Boot features* in depth, or you could skip ahead and read about the “[production ready](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready)” aspects of Spring Boot.