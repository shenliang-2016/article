##### 推导的"抓取"坐标

Spring Boot 通过允许您指定没有组或版本的依赖项（例如，`@Grab('freemarker')`）来扩展 Groovy 的标准 `@Grab` 支持。这样做可以参考 Spring Boot 的默认依赖元数据来推断工件的组和版本。

> 默认元数据与您使用的 CLI 版本相关。仅当您移至新版本的 CLI 时，它才会更改，从而使您可以控制依赖项的版本何时更改。可以在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#appendix-dependency-versions) 中找到。

##### 默认导入语句

为了帮助减少 Groovy 代码的大小，会自动包含几个 `import` 语句。注意，前面的示例如何引用 `@Component`，`@RestController` 和 `@RequestMapping`，而无需使用完全限定的名称或 `import` 语句。

> 许多 Spring 注解无需使用 `import` 语句即可工作。在添加导入之前，请尝试运行您的应用程序以查看失败的原因。

##### 自动 Main 方法

与等效的 Java 应用程序不同，您无需在 Groovy 脚本中包含 `public static void main(String[] args)` 方法。`SpringApplication` 是自动创建的，编译后的代码将作为 `source`。

##### 自定义依赖管理

默认情况下，CLI 在解决 `@Grab` 依赖项时会使用在 `spring-boot-dependencies` 中声明的依赖项管理。可以使用 `@DependencyManagementBom` 注解来配置其他的依赖管理，这些依赖管理将覆盖默认的依赖管理。注解的值应指定一个或多个 Maven BOM 的坐标（`groupId:artifactId:version`）。

例如，考虑以下声明：

```groovy
@DependencyManagementBom("com.example.custom-bom:1.0.0")
```

上面的声明在 Maven repository  `com/example/custom-versions/1.0.0/` 下选取了 `custom-bom-1.0.0.pom` 。

指定多个 BOM 时，它们以声明它们的顺序应用，如下例所示：

```java
@DependencyManagementBom(["com.example.custom-bom:1.0.0",
        "com.example.another-bom:1.0.0"])
```

前面的示例表明， `another-bom` 中的依赖项管理会覆盖 `custom-bom` 中的依赖项管理。

您可以在可以使用 `@Grab` 的任何地方使用 `@DependencyManagementBom`。但是，为了确保依赖性管理的顺序一致，您可以在应用程序中最多使用一次 `@DependencyManagementBom`。