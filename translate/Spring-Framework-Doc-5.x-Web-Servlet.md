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

| 控制器方法参数                                               | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ````WebRequest````，````NativeWebRequest````                 | 一般的对亲故参数和请求和会话属性的访问，不直接使用 Servlet API 。 |
| ````javax.servlet.ServletRequest````<br />````javax.servlet.ServletResponse```` | 选择任何特定的请求或者响应类型－比如，ServletRequest，HttpServletRequest，或者 Spring 的````MultipartRequest````，````MultipartHttpServletRequest````。 |
| ````javax.servlet.http.HttpSession````                       | 强制会话存在。由此，这个参数永远不会为````null````。注意，会话的访问不是线程安全的。设置````RequestMappingHandlerAdapter````实例的````synchronizeOnSession````标识为````true````，如果允许多个请求并发访问一个会话。 |
| ````javax.servlet.http.PushBuilder````                       | Servlet 4.0 的推送构建器 API 用于编程方式 HTTP/2 资源推送。注意，每个 Servlet 规范，注入的 PushBuilder 实例可以为 ````null````，如果客户端不支持 HTTP/2 新特性。 |
| ````java.security.Principal````                              | 当前已认证用户－可能一个特定 Principal 实现类，如果知道。    |
| ````HttpMethod````                                           | 请求的 HTTP 方法。                                           |
| ````java.util.Locale````                                     | 当前请求语言环境，由最精准的可用````LocaleResolver````（实际上就是配置的````LocaleResolver````或者````LocaleContextResolver````）决定。 |
| ````java.util.TimeZone```` +<br />````java.time.ZoneId````   | 当前请求相关的时区，由 LocaleContextResolver 确定。          |
| ````java.io.InputStream````<br />````java.io.Reader````      | 用于访问通过 Serlvet API 暴露的未加工的请求体。              |
| ````java.io.OutputSteam````<br />````java.io.Writer````      | 用于访问通过 Serlvet API 暴露的未加工的响应体。              |
| ````@PathVariable````                                        | 用于访问 URI 模版变量，参考 [URI patterns](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-uri-templates) 。 |
| ````@MatrixVariable````                                      | 用于访问 URI 路径片段中的名值对，参考 [Matrix Variables](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-matrix-variables) 。 |
| ````@RequestParam````                                        | 用于访问 Servlet 请求参数，包含多部分文件。参数值被转换为声明的方法参数类型。参考[`@RequestParam`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestparam) 以及 [Multipart](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-multipart-forms) 。<br />注意，为简单参数值使用````@RequestParam````是可选的。参考本表末尾的“其它参数”。 |
| ````@RequestHeader````                                       | 用于访问请求首部字段。首部字段值呗转化为声明的方法参数类型。参考 [`@RequestHeader`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestheader) 。 |
| ````@CookieValue````                                         | 用于访问 cookies。Cookies 值被转化为声明的方法参数类型。参考 [`@CookieValue`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-cookievalue) 。 |
| ````@RequestBody````                                         | 用来访问 HTTP 请求体。请求体内容通过使用````HttpMessageConverter````实现被转化为声明的方法参数类型。参考 [`@RequestBody`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestbody) 。 |
| ````HttpEntity<B>````                                        | 用于访问请求首部字段和请求体。请求体通过````HttpMessageConverter````转化。参考 [HttpEntity](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-httpentity) 。 |
| ````@RequestPart````                                         | 用于访问````multipart/form-data````请求中的一个部分数据，通过````HttpMessageConverter````转化该部分数据体。参考 [Multipart](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-multipart-forms) 。 |
| ````java.util.Map````<br />````org.springframework.ui.Model````<br />````org.springframework.ui.ModelMap```` | 用于访问数据模型，该模型 HTML 控制器使用，并作为视图渲染的一部分被暴露给视图模版。 |
| ````RedirectAttributes````                                   | 用于重定向场景的特定属性（也就是说，会被添加到查询字符串中），同时清理将被临时存储的属性直到请求重定向完成。参考 [Redirect Attributes](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-redirecting-passing-data) 和 [Flash Attributes](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-flash-attributes) 。 |
| ````ModelAttribute````                                       | 用于访问模型中已经存在的属性，连同数据绑定和应用的验证。参考 [`@ModelAttribute`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-modelattrib-method-args) 以及 [Model](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-modelattrib-methods) 和 [`DataBinder`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-initbinder) 。<br />注意，````@ModelAttribute````的使用是可选的（比如要设置它的属性），参考本表末尾的“其它参数”。 |
| ````Errors````<br />````BindingResult````                    | 用于访问来自对一个命令对象（也就是一个````@ModelAttribute````参数）进行的验证和数据绑定的错误，或者来自````@RequestBody````或者````@RequestPart````参数验证的错误。验证方法参数之后你必须立即声明一个````Errors````或者````BidingResult````参数。 |
| ````SessionStatus````＋ 类层面的 ````@SessionAttributes````  | 为了标识表单处理完成，该状态将触发通过类层面的````@SessionAttributes````注解声明的会话属性的清理。参考 [`@SessionAttributes`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-sessionattributes) 获取更多细节。 |
| ````UriComponentsBuilder````                                 | 准备一个相对于当前请求的主机、端口、协议、上下文路径以及 servlet 映射字面部分的 URL 。参考 [URI Links](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-uri-building) 。 |
| ````@SessionAttribute````                                    | 用于访问任何会话属性，不同于作为类层面的````@SessionAttributes````声明的结果的存储在会话中的模型属性。参考 [`@SessionAttribute`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-sessionattribute) 获取更多细节。 |
| ````@RequestAttribute````                                    | 用于访问请求属性。参考 [`@RequestAttribute`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestattrib) 。 |
| 其它参数                                                     | 任何本表中没有匹配到的简单类型参数（由 [BeanUtils#isSimpleProperty](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/beans/BeanUtils.html#isSimpleProperty-java.lang.Class-) 确定），被作为````@RequestParam````解析。否则，将被作为````@ModelAttribute````解析。 |

**返回值**

下表描述了支持的控制器方法返回值。所有响应值都支持反应式类型。

| 控制器方法返回值                                             | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ````@ResponseBody````                                        | 返回值通过````HttpMessageConverter````实现转化并写入响应。参考 [`@ResponseBody`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-responsebody) 。 |
| ````HttpEntity<B>````，````ResponseEntity<B>````             | 指定完整响应（包括 HTTP 首部字段和主体）的返回值通过````HttpMesssageConverter````实现转化并写入响应。参考 [ResponseEntity](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-responseentity) 。 |
| ````HttpHeaders````                                          | 为了返回一个响应，包含首部字段，但是没有主体。               |
| ````String````                                               | 一个视图名称将被````ViewResolver````实现解析被与明确的模型共同使用－通过命令对象和````@ModelAttribute````方法确定。控制器方法也能够通过编程方式通过声明一个````Model````参数来丰富模型。参考 [Explicit Registrations](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-registration) 。 |
| ````View````                                                 | 一个````View````实例结合明确的数据模型进行渲染－通过命令对象和````@ModelAttribute````方法来确定。处理器方法与能够以编程方式通过声明````Model````参数来丰富模型。参考 [Explicit Registrations](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-registration) 。 |
| ````java.util.Map````<br />````org.springframework.ui.Model```` | 将被添加进入明确模型的属性，连同通过````RequestToViewNameTranslator````显式确定的视图名称。 |
| ````@ModelAttribute````                                      | 一个将被添加进入模型的属性，连同通过````RequestToViewNameTranslator````显式确定的视图名称。<br />注意，````@ModelAttribute````是可选的。参考表末尾的“其它返回值”。 |
| ````ModelAndView````对象                                     | 将要使用的视图和模型属性，以及可选的，响应状态。             |
| ````void````                                                 | 具有````void````返回值（或者````null````返回值）的方法被认为拥有完整的处理之后的响应，如果它也拥有一个````ServletResponse````，一个````OutputStream````参数，或者一个````@ResponseStatus````注解。如果控制器进行一个确定的````ETag````或者````lastModified````时间戳检查时也会是这样。<br />如果上述情况都没有出现，````void````返回值也可以表示没有响应体为 REST 控制器返回，或者为 HTML 控制器选择了默认的视图名称。 |
| ````DeferredResult<V>````                                    | 从任何线程中异步产生前面提到的任何返回值－比如，作为一些事件或者回调的结果。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [`DeferredResult`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-deferredresult) 。 |
| ````Callable<V>````                                          | 从任何 Spring MVC 管理的线程中异步产生任何上面提到的返回值。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [`Callable `](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-callable) 。 |
| ````ListenableFutrue<V>````<br />````java.util.concurrent.CompletionStatege<V>````<br />````java.util.concurrent.CompletableFuture<V>```` | ````DeferredResult````的替代品，为了方便（比如，当一个基础服务返回它们其中之一时）。 |
| ````ResponseBodyEmitter````<br />````SseEmitter````          | 通过````HttpMessageConverter````实现异步发出一个将要被写入响应中的对象流。同时支持作为````ResponseEntity````的主体。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [HTTP Streaming](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-http-streaming) 。 |
| ````StreamingResponseBody````                                | 异步写入响应````OutputStream````。同时支持作为````ResponseEntity````的主体。参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [HTTP Streaming](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-http-streaming) 。 |
| 反应式类型－反应器，RxJava，或者通过````ReactiveAdapterRegistry````得到的其它东西。 | ````DeferredResult````的替代品，将多个值流（比如````Flux````，````Observable````）收集称为一个````List````。<br />流式场景下（比如````text/event-stream````，````application/json+stream````），````SseEmitter````和````ResponseBodyEmitter````被使用，这些地方````ServletOutputStream````阻塞式 I/O 执行在 Spring MVC 管理的线程上并导致了每次写入完成的压力。<br />参考 [Asynchronous Requests](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async) 和 [Reactive Types](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-ann-async-reactive-types) 。 |
| 其它返回值                                                   | 任何没有匹配到此表中提到的返回值的返回值，如果是````String````或者````void````就会被作为视图名称（默认视图名称选择通过````RequestToViewNameTranslator````执行），提供它不是一个简单类型，通过 [BeanUtils#isSimpleProperty](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/beans/BeanUtils.html#isSimpleProperty-java.lang.Class-) 决定。简单类型的返回值就不会被解析。 |

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

