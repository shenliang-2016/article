### 3.2. 构建你的代码

Spring Boot 并不强制任何固定形式的代码组织形式。不过，倒是存在一些很有帮助的最佳实践。

#### 3.2.1. 使用 “default” 包

如果一个类不包含 `package` 声明，它就会被认为处于所谓的默认包中。通常情况下应该尽量避免使用默认包。因为它可能导致使用 `@ComponentScan` ，`@ConfigurationPropertiesScan` ，`@EntityScen` ，`@SpringBootApplication` 等注解的 Spring Boot 应用中发生某些问题，因为每个 jar 中的每个类都会被读取。

> 我们推荐你遵循 Java 推荐的包命名传统，使用逆序的域名作为包名（比如，`com.example.project`）

#### 3.2.2. 定位应用主类

我们通常建议您将应用程序主类放在其他类之上的根包中。通常将 [`@SpringBootApplication` 注解](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-using-springbootapplication-annotation) 放在您的主类上，它隐式定义某些项目的基本“搜索包”。例如，如果您正在编写 JPA 应用程序，则使用 `@SpringBootApplication` 注解修饰的类的包来搜索 `@Entity` 项目。使用根软件包还允许组件扫描仅应用于您的项目。

> 如果您不想使用  `@SpringBootApplication` ，由于它是通过引入 `@EnableAutoConfiguration` 和 `@ComponentScan` 注解来定义该行为，因此也可以直接使用它们来替代。

下面的列表展示了一种典型的项目结构：

```
com
 +- example
     +- myapplication
         +- Application.java
         |
         +- customer
         |   +- Customer.java
         |   +- CustomerController.java
         |   +- CustomerService.java
         |   +- CustomerRepository.java
         |
         +- order
             +- Order.java
             +- OrderController.java
             +- OrderService.java
             +- OrderRepository.java
```

`Application.java` 文件中可以随着基本的 `@SpringBootApplication` 声明 `main` 方法，如下面例子所示：

```java
package com.example.myapplication;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

