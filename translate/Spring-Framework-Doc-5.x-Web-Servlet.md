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

### 1.1.2 特殊类型的 Bean 

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

**解析器链**

你可以通过在你的 Spring 配置文件中声明多个````HandlerExceptionResolver```` beans 并按需设定它们的````order````属性，以形成一个异常解析链。顺序属性值越高，对应的异常解析器的位置越靠后。

````HandlerExceptionResolver````的内部契约指定了它能够返回：

* 一个指向错误视图的````ModelAndView````。
* 如果异常在该解析器中处理，则返回一个空````ModelAndView````。
* 如果异常仍然是未解析的，则返回````null````，以便于后续的解析器尝试处理，同时，如果最终异常仍未解析，就允许将它抛出给 Servlet 容器。

[MVC Config](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config) 自动声明内建的解析器用来处理默认的 Spring MVC 异常、````@ResponseStatus````注解的异常以及支持````@ExceptionHandler````方法。你能够定制该列表或者替换它。

**容器错误页面**

如果异常被所有````HandlerExceptionResolver````处理之后仍然未被解析，只能原样传输，或者，如果响应状态码呗设置为错误状态码（4xx，5xx），Servlet 容器能够渲染一个默认的错误页面为 HTML。为了定制化容器的默认错误页面，你能够在````web.xml````文件中声明一个错误页面映射。如下面例子所示：

````xml
<error-page>
    <location>/error</location>
</error-page>
````

给定上面的例子，当一个异常抛出活着响应是错误状态，Servlet 容器就会在容器中进行一个````ERROR````分发到配置的 URL （比如，````/error````）。接下来由````DispatcherServlet````处理，可能将它映射到一个````@Controller````，该控制器可以被实现为返回一个错误视图名和模型，或者渲染一个 JSON 响应。如下面例子所示：

````java
@RestController
public class ErrorController {
    @RequestMapping(path = "/error")
    public Map<String, Object> handle(HttpServletRequest request) {
        Map<String, Object> map = new HashMap<String, Object>();
        map.put("status", request.getAttribute("javax.servlet.error.status_code"));
        map.put("reason", request.getAttribute("javax.servlet.error.message"));
        return map;
    }
}
````

> Servlet API 没有提供在 Java 中创建错误页面映射的方法。不过，你仍然可以同时使用````WebApplicationInitializer````和一个最小化的````web.xml````。

### 1.1.8 视图解析

Spring MVC 定义了````ViewResolver````和````View````接口来使得你在浏览器中渲染模型而不会把你绑定到特定的视图技术。````ViewResolver````提供了视图名称和实际视图之间的映射。````View````负责在将数据移交给具体的视图技术之前解决数据准备问题。

下面的表列出了有关````ViewResolver````层级结构的更多细节：

| 视图解析器                          | 描述                                       |
| ------------------------------ | ---------------------------------------- |
| AbstractCachingViewResolver    | ````AbstractCachingViewResolver````的子类缓存它们解析的视图实例。缓存可以改善某些视图技术的性能。你可以通过设置````cache````属性为````false````来关闭缓存。进一步地，如果你必须在运行时刷新某个视图（比如，当一个 FreeMarker 模板发生变化时），你可以使用````removeFromCache(String viewName, Locale loc)````方法。 |
| XmlViewResolver                | ````ViewResolver````的实现，接收 XML 形式的配置文件，该文件与 Spring 的 XML bean 工厂遵循同样的 DTD。默认的配置文件是````/WEB-INF/views.xml````。 |
| ResourceBundleViewResolver     | 使用由资源集基础名称指定的````ResourceBundle````中的 bean 定义的````ViewResolver````实现。对每个应该被解析的视图，它使用````[viewname].(class)````属性的值作为视图类型，````[viewname].url````属性值作为视图的 URL。你可以在 [View Technologies](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-view) 章节中找到例子。 |
| UrlBasedViewResolver           | ````ViewResolver````接口的简单实现，影响直接将逻辑视图名称到 URLs ，而不需要显式定义映射关系。这是合适的，如果你的逻辑视图名称直接匹配到你的视图资源名称，而不需要明确的映射关系指定。 |
| InternalResourceViewResolver   | ````UrlBasedViewResolver````的实用子类，支持````InternalResourceView````（实际上是 Servlets 和 JSPs）及其子类，比如````JstlView````和````TileView````。你可以为所有通过该解析器生成的视图指定视图类型，通过使用````setViewClass(..)````。参考文档 [`UrlBasedViewResolver`](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/web/reactive/result/view/UrlBasedViewResolver.html) 获取更多细节。 |
| FreeMarkerViewResolver         | ````UrlBasedViewResolver````的实用子类，支持````FreeMarkerView````及其定制化子类。 |
| ContentNegotiatingViewResolver | ````ViewResolver````接口的实现，解析基于请求文件名或者````Accept````首部字段的视图。参考 [Content Negotiation](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-multiple-representations)。 |

**处理**

你可以通过在你的 Spring 配置文件中声明多个视图解析器 beans 并按需设定它们的````order````属性，以形成一个视图解析链。顺序属性值越高，对应的视图解析器的位置越靠后。

````ViewResolver````的内部契约指定它可以返回````null````来表示请求的视图没有找到。然而，在 JSPs 和````InternalResourceViewResolver````的情况下，确定请求的 JSP 是否存在的唯一方法是通过````RequestDispatcher````执行一次请求分发。因此，你必须永远把一个````InternalResourceViewResolver````放在视图解析器链的最后位置上。

配置视图解析与在 Spring 配置文件中添加````ViewResolver```` beans 一样简单。[MVC Config](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config) 提供了专用的配置 API 用于 [View Resolvers](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-view-resolvers) 以及添加轻逻辑的  [View Controllers](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-view-controller)，它们对没有控制器逻辑的 HTML 模版的渲染是有用的。

**重定向**

视图名称中特殊的````redirect:````前缀使得你执行一次重定向。````UrlBasedViewResolver````以及它的子类将其作为需要一次重定向的指令。视图名称的剩余部分就是重定向 URL。

纯粹的效果就如同控制器已经返回了一个````RedirectView````，不过现在该控制器本身能够根据逻辑视图名称执行重定向。逻辑视图名称（比如````redirect:/myapp/some/resource````）相对于当前 Servlet 上下文路径进行重定向，而形如````redirect:http://myhost.com/some/arbitrary/path````将按照绝对 URL 进行重定向。

注意：如果一个控制器方法被````@ResponseStatus````标注，则该注解值就会优先于````RedirectView````对响应状态码的设置。

**转发**

你也可以在视图名称中使用特殊的````forward````前缀，它最终由````UrlBasedViewResolver````及其子类解析。这会创建一个````InternalResourceView````，它会执行一个````RequestDispatcher.forward()````。因此，这个前缀对````InternalResourceViewResolver````和````InternalResourceView````（为 JSPs）是没用的，但是如果你使用别的视图技术的同时还想强制 Servlet/JSP 引擎执行一次待处理资源的转发，此时这个前缀就是有用的。注意，此时你仍然可以使用视图解析链。

**内容协商**

````ContentNegotiatingViewResolver````自身并不解析视图，它会将视图解析任务委托给其它视图解析器，并且选择视图来组装客户端请求的表示形式。该表示形式可以基于````Accept````首部字段值确定，或者基于查询参数确定（比如````"/path?format=pdf"````）。

````ContentNegotiatingViewResolver````选择合适的````View````来处理请求，通过比较请求的媒体类型和````View````以及与之相关的每个````ViewResolver````所支持的媒体类型（也被称为````Content-Type````）。列表中首个拥有与请求匹配的````Content-type````的````View````将返回该表示形式给客户端。如果视图处理器链并没有给出可用的视图，````DefaultViews````列表中指定的视图就会被考察。后者适合用于产生单例模式的````Views````，该视图可以为当前资源渲染合适的表示形式，而不关心逻辑视图名称。`````Accept```` 首部字段可以包含通配符（比如````text/*````），这种情况下````Content-Type````值是````text/xml````的````View````就是兼容的匹配。

参考 [MVC Config](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config) 下的 [View Resolvers](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-view-resolvers) 获取更多配置细节。

### 1.1.9 语言环境

Spring 架构的绝大部分都支持国际化，Spring web MVC 也是一样。````DispatcherServlet````允许你基于客户端的语言环境首部字段自动解析消息。该动作由````LocaleResolver````对象完成。

当一个请求到来，````DispatcherServlet````查找一个语言环境解析器，如果找到一个，尝试使用它设置语言环境。通过使用````RequestContext.getLocale()````方法，你永远能够获取由语言环境解析器解析出来的语言环境信息。

除了自动语言环境解析，你也可以添加一个拦截器到处理器映射中来改变特定环境（比如基于请求中的参数）下的语言环境设置。

语言环境解析器和拦截器都定义在````org.springframework.web.servlet.i18n````包下，同时被通过普通的方式配置到你的应用上下文中。Spring 中包含以下可选的语言环境解析器：

* [Time Zone](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-timezone)
* [Header Resolver](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-localeresolver-acceptheader)
* [Cookie Resolver](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-localeresolver-cookie)
* [Session Resolver](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-localeresolver-session)
* [Locale Interceptor](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-localeresolver-interceptor)

**TimeZone**

除了获取客户端的语言环境，知道它所在的时区通常也是非常有用的。````LocaleContextResolver````接口提供了一个````LocaleResolver````的扩展，允许解析器提供一个内容丰富的````LocaleContext````，其中可以包含时区信息。

当可用时，用户的````TimeZone````信息可以通过使用````RequestContext.getTimeZone()````方法获取。时区信息会自动被由````ConversionService````注册的任何 Date/Time ````Converter````和````Formatter````对象使用。

**Header Resolver**

语言环境解析器检查客户端（比如浏览器）发送的请求中的````accept-language````首部字段。通常，这个首部字段包含客户端操作系统的语言环境信息。注意，此解析器不支持时区信息。

**Cookie Resolver**

此语言环境解析器检查可能存在于客户端的````Cookie````来确认是否指定了````Locale````或者````TimeZone````。如果指定了，它使用这些指定信息。通过使用此语言环境解析器属性，你能够指定 cookie 的名称和最大年龄。下面的例子定义了一个````CookieLocaleResolver````：

````xml
<bean id="localeResolver" class="org.springframework.web.servlet.i18n.CookieLocaleResolver">
  <property name="cookieName" value="clientLanguage"/>
  <!-- in seconds. If set to -1, the cookie is not persisted (deleted when brower shuts down) -->
  <property name="cookieMaxAge" value="100000"/>
</bean>
````

下表描述了````CookieLocaleResolver````的属性：

| 属性           | 默认值                | 描述                                       |
| ------------ | ------------------ | ---------------------------------------- |
| cookieName   | classname + LOCALE | cookie 的名称                               |
| cookieMaxAge | Servlet 容器的默认值     | cookie 在客户端持久化的最长时间。如果是 -1，则 cookie 将不持久化，在浏览器关闭后就不再可用。 |
| cookiePath   | /                  | 限制 cookie 对你站点的某些部分的可见性。当指定该属性时，cookie 就只对该路径以及其下的路径可见。 |

**Session Resolver**

````SessionLocaleResolver````允许你从当前用户请求相关的会话中获取````Locale````和````TimeZone````信息。与````CookieLocaleResolver````不同，这种策略选择设定在 Servlet 容器的````HttpSession````中的语言环境信息存储。因此，那些设定只是对每个会话临时可用，因此，当会话关闭后这些设定就将丢失。

注意：这跟外部会话管理机制并没有直接关系，比如 Spring Session 项目。此````SessionLocaleResolver````评估和修改与当前````HttpServletRequest````相关的````HttpSession````属性。

**Locale Interceptor**

你可以通过在````HandlerMapping````定义中添加````LocaleChangeInterceptor````来改变语言环境设置。它将探测请求中的一个参数并根据它改变请求的语言环境设置，通过调用请求分发器的应用上下文中的````LocaleResolver````上的````setLocale````方法。下面的例子展示了请求所有的````*.view````资源的请求包含一个名为````siteLanguage````的参数来改变语言环境。也就是说，比如，一个请求的 URL 为 [http://www.sf.net/home.view?siteLanguage=nl](https://www.sf.net/home.view?siteLanguage=nl)，将站点语言改为 Dutch。下面的例子展示如何拦截此语言环境设置：

````xml
<bean id="localeChangeInterceptor"
        class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor">
    <property name="paramName" value="siteLanguage"/>
</bean>

<bean id="localeResolver"
        class="org.springframework.web.servlet.i18n.CookieLocaleResolver"/>

<bean id="urlMapping"
        class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
    <property name="interceptors">
        <list>
            <ref bean="localeChangeInterceptor"/>
        </list>
    </property>
    <property name="mappings">
        <value>/**/*.view=someController</value>
    </property>
</bean>
````

### 1.1.10 主题

你可以应用 Spring Web MVC 主题为你的应用设定一种全局的观感，由此提升用户体验。主题是一系列的静态资源的集合，典型的是样式表和图片，都可以影响应用的视觉风格。

**定义主题**

为了在你的应用中使用主题，你必须准备````org.springframework.ui.context.ThemeSouce````接口的一个实现。````WebApplicationContext````接口扩展了````ThemeSource````并且将它的职责代理给专用的实现。默认地，代理是一个````org.springframework.ui.context.support.ResourceBundleThemeSource````实现，该实现从 classpath 的根目录加载属性文件。为了使用客户化的````ThemeSource````实现或者为了配置````ResourceBundleThemeSource````的基本名前缀，你能够使用预留的名称在应用的上下文中注册 bean ````themeSource````。应用上下文将会根据该名称自动探测 bean 并使用它。

当你使用````ResourceBundleThemeSource````时，一个主题就定义在一个简单的属性文件中。该属性文件列出了构成注意的资源，如下例所示：

````
styleSheet=/themes/cool/style.css
background=/themes/cool/img/coolBg.jpg
````

属性键值对中的键是视图代码中代表主题元素的名称。对 JSP 来说，你典型地可以使用````spring:theme````客户化标签做到这一点，非常类似于````spring:mesage````标签。下面的 JSP 片段使用上面例子中定义的主题来客户化观感：

````jsp
<%@ taglib prefix="spring" uri="http://www.springframework.org/tags"%>
<html>
    <head>
        <link rel="stylesheet" href="<spring:theme code='styleSheet'/>" type="text/css"/>
    </head>
    <body style="background=<spring:theme code='background'/>">
        ...
    </body>
</html>
````

默认地，````ResourceBundleThemeSource````使用空的基本名称前缀。由此，属性文件将会从 classpath 的根目录被加载。因此，你可以将````cool.properties````主题定义在 classpath 根目录下的路径中（比如在````WEB-INF/classes````中）。````ResourceBundleThemeSource````使用标准的 Java 资源集加载机制，允许主题的完整国际化。比如，我们可以拥有一个````/WEB-INF/classes/cool_nl.properties````表示一个上面带有 Dutch  文字的特殊的背景图片。

**解析主题**

定义了主题之后，如上节中所述，你需要决定使用哪个主题。````DispatcherServlet````查找名为````themeResolver````的 bean 以确定要使用哪个````ThemeResolver````实现。主题解析器的工作方式与````LocaleResolver````类似。它探测主题用于特定的请求，同时也能改变请求的主题。下表描述了 Spring 提供的主题解析器：

| 类                    | 描述                                       |
| -------------------- | ---------------------------------------- |
| FixedThemeResolver   | 选择一个固定的主题，使用````defaultThemeName````属性设置。 |
| SessionThemeResolver | 主题呗维护在用户的 HTTP 会话中。它需要为每个会话只设置一次，而不需要在会话之间持久化。 |
| CookieThemeResolver  | 选择的主题被存储在客户端上的 cookie 中。                 |

Spring 也提供了一个````ThemeChangeInterceptor````允许每个请求的主题都发生变化，只需要使用一个简单的请求参数。

### 1.1.11 Multipart Resolver

````org.springframework.web.multipart````包下的````MultipartResolver````是一种策略，用来分析包含文件上传的多部分的请求。这里有一个基于 [Commons FileUpload](https://jakarta.apache.org/commons/fileupload) 的实现和另一个基于 Servlet 3.0 多部分请求分析的实现。

为了开启多部分请求处理，你需要在你的````DispatcherServlet```` Spring 配置中声明一个名为````multipartResolver````的````MultipartResolver```` bean 。````DispatcherServlet````探测到它并将它应用于到来的请求。当一个 content-type 为````multipart/form-data````的 POST 请求被接收到，解析器分析其内容并包装当前````HttpServletRequest````为````MultipartHttpServletRequest````来提供访问到已经解析的部分，额外将他们作为请求参数暴露出来。

**Apache Commons ````FileUpload````**

为了使用 Apache Commons  ````FileUpload````，你可以配置一个名为````multipartResolver````的````CommonsMultipartResolver````的 bean。你同时还需要````commons-fileupload````作为一个 classpath 上的依赖。

**Servlet 3.0**

Servlet 3.0 多部分分析需要通过 Servlet 容器配置来开启。为了做到这个：

* 在 Java 中，在 Servlet 注册上设置一个````MultipartConfigElement````。
* 在````web.xml````文件中，为 servlet 声明添加````<multipart-config>````小节。

下面的例子展示了如何在 Servlet 注册上设置一个````MultipartConfigElement````：

````java
public class AppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {

    // ...

    @Override
    protected void customizeRegistration(ServletRegistration.Dynamic registration) {

        // Optionally also set maxFileSize, maxRequestSize, fileSizeThreshold
        registration.setMultipartConfig(new MultipartConfigElement("/tmp"));
    }

}
````

一旦 Servlet 3.0 配置就位，你可以以名称````multipartResolver````添加一个````StandardServletMultipartResolver````类型的 bean 。

### 1.1.12 日志

DEBUG 级别的日志在 Spring 中被设计为紧凑的、最小的以及人类友好的。它聚焦于高价值的信息，这些信息在调试特定问题时屡次发挥重要作用。

TRACE 级别的日志通常遵循与 DEBUG 级别的日志相同的原则（比如，同样不应该成为消防水管），不过也可以被用于调试各种问题。另外，一些日志信息可能在 TRACE 和 DEBUG 中展示不同的详细程度。

好的日志来自于使用经验。如果你发现任何不符合既定目标的东西，请告诉我们。

**敏感信息**

DEBUG 和 TRACE 日志可能会记录敏感信息。这就是为什么请求参数和首部字段都默认经过伪装，想要在日志中记录它们就必须通过````DispatcherServlet````上的````enableLoggingRequestDetails````属性显式开启。

 下面的例子展示了使用 Java 配置来做到这一点：

````java
public class MyInitializer
        extends AbstractAnnotationConfigDispatcherServletInitializer {

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return ... ;
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return ... ;
    }

    @Override
    protected String[] getServletMappings() {
        return ... ;
    }

    @Override
    protected void customizeRegistration(Dynamic registration) {
        registration.setInitParameter("enableLoggingRequestDetails", "true");
    }

}
````

## 1.2 过滤器

````spring-web````模块提供了一些有用的过滤器：

* [Form Data](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#filters-http-put)
* [Forwarded Headers](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#filters-forwarded-headers)
* [Shallow ETag](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#filters-shallow-etag)
* [CORS](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#filters-cors)

### 1.2.1 表单数据

浏览器能够提交表单数据仅仅通过 HTTP GET 或者 HTTP POST 请求，但是非浏览器客户端还可以使用 HTTP PUT，PATCH 和 DELETE。Servlet API 需要````ServletRequest.getParameter*()````方法来支持通过 HTTP POST 方法访问表单字段。

````spring-web````模块提供了````FormContentFilter````来拦截内容类型为````application/x-www-form-urlencoded````的 HTTP PUT，PATCH 和 DELETE 请求，从请求体中读取数据，包装````ServletRequest````以使得表单数据通过````ServletRequest.getParameter*()````方法族是可访问的。

### 1.2.2 被转发的首部

当请求穿过代理服务器（比如负载均衡服务器）后 host、port 甚至是 scheme 都可能会发生变化，这就提出了一个创建一个客户端视角的指向正确的 host、port 以及 scheme 的链接的挑战。

[RFC 7239](https://tools.ietf.org/html/rfc7239) 定义了````Forwarded```` HTTP 首部字段，代理服务器可以使用该字段来提供有关初始请求的信息。同时还有其它不标准的首部字段，包括````X-Forwarded-Host````，````X-Forwarded-Port````，````X-Forwarded-Proto````，````X-Forwarded-Ssl````以及````X-Forwarded-Prefix````等。

 ````ForwardedHeaderFilter````是一个修改请求的 host、port 以及 scheme 的 Servlet 过滤器，基于````Forwarded````首部字段，然后删除那些首部字段。

关于转发首部的安全考虑，因为应用无法获知这些首部已经被代理添加，有意的，或者是被有问题的客户端错误添加。这就是为什么一个存在于可信集中的代理服务器应该配置为删除到来的请求中的所有不被信任的````Forwarded````首部字段。你也可以在````ForwardedHeaderFilter````中配置````removeOnly=true````，这种情况下，它将会删除但是并不使用这些首部字段。

### 1.2.3 Shallow ETag

````ShallowEtagHeaderFilter````过滤器创建一个“浅” ETag ，通过缓存被写入响应的内容并计算它的 MD5 哈希值。客户端下次发送时，它会重做此动作，但是也会比较计算出的值和````If-None-Match````请求首部字段，如果两者相等，则返回 304（NOT_MODIFIED）状态码响应。

这种策略节省了网络带宽，但是并没有节省 CPU，因为必须为每个请求计算完整的响应的 MD5 哈希值。其它控制器层面的策略，如前所述，可以避免这种计算。参考 [HTTP Caching](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-caching) 。

这种过滤器包含一个````writeWeakETag````参数，该参数配置过滤器写一个弱 ETags，类似于````W/"02a2d595e6ed9a0b24f027f2b63b134d6"````（定义在  [RFC 7232 Section 2.3](https://tools.ietf.org/html/rfc7232#section-2.3) 中）。

### 1.2.4 CORS

Spring MVC 提供了基于控制器注解配置的细粒度的 CORS 支持。然而，当与 Spring Security 配合使用时，我们建议依赖内建的````CorsFilter````，该过滤器必须排在 Spring Security 过滤器链的头部。

参考 [CORS](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-cors) 和 [CORS Filter](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-cors-filter) 获取更多细节。

## 1.3 注解的控制器

Spring MVC 提供了基于注解的编程模型，````@Controller````和````@RestController````组件使用注解来表示请求映射、请求输入、异常处理等等。注解的控制器拥有灵活的方法签名，同时既没有继承基类也没有实现特定的接口。下面的例子展示了注解定义的控制器：

````java
@Controller
public class HelloController {
  
  @GetMapping("/hello")
  public String handle(Model model) {
    model.addAttribute("message", "Hello World!");
    return "index";
  }
}
````

上面例子中的方法接受````Model````类型参数，返回表示视图名称的````String````，不过接下来我们会介绍更多其它选项。

>  [spring.io](https://spring.io/guides) 上的指南和文档都使用了本章节描述的基于注解的编程模型。

###1.3.1 声明

你可以在 Servlet ````WebApplicationContext````中使用标准的 Spring bean 定义来定义控制器 bean 。````@Controller````固定格式允许自动探测，配合 Spring 对 classpath 下的````@Component````类的自动探测和自动注册 bean 定义。它也是注解的类的固定行为格式，表示它作为一个 web 组件的角色。

为了开启这种````@Controller```` beans 的自动探测，你可以在你的 Java 配置类中添加组件扫描，如下所示：

````java
@Configuration
@ComponentScan("org.example.web")
public class WebConfig {
  // ...
}
````

等价的 XML 形式的配置文件内容：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="org.example.web"/>

    <!-- ... -->

</beans>
````

````@RestController````是一个 [组合注解](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-meta-annotations) ，它本身被元注解````@Controller````和````@ResponseBody````修饰，表示控制器中每个犯法都继承类型级别的````@ResponseBody````注解，因此，会将视图解析和由 HTML 摸板渲染的视图直接写入响应体。

**AOP 代理**

某些场景下，你可能需要在运行时用一个 AOP 代理修饰控制器。一个例子是你选择直接用````@Transcational````注解修饰控制器。这种情况下，特别对于控制器，我们推荐使用基于类的代理。这是典型控制器的默认选择。然而，如果控制器必须实现一个接口，而该接口并不是 Spring Context 回调（比如````InitializingBean````，````*Aware````，或者其它），你可能需要显式配置基于类的代理。比如，对````<tx:annotation-driven>````，你可以修改为````<tx:annotation-driven proxy-target-class="true">````。

### 1.3.2 请求映射

你可以使用````@RequestMapping````注解来将请求映射到控制器方法。它包含各种属性由 URL，HTTP 方法，请求参数，首部字段以及媒体类型等来匹配。你可以使用它在类层面表示共享的映射或者在方法层面增强限制到一个特定的服务端点映射。

还有 HTTP 特定的````@RequestMapping````的快捷变体：

* ````@GetMapping````
* ````@PostMapping````
* ````@PutMapping````
* ````@DeleteMapping````
* ````@PatchMapping````

快捷方式是作为 [Custom Annotations](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-composed) 被提供的，因为大多数的控制器方法应该通过使用````@RequestMapping````被映射到一个特定的 HTTP 方法，该注解默认地匹配到所有的 HTTP 方法。同时，````@RequestMapping````仍然需要在类层面表示共享映射。

下面的例子拥有类型和方法层面的映射：

````:3rd_place_medal:
@RestController
@RequestMapping("/persons")
class PersonController {
    
    @GetMapping("/{id}")
    public Person getPerson(@PathVariable Long id) {
        // ...
    }
    
    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public void add(@RequestBody Person person) {
        // ...
    }
}
````

**URI 模式**

你可以使用下列全局模式和通配符来映射请求：

* ````?```` 匹配一个字符
* ````*```` 匹配路径片段中的 0 个或者更多字符
* ````**```` 匹配 0 个或者多个路径片段

你也可以声明 URI 变量同时使用````@PathVariable````访问它们的值，如下面例子所示：

````:3rd_place_medal:
@GetMapping("/owners/{ownerId}/pet/{petId}")
public Pet findPet(@PathVariable Long ownerId, @PathVariable Long petId) {
    // ...
}
````

你可以声明 URI 变量在类层面和方法层面，如下例所示：

````:3rd_place_medal:
@Controller
@RequestMapping("/owners/{ownerId}")
public class OwnerController {

    @GetMapping("/pets/{petId}")
    public Pet findPet(@PathVariable Long ownerId, @PathVariable Long petId) {
        // ...
    }
}
````

URI 变量自动被转化为相应的类型，或者````TypeMismatchException````就会发生。简单类型（````int````，````long````，````Date````等等）默认被支持，同时你还可以注册对任何其它数据类型的支持。参考  [Type Conversion](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-typeconversion) 和 [`DataBinder`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-initbinder) 。

你能够显式命名 URI 变量（比如，````@PathVariable("customId")````），不过你可以不管其中的细节，如果名称相同并且你的代码被携带调试信息进行编译，或者使用 Java 8 上的带````-parameters````编译器标识的编译器编译。

语法````{varName:regex}````声明一个 URI 变量，使用具有````{varName:regex}````语法的正则表达式。比如，给定 URL ````"/spring-web-3.0.5.jar"````，后面跟着的方法提炼名称、版本和文件扩展名：

````:3rd_place_medal:
@GetMapping("/{name:[a-z-]+}-{version:\\d\\.\\d\\.\\d}{ext:\\.[a-z]+}")
public void handle(@PathVariable String version, @PathVariable String ext) {
    // ...
}
````

URI 路径模式也可以内置````${...}````占位符，将通过使用````PropertyPlaceHolderConfigurer````在启动时解析，获取位置、系统、环境以及其它属性源。你可以使用这种机制，比如基于一些外部配置将基 URL 参数化。

> Spring MVC 使用````PathMatcher````契约和来自````spring-core````的````AntPathMatcher````实现来进行 URI 路径匹配。

**模式比较**

当多个模式都匹配到一个 URL，它们必须被比较以发现其中的最佳匹配。这种比较通过使用````AntPathMatcher.getPatternComparator(String path)````来实现，它会寻找更加精准的模式。

一个模式相对不够精准，如果它拥有更低的 URI 变量数（每个变量算1），单个通配符（每个通配符算1）以及双通配符（每个双通配符算2）。给定相等的分数，更长的模式将被选中。给定相等的分数和长度，具有的 URI 变量数超过通配符的模式将被选中。

默认映射模式````/**````不参与评分，它永远都是排在最后的。同时，前缀模式（比如````/public/**````）被认为相比其它不包含双通配符的模式精准度更低。

完整的细节，参考 ````AntPathMatcher````中的````AntPatternComparator````，同时注意你可以订制其中的````PathMatcher````实现。参考配置章节中的  [Path Matching](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-path-matching) 。

**后缀匹配**

默认地，Spring MVC 执行````.*````后缀模式匹配，因而映射到````/person````的控制器同时也显式映射到````/person.*````。文件扩展名然后被用来解读请求内容类型用来构造响应（也就是说，替代````Accept````首部字段），比如，````person.pdf````，````/person.xml````等等。

以这种方式使用文件扩展名是必要的，当浏览器曾发送````Accept````首部字段而很难被解读时。目前，这已经不再必要，同时使用````Accept````首部字段应该是更好的选择。

随着时间推移，文件扩展名的很多使用方式已经被证明是有问题的。当与 URI 变量、路径参数以及 URI 编码共同使用时会导致模棱两可的情况。关于基于 URL 的授权和安全问题的推断将会变的更加困难。

为了彻底禁止文件扩展名的使用，你必须配置一下两个属性：

* ````useSuffixPatternMatching(false)````，参考 [PathMatchConfigurer](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-path-matching)
* ````favorPathExtension(false)````，参考 [ContentNegotiationConfigurer](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-content-negotiation)

基于 URL 的内容协商仍然是有用的（比如，当在浏览器中键入一个 URL）。为了开启这一特性，我们推荐使用基于查询参数的策略来避免大多数使用文件扩展名带来的问题。或者，如果你必须使用文件扩展名，请考虑通过 [ContentNegotiationConfigurer](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-content-negotiation) 的`mediaTypes`属性将它们限制为显式注册的扩展名列表 。

**后缀匹配和反射文件下载 RFD**

反射文件下载攻击类似于 XSS 攻击，都是基于请求输入（比如，一个查询参数和一个 URI 变量）被反射在响应中。不过，替代将 JavaScript 插入 HTML 中，RFD 攻击依赖浏览器切换到执行一个下载，同时将响应作为一个可执行的脚本，当随后被双击时。

在 Spring MVC 中，````@ResponseBody````和````ResponseEntity````方法都处于风险中，因为它们可以渲染不同类型的内容，而客户端能够通过 URL 路径扩展来请求。关闭后缀模式匹配并使用路径扩展来进行内容协商降低了风险，但是并不足够防止 RFD 攻击。

为了防范 RFD 攻击，在渲染响应体之前，Spring MVC 添加一个````Content-Disposition:inline;filename=f.txt````首部字段来建议一个固定的和安全的下载文件。只有当 URL 路径包含一个文件扩展名，该扩展名既不在白名单中，又没有显式注册为内容协商时这一点才能完成。然而，它有个潜在的副作用，当 URLs 被直接键入浏览器中时。

许多通用的路径扩展默认都是在白名单中的。拥有定制化````HttpMessageConverter````实现的应用能够为内容协商显式注册文件扩展，以避免为那些扩展名添加一个````Content-Disposition````首部字段。

参考 [CVE-2015-5211](https://pivotal.io/security/cve-2015-5211) 获取更多有关 RFD 的附加推荐做法。

**可消费媒体类型**

你可以基于````Content-Type````请求首部字段来加强请求映射限制，如下面例子所示：

````java
@PostMapping(path = "/pets", consumes = "application/json")
public void addPet(@RequestBody Pet pet) {
    // ...
}
````

使用一个````consumes````属性通过内容类型来缩窄请求映射范围。

consumes````属性也支持反向表达式，比如````!text/plain````表示````text/plain````之外的所有内容类型。

你可以在类层面声明一个共享````consumes````属性。不像大多数其他请求映射属性，当被使用在类层面时，方法层面的````consumes````属性会覆盖而不是扩展类层面的声明。

> ````MediaType````提供了常用媒体类型常量，比如````APPLICATION_JSON_VALUE````和````APPLICATION_XML_VALUE````。

**可生产的媒体类型**

你可以基于````Accept````请求首部字段以及控制器方法产生的内容类型列表来缩窄请求映射范围，如下面例子所示：

````java
@GetMapping(path = "/pets/{petId}", produces = "application/json;charset=UTF-8")
@ResponseBody
public Pet getPet(@PathVariable String petId) {
    // ...
}
````

使用一个````produces````属性通过内容类型来缩窄请求映射范围。

媒体类型可以指定字符集。支持反向表达式－比如，````!text/plain````表示除了````text/plain````之外的所有内容类型。

> 对 JSON 内容类型来说，UTF-8 字符集应该被指定，即使 [RFC7159](https://tools.ietf.org/html/rfc7159#section-11) 明确指出“没有味此内容类型注册定义字符集参数”，因为一些浏览器需要它来正确解读 UTF-8 特殊字符。

你可以在类层面声明一个共享````produces````属性。不像其他大多数请求映射属性，当被使用在类层面时，方法层面的````produces````属性会覆盖而不会扩展类层面的声明。

> ````MediaType````提供了常用的媒体类型常量，比如````APPLICATION_JSON_UTF-8_CALUE````和````APPLICATION_XML_VALUE```` 。

**参数，首部字段**

你可以基于请求参数条件缩窄请求映射范围。你可以检测存在请求参数````myParam````的情况以及不存在请求参数````!myParam````的情况，或则检测特殊的参数值````myParam=myValue````的情况。下面例子展示了如何检测一个特定的参数值：

````java
@GetMapping(path = "/pets/{petId}", params = "myParam=myValue")
public void findPet(@PathVariable String petId) {
    // ...
}
````

检测参数````myParam````是否等于````myValue````。

你也可以使用请求首部字段条件，如下面例子所示：

````java
@GetMapping(path = "/pets", headers = "myHeader=myValue")
public void findPet(@PathVariable String petId) {
    // ...
}
````

检测````myHeader````是否等于````myValue````。

> 你能够将````Content-Type````和````Accept````首部字段与首部字段进行匹配，不过最好使用 [consumes](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-consumes) 和 [produces](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-produces) 来代替。

**HTTP HEAD, OPTIONS**

````@GetMapping````（以及````@RequestMapping(method=HttpMethod.GET)````）支持 HTTP HEAD 的透明请求映射。控制器方法不需要改变。一个响应包装其，应用于````javax.servlet.http.HttpServlet````，确保````Content-Length````首部字段被设置为被写的字节数（并不实际写入响应）。

````GetMapping````（以及````@RequestMapping(method=HttpMethod.GET````)）被显式映射到而且支持 HTTP HEAD 。一个 HTTP HEAD 请求被等同于 HTTP GET 请求处理，除了写入响应体，字节数会被计算，````Content-Length````首部字段会被设置。

默认地，HTTP OPTIONS 被处理，通过设定````Allow````响应首部字段为匹配到 URL 模式的````@RequestMapping````方法中列出的 HTTP 方法。

对一个没有声明 HTTP 方法的````@RequestMapping````，````Allow````首部字段被设定为````GET, HEAD, POST, PUT, PATCH, DELETE, OPTIONS```` 。控制器方法应用始终声明支持的 HTTP 方法（比如，通过使用 HTTP 特定变体：````@GetMapping````，````@PostMapping````，等等）。

你可以将````@RequestMapping````方法映射到 HTTP HEAD 和 HTTP OPTIONS，不过，通常情况下这不是必须的。

**定制注解**

Spring MVC 支持对请求映射使用 [组合注解](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-meta-annotations) 。那些注解本身是被````@RequestMapping````进行了元注解标注的，同时结合重声明一个子集（或者全部）的````@RequestMapping````属性，为了一个更窄的更精准的目的。

````@GetMapping````，````@PostMapping````，````@PutMapping````，````@DeleteMapping````以及````@PatchMapping````是组合注解的例子。它们被提供的动机，很明显，大部分的控制器方法 应该被映射到特定的 HTTP 方法，而不是使用通过使用````@RequestMapping````匹配到所有的 HTTP 方法。如果你需要一个组合注解的例子，参考如何声明它们。

Spring MVC 也支持定制请求映射属性和定制化请求匹配逻辑。这是一种高级选项，需要子类````RequestMappingHandlerMapping````同时覆盖````getCustomMethodCondition````方法，当你能够检查定制属性并返回你自己的````RequestCondition````。

**明确的注册**

你可以编程方式注册处理方法，你可以用来动态注册或者用于其它高级场景，比如不同 URLs 下同一个处理器的不同实例。下面的例子注册了一个处理器方法：

````java
@Configuration
public class MyConfig {
    @Autowired
    public void setHandlerMapping(RequestMappingHandlerMapping mapping, UserHandler handler) throws NoSuchMethodException {										//(1)
        RequestMappingInfo info = RequestMappingInfo.paths("/user/{id}").methods(RequestMethod.GET).build();  //(2)
        Method method = UserHandler.class.getMethod("getUser", Long.class);	//(3)
        mapping.registerMapping(info, handler, method);						//(4)
    }
}
````

(1) 注入目标处理器和处理器映射到控制器。

(2) 准备请求映射元数据。

(3) 获取处理方法。

(4) 添加注册。

### 1.3.3 处理器方法

````@RequestMapping````处理器方法拥有一个灵活的签名，能够从支持的控制器方法参数和返回值范围中选择。

**方法参数**

下面的表描述了支持的控制器方法参数。任何参数都爱不支持反应式类型。

JDK 8 中与注解相结合的````java.util.Optional````作为一个方法参数被支持，这些注解拥有一个````required````属性（比如，````@RequestParam````，````@RequestHeader````等等）并等价于````required=false````。

| 控制器方法参数                                  | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| ````WebRequest````，````NativeWebRequest```` | 一般的对请求参数和请求和会话属性的访问，不直接使用 Servlet API 。  |
| ````javax.servlet.ServletRequest````<br />````javax.servlet.ServletResponse```` | 选择任何特定的请求或者响应类型－比如，ServletRequest，HttpServletRequest，或者 Spring 的````MultipartRequest````，````MultipartHttpServletRequest````。 |
| ````javax.servlet.http.HttpSession````   | 强制会话存在。由此，这个参数永远不会为````null````。注意，会话的访问不是线程安全的。设置````RequestMappingHandlerAdapter````实例的````synchronizeOnSession````标识为````true````，如果允许多个请求并发访问一个会话。 |
| ````javax.servlet.http.PushBuilder````   | Servlet 4.0 的推送构建器 API 用于编程方式 HTTP/2 资源推送。注意，每个 Servlet 规范，注入的 PushBuilder 实例可以为 ````null````，如果客户端不支持 HTTP/2 新特性。 |
| ````java.security.Principal````          | 当前已认证用户－可能一个特定 Principal 实现类，如果知道。       |
| ````HttpMethod````                       | 请求的 HTTP 方法。                             |
| ````java.util.Locale````                 | 当前请求语言环境，由最精准的可用````LocaleResolver````（实际上就是配置的````LocaleResolver````或者````LocaleContextResolver````）决定。 |
| ````java.util.TimeZone```` +<br />````java.time.ZoneId```` | 当前请求相关的时区，由 LocaleContextResolver 确定。    |
| ````java.io.InputStream````<br />````java.io.Reader```` | 用于访问通过 Serlvet API 暴露的未加工的请求体。           |
| ````java.io.OutputSteam````<br />````java.io.Writer```` | 用于访问通过 Serlvet API 暴露的未加工的响应体。           |
| ````@PathVariable````                    | 用于访问 URI 模版变量，参考 [URI patterns](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-uri-templates) 。 |
| ````@MatrixVariable````                  | 用于访问 URI 路径片段中的名值对，参考 [Matrix Variables](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-matrix-variables) 。 |
| ````@RequestParam````                    | 用于访问 Servlet 请求参数，包含多部分文件。参数值被转换为声明的方法参数类型。参考[`@RequestParam`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestparam) 以及 [Multipart](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-multipart-forms) 。<br />注意，为简单参数值使用````@RequestParam````是可选的。参考本表末尾的“其它参数”。 |
| ````@RequestHeader````                   | 用于访问请求首部字段。首部字段值呗转化为声明的方法参数类型。参考 [`@RequestHeader`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestheader) 。 |
| ````@CookieValue````                     | 用于访问 cookies。Cookies 值被转化为声明的方法参数类型。参考 [`@CookieValue`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-cookievalue) 。 |
| ````@RequestBody````                     | 用来访问 HTTP 请求体。请求体内容通过使用````HttpMessageConverter````实现被转化为声明的方法参数类型。参考 [`@RequestBody`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestbody) 。 |
| ````HttpEntity<B>````                    | 用于访问请求首部字段和请求体。请求体通过````HttpMessageConverter````转化。参考 [HttpEntity](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-httpentity) 。 |
| ````@RequestPart````                     | 用于访问````multipart/form-data````请求中的一个部分数据，通过````HttpMessageConverter````转化该部分数据体。参考 [Multipart](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-multipart-forms) 。 |
| ````java.util.Map````<br />````org.springframework.ui.Model````<br />````org.springframework.ui.ModelMap```` | 用于访问数据模型，该模型 HTML 控制器使用，并作为视图渲染的一部分被暴露给视图模版。 |
| ````RedirectAttributes````               | 用于重定向场景的特定属性（也就是说，会被添加到查询字符串中），同时清理将被临时存储的属性直到请求重定向完成。参考 [Redirect Attributes](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-redirecting-passing-data) 和 [Flash Attributes](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-flash-attributes) 。 |
| ````ModelAttribute````                   | 用于访问模型中已经存在的属性，连同数据绑定和应用的验证。参考 [`@ModelAttribute`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-modelattrib-method-args) 以及 [Model](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-modelattrib-methods) 和 [`DataBinder`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-initbinder) 。<br />注意，````@ModelAttribute````的使用是可选的（比如要设置它的属性），参考本表末尾的“其它参数”。 |
| ````Errors````<br />````BindingResult```` | 用于访问来自对一个命令对象（也就是一个````@ModelAttribute````参数）进行的验证和数据绑定的错误，或者来自````@RequestBody````或者````@RequestPart````参数验证的错误。验证方法参数之后你必须立即声明一个````Errors````或者````BidingResult````参数。 |
| ````SessionStatus````＋ 类层面的 ````@SessionAttributes```` | 为了标识表单处理完成，该状态将触发通过类层面的````@SessionAttributes````注解声明的会话属性的清理。参考 [`@SessionAttributes`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-sessionattributes) 获取更多细节。 |
| ````UriComponentsBuilder````             | 准备一个相对于当前请求的主机、端口、协议、上下文路径以及 servlet 映射字面部分的 URL 。参考 [URI Links](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-uri-building) 。 |
| ````@SessionAttribute````                | 用于访问任何会话属性，不同于作为类层面的````@SessionAttributes````声明的结果的存储在会话中的模型属性。参考 [`@SessionAttribute`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-sessionattribute) 获取更多细节。 |
| ````@RequestAttribute````                | 用于访问请求属性。参考 [`@RequestAttribute`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestattrib) 。 |
| 其它参数                                     | 任何本表中没有匹配到的简单类型参数（由 [BeanUtils#isSimpleProperty](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/beans/BeanUtils.html#isSimpleProperty-java.lang.Class-) 确定），被作为````@RequestParam````解析。否则，将被作为````@ModelAttribute````解析。 |

**返回值**

下表描述了支持的控制器方法返回值。所有响应值都支持反应式类型。

| 控制器方法返回值                                 | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| ````@ResponseBody````                    | 返回值通过````HttpMessageConverter````实现转化并写入响应。参考 [`@ResponseBody`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-responsebody) 。 |
| ````HttpEntity<B>````，````ResponseEntity<B>```` | 指定完整响应（包括 HTTP 首部字段和主体）的返回值通过````HttpMesssageConverter````实现转化并写入响应。参考 [ResponseEntity](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-responseentity) 。 |
| ````HttpHeaders````                      | 为了返回一个响应，包含首部字段，但是没有主体。                  |
| ````String````                           | 一个视图名称将被````ViewResolver````实现解析被与明确的模型共同使用－通过命令对象和````@ModelAttribute````方法确定。控制器方法也能够通过编程方式通过声明一个````Model````参数来丰富模型。参考 [Explicit Registrations](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-registration) 。 |
| ````View````                             | 一个````View````实例结合明确的数据模型进行渲染－通过命令对象和````@ModelAttribute````方法来确定。处理器方法与能够以编程方式通过声明````Model````参数来丰富模型。参考 [Explicit Registrations](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-registration) 。 |
| ````java.util.Map````<br />````org.springframework.ui.Model```` | 将被添加进入明确模型的属性，连同通过````RequestToViewNameTranslator````显式确定的视图名称。 |
| ````@ModelAttribute````                  | 一个将被添加进入模型的属性，连同通过````RequestToViewNameTranslator````显式确定的视图名称。<br />注意，````@ModelAttribute````是可选的。参考表末尾的“其它返回值”。 |
| ````ModelAndView````对象                   | 将要使用的视图和模型属性，以及可选的，响应状态。                 |
| ````void````                             | 具有````void````返回值（或者````null````返回值）的方法被认为拥有完整的处理之后的响应，如果它也拥有一个````ServletResponse````，一个````OutputStream````参数，或者一个````@ResponseStatus````注解。如果控制器进行一个确定的````ETag````或者````lastModified````时间戳检查时也会是这样。<br />如果上述情况都没有出现，````void````返回值也可以表示没有响应体为 REST 控制器返回，或者为 HTML 控制器选择了默认的视图名称。 |
| ````DeferredResult<V>````                | 从任何线程中异步产生前面提到的任何返回值－比如，作为一些事件或者回调的结果。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [`DeferredResult`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-deferredresult) 。 |
| ````Callable<V>````                      | 从任何 Spring MVC 管理的线程中异步产生任何上面提到的返回值。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [`Callable `](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-callable) 。 |
| ````ListenableFutrue<V>````<br />````java.util.concurrent.CompletionStatege<V>````<br />````java.util.concurrent.CompletableFuture<V>```` | ````DeferredResult````的替代品，为了方便（比如，当一个基础服务返回它们其中之一时）。 |
| ````ResponseBodyEmitter````<br />````SseEmitter```` | 通过````HttpMessageConverter````实现异步发出一个将要被写入响应中的对象流。同时支持作为````ResponseEntity````的主体。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [HTTP Streaming](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-http-streaming) 。 |
| ````StreamingResponseBody````            | 异步写入响应````OutputStream````。同时支持作为````ResponseEntity````的主体。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [HTTP Streaming](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-http-streaming) 。 |
| 反应式类型－反应器，RxJava，或者通过````ReactiveAdapterRegistry````得到的其它东西。 | ````DeferredResult````的替代品，将多个值流（比如````Flux````，````Observable````）收集称为一个````List````。<br />流式场景下（比如````text/event-stream````，````application/json+stream````），````SseEmitter````和````ResponseBodyEmitter````被使用，这些地方````ServletOutputStream````阻塞式 I/O 执行在 Spring MVC 管理的线程上并导致了每次写入完成的压力。<br />参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [Reactive Types](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-reactive-types) 。 |
| 其它返回值                                    | 任何没有匹配到此表中提到的返回值的返回值，如果是````String````或者````void````就会被作为视图名称（默认视图名称选择通过````RequestToViewNameTranslator````执行），提供它不是一个简单类型，通过 [BeanUtils#isSimpleProperty](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/beans/BeanUtils.html#isSimpleProperty-java.lang.Class-) 决定。简单类型的返回值就不会被解析。 |

**类型转换**

一些被注解标记的控制器方法参数表示基于````String````的请求输入（比如````@RequestParam````，````@RequestHeader````，````@PathVariable````，````@MatrixVariable````以及````@CookieValue````）会需要类型转换，如果参数被声明为````String````之外的其他类型。

这种情况下，类型转换基于配置的转换器自动执行。默认地，简单类型（````int````，````long````，````Date````等等）都支持。你可以定制类型转换过程，通过````WebDataBinder````（参考 [`DataBinder`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-initbinder)）或者通过使用````FormattingConversionService````注册````Formatters````。参考  [Spring Field Formatting](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#format) 。

**矩阵变量**

[RFC 3986](https://tools.ietf.org/html/rfc3986#section-3.3) 讨论了路径片段中的名值对。在 Spring MVC 中，我们称之为矩阵变量，这个名称基于蒂姆伯纳斯李的 [一篇旧文](https://www.w3.org/DesignIssues/MatrixURIs.html)，不过我们也可以把它们称之为 URI 路径参数。

矩阵变量可以出现在任何路径片段中，每个变量由分号分隔，一个变量的多个值由逗号分隔（比如````/cars;color=red,green;year=2012````）。多个变量值也可以通过相同的变量名指定（比如````color=red;color=green;color=blue````）。

如果一个 URL 被期望包含矩阵变量，则用于控制器方法的请求映射久必须使用 URI 变量累掩盖那些变量的内容，同时确保请求能够成功匹配，无论其中矩阵变量的顺序或者存在与否。下面例子使用了矩阵变量：

````java
// GET /pets/42;q=11;r=22

@GetMapping("/pets/{petId}")
public void findPet(@PathVariable String petId, @MatrixVarialbe int q) {
    // petId == 42
    // q == 11
}
````

考虑到所有路径片段都可能包含矩阵变量，你可能需要确定矩阵变量希望作为哪个路径变量。下面的例子展示了如何做到这一点：

````java
// GET /owners/42;q=11/pets/21;q=22

@GetMapping("/owners/{ownerId}/pets/{petId}")
public void findPet(
    @MatrixVariable(name="q", pathVar="ownerId") int q1,
    @MatrixVariable(name="q", pathVar="petId") int q2) {
    
    // q1 == 11
    // q2 == 22
}
````

矩阵变量可以被定为为可选的，同时指定一个默认值，如下面例子所示：

````java
// GET /pets/42

@GetMapping("/pets/{petId}")
public void findPet(@MatrixVariable(required=false, defaultValue="1") int q) {

    // q == 1
}
````

为了获取所有矩阵变量，你可以使用````MultiValueMap````，如下面例子所示：

````java
// GET /owners/42;q=11;r=12/pets/21;q=22;s=23

@GetMapping("/owners/{ownerId}/pets/{petId}")
public void findPet(
        @MatrixVariable MultiValueMap<String, String> matrixVars,
        @MatrixVariable(pathVar="petId") MultiValueMap<String, String> petMatrixVars) {

    // matrixVars: ["q" : [11,22], "r" : 12, "s" : 23]
    // petMatrixVars: ["q" : 22, "s" : 23]
}
````

注意，你需要开启矩阵变量使用。在 MVC Java 配置类中，你需要通过  [Path Matching](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-config-path-matching) 设置````UrlPathHelper````中的属性````removeSemicolonContent=false````。在 MVC XML 命名空间中，你可以配置````<mvc:annotation-drivenenable-matrix-varialbe="true"/>````。

**````@RequestParam````**

你可以使用````@RequestParam````注解来绑定 Servlet 请求参数（也就是说，查询参数或者表单数据）到控制器方法参数。下面例子展示了如何做：

````java
@Controller
@RequestMapping("/pets")
public class EditPetForm {

    // ...

    @GetMapping
    public String setupForm(@RequestParam("petId") int petId, Model model) { 
        Pet pet = this.clinic.loadPet(petId);
        model.addAttribute("pet", pet);
        return "petForm";
    }

    // ...

}
````

使用````@RequestParam````绑定````petId````。

默认地，使用此注解的方法参数都是必需的，不过你可以指定这些方法参数为可选的，通过设定````@RequestParam````注解的````required````标志为````false````，或者使用````java.util.Optional````包装器声明该参数。

类型转换在目标方法参数类型不是````String````时会自动执行。参考  [Type Conversion](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-typeconversion) 。

声明参数类型为一个数组或者列表允许为相同的参数名称解析多个参数值。

当一个````@RequestParam````注解呗声明为````Map<String, String>````或者````MultiValueMap<String, String>````时，注解中没有制定参数名称，则该 map 就为每个给定的参数名称保存相应的参数值。

注意，````@RequestParam````的使用是可选的（比如，设定它的属性）。默认地，任何简单类型的参数（由  [BeanUtils#isSimpleProperty](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/beans/BeanUtils.html#isSimpleProperty-java.lang.Class-) 确定）以及任何没有被其他参数解析器解析的参数，都会被如同它们被````@RequestParam````注解修饰了那样对待。

**````@RequestHeader````**

你可以使用````@RequestHeader````注解来绑定请求首部到控制器中的方法参数。

考虑下面的请求，包含首部：

````
Host                    localhost:8080
Accept                  text/html,application/xhtml+xml,application/xml;q=0.9
Accept-Language         fr,en-gb;q=0.7,en;q=0.3
Accept-Encoding         gzip,deflate
Accept-Charset          ISO-8859-1,utf-8;q=0.7,*;q=0.7
Keep-Alive              300
````

下面的例子展示了如何获取````Accept-Encoding````和````Keep-Alive````首部字段值：

````java
@GetMapping("/demo")
public void handle(
        @RequestHeader("Accept-Encoding") String encoding, 
        @RequestHeader("Keep-Alive") long keepAlive) { 
    //...
}
````

如果目标方法参数类型不是````String````，类型转换就会自动进行。参考 [Type Conversion](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-typeconversion) 。

当````@RequestHeader````注解用在````Map<String, String>````，````MultiValueMap<String, String>````，或者````HttpHeaders````参数上时，该 map 就包含所有的首部字段值。

> 内建支持可以将逗号分隔的字符串转化为字符串数组或者集合，或者其他类型转换系统知道的类型。比如，一个注解为````@RequestHeader("Accept")````的方法参数可以是````String````类型，也可以是````String[]````，或者````List<String>````。

**````@CookieValue````**

你可以使用````@CookieValue````注解绑定 HTTP cookie 值到控制器方法参数。

考虑携带如下 cookie 的请求：

````
JSESSIONID=415A4AC178C59DACE0B2C9CA727CDD84
````

下面例子展示了如何获取该 cookie 值：

````java
@GetMapping("/demo")
public void handle(@CookieValue("JSESSIONID") String cookie) { 
    //...
}
````

如果目标方法参数类型不是````String````，类型转换就会自动进行。参考 [Type Conversion](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-typeconversion) 。

**````@ModelAttribute````**

你可以在方法参数上使用````@ModelAttribute````注解来访问模型属性或者当该属性不存在时将其实例化。模型属性同时还覆盖了来自 HTTP Servlet 请求参数中名称匹配到字段名称的参数值。这就是所谓的数据绑定，它使得你不需要为每个查询参数和表单字段处理解析和类型转换。下面例子展示了如何使用：

````java
@PostMapping("/owners/{ownerId}/pets/{petId}/edit")
public String processSubmit(@ModelAttribute Pet pet) { } 
````

例子中````Pet````实例解析过程如下：

* 来自模型，如果已经通过 [Model](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-modelattrib-methods) 添加。
* 来自 HTTP 会话，使用````@SessionAttributes````。
* 来自 URI 路径变量，那些变量呗传递通过````Converter````。
* 来自默认构造器方法调用。
* 来自“主要构造器”方法调用，携带匹配到 Servlet 请求参数的方法参数。参数名称通过````@ConstructorProperties```` JavaBeans 确定，或者通过运行时在字节码文件中保持的参数名称。

尽管使用 [Model](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-modelattrib-methods) 来根据属性产生模型的用法非常普遍，另外一种方法依赖于````Converter<String, T>````与 URI 路径变量结合使用的传统做法。下面的例子中，模型属性名````account````匹配到 URI 路径变量````ccount````，则````Account````被加载通过由一个注册的````Converter<String, Account>````传递的````String````类型的 account 数字：

````java
@PutMapping("/accounts/{account}")
public String save(@ModelAttribute("account") Account account) {
    // ...
}
````

当模型属性实例呗获取之后，数据绑定就会执行。````WebDataBinder````类匹配 Servlet 请求参数名（查询参数和表单字段）到目标````Object````的字段名。匹配的字段在类型转换执行之后生成，如果有必要。更多有关数据绑定（以及校验）的细节参考 [Validation](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#validation) 。更多有关定制化数据绑定的细节，参考 [`DataBinder`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-initbinder) 。

数据绑定可能会出错。默认地，一个````BindException````会产生。不过，为了在控制器方法中检查这种错误，你可以添加一个````BindingResult````参数，就在````@ModelAttribute````旁边，如下面例子所示：

````java
@PostMapping("/owners/{ownerId}/pets/{petId}/edit")
public String processSubmit(@ModelAttribute("pet") Pet pet, BindingResult result) {
    if (result.hasErrors()) {
        return "petForm";
    }
    // ...
}
````

某些情况下，你可能希望不进行数据绑定而访问模型属性。此时，你可以注射````Model````进入控制器并直接访问它，或者，设定````@ModelAttribute(binding=false)````，如下面例子所示：

````java
@ModelAttribute
public AccountForm setUpForm() {
    return new AccountForm();
}

@ModelAttribute
public Account findAccount(@PathVariable String accountId) {
    return accountRepository.findOne(accountId);
}

@PostMapping("update")
public String update(@Valid AccountForm form, BindingResult result, @ModelAttribute(binding=false) Account account) {
    // ...
}
````

我们可以在数据绑定之后自动执行验证，通过添加````javax.validation.Valid````注解或者 Spring 的````@Validated````注解（ [Bean Validation](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#validation-beanvalidation) 和 [Spring validation](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#validation)）。下面例子所示：

````java
@PostMapping("/owners/{ownerId}/pets/{petId}/edit")
public String processSubmit(@Valid @ModelAttribute("pet") Pet pet, BindingResult result) {
    if(result.hasErrors()) {
        return "petForm";
    }
    // ...
}
````

注意，````@ModelAttribute````使用是可选的（比如，设定它的属性）。默认地，任何非简单值类型（由 [BeanUtils#isSimpleProperty](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/beans/BeanUtils.html#isSimpleProperty-java.lang.Class-) 确定）并没有被任何其他参数解析器解析的参数都被等同于它被````@ModelAttribute````注解修饰处理。

**````@SessionAttributes````**

此注解用来在请求之间将模型属性存储在 HTTP Servlet 会话中。它是一个类型层面的注解，声明了一个特定控制器所使用的会话属性。这些典型的模型属性名称列表或者模型属性类型应该被透明存储在会话中，供后续请求访问。

下面的例子使用了````@SessionAttributes````注解：

````java
@Controller
@SessionAttributes("pet")
public class EditPetForm {
    // ...
}
````

第一个请求中，当名为````pet````的模型属性被添加到模型中，它就会被自动提交并存储到 HTTP Servlet 会话中。它就会维持在那里，直到别的控制器方法使用````SessionStatus````方法参数来清理存储，如下面例子所示：

````java
@Controller
@SessionAttributes("pet") 
public class EditPetForm {

    // ...

    @PostMapping("/pets/{id}")
    public String handle(Pet pet, BindingResult errors, SessionStatus status) {
        if (errors.hasErrors) {
            // ...
        }
            status.setComplete(); 
            // ...
        }
    }
}
````

**````@SessionAttribute````**

如果你需要访问业已存在的会话属性，那些属性被全局管理（也就是说，在控制器范围之外－比如，由过滤器管理），可能存在也可能不存在，你可以在方法参数上使用````@SessionAttribute````注解，如下面例子所示：

````java
@RequestMapping("/")
public String handle(@SessionAttribute User user) {
    // ...
}
````

需要添加或者删除会话属性的使用案例中，考虑注射````org.springframework.web.context.request.WebRequest````或者````javax.servlet.http.HttpSession````进入控制器方法。

作为控制器工作流一部分，为了临时将模型属性存储在会话中考虑使用````@SessionAttributes````，如 [`@SessionAttributes`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-sessionattributes) 中所描述的。

**````@RequestAttribute````**

类似于````@SessionAttribute````，你可以使用````@RequestAttribute````注解来访问业已存在的早先创建出来的请求属性（比如，由 Servlet ````Filter```` 或者 ````HandlerInterceptor````创建）：

````java
@GetMapping("/")
public String handler(@RequestAttribute Client client) {
    // ...
}
````

**Redirect Attributes**

默认地，所有模型属性都被认为将被在重定向 URL 中作为 URI 模版变量而被暴露出来。剩余的属性，那些基本类型、基本类型的集合或者数组都会自动附加为查询参数。

基本类型的参数附加称为查询参数可以是期望中的结果，如果模型实例专门为重定向准备。不过，在被注解的控制器中，模型能够包含额外的为了渲染目的而添加的属性（例如，下拉字段值）。为了避免这些字段出现在 URL 中的可能性，````@RequestMapping````注解修饰的方法可以声明一个````RedirectAttributes````类型的参数，用来指定扩展属性对````RedirectView````可用。如果该方法执行了重定向，则````RedirectAttributes````的内容就会被使用。否则，使用模型内容。

````RequestMappingHandlerAdapter````提供了一个标志，名为````ignoreDefaultModelOnRedirect````，你可以使用它表示默认````Model````的内容应该永远不被使用，如果控制器方法执行重定向。替代方案，控制器方法应该声明一个````RedirectAttributes````类型的属性，或者，如果不能这么做，就不应该向````RedirectView````传递任何属性。XML 命名空间和 MVC Java 配置都保持此标志值为````false````，以保持向后兼容。不过，对新版本的应用，我们推荐将其设置为````true````。

注意，来自当前请求的 URI 模版变量会自动成为可用的，当展开一个重定向 URL，而你也不需要使用````Model````或者````RedirectAttributes````显式添加它们。下面的例子展示了如何定义重定向：

````java
@PostMapping("/files/{path}")
public String upload(...) {
    // ...
    return "redirect:file/{path}";
}
````

另外一种传递数据到重定向目标的方法是通过使用````flash````属性。不像其他重定向属性，````flash````属性被保存在 HTTP 会话中（因此，不会出现在 URL 中）。参考  [Flash Attributes](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-flash-attributes) 获取更多细节。

**Flash 属性**

Flash 属性提供了一种在一个请求中保存供别的请求使用的属性的方法。这在重定向场景下最常见－比如，所谓的````Post-Redirect-Get````模式。临时保存的 Flash 属性在重定向发生之前对请求是可用的，当重定向发生之后就会被立即删除。

Spring MVC 包含两种主要的抽象来支持 flash 属性。````FlashMap````被用来持有 flash 属性，而````FlashMapManager````则被用来保存、查询以及管理````FlashMap````实例。

Flash 属性支持永远是开启状态，而不需要显式开启。不过，如果不用，它就永远不会导致 HTTP 会话的创建。在每个请求上，存在一个输入````FlashMap````包含从前一个请求（如果存在）传递过来的属性，还有一个输出````FlashMap````用来保存供下一个请求使用的属性。两个````FlashMap````实例可以在 Spring MVC 中的任何地方通过````RequestContextUtils````的静态方法访问。

注解的控制器通常不需要直接与````FlashMap````配合工作。替代方案时，````@RequestMapping````方法可以接受一个````RedirectAttributes````类型的参数，并使用它为重定向场景添加````flash````属性。通过````RedirectAttributes````添加的 Flash 属性被自动传递到输出````FlashMap````。类似的，重定向之后，来自输入````FlashMap````的属性被自动添加到控制器为目标 URL 服务的````Model````中。

> 匹配请求到 flash 属性
>
> flash 属性的概念存在于很多其他 web 框架中，已经被证明有时候会导致并发问题。这是因为，按照定义，flash 属性被存储直到下一个请求。然而，确切的"下一个"请求可能并不是通信对方认为的，而是另外的一个异步请求（例如，资源池化请求），这种情况下 flash 属性就会被过早删除。
>
> 为了减低上述情况的可能性，````RedirectView````自动以目标重定向 URL 的路径和查询参数标记````FlashMap````实例。然后，默认的````FlashMapManager````匹配那些信息到新到来的请求，当它搜索输入````FlashMap````时。
>
> 这样并不能彻底避免并发问题的可能性，只是通过重定向 URL 中可用信息显著降低问题出现的几率。因此，我们推荐你主要在重定向场景下使用 flash 属性。

**Multipart**

当````MultipartResolver````已经 [enabled](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-multipart) ，POST 请求的````multipart/form-data````格式的内容被转化并可作为规则的请求参数访问。下面的例子访问一个规则的表单字段和一个上传的文件：

````java
@Controller
public class FileUploadController {
    
    @PostMapping("/form")
    public String handleFormUpload(@RequestParam("name") String name, @RequestParam("file") MultipartFile file) {
        if(!file.isEmpty()) {
            byte[] bytes = file.getBytes();
            // store the bytes somewhere
            return "redirect:uploadSuccess";
        }
        return "redirect:uploadFailure";
    }
}
````

声明参数类型为````List<MultipartFile>````允许用同一个参数名称包含多个文件。

当````@RequestParam````注解被声明为````Map<String, MultipartFile>````或者````MultiValueMap<String, MultipartFile>````，而注解中没有指定参数名称，则其中的 map 就会基于对应于每个给定参数名称的 multipart 文件产生。

> 配合 Servlet 3.0 multipart 转化机制，你也可以声明````javax.servlet.http.Part````来替代 Spring 的````MultipartFile````，作为一个方法参数或者集合值类型。

你也可以使用 multipart 内容作为部分数据绑定到一个 [command object](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-modelattrib-method-args) 。比如，上面例子中的表单字段和文件可能是一个表单对象上的字段，如下面例子所示：

````java
class MyForm {
    
    private String name;
    
    private MultipartFile file;
    
    // ...
}

@Controller
public class FileUploadController {
    
    @PostMapping("/form")
    public String handleFormUpload(MyForm form, BindingResult errors) {
        if(!form.getFile().isEmpty()) {
            byte[] bytes = form.getFile().getBytes();
            // store the bytes somewhere
            return "redirect:uploadSuccess";
        }
        return "redirect:uploadFailure";
    }
}
````

Multipart 请求还可以由非浏览器客户端发出，典型地是在 RESTful 服务场景中。下面的例子展示了 JSON 文件：

````
POST /someUrl
Content-Type: multipart/mixed

--edt7Tfrdusa7r3lNQc79vXuhIIMlatb7PQg7Vp
Content-Disposition: form-data; name="meta-data"
Content-Type: application/json; charset=UTF-8
Content-Transfer-Encoding: 8bit

{
    "name": "value"
}
--edt7Tfrdusa7r3lNQc79vXuhIIMlatb7PQg7Vp
Content-Disposition: form-data; name="file-data"; filename="file.properties"
Content-Type: text/xml
Content-Transfer-Encoding: 8bit
... File Data ...
````

你可以使用````@RequestParam````访问 meta-data 部分，作为一个````String````，但是你可能希望它被从 JSON 反序列化（类似于````@RequestBody````）。使用````@RequestPart````注解来访问一个 multipart ，在它经过 [HttpMessageConverter](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/integration.html#rest-message-conversion) 转化之后：

````java
@PostMapping("/")
public String handle(@RequestPart("meta-data") MetaData metadata,
        @RequestPart("file-data") MultipartFile file) {
    // ...
}
````

你可以结合使用````@RequestPart````和````javax.validation.Valid````或者使用 Spring 的````@Validated````注解，两种方式都将导致标准的 Bean 验证被执行。默认地，验证错误导致````MethodArgumentNotValidException````，然后变成 400（BAD_REQUEST）响应。或者，你可以在控制器内部局部处理验证错误，通过一个````Errors````或者````BindingResult````参数，如下例所示：

````java
@PostMapping("/")
public String handle(@Valid @RequestPart("meta-data") MetaData metadata,
        BindingResult result) {
    // ...
}
````

**````@RequestBody````**

你可以使用````@RequestBody````注解来读取请求体并通过一个````HttpMessageConverter````将其反序列化为````Object````。下面的例子说明了如何使用：

```java
@PostMapping("/accounts")
public void handle(@RequestBody Account account) {
    // ...
}
```

你可以使用  [MVC Config](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-config)  中的 [Message Converters](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-config-message-converters) 选项来配置或者定制消息转化。

你可以结合使用````@RequestBody````和````javax.validation.Valid````或者 Spring 的````@Validated````注解，两种方式都会导致标准 Bean 验证执行。默认地，验证错误会导致````MethodArgumentNotValidException````，它会变成一个 400（BAD_REQUEST）状态码响应。或者，你可以在控制器内部局部处理验证错误，通过一个````Errors````或者````BindingResult````参数，如下例所示：

````java
@PostMapping("/accounts")
public void handle(@Valid @RequestBody Account account, BindingResult result) {
    // ...
}
````

**HttpEntity**

````HttpEntity````或多或少等同于使用 [`@RequestBody`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-requestbody) ，不过它是基于暴露请求首部字段和请求体的容器对象。如下面例子所示：

````java
@PostMapping("/accounts")
public void handle(HttpEntity<Account> entity) {
    // ...
}
````

**````@ResponseBody````**

你可以将````@ResponseBody````注解使用在拥有返回值，并且返回值将被 [HttpMessageConverter](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/integration.html#rest-message-conversion) 序列化为响应体的方法上。如下面例子所示：

````java
@GetMapping("/accounts/{id}")
@ResponseBody
public Account handle() {
    // ...
}
````

````@ResponseBody````也支持用在类层面，此时它就会被控制器中所有方法继承。````@RestController````注解的效果就是元注解````@Controller````和````@ResponseBody````的组合。

你可以在````@ResponseBody````中使用响应式类型。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [Reactive Types](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-reactive-types) 获取更多细节。

你可以使用  [MVC Config](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-config)  中的 [Message Converters](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-config-message-converters) 选项来配置或者定制消息转化。

你可以结合使用````@ResponseBody````方法和 JSON 序列化视图。参考[Jackson JSON](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-jackson) 。

**ResponseEntity**

````ResponseEntity````类似于 [`@ResponseBody`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-responsebody) ，不过携带状态和首部字段。例如：

````java
@GetMapping("/something")
public ResponseEntity<String> handle() {
    String body = ... ;
    String etag = ... ;
    return ResponseEntity.ok().eTag(etag).build(body);
}
````

Spring MVC 支持使用单个响应式类型的值来异步产生````ResponseEntity````，也支持使用单个字段多个值点响应式类型来产生响应体。

**Jackson JSON**

Spring 提供了对 Jackson JSON 类库的支持。

**JSON Views**

Spring MVC 提供了内建的 [Jackson’s Serialization Views](https://wiki.fasterxml.com/JacksonJsonViews) 支持，它允许仅渲染一个````Object````内部的部分或者所有字段。为了将其用于````@ResponseBody````或者````ResponseEntity````控制器方法，你可以使用 Jackson 的````@JsonView````注解来激活一个序列化视图类。如下面例子所示：

````java
@RestController
public class UserController {
    
    @GetMapping("/user")
    @JsonView(User.WithoutPasswordView.class)
    public User getUser() {
        return new User("eric","7!jd#h23");
    }
}

public class User {
    
    public interface WithoutPasswordView {};
    public interface WithPasswordView extends WithoutPasswordView {};
    
    private String username;
    private String password;
    
    public User() {
    }
    
    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }
    
    @JsonView(WithoutPasswordView.class)
    public String getUsername() {
        return this.username;
    }
    
    @JsonView(WithPasswordView.class)
    public String getPassword() {
        return this.password;
    }
}
````

> ````@JsonView````允许一个视图类数组，不过你可以只为每个控制器方法指定一个。如果你需要激活多个视图，你可以使用组合接口。

对依赖视图解析的控制器，你可以为模型添加序列化视图类，如下面例子所示：

````java
@Controller
public class UserController extends AbstractController {
    
    @GetMapping("/user")
    public String getUser(Model model) {
        model.addAttribute("user", new User("eric", "7!jd#h23"));
        model.addAttribute(JsonView.class.getName(), User.WithoutPasswordView.class);
        return "userView";
    }
}
````

### 1.3.4 Model

你可以使用````@ModelAttribute````注解。

* 用在````@RequestMapping````中的一个 [method argument](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-modelattrib-method-args) 上来在模型中创建或者访问一个````Object````，同时通过````WebDataBinder````将其绑定到请求。
* 作为一个方法层面的注解用在````@Controller````或者````@ControllerAdvice````类中，以在所有````@RequestMapping````方法被调用之前帮助初始化模型。
* 用在````@RequestMapping````方法上来将其返回值标记为一个模型属性。

本章节讨论````@ModelAttribute````方法－先前列表中的第二个元素。控制器可以拥有任何数量的````@ModelAttribute````方法。所有此类方法都在同一个控制器中的````@RequestMapping````方法之前呗调用。通过````@ControllerAdvice````注解，一个````@ModelAttribute````方法也可以在控制器之间共享。参考 [Controller Advice](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-controller-advice) 获取更多细节。

````@ModelAttribute````方法拥有灵活的方法签名。作为````@RequestMapping````方法，它们支持许多相同的参数，除了````@ModelAttribute````本身或者与请求体有关的任何东西。

下面的例子展示了一个````@ModelAttribute````方法：

````java
@ModelAttribute
public void populateModel(@RequestParam String number, Model model) {
    model.addAttribute(accountRepository.findAccount(number));
    // add more ...
}
````

下面的例子仅仅添加一个属性：

````java
@ModelAttribute
public Account addAccount(@RequestParam String number) {
    return accountRepository.findAccount(number);
}
````

> 如果没有显式指定名称，就会基于````Object````类型选择默认名称，如 javadoc [`Conventions`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/core/Conventions.html) 中所述。你可以始终分配一个显式名称通过使用重载方法````addAttribute````方法，或者通过````@ModelAttribute````注解上的````name````属性（用于返回值）。

你也可以将````@ModelAttribute````作为方法层面的注解，用在````@ResponseMapping````方法上，此时该方法的返回值被解读为模型属性。通常不是强制的，因为这是 HTML 控制器的默认行为，除非返回值是一个````String````而可能会被解读为视图名称。````@ModelAttribute````也可以定制模型属性名称，如下面例子所示：

````java
@GetMapping("/accounts/{id}")
@ModelAttribute("myAccount")
public Account handle() {
    // ...
    return account;
}
````

### 1.3.5 ````DataBinder````

````@Controller````或者````@ControllerAdvice````类可以拥有````@InitBinder````方法来初始化````WebDataBinder````实例，然后就可以：

* 将请求参数（表单或者查询数据）绑定到模型对象。
* 转化基于字符串的请求值（比如请求参数、路径变量、首部字段、cookies 等等）到控制器方法参数的目标类型。
* 格式化模型对象值为````String````值当渲染 HTML 表单时。

````@InitBinder````方法可以注册控制器特定的````java.bean.PropertyEditor````或者 Spring 的````Converter````和````Formatter````组件。此外，你可以使用 [MVC config](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-config-conversion) 来注册````Converter````和````Formatter````类型在一个全局共享的````FormattingConversionService````中。

````@InitBinder````方法支持````@RequestMapping````方法拥有多个相同参数，除了````@ModelAttribute````（命令对象）参数。典型地，它们与一个````WebDataBinder````参数以及一个````void````返回值共同声明。如下面例子所示：

````java
@Controller
public class FormController {

    @InitBinder 
    public void initBinder(WebDataBinder binder) {
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
        dateFormat.setLenient(false);
        binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, false));
    }

    // ...
}
````

另外，当你使用一个基于````Formatter````的设置，通过一个共享的````FormattingConversionService````，你可以复用相同的方法并注册控制器特定的````Formatter````实现，如下面例子所示：

````java
@Controller
public class FormController {

    @InitBinder 
    protected void initBinder(WebDataBinder binder) {
        binder.addCustomFormatter(new DateFormatter("yyyy-MM-dd"));
    }

    // ...
}
````

### 1.3.6 异常
````@Controller````和````@ControllerAdvice````类可以拥有````@ExceptionHandler````方法来处理来自控制器方法的异常。如下面例子所示：

````java
@Controller
public class SimpleController {
  
  // ...
  
  @ExceptionHandler
  public ResponseEntity<String> handle(IOException ex) {
    // ...
  }
}
````
该异常可以匹配到一个顶层异常而被传播（也就是说，直接抛出一个````IOException````）或者就是异常的直接原因被放在顶层包装器异常内部（比如，一个````IOException````内容包装了一个````IllegalStateException````）。

为了匹配异常类型，大家更倾向于将目标异常声明为一个方法参数，如前面例子所示。当匹配到多个异常处理方法，匹配到的根异常通常具有比匹配到的原因异常更高的优先级。更特殊的，````ExceptionDepthComparator````被用于对异常进行排序，基于它们相对于抛出的异常类型的深度。

另外，此注解声明可以窄化匹配的异常类型，如下面例子所示：

````java
@ExceptionHandler({FileSystemException.class, RemoteException.class})
public ResponseEntity<String> handle(IOException ex) {
  // ...
}
````
你甚至可以以非常泛化的参数签名使用一个特定异常类型列表，如下面例子所示：

````java
@ExceptionHandler({FileSystemException.class, RemoteException.class})
public ResponseEntity<String> handle(Exception ex) {
    // ...
}
````
根异常和原因异常在异常匹配过程中的区别可能会出乎大家的意料。

在前面展示的 ````IOException```` 变体中，通常使用实际的 ````FileSystemException```` 或者 ````RemoteException```` 实例作为参数来调用该方法，因为它们两者都是从 ````IOException```` 继承而来。不过，如果任何此类匹配异常被包装在包装器异常中传播，而该包装器异常就是 ````IOException```` ，则传入异常实例就是该包装器异常。

在 ````handle(Exception)```` 变体中的行为甚至会更加简单。这将永远会在包装场景下以包装器异常作为参数来调用，此时，实际的匹配异常通过 ````ex.getCause()```` 发现。传入异常就是实际的 ````FileSystemException```` 或者 ````RemoteException```` 实例，仅当这些异常被作为顶级异常抛出。
我们通常推荐使用尽可能精确的参数签名，以减少潜在的从根异常到原因异常类型的匹配错误。可以考虑将一个匹配多种类型的方法拆分成为多个 ````@ExceptionHandler```` 方法，每个方法通过参数签名匹配单一一种特定的异常类型。

在一个多-````@ControllerAdvice```` 配置中，我们建议你在````@ControllerAdvice````中的声明你的首要根异常映射，并基于相应的顺序进行优先级排序。尽管根异常匹配优先于原因异常匹配，但是这是i当一个给定控制器或者````@ControllerAdvice````类中的方法之间定义的。这就意味着在一个更高优先级的````@ControllerAdvice bean```` 上的一个原因异常匹配要优先于所有在低优先级的````@ControllerAdvice bean```` 上的异常匹配（比如根异常匹配）。

最后，一个````@ExceptionHandler````方法实现可以选择退出一个给定异常实例的处理过程，比如以初始形式重新将其抛出。这在某些场景下非常有用，比如你仅仅对根层级的异常匹配或者特定上下文（无法静态确定范围）中的异常匹配感兴趣的时候。一个重新抛出的异常将继续在剩余的异常处理链中传播，就像从来就没有被````@ExceptionHandler````方法处理过一样。

对````@ExceptionHandler````方法的支持在 Spring MVC 中建立在````DispatcherServlet````层面，````HandlerExceptionResolver```` 机制。

**方法参数**

````@ExceptionHandler````方法支持下列参数：

| 方法参数                                     | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| 异常类型                                     | 为了访问产生的异常。                               |
| ````HandlerMethod````                    | 为了访问产生异常的控制器方法。                          |
| ````WebRequest````，````NativeWebRequest```` | 泛型访问请求参数和请求和会话属性，而不需要截止使用 Servlet API。   |
| ````javax.servlet.ServletRequest````，<br />````javax.servlet.ServletResponse```` | 选择任何特定请求或者响应类型（比如，````ServletRequest````或者````HttpServletRequest````或者 Spring 的````MultipartRequest````或者````MultipartHttpServletRequest````）。 |
| ````javax.servlet.http.HttpSession````   | 强制会话的存在。进而，这样的一个参数永远不为````null```` 。<br />注意，会话的访问不是线程安全的。考虑将````RequestMappingHandlerAdapter````实例的````synchronizeOnSession````标志设置为````true````，如果多个请求被允许并发访问同一个会话。 |
| ````java.security.Principal````          | 当前认证过的用户－可能一个特定的````Principal````实现类，如果可知。 |
| ````HttpMethod````                       | 请求的 HTTP 方法。                             |
| ````java.util.Locale````                 | 当前请求的语言环境，由可用的最精确的````LocaleResolver````决定－实际上，就是配置的````LocaleResolver````或者````LocaleContextResolver````。 |
| ````java.util.TimeZone````<br />````java.time.ZoneId```` | 当前请求关联的时区，由````LocaleContextResolver````决定。 |
| ````java.io.OutputStream````<br />````java.io.Writer```` | 用来访问原始响应体，就像通过 Servlet API 暴露出来的那样。      |
| ````java.util.Map````<br />````org.springframework.ui.Model````<br />````org.springframework.ui.ModelMap```` | 用来访问一个错误响应的模型，永远为空。                      |
| ````RedirectAttribute````                | 用于重定向场景的特殊属性－（不会被附加到查询字符串中）同时 flash 属性被临时存储直到请求重定向完成。参考 [Redirect Attributes](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-redirecting-passing-data) 和 [Flash Attributes](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-flash-attributes) 。 |
| ````@SessionAttribute````                | 用来访问任何会话属性，相比之下模型属性存储在会话中，作为一个类层面的````@SessionAttributes````声明的结果。参考 [`@SessionAttribute`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-sessionattribute) 获取更多细节。 |
| ````@RequestAttribute````                | 用来访问请求属性。更多细节参见 [`@RequestAttribute`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-requestattrib) 。 |

**返回值**

````@ExceptionHandler````方法支持如下返回值：

| 返回值                                      | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| ````@ResponseBody````                    | 返回值通过````HttpMessageConverter````实例被转化并写入响应。参考 [`@ResponseBody`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-responsebody) 。 |
| ````HttpEntiry<B>````，<br />````ResponseEntity<B>```` | 返回值制定完整响应（包括 HTTP 首部字段和响应体）被通过````HttpMessageConverter````实例转化并写入响应。参考 [ResponseEntity](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-responseentity) 。 |
| ````String````                           | 视图名称被````ViewResolver````实现解析并被连同显式模型使用，模型通过命令对象和````@ModelAttribute````方法确定。处理方法也能够编程式丰富数据模型，通过声明一个````Model````参数。 |
| ````View````                             | 一个````View````实例，用来连同显式模型共同渲染，模型通过命令对象和````@ModelAttribute````方法确定。处理方法也能够编程式丰富数据模型，通过声明一个````Model````参数。 |
| ````java.util.Map````<br />````org.springframework.ui.Model```` | 将要被添加到显式模型中的属性，模型对应的视图名称通过````RequestToViewNameTranslator````显式确定。 |
| ````@ModelAttribute````                  | 将要被添加到显式模型中的属性，模型对应的视图名称通过````RequestToViewNameTranslator````显式确定。<br />注意，````@ModelAttribute````是可选的。参考此表末尾的“其他返回值”。 |
| ````ModelAndView````对象                   | 要使用的视图和模型属性，以及可选的响应状态。                   |
| ````void````                             | 具有````void````返回值（或者````null````返回值）的方法被认为拥有完整的处理之后的响应，如果它也拥有一个````ServletResponse````，一个````OutputStream````参数，或者一个````@ResponseStatus````注解。如果控制器进行一个确定的````ETag````或者````lastModified````时间戳检查时也会是这样。<br />如果上述情况都没有出现，````void````返回值也可以表示没有响应体为 REST 控制器返回，或者为 HTML 控制器选择了默认的视图名称。 |
| 所有其他返回值                                  | 如果返回值没有匹配到上述所有的类型同时又不是简单类型（由 [BeanUtils#isSimpleProperty](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/beans/BeanUtils.html#isSimpleProperty-java.lang.Class-) 确定），默认地，它就被作为模型属性而被添加到模型中。如果它是简单类型，则不会被解析。 |

**REST API 异常**

在响应体中包含错误细节是对 REST 服务的一个很普通的要求。Spring 框架并不会自动这么做，因为响应体中的错误细节的表示形式是应用特定的。不过，````@RestController````可以使用````@ExceptionHandler````方法和````ResponseEntity````返回值来设置响应状态码和响应体。这些方法也可以被声明在````@ControllerAdvice````类中以便全局使用它们。

实现了全局异常处理并将错误信息放到响应体中的应用应该考虑扩展````ResponseEntityExceptionHandler````，它提供了 Spring MVC 产生并提供了关联到定制化的响应体的钩子方法的异常。为了使用该特性，创建````ResponseEntityExceptionHandler````的一个子类，为它添加注解````@ControllerAdvice````，重写必要的方法，并将其声明为一个 Spring bean。

### 1.3.7 Controller Advice

典型的````@ExceptionHandler````，````@InitBinder````，以及````@ModelAttribute````方法都应用在声明它们的````@Controller````类（或者类继承体系）中。如果你想要全局（跨越控制器）应用这些方法，你可以在以````@ControllerAdvice````或者````@RestControllerAdvice````标注的类中声明它们。

````@ControllerAdvice````被````@Component````标记，该注解意味着这种类可以通过 [component scanning](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#beans-java-instantiating-container-scan) 被注册为 Spring beans 。````@RestControllerAdvice````也是一个元注解，同时被````@ControllerAdvice````和````@ResponseBody````标记，它们的基础意思是````@ExceptionHandler````方法通过消息转换（相对于视图解析或者模版渲染）被渲染为响应体。

在启动时，为````@RequestMapping````和````@ExceptionHandler````方法服务的基础设施类探测````@ControllerAdvice````类型的 Spring beans 然后在运行时应用它们的方法。全局的````@ExceptionHandler````方法（来自一个````@ControllerAdvice````）在局部的相应方法（来自````@Controller````）之后才被应用。作为对比，全局的````@ModelAttribute````和````@InitBinder````方法在局部的相应方法之前被应用。

默认地，````@ControllerAdvice````方法应用于每个请求（也就是说，所有控制器），不过你可以窄化其应用范围为一部分控制器，通过使用注解属性，如下面例子所示：

````java
// Target all Controllers annotated with @RestController
@ControllerAdvice(annotations = RestController.class)
public class ExampleAdvice1 {}

// Target add Controllers within specific packages
@ControllerAdvice("org.example.controllers")
public class ExampleAdvice2 {}

// Target all Controllers assignable to specific classes
@ControllerAdvice(assignableType = {ControllerInterface.class, AbstractController.class})
public class ExampleAdvice3 {}
````

上面例子中的选择器在运行时被解析，如果滥用可能会对性能产生负面影响。参考 [`@ControllerAdvice`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/bind/annotation/ControllerAdvice.html) 文档获取更多细节。

## 1.4 URI Links

本节介绍 Spring Framework 中可用于处理URI的各种选项。

### 1.4.1 UriComponents

````UriComponentsBuilder````帮助大家从 URI 模版和变量来构建 URI，如下面例子所示：

````java
UriComponents uriComponents = UriComponentsBuilder
		.fromUriString("https://example.com/hotels/{hotel}")	// 带有URI模版的静态工厂方法
		.queryParam("q", "{q}")	// 添加或者替换URI组件
		.encode()	// 拥有URI模版和URI变量的请求的编码
		.build();	// 构建一个UriComponents
		
URI uri = uriComponents.expand("Westin", "123").toUri();	// 展开变量并获取URI
````

上面的例子可以通过````buildAndExpand````缩减精简为一个链条，如下面例子所示：

````java
URI uri = UriComponentsBuilder
        .fromUriString("https://example.com/hotels/{hotel}")
        .queryParam("q", "{q}")
        .encode()
        .buildAndExpand("Westin", "123")
        .toUri();
````

再次精简：

````java
URI uri = UriComponentsBuilder
        .fromUriString("https://example.com/hotels/{hotel}")
        .queryParam("q", "{q}")
        .build("Westin", "123");
````

完全使用 URI 模版，可以最终精简为下面的形式：

````java
URI uri = UriComponentsBuilder
        .fromUriString("https://example.com/hotels/{hotel}?q={q}")
        .build("Westin", "123");
````

### 1.4.2 UriBuilder

[`UriComponentsBuilder`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#web-uricomponents) 实现了````UriBuilder````。您可以使用````UriBuilderFactory````创建一个````UriBuilder````。 ````UriBuilderFactory````和````UriBuilder````一起提供了一种可插拔的机制，可以根据共享配置（例如基本URL，编码首选项和其他详细信息）从URI模板构建URI。

你可以通过````UriBuilderFactory````配置````RestTemplate````和````WebClient````以定制化 URI 的准备过程。````DefautUriBuilderFactory````是````UriBuilderFactory````的一个默认实现，内部使用了````UriComponentsBuilder````并将共享配置选项暴露出来。

下面的例子展示了如何配置一个````RestTemplate````：

````java
// import org.springframework.web.util.DefaultUriBuilderFactory.EncodingMode

String baseUrl = "https://example.rog";
DefaultUriBuilderFactory factory = new DefaultUriBuilderFactory(baseUrl);
factory.setEncodingMode(EncodingMode.TEMPLATE_AND_VARIABLES);

RestTemplate restTemplate = new RestTemplate();
restTemplate.setUriTemplateHandler(factory);
````

下面的例子配置一个````WebClient````：

````java
// import org.springframework.web.util.DefaultUriBuilderFactory.EncodingMode;

String baseUrl = "https://example.org";
DefaultUriBuilderFactory factory = new DefaultUriBuilderFactory(baseUrl);
factory.setEncodingMode(EncodingMode.TEMPLATE_AND_VARIABLES);

WebClient client = WebClient.builder().uriBuilderFactory(factory).build();
````

此外，你也可以直接使用````DefaultUriBuilderFactory````。类似于使用````UriComponentsBuilder````，不过，并不是静态工厂方法，而是持有配置和首选项的实际实例。如下面例子所示：

````java
String baseUrl = "https://example.com";
DefaultUriBuilderFactory uriBuilderFactory = new DefaultUriBuilderFactory(baseUrl);

URI uri = uriBuilderFactory.uriString("/hotels/{hotel}")
        .queryParam("q", "{q}")
        .build("Westin", "123");
````

### 1.4.3 URI Encoding

````UriComponentsBuilder````在两个层面暴露编码选项：

* [UriComponentsBuilder#encode()](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/util/UriComponentsBuilder.html#encode--) ：首先对 URI 模版进行预编码然后在扩展时对 URI 变量进行严格的编码。
* [UriComponents#encode()](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/util/UriComponents.html#encode--) ：在 URI 变量被扩展之后对 URI 组件进行编码。

两种方式都会把非 ASCII 码和非法字符替换为转义字符。不过，第一种方式也会替换出现在 URI 变量中具有保留含义的字符。

> 考虑分号";"，它在请求路径中是合法的，但是却具有保留含义。第一种方式会将 URI 变量中的";"替换为"%3B"，而在 URI 模版中的分号则不会被替换。作为对比，第二种方式永远不会替换分号，因为它在路径中是合法字符。

大多数情况下，第一种方式更可能给出人们期望的结果，因为它将 URI 变量作为被完整编码的不透明数据，而第二种方式只有当 URI 变量里确实包含保留字符时才有用。

下面的例子采用了第一种方式：

````java
URI uri = UriComponentsBuilder.fromPath("/hotel list/{city}")
            .queryParam("q", "{q}")
            .encode()
            .buildAndExpand("New York", "foo+bar")
            .toUri();

    // Result is "/hotel%20list/New%20York?q=foo%2Bbar"
````

可以简化为：

````java
URI uri = UriComponentsBuilder.fromPath("/hotel list/{city}")
            .queryParam("q", "{q}")
            .build("New York", "foo+bar")
````

使用完整的 URI 模版，最终简化为：

````java
URI uri = UriComponentsBuilder.fromPath("/hotel list/{city}?q={q}")
            .build("New York", "foo+bar")
````

````WebClient````和````RestTemplate```` 通过````UriBuilderFactory````策略内部扩展并编码 URI 模版。两者都可以被配置为一个客户化策略，如下面例子所示：

````java
String baseUrl = "https://example.com";
DefaultUriBuilderFactory factory = new DefaultUriBuilderFactory(baseUrl);
factory.setEncodingMode(EncodingMode.TEMPLATE_AND_VALUES);

// Customize the RestTemplate..
RestTemplate restTemplate = new RestTemplate();
restTemplate.setUriTemplateHandler(factory);

// Customize the WebClient..
WebClient client = WebClient.builder().uriBuilderFactory(factory).build();
````

````DefaultUriBuilderFactory````实现内部使用````UriComponentsBuilder````来扩展并编码 URI 模版。作为一个工厂，它提供配置编码方法的唯一场所，基于下列编码模式之一：

* ````TEMPLATE_AND_VALUES````：使用````UriComponentsBuilder#encode()````，对应于先前列表中的第一个选项，来预编码 URI 模版并在扩展时严格编码 URI 变量。
* ````VALUES_ONLY````：不编码 URI 模版，而是通过使用````UriUtils#encodeUriVariables````在将它们扩展进入模版之前严格编码 URI 变量。
* ````URI_COMPONENTS````：使用````UriComponents#encode()````，对应于先前列表中的第二个选项，在 URI 变量被扩展之后编码 URI 组件值。
* ````NONE````：不应用任何编码。

````RestTemplate````被设定为````EncodingMode.URI_COMPONENTS````，由于历史原因以及保持向后兼容的考虑。````WebClient````依赖于````DefaultUriBuilderFactory````中的默认值，它们在 Spring 5.0.x 版本中是````EncodingMode.URI_COMPONENTS````，而在 Spring 5.1 版本中变成了````EncodingMode.TEMPLATE_AND_VALUES````。

### 1.4.4 相对 Servlet 请求

你能够使用````ServletUriComponentsBuilder````来创建相对于当前请求的 URIs，如下面例子所示：

````java
HttpServletRequest request = ...

// Re-uses host, scheme, port, path and query string...

ServletUriComponentsBuilder ucb = ServletUriComponentsBuilder.fromRequest(request)
        .replaceQueryParam("accountId", "{id}").build()
        .expand("123")
        .encode();
````

你可以创建相对于当前上下文路径的 URIs，如下面例子所示：

````java
// Re-uses host, port and context path...

ServletUriComponentsBuilder ucb = ServletUriComponentsBuilder.fromContextPath(request)
    	.path("/accounts").build();
````

你可以创建相对于一个 Servlet（比如，````/main/*````）的 URIs，如下面例子所示：

````java
// Re-uses host, port, context path, and Servlet prefix...

ServletUriComponentsBuilder ucb = ServletUriComponentsBuilder.fromServletMapping(request)
        .path("/accounts").build()
````

> 作为 5.1 版本，````ServletUriComponentsBuilder````忽略来自````Forwarded````和````X-Forwarded-*````首部字段的信息，它们指定客户端发起的地址。考虑使用 [`ForwardedHeaderFilter`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#filters-forwarded-headers) 来提取并使用或者忽略这些首部字段。

### 1.4.5 链接到控制器

Spring MVC 提供了一种机制来准备链接到控制器方法。比如，下面的 MVC 控制器允许链接创建：

````java
@Controller
@RequestMapping("/hotels/{hotel}")
public class BookingController {
    
    @GetMapping("/bookings/{booking}")
    public ModelAndView getBooking(@PathVariable Long booking) {
        // ...
    }
}
````

我们可以通过名称表示控制器方法来准备一个链接，如下面例子所示：

````java
UriComponents uriComponents = MvcUriComponentsBuilder
	.fromMethodName(BookingController.class, "getBooking", 21).buildAndExpand(42);

URI uri = uriComponents.encode().toUri();
````

在前面的例子中，我们提供了实际的方法参数值（例子中，长整型值：````21````）被用来作为一个路径变量并被插入 URL 。进一步地，我们提供值 ````42```` 来填充所有剩余的 URI 变量，比如````hotel````变量，该变量从类型层面的请求映射继承而来。如果该方法拥有更多参数，我们可以提供````null````值给那些 URL 不需要的参数。通常，只有````@PathVariable````和````@RequestParam````参数与 URL 构建相关。

还存在其它使用````MvcUriComponentsBuilder````的方法。例如，您可以使用类似于通过代理进行模拟测试的技术，以避免按名称引用控制器方法，如下面例子所示（例子假定静态导入````MvcUriComponentsBuilder.on````）：

````java
UriComponents uriComponents = MvcUriComponentsBuilder
	.fromMethodCall(on(BookingController.class).getBooking(21)).buildAndExpand(42);

URI uri = uriComponents.encode().toUri();
````

> 控制器方法签名在它们被设计时受到限制，当它们假定被用来使用````fromMethodCall````进行链接创建。除了需要一个合适的参数签名，对返回值类型还（名义上，为链接创建器调用产生一个运行时代理）存在一个技术局限，因而返回值类型绝对不能是````final````的。特别地，作为视图名称的普通的````String````返回值类型在这里不会使用。你应该使用````ModelAndView````或者甚至是直白的````Object````（连同一个````String````返回值）来代替。

先前的例子使用了````MvcUriComponentsBuilder````中的静态方法。内部地，它们依赖````ServletUriComponentsBuilder```` 由协议、主机、端口、上下文路径以及当前请求的 servlet 路径来准备一个基本 URL 。大多数情况下这种机制可以很好地工作。不过，有时候它并不足够。比如，你可能处于请求的上下文之外（如准备链接的批处理过程），或者可能你需要插入一个路径前缀（注入一个语言环境前缀，该前缀被从请求路径中删除，而需要被重新插入链接中）。

这种情况下，你可以使用静态的````fromXxx````重载方法，该方法接受一个````UriComponentsBuilder````来使用一个基本 URL。另外，你可以基于基本 URL 创建一个````MvcUriComponentsBuilder````实例然后使用基于实例的````withXxx````方法。比如，下面的例子使用````withMethodCall````：

````java
UriComponentsBuilder base = ServletUriComponentsBuilder.fromCurrentContextPath().path("/en");
MvcUriComponentsBuilder builder = MvcUriComponentsBuilder.relativeTo(base);
builder.withMethodCall(on(BookingController.class).getBooking(21)).buildAndExpand(42);

URI uri = uriComponents.encode().toUri();
````

> 作为 5.1 版本，````MvcUriComponentsBuilder````忽略来自````Forwarded````和````X-Forwarded-*````首部字段的信息，它们指定客户端发起的地址。考虑使用 [`ForwardedHeaderFilter`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#filters-forwarded-headers) 来提取并使用或者忽略这些首部字段。

### 1.4.6 链接到视图

在诸如 Thylmeleaf, FreeMarker, 或者 JSP 视图中，你可以创建链接到注解标注的控制器，通过引用为每个请求映射显式的或者隐式的分配的名称。

考虑下面的例子：

````java
@RequestMapping("/people/{id}/addresses")
public class PersonAddressController {

    @RequestMapping("/{country}")
    public HttpEntity getAddress(@PathVariable String country) { ... }
}
````

给定上面的控制器，你可以由 JSP 准备一个链接，如下：

````
<%@ taglib uri="http://www.springframework.org/tags" prefix="s" %>
...
<a href="${s:mvcUrl('PAC#getAddress').arg(0,'US').buildAndExpand('123')}">Get Address</a>
````

上面的例子依赖声明在 Spring 标签库（也就是````META-INF/spring.tld````）中的````mvcUrl````函数，不过你也可以很简单地定义你自己的函数，或者准备一种类似的函数用于其它的模版技术。

它的工作原理如下：在启动时，每个````@RequestMapping````通过````HandlerMethodMappingNamingStrategy````被分配一个默认名称，其默认实现使用类名中的大写字母和方法名（比如，````ThingController````中的````getThing````方法变成````TC#getThing````）。如果存在命名冲突，你可以使用````@RequestMapping(name="...")````来显式指定一个名称，或者实现你自己的````HandlerMethodMappingNamingStrategy````。

## 1.5 异步请求

Spring MVC 中对 Servlet 3.0 异步请求处理进行了广泛集成：

* 在控制器方法中的 [`DeferredResult`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-deferredresult) 和 [`Callable`](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-callable) 返回值提供了对单个异步返回值的基本支持。
* 控制器可以将多个返回值包装成  [stream](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-http-streaming) ，包括  [SSE](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-sse) 和 [raw data](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-output-stream) 。
* 控制器可以使用响应式客户端并为响应处理返回 [reactive types](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-reactive-types) 。

### 1.5.1 ````DeferredResult````

一旦 Servlet 容器中开启了异步请求处理特性，控制器方法可以包装任何支持的控制器方法返回值为````DeferredResult````，如下面例子所示：

````java
@GetMapping("/quotes")
@ResponseBody
public DeferredResult<String> quotes() {
    DeferredResult<String> deferredResult = new DeferredResult<String>();
    // Save the deferredResult somewhere..
    return deferredResult;
}

// From some other thread...
deferredResult.setResult(data);
````

控制器可以异步地产生返回值，在不同的线程中产生返回值－比如，响应一个外部事件（JMS 消息），一个调度任务，或者其他事件。

### 1.5.2 ````Callable````

控制器能将任何支持的返回值包装为````java.util.concurrent.Callable````，如下面例子所示：

````java
@PostMapping
public Callable<String> processUpload(final MultipartFile file) {
    
    return new Callable<String>() {
        public String call() throws Exception {
            // ...
            return "someView";
        }
    };
}
````

该返回值然后就可以通过配置的````TaskExecutor````运行给定的任务来获取。

### 1.5.3 处理

下面是 Servlet 异步请求处理过程的一个非常简洁的概述：

* 一个````ServletRequest````能够被放入异步模式，通过调用````request.startAsync()````。这样做的主要影响就是该 Servlet （以及任何过滤器）能够退出，但是响应保持打开以使得处理过程随后结束。
* ````request.startAsync()````调用返回````AsyncContext````，你可以使用它进一步控制异步处理过程。比如，它提供````dispatch````方法，类似于 Servlet API 中的````forward````方法，区别在于它允许一个应用在一个 Servlet 容器线程上恢复请求处理过程。
* ````ServletRequest````提供了对当前````DispatcherType````的访问，你可以使用它来区别于对初始请求的处理，一个异步分发、一个转发或者其他分发类型。

````DeferredResult````处理过程如下：

* 控制器返回一个````DeferredResult````并将它保存在它可以被访问的一些内存队列或者列表中。
* Spring MVC 调用````request.startAsync()````。
* 同时，````DispatcherServlet````和所有配置的过滤器退出请求处理线程，但是响应保持打开状态。
* 应用设置来自一些线程的````DeferredResult````，同时 Spring MVC 将该请求分发回到 Servlet 容器。
* ````DispatcherServlet````被再次调用，处理过程恢复以异步产生返回值。

````Callable````处理过程如下：

* 控制器返回一个````Callable````。
* Spring MVC 调用````request.startAsync()````并提交````Callable````到````TaskExecutor````以在一个单独的线程中处理。
* 同时，````DispatcherServlet````和所有过滤器退出 Servlet 容器线程，但是响应保持打开状态。
* 终于，````Callable````产生一个结果，同时 Spring MVC 将请求分发回 Servlet 容器以完成处理。
* ````DispatcherServlet````再次被调用，并且处理过程恢复以从````Callable````异步产生返回值。

更多背景知识和上下文细节，可以参考相关 [博文](https://spring.io/blog/2012/05/07/spring-mvc-3-2-preview-introducing-servlet-3-async-support) ，其中介绍了 Spring MVC 3.2 中的异步请求处理支持。

**异常处理**

当你使用````DeferredResult````时，你可以选择是否为异常调用````setResult````或者````setErrorResult````。两种情况下，Spring MVC 分发请求回到 Servlet 容器来完成处理。然后对其进行处理，就像控制器方法返回了给定值，或者好像它产生了给定的异常。接下来异常就通过常规的异常处理机制处理（比如，调用````@ExceptionHandler````方法）。

当你使用````Callable````时，类似的处理逻辑会发生，主要的不同在于结果来自````Callable````或者它产生的异常。

**拦截**

````HandlerInterceptor````实例可以是````AsyncHandlerInterceptor````类型，来接收初始请求上的````afterConcurrentHandlingStarted````回调以开始异步处理（替代````postHandle````和````afterCompletion````）。

````HandlerInterceptor````实现也能够注册一个````CallableProcessingInterceptor````或者一个````DeferredResultProcessingInterceptor````，来更深入地与异步请求的生命周期集成（比如，处理超时事件）。参考  [`AsyncHandlerInterceptor`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/AsyncHandlerInterceptor.html) 获取更多细节。

````DeferredResult````提供````onTimeout(Runnable)````和````onCompletion(Runnable)````回调。参考  [javadoc of `DeferredResult`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/context/request/async/DeferredResult.html) 获取更多细节。````Callable````能够替代````WebAsyncTask````来暴露关于超时和回调完成的附加方法。

**对比 WebFlux**

Servlet API 最初是为了通过过滤器 Servlet 链进行单词传输而设计。被添加到 Servlet 3.0 中的异步请求处理允许应用退出过滤器 Servlet 链的同时保持响应的打开状态已进行进一步处理。Spring MVC 的异步支持都围绕此机制构建。当控制器返回````DeferredResult````时，过滤器 Servlet 链退出，Servlet 容器线程被释放。随后，当````DeferredReuslt````被设定，一个````ASYNC````分发（指向同一个 URL）被执行，同时，控制器会再次被映射，而不会再次调用它，````DeferredResult````值（如果控制器返回了它）被用来恢复处理。

作为对比，Spring WebFlux 并不是构建在 Servlet API 之上，也不需要那种异步请求处理特性，因为它本来就是为异步处理而设计。异步处理被构建在所有框架内的契约中，在请求处理的各个层面被原生支持。

从编程模型角度讲，Spring MVC 和 Spring WebFlux 都支持异步，并都将 [Reactive Types](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-reactive-types) 作为控制器方法的返回值。Spring MVC 甚至支持流式处理，包括反应式反向压力。不过，每个向响应中写入仍然是阻塞式的，在单独的线程上执行，不像 WebFlux，它基于非阻塞式 I/O 而不需要为每个写入任务准备一个额外的线程。

另外一个根本区别是，Spring MVC 不支持异步或者反应式类型使用在控制器方法参数中（比如，````@RequestBody````，等等），同时也没有对异步和反应式类型作为模型属性提供任何显式支持。而以上特性Spring WebFlux 统统支持。

### 1.5.4 HTTP 流

你能够使用````DeferredResult````以及````Callable````为一个单独的异步返回值。如果想要产生多个异步值并将他们写入响应中，应该怎么办呢？本章节将会介绍。

**Objects**

你能够使用````ResponseBodyEmitter````返回值来产生一个对象流，其中每个对象都被````HttpMessageConverter````序列化并被写入响应，如下面例子所示：

````java
@GetMapping("/events")
public ResponseBodyEmitter handle() {
  ResponseBodyEmitter emitter = new ResponseBodyEmitter();
  // Save the emitter somewhere..
  return emitter;
}

// In some other thread
emitter.send("Hello once");
  
// and again later on
emitter.send("Hello again");
  
// and done at some point
emitter.complete();
````

你也可以使用````ResponseBodyEmitter````作为````ResponseEntity````中的主体，允许你定制响应的状态码和首部字段。

当一个````emitter````抛出一个````IOException````（比如，如果远程客户端掉线），应用没有责任清理连接，同时也不应该调用````emitter.complete````或者````emitter.completeWithError````。取而代之的，servlet 容器自动初始化一个````AsyncListener````错误通知，其中 Spring MVC 执行一个````completeWithError````调用。这个调用，接下来，执行一个最终的````ASYNC````分发到应用，在其过程中 Spring MVC 调用配置的异常解析器并完成请求处理。

**SSE**

````SseEmitter````（一个````ResponseBodyEmitter````的子类）为 [Server-Sent Events](https://www.w3.org/TR/eventsource/) 提供支持，其中的事件从服务端发出并按照 W3C SSE 规范进行格式化。为了从控制器产生 SSE 流，返回````SseEmitter````，如下面例子所示：

````java
@GetMapping(path="/events", produces=MediaType.TEXT_EVENT_STREAM_VALUE)
public SseEmitter handle() {
    SseEmitter emitter = new SseEmitter();
    // Save the emitter somewhere..
    return emitter;
}

// In some other thread
emitter.send("Hello once");

// and again later on
emitter.send("Hello again");

// and done at some point
emitter.complete();
````

尽管 SSE 是流进入浏览器的主要选项，注意 IE 是不支持服务端发送的事件的。考虑使用 Spring 的 [WebSocket messaging](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#websocket) 以及 [SockJS fallback](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#websocket-fallback) 来兼容不同类型的浏览器。

**原始数据**

某些时候，绕过消息转化而直接将流写入响应````OutputStream````（比如，文件下载）是很有用的。你可以使用````StreamingResponseBody````返回值类型来实现，如下面例子所示：

````java
@GetMapping("/download")
public StreamingResponseBody handle() {
  return new StreamingResponseBody() {
    @Override
    public void writeTo(OutputStream outputStream) throws IOException {
      // write...
    }
  };
}
````

你可以使用````StreamingResponseBody````作为````ResponseEntiry````中的主体来定制响应状态码和首部字段。

### 1.5.5 响应式类型

Spring MVC 支持在控制器中使用响应式客户端类库（参考 WebFlux 章节的 [Reactive Libraries](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web-reactive.html#webflux-reactive-libraries)）。这就包括来自````spring-webflux````的````WebClient````等，比如 Spring Data 响应式数据仓库。这些场景下，从控制器方法中返回响应式类型是很方便的。

响应式返回值处理过程如下：

* 单个的 promise 适配到其上，类似于````DeferredResult````的使用。例子包含````Mono````(Reactor)或者````Single````(RxJava)。
* 一个流媒体类型的多值流（比如````application/stream+json````或者````text/event-stream````）被适配到其上，类似于使用````ResponseBodyEmitter````或者````SseEmitter````。例子包含````Flux````(Reactor)或者````Observable````(RxJava)。应用也可以返回````Flux<ServerSentEvent>````或者````Observable<ServerSentEvent>````。
* 一个其他媒体类型的多值流（比如````application/json````）被适配到其上，类似于使用````DeferredResult<List<?>>````。

> Spring MVC 通过来自````spring-core````的 [`ReactiveAdapterRegistry`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/core/ReactiveAdapterRegistry.html) 来支持 Reactor 和 RxJava，这就允许它适配到多种响应式类库。

对流式响应，响应式反响压力是支持的，但是向响应写入数据仍然是阻塞式的，通过配置的````TaskExecutor````在一个单独的线程上执行，以避免阻塞上游数据源（比如````WebClient````返回的````Flux````）。默认情况下，````SompleAsyncTaskExecutor````被用来进行阻塞式写，但是在高负载情况下是不合适的。如果你打算将响应式类型流化，你应该使用 [MVC configuration](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-configuration-spring-mvc) 来配置一个任务执行器。

### 1.5.6 Disconnects

当一个远端客户端断开连接时，Servlet API 没有提供任何通知机制。因此，当向响应流式写入时，无论是通过 [SseEmitter](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-sse) 还是 [reactive types](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-async-reactive-types) ，周期性地发送数据是非常重要的，因为当客户端已经断开连接情况下，数据写入肯定会失败。数据发送可以作为空 SSE 事件的形式或者任何通信对方将解读为心跳信号而忽略的其他数据的形式。

另外，考虑使用 web 消息解决方案（比如 [STOMP over WebSocket](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#websocket-stomp) 或者基于 [SockJS](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#websocket-fallback) 的 WebSocket），其中包含内建的心跳机制。

### 1.5.7 配置

异步请求处理特性必须在 Servlet 容器层面开启。MVC 配置也暴露了若干有关异步请求处理的开关选项。

**Servlet Container**

Filter 和 Servlet 声明拥有一个````asyncSupported````标志，该标志需要被设置为````true````来开启异步请求处理。另外，Filter 映射应该被声明为处理````ASYNC````的````javax.servlet.DispatchType````。

在 Java 配置类中，当你使用````AbstractAnnotationConfigDispatcherServletInitializer````来初始化 Servlet 容器时，该配置就是自动完成的。

在````web.xml````配置文件中，你可以添加````<async-supported>true</async-supported>````到````DispatcherServlet```` 和 ````Filter```` 声明中，并添加````<dispatcher>ASYNC</dispatcher>````到过滤器映射中。

**Spring MVC**

MVC 配置暴露了下列与异步请求处理相关的选项：

* Java 配置类：使用````WebMvcConfigurer````上的````configureAsyncSupport````回调。
* XML 命名空间：在````<mvc:annotation-driven>````下使用````<async-support>````。

你可以配置以下内容：

* 异步请求的默认超时时间，如果没有设定，就取决于潜在的 Servlet 容器（比如，Tomcat 上配置的 10 秒）。
* 用于在流化响应式类型数据时进行阻塞式写入的````AsyncTaskExecutor````，同时也用于执行控制器方法返回的````Callable````实例。我们强烈建议配置此属性，如果你需要流化响应式类型数据或者你的控制器方法返回````Callable````，因为默认情况下，执行器是````SimpleAsyncTaskExecutor````。
* ````DeferredResultProcessingInterceptor````实现和````CallableProcessingInterceptor````实现。

注意，你还可以设置````DeferredResult````、````ResponseBodyEmitter````以及````SseEmitter````上的默认超时时间。对于````Callable````，你可以使用````WebAsyncTask````来提供一个超时时间。

## 1.6 CORS

Spring MVC 使得你可以处理 CORS 跨域资源共享。本章节描述如何做。

### 1.6.1 介绍

由于安全原因，浏览器禁止 AJAX 访问当前域之外的资源。比如，你可以在一个浏览器页签中输入你的银行账号，而在另外一个页签中访问 evil.com。该网站中的脚本不应该能够使用你的身份凭证发送 AJAX 请求到你的银行 API-比如，从你的账号中偷钱。

跨域资源共享 CORS 是一个  [W3C specification](https://www.w3.org/TR/cors/) ，被 [most browsers](https://caniuse.com/#feat=cors) 实现，允许你指定何种跨域请求是经过认证的，而不需要使用风险更高而功能更弱的权变方案 IFRAME 或者 JSONP。

## 1.6.2 处理

CORS 规范特别区分了预检请求、简单请求以及实际请求。为了了解 CORS 如何工作，可以参考 [this article](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)，或者参考相关规范获取更多细节。

Spring MVC ````HandlerMapping```` 实现提供对 CORS 的内建支持。将一个请求成功映射到处理器之后，````HandlerMapping````实现检查关于给定请求和处理器的 CORS 配置以采取进一步操作。预检请求被直接处理，简单的和实际的 CORS 请求被解读、校验，同时强制需要 CORS 响应首部字段集合。

为了进行跨域请求（也就是说，````Origin````首部字段存在，同时不同于发出请求的主机域名），你需要显式声明 CORS 配置。如果没有匹配的 CORS 配置被发现，预检请求就会被拒绝。No CORS 首部字段被添加到简单和实际请求的响应中，随后，浏览器拒绝它们。

每个````HandlerMapping````可以被使用基于````CorsConfiguration````的 URL 模式单独 [配置](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/handler/AbstractHandlerMapping.html#setCorsConfigurations-java.util.Map-) 。大多数情况下，应用使用 MVC 的 Java 配置类或者 XML 命名空间来声明此类映射，最终产生一个单独的全局映射并被传递给所有````HandlerMapping````实例。

你可以将````HandlerMapping````层面的全局 CORS 配置结合更细粒度的处理器层面的 CORS 配置使用。比如，注解的控制器可以使用类型或者方法层面的````@CrossOrigin````注解（其他处理器可以实现````CorsConfigurationSource````）。

结合全局和局部配置的规则就是普通的添加。比如，所有全局的和所有局部的添加在一起。所有只有一个值的属性都会被接受（比如````allowCredentials````和````maxAge````），局部值覆盖全局值。参考 [`CorsConfiguration#combine(CorsConfiguration)`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/cors/CorsConfiguration.html#combine-org.springframework.web.cors.CorsConfiguration-) 获取更多细节。

> 想要从源码学习更多，或者希望更深入地定制化，检查下面的代码：
>
> * ````CorsConfiguration````
> * ````CorsProcessor````，````DefaultCorsProcessor````
> * ````AbstractHandlerMapping````

### 1.6.3 ````@CrossOrigin````

````@CrossOrigin````注解在被注解的控制方法上开启跨域请求处理，如下面例子所示：

````java
@RestController
@RequestMapping("/account")
public class AccountController {
  
  @CrossOrigin
  @GetMapping("/{id}")
  public Account retrieve(@PathVariable Long id) {
    // ...
  }
  
  @DeleteMapping("/{id}")
  public void remove(@PathVariable Long id) {
    // ...
  }
}
````

默认地，````@CrossOrigin````允许：

* 所有域
* 所有首部字段
* 所有该控制器方法被映射到的 HTTP 方法

````allowedCredentials````默认不被开启，因为那会建立一个层次的信任，暴露敏感的特定用户的信息（比如 cookies 和 CSRF tokens）因而只能在何时的场景才能使用。

````maxAge````被设定为 30 分钟。

````@CrossOrigin````在类型层面被支持，此时会被所有方法集成，如下面例子所示：

````java
@CrossOrigin(origins = "https://domain2.com", maxAge = 3600)
@RestController
@RequestMapping("/account")
public class AccountController {

    @GetMapping("/{id}")
    public Account retrieve(@PathVariable Long id) {
        // ...
    }

    @DeleteMapping("/{id}")
    public void remove(@PathVariable Long id) {
        // ...
    }
}
````

你也可以同时在类型层面和方法层面使用````@CrossOrigin````注解，如下面例子所示：

````java
@CrossOrigin(maxAge = 3600)
@RestController
@RequestMapping("/account")
public class AccountController {

    @CrossOrigin("https://domain2.com")
    @GetMapping("/{id}")
    public Account retrieve(@PathVariable Long id) {
        // ...
    }

    @DeleteMapping("/{id}")
    public void remove(@PathVariable Long id) {
        // ...
    }
}
````

### 1.6.4 全局配置

除了细粒度的控制器方法层面的配置，你可能也希望配置一些全局 CORS 配置。你可以在任何````HandlerMapping````上单独设定基于 URL 的````CorsConfiguration````映射。不过，大多数应用使用 MVC Java 配置类或者 MVC XNM 命名空间来进行这些配置。

默认地，全局配置可以为以下对象开启：

* 所有域
* 所有首部字段
* ````GET````，````HEAD````，````POST````方法

````allowedCredentials````默认不会开启，因为那会建立一个层次的信任，暴露敏感的特定用户的信息（比如 cookies 和 CSRF tokens）因而只能在何时的场景才能使用。

````maxAge````被设定为 30 分钟。

**Java 配置**

想要在 MVC Java 配置中开启 CORS，可以使用````CorsRegistry````回调，如下面例子所示：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
  
  @Override
  public void addCorsMappings(CorsRegistry registry) {
    
    registry.addMapping("/api/**")
      .allowedOrigins("https://domain2.com")
      .allowedMethods("PUT", "DELETE")
      .allowedHeaders("header1", "header2", "header3")
      .exposedHeaders("header1", "header2")
      .allowCredentials(true).maxAge(3600);
    
    // Add more mappings...
  }
}
````

**XML 配置**

要在 XML 命名空间中开启 CORS ，你可以是使用````<mvc:cors>````元素，如下面例子所示：

````xml
<mvc:cors>

    <mvc:mapping path="/api/**"
        allowed-origins="https://domain1.com, https://domain2.com"
        allowed-methods="GET, PUT"
        allowed-headers="header1, header2, header3"
        exposed-headers="header1, header2" allow-credentials="true"
        max-age="123" />

    <mvc:mapping path="/resources/**"
        allowed-origins="https://domain1.com" />

</mvc:cors>
````

### 1.6.5 CORS Filter

我们可以通过内建的 [`CorsFilter`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/filter/CorsFilter.html) 来提供 CORS 支持。

> 如果你试图结合 Spring Security 使用````CorsFilter````，记住 Spring Security 拥有CORS [内建支持](https://docs.spring.io/spring-security/site/docs/current/reference/htmlsingle/#cors) 。

为了配置该过滤器，传递````CorsConfigurationSource````给它的构造器，如下面例子所示：

````java
CorsConfiguration config = new CorsConfiguration();

// Possibly...
// config.applyPermitDefaultValues()

config.setAllowCredentials(true);
config.addAllowedOrigin("https://domain1.com");
config.addAllowedHeader("*");
config.addAllowedMethod("*");

UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
source.registerCorsConfiguration("/**", config);

CorsFilter filter = new CorsFilter(source);
````

## 1.7 Web 安全

 [Spring Security](https://projects.spring.io/spring-security/) 项目提供了支持来保护 web 应用免遭攻击。参考 Spring Security 项目参考文档，包括：

* [Spring MVC Security](https://docs.spring.io/spring-security/site/docs/current/reference/html5/#mvc)
* [Spring MVC Test Support](https://docs.spring.io/spring-security/site/docs/current/reference/html5/#test-mockmvc)
* [CSRF protection](https://docs.spring.io/spring-security/site/docs/current/reference/html5/#csrf)
* [Security Response Headers](https://docs.spring.io/spring-security/site/docs/current/reference/html5/#headers)

Spring MVC 框架还集成了 [HDIV](https://hdiv.org/)  这个 web 安全框架。

## 1.8 HTTP 缓存

HTTP 缓存可以显著改善 web 应用的性能。HTTP 缓存围绕着````Cache-Control````响应首部字段，然后，有条件地使用请求首部字段（比如````Last-Modified````和````ETag````）。````Cache-Control````指明了浏览器上的私有缓存和代理服务器上的公共缓存如何缓存和重用响应。一个````ETag````首部字段被用于生成一个条件请求，该请求可能导致一个 304 (NOT_MODIFIED) 状态码而不包括消息主体的响应，如果内容没有变化。````ETag````能够被看作是````Last-Modified````首部字段的一个更复杂的继承者。

### 1.8.1 ````CacheControl````

[`CacheControl`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/http/CacheControl.html) 为配置有关````Cache-Control````首部字段提供了支持并被在很多地方被作为一个参数：

- [`WebContentInterceptor`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/mvc/WebContentInterceptor.html)
- [`WebContentGenerator`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/support/WebContentGenerator.html)
- [Controllers](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-caching-etag-lastmodified)
- [Static Resources](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-caching-static-resources)

尽管 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2) 描述了有关````Cache-Control````响应首部字段的所有可能的指令，但是````CacheControl````类型采用面向场景的方法，聚焦于通用场景：

````java
// Cache for an hour - "Cache-Control: max-age=3600"
CacheControl ccCacheOneHour = CacheControl.maxAge(1, TimeUnit.HOURS);

// Prevent caching - "Cache-Control: no-store"
CacheControl ccNoStore = CacheControl.noStore();

// Cache for ten days in public and private caches,
// public caches should not transform the response
// "Cache-Control: max-age=864000, public, no-transform"
CacheControl ccCustom = CacheControl.maxAge(10, TimeUnit.DAYS).noTransform().cachePublic();
````

````WebContentGenerator````也接受一个更简单的````cachePeriod````属性（单位为秒），如下工作：

* ````-1````值不会产生````Cache-Control````响应首部字段。
* ````0````值防止被使用````'Cache-Control: no-store'````指令缓存。
* ````n>0````值缓存给定的响应````n````秒，通过使用````'Cache-Control: max-age=n'````指令。

### 1.8.2 控制器

控制器可以显式添加 HTTP 缓存支持。我们推荐这样做，因为有关一个资源的````lastModified````或者````ETag````值需要在它与条件请求首部字段进行比较之前被计算。一个控制器可以添加一个````ETag````首部字段和````Cache-Control````设定到一个````ResponseEntity````，如下面例子所示：

````java
@GetMapping("/book/{id}")
public ResponseEntity<Book> showBook(@PathVariable Long id) {

    Book book = findBook(id);
    String version = book.getVersion();

    return ResponseEntity
            .ok()
            .cacheControl(CacheControl.maxAge(30, TimeUnit.DAYS))
            .eTag(version) // lastModified is also available
            .body(book);
}
````

上面的例子发送一个 304 (NOT_MODIFIED) 状态码响应，包含以俄国空主体，如果与条件请求首部字段比较的结果表明内容没有变化。否则，````ETag````和````Cache-Control````首部字段被添加到响应中。

你也可以在控制器中进行条件请求首部字段的检查。如下面例子所示：

````java
@RequestMapping
public String myHandleMethod(WebRequest webRequest, Model model) {

    long eTag = ...				// 应用特定的计算

    if (request.checkNotModified(eTag)) {
        return null; 			// 304 状态码响应，没有进一步处理
    }

    model.addAttribute(...); 			// 继续请求处理
    return "myViewName";
}
````

有三种方法基于````ETag````或者````lastModified````字段值，或者同时使用两者检查条件请求首部字段。对条件````GET````和````HEAD````请求，你可以发送 304 状态码响应。对条件````POST````，````PUT````以及````DELETE````请求，你可以发送 409 (PRECONDITION_FAILED) 状态码响应，以防止并发修改。

### 1.8.3 静态资源

你应该在包含静态资源数据的响应中使用````Cache-Control````和条件响应首部字段来优化性能。参考 [静态资源配置](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-config-static-resources) 。

### 1.8.4 ````ETag````过滤器

你可以使用````ShallowEtagHeaderFilter````来添加"shallow"````eTag````值，该值由响应内容计算而来，因而，节约了网络带宽但是消耗了 CPU 时间。参考 [Shallow ETag](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#filters-shallow-etag) 。

## 1.9 视图技术







## 1.10 MVC 配置

MVC Java 配置类和 MVC XML 命名空间提供的默认配置适用于大部分应用，同时还有一个配置 API 用来定制配置。

为了进行更高级的个性化配置，而这种高级个性化无法通过配置 API 实现，参考 [Advanced Java Config](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-config-advanced-java) 和 [Advanced XML Config](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-config-advanced-xml) 。

你不需要理解由 MVC Java 配置类和 MVC 命名空间创建的内部 beans 。如果你希望了解更多，参考  [Special Bean Types](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-servlet-special-bean-types) and [Web MVC Config](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-servlet-config) 。

### 1.10.1 启用 MVC 配置

在 Java 配置类中，你可以使用````@EnableWebMvc````注解来启用 MVC 配置，如下面例子所示：

````java
@Configuration
@EnableWebMvc
public class WebConfig {
  
}
````

在 XML 配置中，你可以使用````<mvc:annotation-driven>````元素来启用 MVC 配置，如下面例子所示：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven/>

</beans>
````

上面的例子注册了一系列 Spring MVC  [infrastructure beans](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-servlet-special-bean-types) 同时适应 classpath 上可用的依赖（比如，用于 JSON、XML 等等负载的转换器）。

### 1.10.2 MVC 配置 API

在 Java 配置类中，你可以实现````WebMvcConfiguration````接口，如下面例子所示：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
  // 实现配置方法
}
````

在 XML 中，你可以检查````<mvc:annotation-driven>````属性和子元素。你可以参考 [Spring MVC XML schema](https://schema.spring.io/mvc/spring-mvc.xsd) 或者使用你的 IDE 的代码自动完成特性来发现哪些属性和子元素是可用的。

### 1.10.3 类型转换

默认安装的````Number````和````Date````类型的格式化器包含了对````@NumberFormat````和````@DateTimeFormat````注解的支持。如果 Joda-Time 出现在 classpath 上，则会安装 Joda-Time 格式类库的完整支持。

在 Java 配置类中，你可以注册定制化的格式化器和转换器，如下面例子所示：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
  
  @Override
  public void addFormatters(FormatterRegistry registry) {
    // ...
  }
}
````

等效的 XML 配置如下：

````xml
1.10.3. Type Conversion
Same as in Spring WebFlux

By default formatters, for Number and Date types are installed, including support for the @NumberFormat and @DateTimeFormat annotations. Full support for the Joda-Time formatting library is also installed if Joda-Time is present on the classpath.

In Java configuration, you can register custom formatters and converters, as the following example shows:

@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addFormatters(FormatterRegistry registry) {
        // ...
    }
}
The following example shows how to achieve the same configuration in XML:

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven conversion-service="conversionService"/>

    <bean id="conversionService"
            class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
        <property name="converters">
            <set>
                <bean class="org.example.MyConverter"/>
            </set>
        </property>
        <property name="formatters">
            <set>
                <bean class="org.example.MyFormatter"/>
                <bean class="org.example.MyAnnotationFormatterFactory"/>
            </set>
        </property>
        <property name="formatterRegistrars">
            <set>
                <bean class="org.example.MyFormatterRegistrar"/>
            </set>
        </property>
    </bean>

</beans>
````

> 参考  [the `FormatterRegistrar` SPI](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#format-FormatterRegistrar-SPI)  和````FormattingConversionServiceFactoryBean````获取更多何时使用````FormatterRegistrar````接口实现的信息。

### 1.10.4 验证

默认地，如果 [Bean Validation](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#validation-beanvalidation-overview) 出现在 classpath 上（比如，Hibernate Validator），则````LocalValidatorFactoryBean````被注册为全局 [Validator](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#validator) ，用来验证被````@Valid````和````@Validated````注解修饰的控制器方法参数。

在 Java 配置类中，你可以如下定制化全局````Validator````实例：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public Validator getValidator(); {
        // ...
    }
}
````

等效的 XML 配置文件：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven validator="globalValidator"/>

</beans>
````

你也可以注册局部的````Validator````实例，如下面例子所示：

````java
@Controller
public class MyController {

    @InitBinder
    protected void initBinder(WebDataBinder binder) {
        binder.addValidators(new FooValidator());
    }

}
````

> 如果你需要在某处注入````LocalValidatorFactoryBean````实例，创建一个 bean 并将其标记为````@Primary````，来避免与 MVC 配置中声明的那个实例发生冲突。

### 1.10.5 拦截器

在 Java 配置类中，你可以注册施加到到来的请求之上的拦截器，如下面例子所示：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LocaleChangeInterceptor());
        registry.addInterceptor(new ThemeChangeInterceptor()).addPathPatterns("/**").excludePathPatterns("/admin/**");
        registry.addInterceptor(new SecurityInterceptor()).addPathPatterns("/secure/*");
    }
}
````

下面是相同效果的 XML 配置：

````xml
<mvc:interceptors>
    <bean class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor"/>
    <mvc:interceptor>
        <mvc:mapping path="/**"/>
        <mvc:exclude-mapping path="/admin/**"/>
        <bean class="org.springframework.web.servlet.theme.ThemeChangeInterceptor"/>
    </mvc:interceptor>
    <mvc:interceptor>
        <mvc:mapping path="/secure/*"/>
        <bean class="org.example.SecurityInterceptor"/>
    </mvc:interceptor>
</mvc:interceptors>
````

### 1.10.6 Content Types

你可以配置 Spring MVC 如何从请求中确定其请求媒体类型（比如，````Accept````首部字段、URL 路径扩展、查询参数等等）。

默认地，首先被检查的是 URL 路径扩展－将````json````、````xml````、````rss````和````atom````注册为已知扩展（依赖 classpath 上的依赖）。第二顺位检查````Accept````首部字段。

请考虑将默认设置更改为````Accept````首部字段，同时，如果你必须使用基于 URL 的内容类型解析，考虑使用基于路径扩展的查询参数策略。参考  [Suffix Match](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-suffix-pattern-match) 和 [Suffix Match and RFD](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-rfd) 获取更多信息。

在 Java 配置类中，你可以定制化请求内容类型解析，如下面例子所示：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
        configurer.mediaType("json", MediaType.APPLICATION_JSON);
        configurer.mediaType("xml", MediaType.APPLICATION_XML);
    }
}
````

等效的 XML 配置：

````xml
<mvc:annotation-driven content-negotiation-manager="contentNegotiationManager"/>

<bean id="contentNegotiationManager" class="org.springframework.web.accept.ContentNegotiationManagerFactoryBean">
    <property name="mediaTypes">
        <value>
            json=application/json
            xml=application/xml
        </value>
    </property>
</bean>
````

### 1.10.7 Message Converters

你可以在 Java 配置类中定制化````HttpMessageConverter````，通过覆盖 [`configureMessageConverters()`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/config/annotation/WebMvcConfigurer.html#configureMessageConverters-java.util.List-) （替换 Spring MVC 创建的默认转换器）或者覆盖 [`extendMessageConverters()`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/config/annotation/WebMvcConfigurer.html#extendMessageConverters-java.util.List-) （定制化默认转换器或者将附加转换器添加到默认转换器中）。

下面的例子将定制化的````ObjectMapper````添加为 XML 和 Jackson JSON 的默认转换器：

 ````java
@Configuration
@EnableWebMvc
public class WebConfiguration implements WebMvcConfigurer {

    @Override
    public void configureMessageConverters(List<HttpMessageConverter<?>> converters) {
        Jackson2ObjectMapperBuilder builder = new Jackson2ObjectMapperBuilder()
                .indentOutput(true)
                .dateFormat(new SimpleDateFormat("yyyy-MM-dd"))
                .modulesToInstall(new ParameterNamesModule());
        converters.add(new MappingJackson2HttpMessageConverter(builder.build()));
        converters.add(new MappingJackson2XmlHttpMessageConverter(builder.createXmlMapper(true).build()));
    }
}
 ````

上面的例子中， [`Jackson2ObjectMapperBuilder`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/http/converter/json/Jackson2ObjectMapperBuilder.html) 被用于为````MappingJackson2HttpMessageConverter````和````MappingJackson2XmlHttpMessageConverter````创建一个通用配置，开启缩进，定制化的数据格式，以及注册 [`jackson-module-parameter-names`](https://github.com/FasterXML/jackson-module-parameter-names)，同时添加了参数名称访问（Java 8 添加的新特性）支持。

该创建器定制化 Jackson 的默认属性如下：

* [`DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES`](https://fasterxml.github.io/jackson-databind/javadoc/2.6/com/fasterxml/jackson/databind/DeserializationFeature.html#FAIL_ON_UNKNOWN_PROPERTIES) 不可用。
* [`MapperFeature.DEFAULT_VIEW_INCLUSION`](https://fasterxml.github.io/jackson-databind/javadoc/2.6/com/fasterxml/jackson/databind/MapperFeature.html#DEFAULT_VIEW_INCLUSION) 不可用。

同时，也自动注册下面周知的模块，如果 classpath 上探测到它们：

- [jackson-datatype-jdk7](https://github.com/FasterXML/jackson-datatype-jdk7)：支持 Java 7 类型，比如 `java.nio.file.Path`。
- [jackson-datatype-joda](https://github.com/FasterXML/jackson-datatype-joda)：支持 Joda-Time 类型。
- [jackson-datatype-jsr310](https://github.com/FasterXML/jackson-datatype-jsr310)：支持 Java 8 Date 和 Time API 类型。
- [jackson-datatype-jdk8](https://github.com/FasterXML/jackson-datatype-jdk8)：支持其他 Java 8 类型，比如 `Optional`。

> Jackson XML 支持中启用缩进出了需要 [`jackson-dataformat-xml`](https://search.maven.org/#search|ga|1|a%3A"jackson-dataformat-xml") 还需要 [`woodstox-core-asl`](https://search.maven.org/#search|gav|1|g%3A"org.codehaus.woodstox" AND a%3A"woodstox-core-asl") 依赖。

其他有趣的可用的 Jackson 模块：

* [jackson-datatype-money](https://github.com/zalando/jackson-datatype-money)：支持````javax.money````（非官方模块）。
* [jackson-datatype-hibernate](https://github.com/FasterXML/jackson-datatype-hibernate)：支持 Hibernate 特定类型和属性（包括懒加载切面）。

下面是等效的 XML 配置：

````xml
<mvc:annotation-driven>
    <mvc:message-converters>
        <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
            <property name="objectMapper" ref="objectMapper"/>
        </bean>
        <bean class="org.springframework.http.converter.xml.MappingJackson2XmlHttpMessageConverter">
            <property name="objectMapper" ref="xmlMapper"/>
        </bean>
    </mvc:message-converters>
</mvc:annotation-driven>

<bean id="objectMapper" class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean"
      p:indentOutput="true"
      p:simpleDateFormat="yyyy-MM-dd"
      p:modulesToInstall="com.fasterxml.jackson.module.paramnames.ParameterNamesModule"/>

<bean id="xmlMapper" parent="objectMapper" p:createXmlMapper="true"/>
````

### 1.10.8 视图控制器

这是一个定义````ParameterizableViewController````的快捷方法，该控制器在被调用时会立即将请求转发到一个视图。你可以在某些静态场景中使用，如果在视图产生响应之前没有 Java 控制器逻辑执行。

下面的例子展示了如何在 Java 配置类中配置将对````/````的请求转发到名为````home````的视图：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
  
  @Override
  public void addViewControllers(ViewControllerRegistry registry) {
    registry.addViewController("/").setViewName("home");
  }
}
````

下面是等效的 XML 配置：

````xml
<mvc:view-controller path="/" view-name="home"/>
````

### 1.10.9 视图解析器

Spring MVC 配置简化了视图解析器的注册。

下面的 Java 配置类展示了如何配置内容协商视图解析，通过使用 JSP 和 Jackson 作为 JSON 渲染的默认````View````：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
  
  @Override
  public void configureViewResolvers(ViewResolverRegistry registry) {
    registry.enableContentNegotiation(new MappingJackson2JsonView());
    registry.jsp();
  }
}
````

等价的 XML 配置：

````xml
<mvc:view-resolvers>
    <mvc:content-negotiation>
        <mvc:default-views>
            <bean class="org.springframework.web.servlet.view.json.MappingJackson2JsonView"/>
        </mvc:default-views>
    </mvc:content-negotiation>
    <mvc:jsp/>
</mvc:view-resolvers>
````

注意，FreeMarker，Tiles，Groovy Markup 以及脚本模板也需要底层视图技术配置。

MVC 命名空间提供了专用元素。下面的例子使用 FreeMarker：

````xml
<mvc:view-resolvers>
    <mvc:content-negotiation>
        <mvc:default-views>
            <bean class="org.springframework.web.servlet.view.json.MappingJackson2JsonView"/>
        </mvc:default-views>
    </mvc:content-negotiation>
    <mvc:freemarker cache="false"/>
</mvc:view-resolvers>

<mvc:freemarker-configurer>
    <mvc:template-loader-path location="/freemarker"/>
</mvc:freemarker-configurer>
````

在 Java 配置类中，你可以添加各自的````Configurer```` bean，如下面例子所示：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void configureViewResolvers(ViewResolverRegistry registry) {
        registry.enableContentNegotiation(new MappingJackson2JsonView());
        registry.freeMarker().cache(false);
    }

    @Bean
    public FreeMarkerConfigurer freeMarkerConfigurer() {
        FreeMarkerConfigurer configurer = new FreeMarkerConfigurer();
        configurer.setTemplateLoaderPath("/freemarker");
        return configurer;
    }
}
````

### 1.10.10 静态资源

此选项提供了一种方便的方法来从一个 [`Resource`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/core/io/Resource.html) 位置列表中提供静态资源。

在下面的例子中，给定一个````/resources````开头的请求，该相对路径被用于发现并提供相对于应用根路径下的````/public````或者````/static````下的 classpath 上的静态资源。这些资源被提供为超时时间为将来一年的形式来确保最大化利用浏览器缓存并减少浏览器产生的 HTTP 请求。````Last-Modified````首部字段也会被评估，同时，如果该字段存在，则````304````状态码响应会被返回。

下面的列表展示了 Java 配置类中如何使用：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/resources/**")
            .addResourceLocations("/public", "classpath:/static/")
            .setCachePeriod(31556926);
    }
}
````

等效的 XML 配置：

````xml
<mvc:resources mapping="/resources/**"
    location="/public, classpath:/static/"
    cache-period="31556926" />
````

参考 [HTTP caching support for static resources](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web.html#mvc-caching-static-resources) 。

资源处理器也支持一系列的 [`ResourceResolver`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/resource/ResourceResolver.html) 实现和 [`ResourceTransformer`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/resource/ResourceTransformer.html) 实现，你可以用来创建一个工具链以使用优化的资源。

你可以使用````VersionResourceResolver````来版本化资源 URLs，基于从内容计算而来的 MD5 哈希值、一个固定的应用版本、或者其他。````ContentVersionStrategy```` (MD5 哈希) 是一个好的选择－连同一些显著的异常，比如使用模块加载器的 JavaScript 资源。

下面的例子展示了如何在 Java 配置类中使用````VersionResourceResolver````：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/resources/**")
                .addResourceLocations("/public/")
                .resourceChain(true)
                .addResolver(new VersionResourceResolver().addContentVersionStrategy("/**"));
    }
}
````

等效的 XML 配置：

````xml
<mvc:resources mapping="/resources/**" location="/public/">
    <mvc:resource-chain>
        <mvc:resource-cache/>
        <mvc:resolvers>
            <mvc:version-resolver>
                <mvc:content-version-strategy patterns="/**"/>
            </mvc:version-resolver>
        </mvc:resolvers>
    </mvc:resource-chain>
</mvc:resources>
````

然后你可以使用````ResourceUrlProvider````来重写 URLs 并应用完整的解析器链和转换器链－比如，来插入版本。MVC 配置提供了````ResourceUrlProvider```` bean 因而他可以被注入其他 bean 中。你也可以为 Thymeleaf、JSPs、FreeMarker 以及其他连同 URL 标签依赖于````HttpServletResponse#encodeURL````使用````ResourceUrlEncodingFilter````实现透明重写。

注意，当同时使用````EncodingResourceResolver````和````VersionedResourceResolver````时，你必须按照此顺序注册它们。这才能确保基于内容的版本永远是可靠基于未编码的文件计算而来。

[WebJars](https://www.webjars.org/documentation) 也通过````WebJarsResourceResolver````被支持，如果````org.webjars:webjars-locator-core````类库出现在 classpath 上，它就会被自动注册。解析器能够重写 URLs 以包括 jar 包的版本，同时也可以无视版本匹配到来的请求 URLs－比如，从````/jquery/jquery.min.js````到````/jquery/1.2.0/jquery.min.js````。

### 1.10.11 默认 Servlet

Spring MVC 允许将````DispatcherServlet````映射到````/````（从而覆盖了容器的默认 Servlet 映射），同时仍然允许静态资源请求被容器的默认 Servlet 处理。它配置一个````DefaultServletHttpRequestHandler````到一个 URL 映射````/**````，同时相对于其他 URL 映射的优先级最低。

此处理器将所有请求转发到默认 Servlet 。因此，它必须留在所有其他 URL ````HandleMappings````的最后。这是你使用````<mvc:annotation-driven>````。另外，如果你设定你自己定制的````HandlerMapping````实例，确保设定其````order````属性比````DefaultServletHttpRequestHandler````更低，后者的````order````属性值为````Integer.MAX_VALUE````。

下面的例子展示了如何通过默认设置开启该特性：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable();
    }
}
````

等效的 XML 配置：

````xml
<mvc:default-servlet-handler/>
````

覆盖````/ ````Servlet 映射的警告是，必须通过名称而不是路径来检索默认 Servlet 的````RequestDispatcher````。 ````DefaultServletHttpRequestHandler````尝试使用大多数主要 Servlet 容器（包括 Tomcat，Jetty，GlassFish，JBoss，Resin，WebLogic 和 WebSphere）的已知名称列表，在启动时自动检测容器的默认 Servlet。 如果默认Servlet 已使用其他名称进行自定义配置，或者在默认 Servlet 名称未知的情况下使用其他 Servlet 容器，则必须显式提供默认 Servlet 名称，如以下示例所示：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable("myCustomDefaultServlet");
    }

}
````

等效的 XML 配置：

````xml
<mvc:default-servlet-handler default-servlet-name="myCustomDefaultServlet"/>
````

### 1.10.12 路径匹配

您可以自定义与路径匹配和 URL 处理相关的选项。 有关各个选项的详细信息，请参阅 [`PathMatchConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/web/servlet/config/annotation/PathMatchConfigurer.html) javadoc。

下面的例子展示了如何在 Java 配置类中使用定制化路径匹配：

````java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void configurePathMatch(PathMatchConfigurer configurer) {
        configurer
            .setUseSuffixPatternMatch(true)
            .setUseTrailingSlashMatch(false)
            .setUseRegisteredSuffixPatternMatch(true)
            .setPathMatcher(antPathMatcher())
            .setUrlPathHelper(urlPathHelper())
            .addPathPrefix("/api",
                    HandlerTypePredicate.forAnnotation(RestController.class));
    }

    @Bean
    public UrlPathHelper urlPathHelper() {
        //...
    }

    @Bean
    public PathMatcher antPathMatcher() {
        //...
    }

}
````

等效的 XML 配置：

````xml
<mvc:annotation-driven>
    <mvc:path-matching
        suffix-pattern="true"
        trailing-slash="false"
        registered-suffixes-only="true"
        path-helper="pathHelper"
        path-matcher="pathMatcher"/>
</mvc:annotation-driven>

<bean id="pathHelper" class="org.example.app.MyPathHelper"/>
<bean id="pathMatcher" class="org.example.app.MyPathMatcher"/>
````

### 1.10.13 高级 Java 配置

````@EnableWebMvc````导入````DelegatingWebMvcConfiguration````，它可以：

* 为 Spring MVC 应用提供默认的 Spring 配置。
* 检测并委派给 WebMvcConfigurer 实现以自定义该配置。

高级模式中，你可以删除````@EnableWebMvc````并直接扩展自````DelegatingWebMvcConfiguration````替代````WebMvcConfigurer````实现，如下面例子所示：

````java
@Configuration
public class WebConfig extends DelegatingWebMvcConfiguration {

    // ...

}
````

你可以在````WebConfig````中保留方法，但是你现在也可以覆盖来自基类的 bean 声明，同时你还可以在 classpath 上拥有任意数量的其他````WebMvcConfigurer````实现。

### 1.10.14 高级 XML 配置

MVC 命名空间没有高级模式。如果你需要自定义 bean 上你不能修改的属性，你可以使用````BeanPostProcessor````上的 Spring ````ApplicationContext````生命周期钩子，如下面例子所示：

````java
@Component
public class MyPostProcessor implements BeanPostProcessor {

    public Object postProcessBeforeInitialization(Object bean, String name) throws BeansException {
        // ...
    }
}
````

注意，你需要声明````MyPostProcessor````为一个 bean ，要么在 XML 中显式声明，要么使它通过````<component-scan/>````声明被探测到。

## 1.11 HTTP/2

Servlet 4 容器需要支持 HTTP / 2，Spring Framework 5 与 Servlet API 4 兼容。从编程模型的角度来看，应用程序不需要特定的任何操作。 但是，存在与服务器配置相关的注意事项。 更多有关详细信息，请参阅 HTTP / 2 Wiki页面。

Servlet API 确实暴露了一个与 HTTP / 2 相关的构造。 您可以使用````javax.servlet.http.PushBuilder````主动将资源推送到客户端，并且它被支持作为````@RequestMapping````方法的方法参数。

# 2. Rest 客户端

本章节介绍客户端访问 REST 服务端点得配置。

## 2.1 ````RestTemplate````

````RestTemplate````是执行 HTTP 请求的同步客户端。它是一个原生的 Spring REST 客户端，同时基于底层的 HTTP 客户端类库暴露了一个简单的、模板方法 API 。

> 作为 5.0 版本，非阻塞、响应式````WebClient````带来了现代版本的````RestTemplate````，提供了对 [synchronous and asynchronous](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web-reactive.html#webflux-client-synchronous) 的有效支持，比如在流式处理场景下。````RestTemplate````将在将来版本中废弃，因而后续不会再有主要的新特性加入。

更多细节参考 [REST Endpoints](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/integration.html#rest-client-access)。

## 2.2 ````WebClient````

````WebClient````是一个非阻塞式、响应式的客户端，用来执行 HTTP 请求。它被引入 5.0 版本框架，提供了````RestTemplate````的现代进化版本，同时有效支持流式处理场景下的同步和异步处理。

相对于````RestTemplate````，````WebClient````支持如下特性：

* 非阻塞 I/O。
* 响应式流反向施压。
* 更低硬件资源消耗的高并发。
* 函数式风格，继承了 Java 8 lambdas 优点的 fluent API。
* 同步和异步交互。
* 流式上传下载。

更多细节参考 [WebClient](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/web-reactive.html#webflux-client)。

# 3. 测试

本章节简要介绍 Spring MVC 应用可以使用的````spring-test````中的测试选项。

* Servlet API Mocks：为控制器、过滤器以及其他 web 组件的单元测试模拟 Servlet API 契约的实现。更多细节参考 [Servlet API](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/testing.html#mock-objects-servlet) 。
* TestContext Framework：支持在 JUnit 和 TestNG 测试中加载 Spring 配置，包括通过测试方法加载的配置的有效缓存，支持通过````MockServletContext````加载````WebApplicationContext````。更多细节参考 [TestContext Framework](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/testing.html#testcontext-framework) 。
* Spring MVC Test：也被称为````MockMvc````，通过````DispatcherServlet````测试注解修饰的控制器。包含完整的 Spring MVC 基础设施，除了 HTTP server。更多细节参考 [Spring MVC Test](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/testing.html#spring-mvc-test-framework)。
* 客户端 REST：````spring-test````提供了一个````MockRestServiceServer````，你可以将其作为一个模拟服务器来测试内部使用````RestTemplate````的客户端代码。更多细节参考 [Client REST Tests](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/testing.html#spring-mvc-test-client)。
* ````WebTestClient````：用来测试 WebFlux 应用，不过也可以用来进行端到端的集成测试，到任何服务器，通过 HTTP 连接。它是一个非阻塞、响应式的客户端，非常适合流式处理场景下的异步测试。

# 4. WebSockets





# 5. 其他 Web 框架







