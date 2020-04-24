#### 6.2.1. Cloud Foundry

如果未指定其他构建包，Cloud Foundry 将提供默认的构建包。 Cloud Foundry [Java buildpack](https://github.com/cloudfoundry/java-buildpack) 对 Spring 应用程序（包括 Spring Boot）具有出色的支持。您可以部署独立的可执行 jar 应用程序以及传统的 `.war` 打包应用程序。

一旦构建了应用程序（例如，使用 `mvn clean package` ），并 [安装了cf命令行工具](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html) ，使用 `cf push` 命令部署您的应用程序，替换为已编译的 `.jar` 的路径。在推送应用程序之前，请确保 [使用您的`cf`命令行客户端登录](https://docs.cloudfoundry.org/cf-cli/getting-started.html#login)。下面的行显示了使用 `cf push` 命令来部署应用程序：

```
$ cf push acloudyspringtime -p target/demo-0.0.1-SNAPSHOT.jar
```

> 在前面的示例中，我们用 `acloudyspringtime` 替换为 `cf` 作为应用程序名称的任何值。

参考 [`cf push` 文档](https://docs.cloudfoundry.org/cf-cli/getting-started.html#push) 了解更多选项。如果该目录下存在 Cloud Foundry [`manifest.yml`](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html) 文件，它将会生效。

此时， `cf` 开始更新你的应用，产生类似下面的输出：

```
Uploading acloudyspringtime... OK
Preparing to start acloudyspringtime... OK
-----> Downloaded app package (8.9M)
-----> Java Buildpack Version: v3.12 (offline) | https://github.com/cloudfoundry/java-buildpack.git#6f25b7e
-----> Downloading Open Jdk JRE 1.8.0_121 from https://java-buildpack.cloudfoundry.org/openjdk/trusty/x86_64/openjdk-1.8.0_121.tar.gz (found in cache)
       Expanding Open Jdk JRE to .java-buildpack/open_jdk_jre (1.6s)
-----> Downloading Open JDK Like Memory Calculator 2.0.2_RELEASE from https://java-buildpack.cloudfoundry.org/memory-calculator/trusty/x86_64/memory-calculator-2.0.2_RELEASE.tar.gz (found in cache)
       Memory Settings: -Xss349K -Xmx681574K -XX:MaxMetaspaceSize=104857K -Xms681574K -XX:MetaspaceSize=104857K
-----> Downloading Container Certificate Trust Store 1.0.0_RELEASE from https://java-buildpack.cloudfoundry.org/container-certificate-trust-store/container-certificate-trust-store-1.0.0_RELEASE.jar (found in cache)
       Adding certificates to .java-buildpack/container_certificate_trust_store/truststore.jks (0.6s)
-----> Downloading Spring Auto Reconfiguration 1.10.0_RELEASE from https://java-buildpack.cloudfoundry.org/auto-reconfiguration/auto-reconfiguration-1.10.0_RELEASE.jar (found in cache)
Checking status of app 'acloudyspringtime'...
  0 of 1 instances running (1 starting)
  ...
  0 of 1 instances running (1 starting)
  ...
  0 of 1 instances running (1 starting)
  ...
  1 of 1 instances running (1 running)

App started
```

祝贺你！应用已经运行起来了！

一旦应用运行起来，你就可以验证应用的状态，通过使用 `cf apps` 命令，如下所示：

```
$ cf apps
Getting applications in ...
OK

name                 requested state   instances   memory   disk   urls
...
acloudyspringtime    started           1/1         512M     1G     acloudyspringtime.cfapps.io
...
```

一旦 Cloud Foundry 确认已经部署了您的应用程序，您就应该能够在给定的 URI 上找到该应用程序。在前面的示例中，您可以在以下位置找到它 `https://acloudyspringtime.cfapps.io/`。

##### 绑定到服务

默认情况下，有关正在运行的应用程序以及服务连接信息的元数据作为环境变量（例如：`$VCAP_SERVICES`）公开给应用程序。做出此架构决定是由于 Cloud Foundry 具有多种语言（可以将任何语言和平台作为 buildpack 支持）。进程范围的环境变量与语言无关。

环境变量并不总是使用最简单的API，因此 Spring Boot 会自动提取它们并将数据平整为可通过 Spring  `Environment` 抽象访问的属性，如以下示例所示：

```java
@Component
class MyBean implements EnvironmentAware {

    private String instanceId;

    @Override
    public void setEnvironment(Environment environment) {
        this.instanceId = environment.getProperty("vcap.application.instance_id");
    }

    // ...

}
```

所有 Cloud Foundry 属性均以 `vcap` 为前缀。您可以使用 `vcap` 属性来访问应用程序信息（例如应用程序的公共 URL）和服务信息（例如数据库凭据）。有关完整的详细信息，请参见 [`CloudFoundryVcapEnvironmentPostProcessor`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/cloud/CloudFoundryVcapEnvironmentPostProcessor.html) Javadoc。

>  [Java CFEnv](https://github.com/pivotal-cf/java-cfenv/) 项目更适合诸如配置数据源之类的任务。

