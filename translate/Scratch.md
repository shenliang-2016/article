### 6.2. 部署到云端

Spring Boot 的可执行 jar 已为大多数流行的云 PaaS（平台即服务）提供商准备。这些提供者往往要求您“自带容器”。他们管理应用进程（不是专门用于 Java 应用程序），因此他们需要一个中间层，以使您的应用程序适配运行进程的“云”概念。

两家受欢迎的云提供商，Heroku 和 Cloud Foundry，采用了“ buildpack”方法。 buildpack 将您部署的代码包装在*启动*应用程序所需的任何内容中。它可能是一个 JDK，可能是对 Java，嵌入式 Web 服务器或成熟的应用程序服务器的调用。一个 buildpack 是可插拔的，但是理想情况下，您应该能够通过尽可能少的自定义来获得它。这减少了您无法控制的功能的占用空间。它最大程度地减少了开发和生产环境之间的差异。

理想情况下，您的应用程序像 Spring Boot 可执行 jar 一样，具有打包运行所需的一切。

在本节中，我们研究如何获取在“入门”部分中启动并运行的 [我们开发的简单应用程序](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-first-application) 。