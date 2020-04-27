##### 安装为 `systemd` 服务

`systemd` 是S ystem V init 系统的后继产品，现在被许多现代 Linux 发行版使用。尽管您可以继续将 `init.d` 脚本与 `systemd` 一起使用，但也可以通过使用 `systemd` “service” 脚本来启动 Spring Boot 应用程序。

假设您在 `/var/myapp` 中安装了一个 Spring Boot 应用程序，要将 Spring Boot 应用程序作为 `systemd` 服务安装，请创建一个名为 `myapp.service` 的脚本并将其放置在 `/etc/systemd/system` 目录。以下脚本提供了一个示例：

```
[Unit]
Description=myapp
After=syslog.target

[Service]
User=myapp
ExecStart=/var/myapp/myapp.jar
SuccessExitStatus=143

[Install]
WantedBy=multi-user.target
```

> 记得要修改你的应用的 `Description`， `User`，以及 `ExecStart` 字段。

>  `ExecStart` 字段并未声明脚本动作命令，这意味着默认使用 `run` 命令。

请注意，与作为 `init.d` 服务运行时不同，运行应用程序的用户，PID 文件和控制台日志文件均由 `systemd` 本身管理，因此必须通过使用 ‘service’ 脚本。有关更多详细信息，请查阅 [服务单元配置手册页](https://www.freedesktop.org/software/systemd/man/systemd.service.html) 。

要将应用程序标记为在系统启动时自动启动，请使用以下命令：

```
$ systemctl enable myapp.service
```

参考 `man systemctl` 了解更多细节。