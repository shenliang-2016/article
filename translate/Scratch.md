保护 `init.d` 服务

> 以下是一组有关如何保护作为 `init.d` 服务运行的 Spring Boot 应用程序的准则。它并不旨在详尽列出增强应用程序及其运行环境所需的所有工作。

当以 root 身份执行时（例如使用 root 来启动 `init.d` 服务时），默认的可执行脚本以 `RUN_AS_USER` 环境变量中指定的用户身份运行应用程序。如果未设置环境变量，则使用拥有 jar 文件的用户。您永远不要以 root 用户身份运行 Spring Boot 应用程序，因此 `RUN_AS_USER` 不应该是 root 用户，而应用程序的 jar 文件也不应归 root 用户所有。而是创建一个特定的用户来运行您的应用程序，并设置环境变量 `RUN_AS_USER` 或使用 `chown` 使其成为 jar 文件的所有者，如以下示例所示：

```
$ chown bootapp:bootapp your-app.jar
```

在这种情况下，默认的可执行脚本以 `bootapp` 用户身份运行应用程序。

> 为了减少应用程序的用户帐户被盗的机会，您应该考虑阻止它使用登录 shell。例如，您可以将帐户的 shell 程序设置为 `/usr/sbin/nologin`。

您还应该采取措施防止修改应用程序的 jar 文件。首先，配置其权限，使其不能被写入，只能由其所有者读取或执行，如以下示例所示：

```
$ chmod 500 your-app.jar
```

其次，如果您的应用程序或运行该应用程序的帐户受到威胁，您还应采取措施限制损害。如果攻击者确实获得了访问权限，则他们可以使 jar 文件可写并更改其内容。防止这种情况发生的一种方法是通过使用 `chattr` 使它不变，如以下示例所示：

```
$ sudo chattr +i your-app.jar
```

这将阻止任何用户（包括 root 用户）修改 jar。

如果使用 root 来控制应用程序的服务，并且您 [使用`.conf`文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-script-customization-conf-file) 以自定义其启动，root 用户读取并评估 `.conf` 文件。应该相应地对其进行保护。使用 `chmod` 以便文件只能由所有者读取，并使用 `chown` 使 root 用户成为所有者，如以下示例所示：

```
$ chmod 400 your-app.conf
$ sudo chown root:root your-app.conf
```