## 5. Spring Boot Actuator：生产就绪特性

当你把应用发布到生产环境，Spring Boot 包含大量特性帮助你监控和管理你的应用。你可以选择通过使用 HTTP 端点或者 JMX 监控管理你的应用。审计、健康监测、性能指标收集等功能也会自动应用到你的应用。

### 5.1. 启用生产就绪特性

[`spring-boot-actuator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator) 模块提供了所有 Spring Boot 的生产就绪特性。开启这一特性最简单的方法就是添加一个 `spring-boot-starter-actuator` 启动器的依赖。

> Actuator 定义
>
> 执行器是制造业术语，是指用于移动或控制某些物体的机械设备。执行器可以通过很小的变化产生大量的运动。

添加执行器到基于 Maven 的项目，添加下面的启动器依赖：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
</dependencies>
```

对于 Gradle，使用下面的声明：

```groovy
dependencies {
    compile("org.springframework.boot:spring-boot-starter-actuator")
}
```