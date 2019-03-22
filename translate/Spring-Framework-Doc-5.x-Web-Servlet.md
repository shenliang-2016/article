# Web on Servlet Stack

Version 5.1.5.RELEASE

----

文档的这一部分介绍基于 Servlet API 构建并部署在 Servlet 容器中的 Servlet-stack web 应用的支撑技术。包括以下单独的章节 [Spring MVC](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc), [View Technologies](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-view), [CORS Support](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-cors), 和 [WebSocket Support](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#websocket).。有关 reactive-stack web applications, 可以参考 [Web on Reactive Stack](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web-reactive.html#spring-web-reactive).

# 1. Spring Web MVC

Spring Web MVC 是建立在 Servlet API 基础上的原生 web 框架，从一开始就已经被包含在 Spring 框架中。正式名称````Spring Web MVC````，来自它的源代码模块名([`spring-webmvc`](https://github.com/spring-projects/spring-framework/tree/master/spring-webmvc))，不过它更广泛为人所知的却是名字````Spring MVC````。

与 Spring Web MVC 并列，Spring 框架 5.0 引入了名为````Spring WebFlux````的基于响应式技术栈的 web 框架，名字同样来自它的源代码模块名 ([`spring-webflux`](https://github.com/spring-projects/spring-framework/tree/master/spring-webflux))。本章介绍 Spring Web MVC，下一章介绍 Spring WebFlux。

获取基线信息以及与 Servlet 容器和 Java EE 版本范围的兼容性，参考 Spring 框架 [Wiki](https://github.com/spring-projects/spring-framework/wiki/Spring-Framework-Versions)。

## 1.1 DispatcherServlet

Spring MVC，如同许多其它 web 框架，围绕一个中央````Servlet````按照前端控制器模式进行设计。该中央````Servlet````，也就是````DispatcherServlet````，为请求处理提供了共享算法，同时实际的工作其实是由可配置的代理组件执行。这种模型是灵活的，而且可以支持各种各样的工作流程。

````DispatcherServlet````，如同任何其它````Servlet````，需要按照 Servlet 规范使用 Java 配置类或者在部署描述器文件````web.xml````中声明和映射。然后，该````DispatcherServlet````使用 Spring 配置来发现它进行请求映射所需要的代理组件、视图解析器、异常处理器等等。

下面的例子展示了通过 Java 配置类注册和初始化````DispatcherServlet````，可以被 Servlet 容器自动探测到（参考  [Servlet Config](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-container-config)）：

````java
public class MyWebApplicationInitializer implements WebApplicationInitializer {
    
    @Override
    public void onStartup(ServletContext servletCxt) {
        // Load Spring web application configuration
        AnnotationConfigWebApplicationContext ac = new AnnotationConfigWebApplicationContext();
        ac.register(AppConfig.class);
        ac.refresh();
        
        // Create and register the DispatcherServlet
        DispatcherServlet servlet = new DispatcherServlet(ac);
        ServletRegistration.Dynamic registration = servletCxt.addServlet("app", servlet);
        registration.setLoadOnStartup(1);
        registration.addMapping("/app/*");
    }
}
````

> 除了直接使用 ServletContext API，你还可以继承````AbstractAnnotationConfigDispatcherServletInitializer````并且覆盖其中的特定方法（参考  [Context Hierarchy](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-servlet-context-hierarchy) 下的例子）。

下面的例子展示了在````web.xml````配置文件中注册和初始化````DispatcherServlet````：

````xml
<web-app>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/app-context.xml</param-value>
    </context-param>
    
    <servlet>
        <servlet-name>app</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value></param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>app</servlet-name>
        <url-pattern>/app/*</url-pattern>
    </servlet-mapping>
</web-app>
````

> Spring Boot 遵循不同的初始化序列。Spring Boot 使用 Spring 配置来引导它自己以及内置的 Servlet   容器，而不依靠 Servlet 容器进行生命周期管理。Spring 配置中被探测到的````Filter````和````Servlet````声明会随着 Servlet 容器注册。更多细节参考 [Spring Boot documentation](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-embedded-container)。

### 1.1.1 Context 层级结构

````DsipatcherServlet````期望一个````WebApplicationContext````（普通的````ApplicationContext````的扩展）为了它自己的配置。````WebApplicationContext````拥有一个指向````ServletContext````以及与之相关的````Servlet````的链接。它们也会被绑定到````ServletContext````因而应用可以使用````RequestContextUtils````中的静态方法来寻找````WebApplicationContext````，如果它们需要访问它。

对很多应用来说，拥有唯一一个````WebApplicationContext````是简单而又足够的。不过也可能存在一个 context 的层级结构，作为根的````WebApplicationContext````在多个````DispatcherServlet````或者其它````Servlet````实例之间共享，每个都拥有它们自己的子````WebApplicationContext````配置。更多信息参见  [Additional Capabilities of the `ApplicationContext`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#context-introduction)。

根````WebApplicationContext````典型地包含基础设施 beans，比如数据存取类和业务服务类等需要在多个````Servlet````实例之间共享的 beans。这些 beans 可以在 Servlet 各自的子````WebApplicationContext````中有效地继承和覆盖，这些````WebApplicationContext````中通常包含属于给定````Servlet````的 beans 。下面的图展示了上述关系：

![Context 层级结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/spring/image-20190321204627481.png)

下面的例子配置了一个````WebApplicationContext````层级结构：

````java
public class MyWebAppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class<?>[] { RootConfig.class };
    }
    
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class<?>[] { App1Config.class };
    }
    
    @Override
    protected String[] getServletMapping() {
        return new String[] { "/app1/*" };
    }
}
````

>  如果一个应用上下文层级结构不是必需的，则应用可以通过````getRootConfigClasses()````返回所有的配置，同时通过````getServletConfigClasses()````方法返回````null````。

下面的例子是等效的````web.xml````：

````xml
<web-app>

    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/root-context.xml</param-value>
    </context-param>

    <servlet>
        <servlet-name>app1</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/app1-context.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>app1</servlet-name>
        <url-pattern>/app1/*</url-pattern>
    </servlet-mapping>

</web-app>
````

> 如果一个应用中上下文层级结构不是必需的，则应用可以只配置````root````上下文，同时将````contextConfigLocation```` Servlet 参数置空。

<<<<<<< 74ca7d9af9b51ebed2ccd1f29c13210462afd66f
### 1.1.2 指定 Bean 类型
=======
### 1.1.2 特殊 Bean 类型

````DispatcherServlet````委托特殊的 beans 处理请求和渲染适当的响应。这里的"特殊"意思是实现了框架契约的 Spring 管理的````Object````实例。它们通常包含内建契约，不过你可以客户化他们的属性，扩展或者替换它们。

下面的表列出了````DispatcherServlet````探测到的特殊的 beans ：

| Bean 类型                                  | 解释                                       |
| :--------------------------------------- | ---------------------------------------- |
| HandlerMapping                           | 将一个请求映射到一个处理器以及一系列的拦截器，进行前处理和后处理。映射基于某些约束，其中细节取决于````HandlerMapping````实现。<br />最主要的两个````HandlerMapping````实现是````RequestMappingHandlerMapping````（支持````@RequestMapping````注解的方法）和````SimpleUrlHandlerMapping````（保持请求处理器上显式注册的 URI 路径模式） |
| HandlerAdapter                           | 帮助````DispatcherServlet````调用映射到请求的处理器，无论该处理器实际上是如何被调用的。比如，调用一个注解了的控制器需要解析注解。````HandlerAdapter````的主要目的就是让````DispatcherServlet```` 从这些细节中解脱出来。 |
| [`HandlerExceptionResolver`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-exceptionhandlers) | 解析处理异常的策略，可能将它们映射到处理器、到 HTML 错误视图或者其它目标。参考 [Exceptions](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-exceptionhandlers)。 |
| [`ViewResolver`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-viewresolver) | 解析从处理器返回的基于字符串的逻辑视图名称为一个实际的视图，该视图可以用于渲染响应。参考 [View Resolution](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-viewresolver) 和 [View Technologies](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-view)。 |
| [`LocaleResolver`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-localeresolver), [LocaleContextResolver](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-timezone) | 解析客户端使用的````Locale````，科恩感表示它们的时区，目的是可以提供国际化的视图。参考 [Locale](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-localeresolver)。 |
| [`ThemeResolver`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-themeresolver) | 解析你的应该可以使用的主体－比如，为了提供个性化的布局。参考 [Themes](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-themeresolver)。 |
| [`MultipartResolver`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-multipart) | 转化一个多部分请求（比如，浏览器表单文件上传）的抽象，以及一些多部分转化类库的帮助。参考 [Multipart Resolver](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-multipart)。 |
| [`FlashMapManager`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-flash-attributes) | 存储和获取“输入”和“输出”````FlashMap````，可以被用于从一个请求向另外一个请求传递属性，通常跨越转发。参考 [Flash Attributes](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-flash-attributes)。 |

### 1.1.3 Web MVC Config

应用可以声明在  [Special Bean Types](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-servlet-special-bean-types) 中列出处理请求所必须的基础设施 beans 。````DispatcherServlet````检查````WebApplicationContext````为每个特殊 bean。如果不存在匹配的 bean 类型，就会降级到 [`DispatcherServlet.properties`](https://github.com/spring-projects/spring-framework/blob/master/spring-webmvc/src/main/resources/org/springframework/web/servlet/DispatcherServlet.properties) 中列出的默认类型。

大多数情况下，[MVC Config](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config) 都是最好的开始点。它以 XML 或者 Java 代码形式声明了必需的 beans，并提供了可用于对其进行定制的回调方法。

> Spring Boot 依赖 MVC Java 配置来配置 Spring MVC 并提供许多附加的方便选项。

### 1.1.4 Servlet Config

在 Servlet 3.0+ 环境中，你可以选择通过编程方式配置 Servlet 容器，或者结合使用部署描述器文件````web.xml````。下面的例子注册了一个````DispatcherServlet````：

````java
import org.springframework.web.WebApplicationInitializer

public class MyWebApplicationInitializer implements WebApplicationInitializer {

	@Override
    public void onStartup(ServletContext container) {
    	XmlWebApplicationContext appContext = new XmlWebApplicationContext();
    	appContext.setConfigLocation("/WEB-INF/spring/dispatcher-config.xml");
    	
    	ServletRegistration.Dynamic registration = container.addServlet("dispatcher". new DispatcherServlet(appContext));
    	registration.setLoadOnStartup(1);
    	registration.addMapping("/");
    }
}
````

````WebApplicationInitializer````是 Spring MVC 提供的接口，用以确保你的实现被检测到，同时自动被用来初始化任何 Servlet 3 容器。````WebApplicationInitializer````的一个抽象基类实现名为````AbstractDispatcherServlet````使得注册````DispatcherServlet````并通过覆盖方法来指定 servlet 映射和````DispatcherServlet````配置的位置等变得更加方便。

推荐应用使用基于 Java 的 Spring 配置，如下面例子所示：

````java
public class MyWebAppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {
  
  @Override
  protected Class<?>[] getRootConfigClasses() {
    return null;
  }
  
  @Override
  protected Class<?>[] getServletConfigClasses() {
    return new Class<?>[] { MyWebConfig.class };
  }
  
  @Override
  protected String[] getServletMappings() {
    return new String[] { "/" };
  }
}
````

如果你使用基于 XML  的 Spring 配置，你应该直接从````AbstractDispatcherServletInitializer````继承，如下面例子所示：

````java
public class MyWebAppInitializer extends AbstractDispatcherServletInitializer {
  
  @Overrid
  protected WebApplicationContext createRootApplicationContetx() {
    return null;
  }
  
  @Override
  protected WebApplicationContext createServletApplicationContext() {
    XmlWebApplicationContext cxt = new XmlWebApplicationContext();
    cxt.setConfigLocation("/WEB-INF/spring/dispatcher-config.xml");
    return cxt;
  }
  
  @Override
  protected String[] getServletMappings() {
    return new String[] { "/" };
  }
}
````

````AbstractDispatcherServletInitializer````也提供了一种方便的方法来添加````Filter````实例，同时这些实例会被自动映射到````DispatcherServlet````，如下面例子所示：

````java
public class MyWebAppInitializer extends AbstractDispatcherServletInitializer {
  // ...
  
  @Override
  protected Filter[] getServletFilters() {
    return new Filter[] {
      new HiddenHttpMethodFilter(), new CharacterEncodingFilter()
    };
  }
}
````

每个过滤器都有一个基于其具体类型的默认名称，同时会被自动映射到````DispatcherServlet````。

````AbstractDispatcherServletInitializer````的 protected 方法````isAsyncSupported````提供了一个单一的位置来使得异步支持在````DispatcherServlet````以及所有映射到其上的过滤器上都是可用的。默认情况下，这个标志被设置为````true````。

最后，如果你需要进一步的定制化````DispatcherServlet````本身，你可以覆盖````createDispatcherServlet````方法。

### 1.1.5 处理

````DispatcherServlet````处理请求的步骤如下：

* ````WebApplicationContext````被搜索到并绑定到请求中作为一个属性以便于处理该请求的控制器和其它元素使用。它默认被绑定在````DispatcherServlet.WEB_APPLICATION_CONTEXT_ATTRIBUTE````键下。
* 区域解析器被绑定到请求以使得处理该请求的元素可以解析并使用区域信息，比如渲染视图、准备数据等等。如果你不需要区域解析，你就不需要区域解析器。
* 主题解析器被绑定到请求以使得视图解析器可以确定应该使用何种主题。如果你没有使用主题，可以忽略它。
* 如果你制定了一个多部分文件解析器，请求就会作为多部分请求被检查。如果确实发现了多个部分，请求就会被包装进入````MultipartHttpServletRequest````并由其它元素继续处理。更多细节参考  [Multipart Resolver](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-multipart) 。
* 查找一个合适的处理器。如果找到了，有关该处理器的执行链（预处理器、后处理器以及控制器等）会按照顺序执行以准备数据模型或者渲染。另外，对于注解的控制器，响应会被渲染（由````HandlerAdapter````）来取代返回一个视图。
* 如果一个模型被返回，视图就会被渲染。如果没有模型被返回（可能由于预处理器或者后处理器拦截了请求，可能是基于安全原因），就没有视图会被渲染，因为请求实际上被没有被满足。

````WebApplicationContext````中声明的````HandlerExceptionResolver```` beans 被用来解析请求处理过程中抛出的异常。那些异常解析器允许客户化逻辑以定位异常。更多细节参见  [Exceptions](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-exceptionhandlers) 。

Spring ````DispatcherServlet````也支持返回````last-modification-date````，就像由 Servlet API 指定的那样。为特定请求确定最后修改时间的过程相当直接：````DispatcherServlet````寻找一个合适的处理器映射并测试是否它实现了````LastModified````接口。如果是，````LastModified````接口的````long getLastModified(request)````方法的返回值将被返回给客户端。

你可以定制单个的````DispatcherServlet````实例，通过在````web.xml````文件中 Servlet 声明中添加 Servlet 初始化参数（````init-param````元素）。下表列出了支持的参数：

| 参数                             | 解释                                       |
| ------------------------------ | ---------------------------------------- |
| contextClass                   | 实现了````ConfigurableWebApplicationContext````的类，将被 Servlet 实例化并本地配置。默认地，````XmlWebApplicationContext````会被使用。 |
| contextConfigLocation          | 被传递给 context 实例（由````contextClass````指定）用以表示 contexts 在哪里可以找到的字符串。该字符串可能由多个字符串组成（逗号或者分号分隔）以支持多 contexts。在多个 contexts 位置在 beans 中被定义两次的情况下，最后定义的位置具有优先权。 |
| namespace                      | ````WebApplicationContext````的命名空间，默认为````[servlet-name]-servlet````。 |
| throwExceptionIfNoHandlerFound | 当无法找到对应于请求的处理器时是否应该抛出````NoHandlerFoundException````。该异常随后会被````HandlerExceptionResolver````捕获（比如，通过使用````@ExceptionHandler````控制器方法）并处理。<br />默认地，该属性设置为````false````。这种情况下````DispatcherServlet````会返回 404（NOT_FOUND）状态码响应，而不会抛出异常。<br />注意：如果同时也配置了   [default servlet handling](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-default-servlet-handler)，无法解析的请求就永远会被转发给默认的 servlet，因此永远不会出现 404 。 |

### 1.1.6 拦截

所有的````HandlerMapping````实现都支持处理器拦截器，当你希望对某些请求执行特定功能逻辑时，拦截器就是非常有用的。比如，检查请求主体的身份。拦截器必需实现来自````org.springframework.web.servlet````包的````HandlerInterceptor````接口，该接口包含三个方法，提供了足够的灵活性进行各种预处理和后处理。

* ````preHandle(..)````：在实际的请求处理器之前执行。
* ````postHandle(..)````：在实际的请求处理器之后执行。
* ````afterCompletion(..)````：请求处理完全结束之后执行。

````preHandle(..)````方法返回一个布尔值。你可以使用该方法打断或者继续请求处理执行链的执行过程。当该方法返回````true````，处理器执行链继续。否则，````DispatcherServlet````会假定该拦截器自己负责处理请求（同时，比如，渲染相应的视图）而不再继续执行执行链上的其它拦截器和实际的请求处理器。

参考 [Interceptors](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-interceptors) 获取关于拦截器配置的更多信息。你也可以直接使用````HandlerMapping````实现上的````setters````来注册它们。

注意，````postHandle````不适合与````@ResponseBody````和````ResponseEntity````共同使用，因为此时响应会在````HandlerAdapter````中被写入和提交，并且都在````postHandle````之前执行。也就是说，此时已经太晚了，因而不可能再对响应做任何修改，比如添加额外的首部字段等。这种场景下，你可以实现````ResponseBodyAdvice````并要么将它声明为 [Controller Advice](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-controller-advice) bean 或者直接将它配置到````RequestMappingHandlerAdapter````上。

### 1.1.7 异常

如果在请求映射过程中发生异常，或者请求处理器（比如````@Controller````）抛出异常，````DispatcherServlet````会委托一个````HandlerExceptionResolver```` beans 链来解析异常并提供替代的处理逻辑，通常会返回一个错误响应。

下面的表列出了可用的````HandlerExceptionResolver````实现：

| HandlerExceptionResolver                 | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| SimpleMappingExceptionResolver           | 异常类名称和错误视图名称之间的映射。对浏览器应用渲染错误页面非常有用。      |
| [`DefaultHandlerExceptionResolver`](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/web/servlet/mvc/support/DefaultHandlerExceptionResolver.html) | 解析由 Spring MVC 抛出的异常并将它们映射到 HTTP 状态码。参考可替代它的````ResponseEntityExceptionHandler````和  [REST API exceptions](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-rest-exceptions)。 |
| ResponseStatusExceptionResolver          | 解析由````@ResponseStatus````注解的异常并基于注解指定的值将其映射到 HTTP 状态码。 |
| ExceptionHandlerExceptionResolver        | 通过调用````@Controller````或者````@ControllerAdvice````注解的类中注解了````@ExceptionHandler````的方法解析异常。参考  [@ExceptionHandler methods](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-exceptionhandler)。 |

