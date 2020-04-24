#### 6.2.2. Heroku

Heroku 是另一个流行的 PaaS 平台。要自定义 Heroku 构建，请提供一个 `Procfile`，该文件提供了部署应用程序所需的内容。Heroku 为 Java 应用程序分配一个 `port` 以供使用，然后确保到外部 URI 的路由起作用。

您必须配置您的应用程序以侦听正确的端口。以下示例显示了我们的入门 REST 应用程序的 `Procfile`：

```
web: java -Dserver.port=$PORT -jar target/demo-0.0.1-SNAPSHOT.jar
```

Spring Boot 使 `-D` 参数作为可从 Spring `Environment` 实例访问的属性。 `server.port` 配置属性被馈送到内置的 Tomcat，Jetty 或 Undertow 实例，然后在启动时使用该端口。 `$PORT` 环境变量是由 Heroku PaaS 分配给我们的。

这应该是您需要的一切。Heroku 部署最常见的部署工作流程是将代码 `git push` 到生产中，如以下示例所示：

```
$ git push heroku master

Initializing repository, done.
Counting objects: 95, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (78/78), done.
Writing objects: 100% (95/95), 8.66 MiB | 606.00 KiB/s, done.
Total 95 (delta 31), reused 0 (delta 0)

-----> Java app detected
-----> Installing OpenJDK 1.8... done
-----> Installing Maven 3.3.1... done
-----> Installing settings.xml... done
-----> Executing: mvn -B -DskipTests=true clean install

       [INFO] Scanning for projects...
       Downloading: https://repo.spring.io/...
       Downloaded: https://repo.spring.io/... (818 B at 1.8 KB/sec)
        ....
       Downloaded: https://s3pository.heroku.com/jvm/... (152 KB at 595.3 KB/sec)
       [INFO] Installing /tmp/build_0c35a5d2-a067-4abc-a232-14b1fb7a8229/target/...
       [INFO] Installing /tmp/build_0c35a5d2-a067-4abc-a232-14b1fb7a8229/pom.xml ...
       [INFO] ------------------------------------------------------------------------
       [INFO] BUILD SUCCESS
       [INFO] ------------------------------------------------------------------------
       [INFO] Total time: 59.358s
       [INFO] Finished at: Fri Mar 07 07:28:25 UTC 2014
       [INFO] Final Memory: 20M/493M
       [INFO] ------------------------------------------------------------------------

-----> Discovering process types
       Procfile declares types -> web

-----> Compressing... done, 70.4MB
-----> Launching... done, v6
       https://agile-sierra-1405.herokuapp.com/ deployed to Heroku

To git@heroku.com:agile-sierra-1405.git
 * [new branch]      master -> master
```

您的应用程序现在应该已经在 Heroku 上启动并运行了。有关更多详细信息，请参阅 [将 Spring Boot 应用程序部署到 Heroku](https://devcenter.heroku.com/articles/deploying-spring-boot-apps-to-heroku)。

