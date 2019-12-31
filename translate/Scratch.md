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

##### Logging changes in condition evaluation

By default, each time your application restarts, a report showing the condition evaluation delta is logged. The report shows the changes to your application’s auto-configuration as you make changes such as adding or removing beans and setting configuration properties.

To disable the logging of the report, set the following property:

```
spring.devtools.restart.log-condition-evaluation-delta=false
```

##### Excluding Resources

Certain resources do not necessarily need to trigger a restart when they are changed. For example, Thymeleaf templates can be edited in-place. By default, changing resources in `/META-INF/maven`, `/META-INF/resources`, `/resources`, `/static`, `/public`, or `/templates` does not trigger a restart but does trigger a [live reload](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-livereload). If you want to customize these exclusions, you can use the `spring.devtools.restart.exclude` property. For example, to exclude only `/static` and `/public` you would set the following property:

```
spring.devtools.restart.exclude=static/**,public/**
```

> If you want to keep those defaults and *add* additional exclusions, use the `spring.devtools.restart.additional-exclude` property instead.

##### Watching Additional Paths

You may want your application to be restarted or reloaded when you make changes to files that are not on the classpath. To do so, use the `spring.devtools.restart.additional-paths` property to configure additional paths to watch for changes. You can use the `spring.devtools.restart.exclude` property [described earlier](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart-exclude) to control whether changes beneath the additional paths trigger a full restart or a [live reload](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-livereload).

##### Disabling Restart

If you do not want to use the restart feature, you can disable it by using the `spring.devtools.restart.enabled` property. In most cases, you can set this property in your `application.properties` (doing so still initializes the restart classloader, but it does not watch for file changes).

If you need to *completely* disable restart support (for example, because it does not work with a specific library), you need to set the `spring.devtools.restart.enabled` `System` property to `false` before calling `SpringApplication.run(…)`, as shown in the following example:

```java
public static void main(String[] args) {
    System.setProperty("spring.devtools.restart.enabled", "false");
    SpringApplication.run(MyApp.class, args);
}
```

##### Using a Trigger File

If you work with an IDE that continuously compiles changed files, you might prefer to trigger restarts only at specific times. To do so, you can use a “trigger file”, which is a special file that must be modified when you want to actually trigger a restart check.

> Any update to the file will trigger a check, but restart only actually occurs if Devtools has detected it has something to do.

To use a trigger file, set the `spring.devtools.restart.trigger-file` property to the name (excluding any path) of your trigger file. The trigger file must appear somewhere on your classpath.

For example, if you have a project with the following structure:

```
src
+- main
   +- resources
      +- .reloadtrigger
```

Then your `trigger-file` property would be:

```properties
spring.devtools.restart.trigger-file=.reloadtrigger
```

Restarts will now only happen when the `src/main/resources/.reloadtrigger` is updated.

> You might want to set `spring.devtools.restart.trigger-file` as a [global setting](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-globalsettings), so that all your projects behave in the same way.

Some IDEs have features that save you from needing to update your trigger file manually. [Spring Tools for Eclipse](https://spring.io/tools) and [IntelliJ IDEA (Ultimate Edition)](https://www.jetbrains.com/idea/) both have such support. With Spring Tools, you can use the “reload” button from the console view (as long as your `trigger-file` is named `.reloadtrigger`). For IntelliJ, you can follow the [instructions in their documentation](https://www.jetbrains.com/help/idea/spring-boot.html#configure-application-update-policies-with-devtools).

##### Customizing the Restart Classloader

As described earlier in the [Restart vs Reload](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-spring-boot-restart-vs-reload) section, restart functionality is implemented by using two classloaders. For most applications, this approach works well. However, it can sometimes cause classloading issues.

By default, any open project in your IDE is loaded with the “restart” classloader, and any regular `.jar` file is loaded with the “base” classloader. If you work on a multi-module project, and not every module is imported into your IDE, you may need to customize things. To do so, you can create a `META-INF/spring-devtools.properties` file.

The `spring-devtools.properties` file can contain properties prefixed with `restart.exclude` and `restart.include`. The `include` elements are items that should be pulled up into the “restart” classloader, and the `exclude` elements are items that should be pushed down into the “base” classloader. The value of the property is a regex pattern that is applied to the classpath, as shown in the following example:

```properties
restart.exclude.companycommonlibs=/mycorp-common-[\\w\\d-\.]+\.jar
restart.include.projectcommon=/mycorp-myproj-[\\w\\d-\.]+\.jar
```

> All property keys must be unique. As long as a property starts with `restart.include.` or `restart.exclude.` it is considered.

> All `META-INF/spring-devtools.properties` from the classpath are loaded. You can package files inside your project, or in the libraries that the project consumes.

##### Known Limitations

Restart functionality does not work well with objects that are deserialized by using a standard `ObjectInputStream`. If you need to deserialize data, you may need to use Spring’s `ConfigurableObjectInputStream` in combination with `Thread.currentThread().getContextClassLoader()`.

Unfortunately, several third-party libraries deserialize without considering the context classloader. If you find such a problem, you need to request a fix with the original authors.