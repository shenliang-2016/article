#### 6.2.4. Amazon Web Services (AWS)

Amazon Web Services 提供多种方法安装 Spring Boot 应用，可以是传统 web 应用的 war 包形式，也可以是包含内置 web 服务器的可执行 jar 文件形式。选项包括：

- AWS Elastic Beanstalk
- AWS Code Deploy
- AWS OPS Works
- AWS Cloud Formation
- AWS Container Registry

每种都有不同的特性和评价模型。本文档中，我们只描述最简单的选项： AWS Elastic Beanstalk。

##### AWS Elastic Beanstalk

如官方文档 [Elastic Beanstalk Java guide](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_Java.html) 中所述，有两种部署 java 应用的选择。可以选择使用 “Tomcat Platform” 或者 “Java SE platform”。

###### 使用 Tomcat Platform

这种方式将 Spring Boot 项目打包成 war 文件。不需要任何特殊配置。你只需要按照官方向导操作即可。

###### 使用 Java SE Platform

这种方式将 Spring Boot 项目打包成 jar 文件并执行内置的 web 容器。Elastic Beanstalk 环境运行一个 nginx 实例监听 80 端口以代理运行在 5000 端口上的实际的应用。想要配置它，添加下列内容到你的 `application.properties` 文件：

```
server.port=5000
```

> 上传二进制文件而不是源代码
>
> 默认情况下，Elastic Beanstalk 上传源代码并在 AWS 中编译它们。不过，还是上传二进制文件。为了做到这一点，添加类似于下面的内容到你的 `.elasticbeanstalk/config.yml` 文件中：
>
> ```xml
> deploy:
>     artifact: target/demo-0.0.1-SNAPSHOT.jar
> ```

> 通过设定环境类型降低资源消耗
>
> 默认情况下，Elastic Beanstalk 环境是负载均衡的。负载均衡将会带来显著的资源消耗。为了避免此类资源消耗，将环境类型设定为 “Single instance”，如 [the Amazon documentation](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environments-create-wizard.html#environments-create-wizard-capacity) 中所述。你也可以通过使用 CLI 命令创建单实例环境：
>
> ```
> eb create -s
> ```

##### 总结

这是使用 AWS 的最简单方法之一，但还有更多内容需要介绍，例如如何将 Elastic Beanstalk 集成到任何 CI / CD 工具中，如何使用 Elastic Beanstalk Maven 插件而不是 CLI 等等。有 [博客帖子](https://exampledriven.wordpress.com/2017/01/09/spring-boot-aws-elastic-beanstalk-example/) 更加详细地介绍了这些主题。