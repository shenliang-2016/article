## 6. 部署 Spring Boot 应用

在部署应用程序时，Spring Boot 的灵活打包选项提供了很多选择。您可以将 Spring Boot 应用程序部署到各种云平台，容器映像（例如 Docker）或虚拟机/真实机上。

本节介绍一些更常见的部署方案。

### 6.1. 部署到容器

如果从容器中运行应用程序，则可以使用可执行 jar，但是将其解压并以其他方式运行通常也是一个优点。某些 PaaS 实施也可能选择在运行存档之前将其解压缩。例如，Cloud Foundry 以这种方式运行。运行解压缩存档的最简单方法是启动相应的启动器，如下所示：

```
$ jar -xf myapp.jar
$ java org.springframework.boot.loader.JarLauncher
```

实际上，这在启动时（取决于 jar 的大小）比从未解压的存档中运行要快一些。在运行时，您不应期望有任何差异。

解压缩 jar 文件后，您还可以通过使用其“自然”主方法（而不是 ` JarLauncher`）运行应用程序来缩短启动时间。例如：

```
$ jar -xf myapp.jar
$ java -cp BOOT-INF/classes:BOOT-INF/lib/* com.example.MyApplication
```

还可以通过将依赖项作为与应用程序类和资源（通常会更频繁地更改）分开的一层复制到映像中来创建更有效的容器映像。实现这一层分离的方法不止一种。例如，使用 `Dockerfile` 可以将其表示为以下形式：

```
FROM openjdk:8-jdk-alpine AS builder
WORKDIR target/dependency
ARG APPJAR=target/*.jar
COPY ${APPJAR} app.jar
RUN jar -xf ./app.jar

FROM openjdk:8-jre-alpine
VOLUME /tmp
ARG DEPENDENCY=target/dependency
COPY --from=builder ${DEPENDENCY}/BOOT-INF/lib /app/lib
COPY --from=builder ${DEPENDENCY}/META-INF /app/META-INF
COPY --from=builder ${DEPENDENCY}/BOOT-INF/classes /app
ENTRYPOINT ["java","-cp","app:app/lib/*","com.example.MyApplication"]
```

假设上面的 `Dockerfile` 是当前目录，则可以使用 `docker build .`。或可选地指定应用程序 jar 的路径来构建 docker 映像，如以下示例所示：

```
docker build --build-arg APPJAR=path/to/myapp.jar .
```