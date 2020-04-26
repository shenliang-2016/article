### 6.3. 安装 Spring Boot 应用

除了通过使用 `java -jar` 运行 Spring Boot 应用程序之外，还可以为 Unix 系统制作完全可执行的应用程序。完全可执行的 jar 可以像其他任何可执行二进制文件一样执行，也可以 [通过 `init.d` 或 `systemd` 注册](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-service)。这使得在普通生产环境中安装和管理 Spring Boot 应用程序变得非常容易。

> 完全可执行的 jar 通过在文件的开头嵌入一个额外的脚本来工作。当前，某些工具不接受此格式，因此您可能无法始终使用此技术。例如，`jar -xf` 可能会无声地提取无法完全执行的 jar 或 war。建议仅当您打算直接执行 jar 或 war 时才使其完全可执行，而不是使用 `java -jar` 来运行它或将其部署到 servlet 容器中。

> 不能使 zip64 格式的 jar 文件完全可执行。尝试这样做将导致一个 jar 文件，当直接执行该文件或使用 `java -jar` 时，该文件被报告为已损坏。包含一个或多个 zip64 格式嵌套 jar 的标准格式 jar 文件可以完全执行。

要使用 Maven 创建“完全可执行”的 jar，请使用以下插件配置：

```xml
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <executable>true</executable>
    </configuration>
</plugin>
```

下面的例子展示了等效的 Gradle 配置：

```groovy
bootJar {
    launchScript()
}
```

然后，您可以通过键入 `./my-application.jar` （其中 `my-application` 是你的组件的名称）来运行您的应用程序。包含 jar 的目录用作应用程序的工作目录。