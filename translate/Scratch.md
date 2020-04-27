#### 6.3.1. 支持的操作系统

默认脚本支持大部分的 Linux 发布版，在 CentOS 和 Ubuntu 上测试过。其他平台，比如 OS X 和 FreeBSD，需要使用自定义的 `embeddedLaunchScript`。

#### 6.3.2. Unix/Linux 服务

Spring Boot 应用可以很容易地作为 Unix/Linux 服务启动，通过使用 `init.d` 或者 `systemd`。

##### 安装为 `init.d` 服务 (System V)

如果你配置 Spring Boot 的 Maven 或者 Gradle 插件来产生 [fully executable jar](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-install)，你并没有使用自定义 `embeddedLaunchScript`，你的应用就可以作为 `init.d` 服务使用。要做到这一点，链接该 jar 倒 `init.d` 以支持标准的 `start`， `stop`， `restart`， 以及 `status` 命令。

脚本支持以下特性：

- 以拥有 jar 文件的用户身份启动服务
- 通过使用 `/var/run/<appname>/<appname>.pid` 跟踪应用的 PID 
- 将控制台日志写入 `/var/log/<appname>.log`

假定你的应用安装在 `/var/myapp`，为了将其作为 `init.d` 服务，创建链接，如下：

```
$ sudo ln -s /var/myapp/myapp.jar /etc/init.d/myapp
```

一旦安装，你可以通过通用方式启动和关闭该服务。比如，在基于 Debian 的系统上，你可以通过下面的命令启动它：

```
$ service myapp start
```

> 如果应用没有启动，检查写入 `/var/log/<appname>.log` 的日志。

您还可以使用标准操作系统工具将应用程序标记为自动启动。例如，在 Debian 上，您可以使用以下命令：

```
$ update-rc.d myapp defaults <priority>
```