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

