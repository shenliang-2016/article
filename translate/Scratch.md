#### 6.2.6. Google Cloud

Google Cloud 有几种可用于启动 Spring Boot 应用程序的选项。最容易上手的可能是 App Engine，但您也可以找到在 Container Engine 的容器中或 Compute Engine 的虚拟机上运行 Spring Boot 应用的方法。

要在 App Engine 中运行，您可以先在用户界面中创建一个项目，该项目将为您设置一个唯一的标识符，并还设置 HTTP 路由。将 Java 应用程序添加到项目中，然后将其保留为空，然后使用 [Google Cloud SDK](https://cloud.google.com/sdk/install) 从命令行或 CI 将 Spring Boot 应用程序推送到该插槽中建立。

App Engine Standard 要求您使用 WAR 包装。请按照 [这些步骤](https://github.com/GoogleCloudPlatform/getting-started-java/blob/master/appengine-standard-java8/springboot-appengine-standard/README.md) 将 App Engine Standard 应用程序部署到 Google Cloud。

另外，App Engine Flex 要求您创建一个 `app.yaml` 文件来描述您的应用程序所需的资源。通常，您将此文件放在 `src/main/appengine` 中，它应类似于以下文件：

```yaml
service: default

runtime: java
env: flex

runtime_config:
  jdk: openjdk8

handlers:
- url: /.*
  script: this field is required, but ignored

manual_scaling:
  instances: 1

health_check:
  enable_health_check: False

env_variables:
  ENCRYPT_KEY: your_encryption_key_here
```

您可以通过将项目 ID 添加到构建配置中来部署应用程序（例如，使用 Maven 插件），如以下示例所示：

```xml
<plugin>
    <groupId>com.google.cloud.tools</groupId>
    <artifactId>appengine-maven-plugin</artifactId>
    <version>1.3.0</version>
    <configuration>
        <project>myproject</project>
    </configuration>
</plugin>
```

然后使用 `mvn appengine:deploy` 部署(如果你需要首先进行身份认证，则构建将会失败)。