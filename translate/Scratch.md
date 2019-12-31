#### 3.8.2. Automatic Restart

每当类路径上的文件改变时，使用 `spring-boot-devtools` 的应用程序会自动重启。在 IDE 中工作时，这可能是一个有用的功能，因为它为代码更改提供了非常快速的反馈循环。默认情况下，将监视类路径上指向文件夹的任何条目的更改。请注意，某些资源，例如静态资产和视图模板，[不需要重启应用](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart-exclude)。

> 触发重启
>
> 当 DevTools 监视类路径资源时，触发重启的唯一方法是更新类路径。导致类路径更新的方式取决于所使用的 IDE。在 Eclipse 中，保存修改后的文件将导致类路径被更新并触发重新启动。在 IntelliJ IDEA 中，构建项目（`Build +→+ Build Project`）具有相同的效果。

> 只要启用了分叉，您还可以使用受支持的构建插件（Maven 和 Gradle）启动应用程序，因为 DevTools 需要隔离的应用程序类加载器才能正常运行。默认情况下，Gradle 和 Maven 插件会分叉应用程序进程。

>使用 LiveReload 时，自动重新启动效果很好。详情请参阅 [LiveReload](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-livereload) 部分。如果使用 JRebel，则禁用自动重新启动，而支持动态类重新加载。其他 devtools 功能（例如 LiveReload 和属性覆盖）仍可以使用。

> DevTools 依赖于应用程序上下文的关闭挂钩在重新启动期间将其关闭。如果禁用了关机挂钩，它将无法正常工作 (`SpringApplication.setRegisterShutdownHook(false)`)。

> 在确定类路径上的条目是否应在更改后触发重新启动时，DevTools 会自动忽略名为 `spring-boot`，`spring-boot-devtools`，`spring-boot-autoconfigure`，`spring-boot-actuator` 以及 `spring-boot-starter`。

> DevTools 需要自定义 `ApplicationContext` 使用的 `ResourceLoader`。如果您的应用程序已经提供了，它将被包装。不支持在 `ApplicationContext` 上直接覆盖 `getResource` 方法。

> 重新启动与重新加载
>
> Spring Boot 提供的重启技术通过使用两个类加载器来工作。不变的类（例如，来自第三方 jar 的类）将被加载到*base*类加载器中。您正在开发的类将加载到*restart*类加载器中。重新启动应用程序后，将丢弃*restart*类加载器，并创建一个新的类加载器。这种方法意味着应用程序的重启通常比“冷启动”要快得多，因为*bas*类加载器已经可用并已填充。
>
> 如果发现重新启动不适合您的应用程序，或者遇到类加载问题，则可以考虑从 ZeroTurnaround 重新加载诸如 [JRebel](https://jrebel.com/software/jrebel/) 之类的技术。这些方法通过在加载类时重写类来使其更易于重新加载。

##### 根据条件解析纪录变更

默认情况下，每次应用程序重新启动时，都会记录一个报告，其中显示了条件评估增量。该报告显示了您进行更改（例如添加或删除Bean以及设置配置属性）时对应用程序自动配置的更改。

要禁用报告的日志记录，请设置以下属性：

```
spring.devtools.restart.log-condition-evaluation-delta=false
```

##### 排除资源

某些资源在更改时不一定需要触发重新启动。例如，Thymeleaf 模板可以就地编辑。默认情况下，更改 `/META-INF/maven`，`/META-INF/resources`，`/resources`，`/static`，`/public` 或 `/templates` 中的资源不会触发重新启动，但是确实会触发 [实时重新加载](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-livereload)。如果要自定义这些排除项，可以使用 `spring.devtools.restart.exclude` 属性。例如，要仅排除 `/static` 和 `/public`，可以设置以下属性：

```
spring.devtools.restart.exclude=static/**,public/**
```

> 如果你想保持默认选项并添加额外的排除配置，使用 `spring.devtools.restart.additional-exclude` 属性。

##### 监控额外路径

当您对不在类路径上的文件进行更改时，您可能希望重新启动或重新加载应用程序。为此，请使用 `spring.devtools.restart.additional-paths` 属性配置其他路径以监视更改。您可以使用 [spring.devtools.restart.exclude](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart-exclude) 属性来控制其他路径下的更改是触发完全重启还是 [实时重新加载](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-livereload)。

##### 关闭重启

如果不想使用重启功能，可以通过使用 `spring.devtools.restart.enabled` 属性来禁用它。在大多数情况下，您可以在 `application.properties` 中设置此属性（这样做仍会初始化重启类加载器，但它不会监视文件更改）。

如果您需要*完全*禁用重启支持（例如，因为它不适用于特定的库），则需要在调用 `SpringApplication.run(…)` 之前将 `Spring.devtools.restart.enabled` `System` 属性设置为 `false`。如以下示例所示：

```java
public static void main(String[] args) {
    System.setProperty("spring.devtools.restart.enabled", "false");
    SpringApplication.run(MyApp.class, args);
}
```

##### 使用触发器文件

如果使用持续编译更改文件的 IDE，则可能更喜欢仅在特定时间触发重新启动。为此，您可以使用“触发文件”，这是一个特殊文件，当您要实际触发重新启动检查时必须对其进行修改。

> 对文件的任何更新都将触发检查，但是只有在 Devtools 检测到有事情要做的情况下，重启才真正发生。

要使用触发文件，请将 `spring.devtools.restart.trigger-file` 属性设置为触发文件的名称（不包括任何路径）。触发文件必须出现在类路径上的某个位置。

例如，如果您的项目具有以下结构：

```
src
+- main
   +- resources
      +- .reloadtrigger
```

 则你的 `trigger-file` 属性应该是：

```properties
spring.devtools.restart.trigger-file=.reloadtrigger
```

此时重启只会发生在 `src/main/resources/.reloadtrigger` 文件更新之后。

> 你可能会想将 `spring.devtools.restart.trigger-file` 设置为一个 [global setting](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-globalsettings)，从而你的所有项目行为都会保持一致。

某些 IDE 具有使您不必手动更新触发器文件的功能。 [用于Eclipse的Spring工具](https://spring.io/tools) 和 [IntelliJ IDEA（旗舰版）](https://www.jetbrains.com/idea/) 都具有这种支持。 使用 Spring Tools，您可以从控制台视图使用“重新加载”按钮（只要您的“触发文件”被命名为 `.reloadtrigger`）。对于 IntelliJ，您可以按照 [文档说明](https://www.jetbrains.com/help/idea/spring-boot.html#configure-application-update-policies-with-devtools)。

##### 自定义重启类加载器

如之前 [重新启动与重新加载](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-spring-boot-restart-vs-reload) 部分中所述，重新启动功能是通过使用两个类加载器实现的。对于大多数应用程序，此方法效果很好。但是，有时可能会导致类加载问题。

默认情况下，IDE 中任何打开的项目都使用“重新启动”类加载器加载，而任何常规的 `.jar` 文件都使用“基本”类加载器加载。如果您在多模块项目上工作，并且并非每个模块都导入到 IDE 中，则可能需要自定义内容。为此，您可以创建一个 `META-INF/spring-devtools.properties` 文件。

`spring-devtools.properties` 文件可以包含以 `restart.exclude` 和 `restart.include` 为前缀的属性。 `include` 元素是应提升到“重新启动”类加载器中的项目，而 `exclude` 元素是应下推到“基本”类加载器中的项目。该属性的值是应用于类路径的正则表达式模式，如以下示例所示：

```properties
restart.exclude.companycommonlibs=/mycorp-common-[\\w\\d-\.]+\.jar
restart.include.projectcommon=/mycorp-myproj-[\\w\\d-\.]+\.jar
```

> 所有属性键都必须是唯一的。只要属性以 `restart.include` 或 `restart.exclude` 开头即可。

> 所有来自类路径的 `META-INF/spring-devtools.properties` 都被加载。您可以将文件打包到项目内部，也可以打包到项目使用的库中。

##### 周知的局限性

重新启动功能不适用于使用标准的 `ObjectInputStream` 反序列化的对象。如果您需要反序列化数据，则可能需要结合使用 Spring 的 `ConfigurableObjectInputStream` 和 `Thread.currentThread().getContextClassLoader()`。

不幸的是，一些第三方库在不考虑上下文类加载器的情况下反序列化。 如果发现这样的问题，则需要向原始作者请求修复。

