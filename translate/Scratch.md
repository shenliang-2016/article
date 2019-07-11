#### 1.12.2 使用 `AnnotationConfigApplicationContext` 实例化 Spring 容器

接下来的章节介绍了 Spring 的`AnnotationConfigApplicationContext`，它在 Spring 3.0 中引入。这个多功能的`ApplicationContext`实现不仅能够接受`@Configuration`类作为输入，还能接受`@Component`注解修饰的普通类，以及由 JSR-330 元数据注解的类。

当`@Configuration`类被作为输入时，该`@Configuration`类本身作为bean定义被注册，同时该类中声明的所有`@Bean`方法也被作为bean定义注册。

当`@Component`类和 JSR-330 类被作为输入时，它们也被作为bean定义注册，同时假定诸如`@Autovired`或者`@Inject`之类的依赖注入元数据被用在这些类中必要的位置。

**简单构造**

以在实例化`ClassPathXmlApplicationContext`时提供 Spring XML 文件作为输入完全相同的方式，你可以在实例化`AnnotationConfigApplicationContext`时使用`@Configuration`类作为输入。这就允许无 XML 的 Spring 容器，入下面例子所示：

````java
public static void main(String[] args) {
  ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
  MyService myService = ctx.getBean(MyService.class);
  myService.doStuff();
}
````

如前文所述，`AnnotationConfigApplicationContext`并不仅限于配合`@Configuration`类使用。任何`@Component`或者JSR-330 注解修饰的类都可以作为构造器的输入，如下面例子所示：

````java
public static void main(String[] args) {
  ApplicationContext ctx = new AnnotationConfigApplicationContext(MyServiceImpl.class, Dependency1.class, Dependency2.class);
  MyService myService = ctx.getBean(MyService.class);
  myService.doStuff();
}
````

上面的例子假定`MyServiceImpl`，`Dependency1`，`Dependency2`都使用了 Spring 的依赖注入注解，比如`@Autowired` 。

**使用`register(Class<?>...)`以编程方式创建容器**

你可以使用一个无参构造器来实例化`AnnotationConfigApplicationContext`，然后使用`register()`方法来配置它。这种方法在以编程方式构造`AnnotataionConfigApplicationContext`时非常有用。下面的例子展示了这种方法：

````java
public static void main(String[] args) {
  AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();
  ctx.register(AppConfig.class, OtherConfig.class);
  ctx.register(AdditionalConfig.class);
  ctx.refresh();
  MyService myService = ctx.getBean(MyService.class);
  myService.doStuff();
}
````

**使用`scan(String...)`开启组件扫描**

为了开启组件扫描，你可以如下修饰你的`@Configuration`类：

````java
@Configuration
@ComponentScan(basePackages = "com.acme")	//	This annotation enables component scanning.
public class AppConfig {
  //...
}
````

> 有经验的 Spring 用户会发现这中写法类似于 XML 中声明的 `context:namespace` 。如下面例子所示：
>
> ```xml
> <beans>
>     <context:component-scan base-package="com.acme"/>
> </beans>
> ```

在前面的例子中，`com.acme`包被扫描来寻找任何`@Component`注解修饰的类，同时这些类作为 Spring bean 定义被注册进入容器中。`AnnotationConfigApplicationContext`暴露`scan(String...)`方法以允许相同的组件扫描功能性。如下面例子所示：

````java
public static void main(String[] args) {
  AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();
  ctx.scan("com.acme");
  ctx.refresh();
  MyService myService = ctx.getBean(MyService.class);
}
````

> 请记住`@Configuration`类是使用`@Component`进行 [元注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-meta-annotations) 的，因此它们是组件扫描的候选者。在前面的示例中，假设`AppConfig`在`com.acmepackage`（或下面的任何包）中声明，它将在`scan()`调用期间被拾取。在`refresh()`之后，它的所有`@Bean`方法都被处理并在容器中注册为bean定义。

**使用`AnnotationConfigWebApplicationContext`支持Web应用程序**

`AnnotationConfigApplicationContext`的`WebApplicationContext`变体与`AnnotationConfigWebApplicationContext`一起提供。配置Spring `ContextLoaderListener` servlet 侦听器，Spring MVC `DispatcherServlet`等时，可以使用此实现。以下`web.xml`代码段配置典型的Spring MVC Web应用程序（请注意`contextClass` context-param和init-param的使用）：

```xml
<web-app>
    <!-- Configure ContextLoaderListener to use AnnotationConfigWebApplicationContext
        instead of the default XmlWebApplicationContext -->
    <context-param>
        <param-name>contextClass</param-name>
        <param-value>
            org.springframework.web.context.support.AnnotationConfigWebApplicationContext
        </param-value>
    </context-param>

    <!-- Configuration locations must consist of one or more comma- or space-delimited
        fully-qualified @Configuration classes. Fully-qualified packages may also be
        specified for component-scanning -->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>com.acme.AppConfig</param-value>
    </context-param>

    <!-- Bootstrap the root application context as usual using ContextLoaderListener -->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <!-- Declare a Spring MVC DispatcherServlet as usual -->
    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- Configure DispatcherServlet to use AnnotationConfigWebApplicationContext
            instead of the default XmlWebApplicationContext -->
        <init-param>
            <param-name>contextClass</param-name>
            <param-value>
                org.springframework.web.context.support.AnnotationConfigWebApplicationContext
            </param-value>
        </init-param>
        <!-- Again, config locations must consist of one or more comma- or space-delimited
            and fully-qualified @Configuration classes -->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>com.acme.web.MvcConfig</param-value>
        </init-param>
    </servlet>

    <!-- map all requests for /app/* to the dispatcher servlet -->
    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/app/*</url-pattern>
    </servlet-mapping>
</web-app>
```

#### 1.12.3 使用 `@Bean` 注解

`@Bean`是方法级别的注解，是 XML 配置文件中的`<bean/>`元素的直接等价物。该注解支持`<bean/>`提供的一些属性，比如：[init-method](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-initializingbean) 、 [destroy-method](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-disposablebean) 、 [autowiring](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-autowire) 、以及 `name` 等。

你可以在`@Configuration`或者`@Component`注解修饰的类中使用`@Bean`注解。

**声明一个 Bean**

为了声明一个 bean，你可以用`@Bean`注解修饰一个方法。你使用这个方法来在`ApplicationContext`中注册一个 bean 定义，该 bean 定义的类型由该方法返回值的类型指定。默认地，bean 名称就是该方法名。下面的例子展示了`@Bean`方法声明：

````java
@Configuration
public class AppConfig {
  @Bean
  public TransferServiceImpl transferService() {
    return new TransferServiceImpl();
  }
}
````

完全等价于下面的 Spring XML 片段：

````xml
<beans>
  <bean id="transferService" class="com.acme.TransferServiceImpl"/>
</beans>
````

上面两种声明都使得`ApplicationContext`中名为`transferService`的 bean 成为可用，绑定到一个类型为`TransferServiceImpl`的一个对象实例，如下面文字图所示：

````
transferService -> com.acme.TransferServiceImpl
````

你也可以声明你的`@Bean`方法，其返回值类型为接口或者基类。如下面例子所示：

````java
@Configuration
public class AppConfig {
  @Bean
  public TransferService transferService() {
    return new TransferServiceImpl();
  }
}
````

但是，这会将高级类型预测的可见性限制为指定的接口类型（`TransferService`）。然后，只要容器了解完整类型（`TransferServiceImpl`）一次，受影响的单例 bean 就已经被实例化。非懒加载的单例 bean 按照它们被声明的顺序实例化，因而你可能会看到不同的类型匹配结果，具体取决于另一个组件何时尝试通过非声明类型进行匹配（比如`@Autowired TransferServiceImp`，只会在`transferService` bean 已经被实例化时被解析一次）。

> 如果您始终通过声明的服务接口引用您的类型，则`@Bean`返回类型可以安全地加入该设计决策。但是，对于实现多个接口的组件或可能由其实现类型引用的组件，更安全的做法是声明可能的最具体的返回类型（至少与引用您的bean的注入点所需的具体类型相同）。

