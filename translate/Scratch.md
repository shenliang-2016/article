#### 4.1.4. 自定义 SpringApplication

如果默认的 `SpringApplication` 不适合你，你可以创建一个本地实例并自定义它。比如，想要关闭横幅，你可以编写：

```java
public static void main(String[] args) {
    SpringApplication app = new SpringApplication(MySpringConfiguration.class);
    app.setBannerMode(Banner.Mode.OFF);
    app.run(args);
}
```

> 传递给 `SpringApplication` 的构造函数参数是 Spring bean 的配置源。在大多数情况下，它们是对 `@Configuration` 类的引用，但它们也可以对 XML 配置或应扫描的包进行引用。

通过使用 `application.properties` 文件配置 `SpringApplication` 是可能的。参考 *Externalized Configuration* 获取更多细节。

配置选项的完整列表，参考 [`SpringApplication` Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/SpringApplication.html) 。

#### 4.1.5. Fluent Builder API

If you need to build an `ApplicationContext` hierarchy (multiple contexts with a parent/child relationship) or if you prefer using a “fluent” builder API, you can use the `SpringApplicationBuilder`.

The `SpringApplicationBuilder` lets you chain together multiple method calls and includes `parent` and `child` methods that let you create a hierarchy, as shown in the following example:

```java
new SpringApplicationBuilder()
        .sources(Parent.class)
        .child(Application.class)
        .bannerMode(Banner.Mode.OFF)
        .run(args);
```

> There are some restrictions when creating an `ApplicationContext` hierarchy. For example, Web components **must** be contained within the child context, and the same `Environment` is used for both parent and child contexts. See the [`SpringApplicationBuilder` Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/builder/SpringApplicationBuilder.html) for full details.