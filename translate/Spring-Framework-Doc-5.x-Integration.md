# Integration

Version 5.1.9.RELEASE

----

本参考文档涵盖 Spring 框架与大量 Java EE 以及相关技术的集成技术。

## 1. Spring 的 Remoting 和 Web Services

Spring 使用各种不同的技术实现远程支持集成类。由你自己普通的 POJOs 实现，远程支持简化了远程服务开发。目前，Spring 支持下列远程技术：

- **远程方法调用 (RMI)**: 通过使用 `RmiProxyFactoryBean` 和 `RmiServiceExporter`，Spring 支持传统的 RMI （使用 `java.rmi.Remote` 接口和 `java.rmi.RemoteException` ）的同时，通过 RMI 调用器（使用任意 Java  接口）支持透明远程调用。
- **Spring 的 HTTP 调用器**: Spring 提供了一种特殊的远程调用策略，允许通过 HTTP 进行 Java 序列化，支持任何 Java 接口（如 RMI 调用器所作所为）。相应的支持类有 `HttpInvokerProxyFactoryBean` 和 `HttpInvokerServiceExporter` 。
- **Hessian**: 通过使用 Spring 的 `HessianProxyFactoryBean` 和 `HessianServiceExporter`，你可以通过由 Caucho 提供的轻量级基于 HTTP 的二进制协议透明地暴露你的服务。
- **JAX-WS**: Spring 通过 JAX-WS 提供了对 Web services 的远程支持。
- **JMS**: 通过 `spring-jms` 模块中的 `JmsInvokerServiceExporter` 和 `JmsInvokerProxyFactoryBean` 类支持通过 JMS 作为基础协议进行远程处理。
- **AMQP**: 单独的 Spring AMQP 项目支持通过 AMQP 作为基础协议进行远程处理。

在讨论 Spring 的远程功能时，我们使用以下域模型和相应的服务：

```java
public class Account implements Serializable{

    private String name;

    public String getName(){
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

````java
public interface AccountService {

    public void insertAccount(Account account);

    public List<Account> getAccounts(String name);
}
````

````java
// the implementation doing nothing at the moment
public class AccountServiceImpl implements AccountService {

    public void insertAccount(Account acc) {
        // do something...
    }

    public List<Account> getAccounts(String name) {
        // do something...
    }
}
````

本节首先使用 RMI 将服务公开给远程客户端，然后再谈谈使用 RMI 的缺点。然后继续以使用 Hessian 作为协议的示例。

### 1.1 使用 RMI 暴露服务

通过使用 Spring 对 RMI 的支持，您可以通过 RMI 基础设施透明地暴露服务。进行了此设置之后，除了不存在对安全上下文传播或远程事务传播的标准支持这一事实之外，您基本上具有与远程 EJB 相似的配置。当您使用 RMI 调用程序时，Spring 确实为此类附加调用上下文提供了挂钩，因此，例如，您可以插入安全框架或自定义安全凭证。

#### 1.1.1 使用 `RmiServiceExporter` 导出服务

使用 `RmiServiceExporter`，我们可以将 `AccountService` 对象的接口暴露为 RMI 对象。可以使用 `RmiProxyFactoryBean` 来访问该接口，或者在传统 RMI 服务的情况下可以通过普通 RMI 来访问该接口。`RmiServiceExporter` 明确支持通过 RMI 调用器暴露任何非 RMI 服务。

我们首先必须在 Spring 容器中配置服务。以下示例显示了如何执行此操作：

```xml
<bean id="accountService" class="example.AccountServiceImpl">
    <!-- any additional properties, maybe a DAO? -->
</bean>
```

接下来，我们需要通过使用 `RmiServiceExporter` 暴露我们的服务。下面的例子展示了如何做：

```xml
<bean class="org.springframework.remoting.rmi.RmiServiceExporter">
    <!-- does not necessarily have to be the same name as the bean to be exported -->
    <property name="serviceName" value="AccountService"/>
    <property name="service" ref="accountService"/>
    <property name="serviceInterface" value="example.AccountService"/>
    <!-- defaults to 1099 -->
    <property name="registryPort" value="1199"/>
</bean>
```

上面例子中，我们覆写了 RMI 注册端口。通常，你的应用服务器也会维护 RMI 注册，要防止这两者发生冲突。此外，服务名称用来绑定服务。因此，在上面例子中，服务绑定到 `rmi/HOST:1199/AccountService`。我们稍后将在客户端使用这个 URL 来连接到服务。

> `servicePort` 属性已经被省略（默认为 `0` ）。这就意味着一个匿名端口被用来与服务进行交互。

#### 1.1.2 在客户端连接服务

我们的客户是一个简单的对象，使用 `AccountService` 来管理帐户，如以下示例所示：

```java
public class SimpleObject {

    private AccountService accountService;

    public void setAccountService(AccountService accountService) {
        this.accountService = accountService;
    }

    // additional methods using the accountService
}
```

为了在客户端上链接服务，我们创建了一个单独的 Spring 容器，其中包含以下简单对象和服务链接配置：

```xml
<bean class="example.SimpleObject">
    <property name="accountService" ref="accountService"/>
</bean>

<bean id="accountService" class="org.springframework.remoting.rmi.RmiProxyFactoryBean">
    <property name="serviceUrl" value="rmi://HOST:1199/AccountService"/>
    <property name="serviceInterface" value="example.AccountService"/>
</bean>
```

这就是我们要在客户端上支持远程帐户服务所需要做的一切。Spring 透明地创建一个调用程序，并通过 `RmiServiceExporter` 远程启用并暴露帐户服务。在客户端，我们使用 `RmiProxyFactoryBean` 连接到该服务。

### 1.2 使用 Hessian 通过 HTTP 进行远程服务调用

Hessian 提供了一种基于 HTTP 的二进制远程协议。由 Caucho 开发，你可以在 https://www.caucho.com/ 找到更多有关 Hessian 的信息。

#### 1.2.1 为 Hessian 连接 `DispatcherServlet`

Hessian 通过 HTTP 进行通信，并不使用开发者自定义的 servlet。通过使用 Spring 的 `DispatcherServlet` 原理（参考 [mvc-servlet](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/webmvc.html#mvc-servlet) ），我们可以连接这样一个 servlet 来暴露你的服务。首先，我们需要在我们的应用中创建一个新的 servlet，如下面示例 `web.xml` 片段所示：

```xml
<servlet>
    <servlet-name>remoting</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
    <servlet-name>remoting</servlet-name>
    <url-pattern>/remoting/*</url-pattern>
</servlet-mapping>
```

如果你熟悉 Spring 的 `DispatcherServlet` 原理，你可能会知道现在你需要创建一个 Spring 容器配置资源文件，名为 `remoting-servlet.xml` （在你的 servlet 名称之后）在 `WEB-INF` 目录下。该应用上下文在下一节中使用。

另外，考虑使用更简单的 Spring `HttpRequestHandlerServlet` 。这样做允许你讲远程服务暴露器定义内置到你的应用根上下文中（默认位置 `WEB-INF/applicationContext.xml`），每个单独的 servlet 指向特定的服务暴露器 bean。这种情况下，每个 servlet 名称需要与它所对应的目标服务暴露器名称相互匹配。

#### 1.2.2 使用 `HessianServiceExporter` 暴露你的 Beans 

在新创建的名为 `remoting-servlet.xml` 的应用上下文中，我们创建一个 `HessianServiceExporter` 来暴露你的服务，如下面例子所示：

```xml
<bean id="accountService" class="example.AccountServiceImpl">
    <!-- any additional properties, maybe a DAO? -->
</bean>

<bean name="/AccountService" class="org.springframework.remoting.caucho.HessianServiceExporter">
    <property name="service" ref="accountService"/>
    <property name="serviceInterface" value="example.AccountService"/>
</bean>
```

现在我们已经准备在客户端连接到服务。由于没有显式指定处理器映射（将请求 URLs 映射到服务），因此我们使用 `BeanNameUrlHandlerMapping` 。因此，服务被暴露在 URL 上，该 URL 通过将服务的 bean 名称包含在 `DispatcherServlet` 实例映射（如前面定义所示）中来表示：`http://HOST:8080/remoting/AccountService`。

另外，你可以在你的根应用上下文中创建一个`HessianServiceExporter` （比如，在 `WEB-INF/applicationContext.xml`），如下面例子所示：

```xml
<bean name="accountExporter" class="org.springframework.remoting.caucho.HessianServiceExporter">
    <property name="service" ref="accountService"/>
    <property name="serviceInterface" value="example.AccountService"/>
</bean>
```

在后一种情况下，您应该在 `web.xml` 中为此导出程序定义一个相应的 servlet，并得到相同的最终结果：导出程序映射到 `/remoting/AccountService` 的请求路径。注意，servlet 名称需要与目标导出器的 bean 名称匹配。以下示例显示了如何执行此操作：

```xml
<servlet>
    <servlet-name>accountExporter</servlet-name>
    <servlet-class>org.springframework.web.context.support.HttpRequestHandlerServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>accountExporter</servlet-name>
    <url-pattern>/remoting/AccountService</url-pattern>
</servlet-mapping>
```

#### 1.2.3 从客户端连接到服务

通过使用 `HessianProxyFactoryBean` ，我们可以从客户端连接到服务。相同的原理也应用在 RMI 示例中。我们创建一个独立的 bean 工厂或应用上下文，提到了下面 `SimpleObject` 所在的 beans ，通过使用 `AccountService` 管理账户。如下面例子所示：

``` xml
<bean class="example.SimpleObject">
    <property name="accountService" ref="accountService"/>
</bean>

<bean id="accountService" class="org.springframework.remoting.caucho.HessianProxyFactoryBean">
    <property name="serviceUrl" value="http://remotehost:8080/remoting/AccountService"/>
    <property name="serviceInterface" value="example.AccountService"/>
</bean>
```

#### 1.2.4 应用 HTTP 基本身份认证到通过 Hessian 暴露的服务上

Hessian 的一个优点就是我们可以很容易地应用 HTTP 基本身份认证，因为两者都是基于 HTTP 的。通常的 HTTP 服务器安全机制可以通过使用诸如 `web.xml` 安全特性等方式来应用。通常，这里你不需要使用针对每个用户的安全凭证。你可以使用定义在 `HessianProxyFactoryBean` 层级上的共享凭证（类似于 JDBC `DataSource` ），如下面例子所示：

```xml
<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping">
    <property name="interceptors" ref="authorizationInterceptor"/>
</bean>

<bean id="authorizationInterceptor"
        class="org.springframework.web.servlet.handler.UserRoleAuthorizationInterceptor">
    <property name="authorizedRoles" value="administrator,operator"/>
</bean>
```

在前面的例子中，我们显式提到 `BeanNameUrlHandlerMapping` 并设置一个拦截器，仅仅允许管理员和管理者调用应用上下文中提到的 beans 。

> 前面的示例并未展示灵活的安全基础设施。有关安全性的更多选项，请参阅 https://projects.spring.io/spring-security/ 上的 Spring Security 项目。

### 1.3 使用 HTTP 调用器暴露服务

除了 Hessian，Spring HTTP 调用器也是一种轻量级的协议，可以使用它们自己的精简的序列化机制或者 Java 标准序列化机制通过 HTTP 暴露服务。如果你的参数和返回值类型是无法通过 Hessian 使用的序列化机制序列化的复杂类型，这就是一种巨大的优势。参考下一章节了解有关远程技术选择的更多考量。

在底层，Spring 使用 JDK 或者 Apache `HttpComponents` 提供的标准类库执行 HTTP 调用。如果你需要更多高级和易用的功能，使用后者。参考 [hc.apache.org/httpcomponents-client-ga/](https://hc.apache.org/httpcomponents-client-ga/) 获取更多信息。

> 警惕不安全的 Java 序列化带来的风险：操作输入流可能导致反序列化过程中意料之外的服务器上的代码执行。因此，不要将 HTTP 调用者端点暴露给不信任的客户端。进一步地，仅在你自己的服务之间暴露它们。通常，我们强烈推荐使用任何其它消息格式（比如 JSON）来替代。
>
> 如果你考虑 Java 序列化带来的安全风险，考虑在核心 JVM 层面使用通用的序列化过滤器机制，该机制随着 JDK 9 发布，不过向下支持 JDK 8, 7 以及 6 。参考 https://blogs.oracle.com/java-platform-group/entry/incoming_filter_serialization_data_a 和 https://openjdk.java.net/jeps/290 。

#### 1.3.1 暴露服务对象

为服务对象设置 HTTP 调用程序基础设施与使用 Hessian 进行操作的方式非常相似。Hessian 支持提供了 `HessianServiceExporter`，Spring 的 `HttpInvoker` 支持提供了 `org.springframework.remoting.httpinvoker.HttpInvokerServiceExporter`。

为了在 Spring Web MVC `DispatcherServlet` 中暴露 `AccountService`，需要将下面的配置添加到请求分发器的应用上下文配置文件中：

```xml
<bean name="/AccountService" class="org.springframework.remoting.httpinvoker.HttpInvokerServiceExporter">
    <property name="service" ref="accountService"/>
    <property name="serviceInterface" value="example.AccountService"/>
</bean>
```

这样的暴露器定义通过 `DispatcherServlet` 实例的标准映射工具暴露，如 [the section on Hessian](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#remoting-caucho-protocols) 中所述。

或者，你可以在你的根应用上下文中（比如，在 `WEB-INF/applicationContext.xml` 中）创建一个 `HttpInvokerServiceExporter` 。如下面例子所示：

```xml
<bean name="accountExporter" class="org.springframework.remoting.httpinvoker.HttpInvokerServiceExporter">
    <property name="service" ref="accountService"/>
    <property name="serviceInterface" value="example.AccountService"/>
</bean>
```

另外，你可以为这个暴露器在 `web.xml` 中定义对应的 servlet 。该 servlet 的名称匹配目标暴露器的 bean 名称。如下面例子所示：

```xml
<servlet>
    <servlet-name>accountExporter</servlet-name>
    <servlet-class>org.springframework.web.context.support.HttpRequestHandlerServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>accountExporter</servlet-name>
    <url-pattern>/remoting/AccountService</url-pattern>
</servlet-mapping>
```

#### 1.3.2 从客户端连接服务

同样，从客户端链接服务与使用 Hessian 时的方式非常相似。通过使用代理，Spring 可以将对 HTTP POST 请求的调用转换为指向导出服务的 URL。以下示例显示如何配置：

```xml
<bean id="httpInvokerProxy" class="org.springframework.remoting.httpinvoker.HttpInvokerProxyFactoryBean">
    <property name="serviceUrl" value="http://remotehost:8080/remoting/AccountService"/>
    <property name="serviceInterface" value="example.AccountService"/>
</bean>
```

如前所述，您可以选择要使用的 HTTP 客户端。默认情况下，`HttpInvokerProxy` 使用 JDK 的 HTTP 功能，但是您也可以通过设置 `HTTPInvokerRequestExecutor` 属性来使用 Apache `HttpComponents` 客户端。以下示例显示了如何执行此操作：

```xml
<property name="httpInvokerRequestExecutor">
    <bean class="org.springframework.remoting.httpinvoker.HttpComponentsHttpInvokerRequestExecutor"/>
</property>
```

### 1.4 Web Services

Spring 提供了对标准 Java web services APIs 的完整支持：

- 使用 JAX-WS 暴露 web services
- 使用 JAX-WS 访问 web services 

除了在 Spring Core 中对 JAX-WS 的完整支持之外，Spring 产品组合还具有 [Spring Web Services](http://www.springframework.org/spring-ws) ，这是一种契约优先，文档驱动的 web services 解决方案—强烈建议用来构建现代的，面向未来的 Web 服务。

#### 1.4.1 使用 JAX-WS 暴露基于 Servlet 的 Web Services

Spring 为 JAX-WS servlet 端点实现提供了一个方便的基类：`SpringBeanAutowiringSupport`。为了公开我们的 `AccountService`，我们扩展 Spring 的 `SpringBeanAutowiringSupport` 类并在此处实现我们的业务逻辑，通常将调用委托给业务层。我们使用 Spring 的 `@Autowired` 注解来表达对 Spring 管理的 bean 的依赖。以下示例显示了扩展 `SpringBeanAutowiringSupport` 的类：

```java
/**
 * JAX-WS compliant AccountService implementation that simply delegates
 * to the AccountService implementation in the root web application context.
 *
 * This wrapper class is necessary because JAX-WS requires working with dedicated
 * endpoint classes. If an existing service needs to be exported, a wrapper that
 * extends SpringBeanAutowiringSupport for simple Spring bean autowiring (through
 * the @Autowired annotation) is the simplest JAX-WS compliant way.
 *
 * This is the class registered with the server-side JAX-WS implementation.
 * In the case of a Java EE server, this would simply be defined as a servlet
 * in web.xml, with the server detecting that this is a JAX-WS endpoint and reacting
 * accordingly. The servlet name usually needs to match the specified WS service name.
 *
 * The web service engine manages the lifecycle of instances of this class.
 * Spring bean references will just be wired in here.
 */
import org.springframework.web.context.support.SpringBeanAutowiringSupport;

@WebService(serviceName="AccountService")
public class AccountServiceEndpoint extends SpringBeanAutowiringSupport {

    @Autowired
    private AccountService biz;

    @WebMethod
    public void insertAccount(Account acc) {
        biz.insertAccount(acc);
    }

    @WebMethod
    public Account[] getAccounts(String name) {
        return biz.getAccounts(name);
    }
}
```

我们的 `AccountServiceEndpoint` 需要在与 Spring 上下文相同的 Web 应用程序中运行，以允许访问 Spring 的基础设施。在 Java EE 环境中，默认情况下是这种情况，使用标准契约进行 JAX-WS Servlet 端点部署。有关详细信息，请参见各种 Java EE Web 服务教程。

#### 1.4.2 使用 JAX-WS 暴露独立 Web Services

Oracle JDK 随附的内置 JAX-WS 提供程序通过使用 JDK 中也包含的内置 HTTP 服务器来支持 Web 服务公开。Spring 的 `SimpleJaxWsServiceExporter` 会在 Spring 应用程序上下文中检测到所有带有 `@WebService` 注解的 bean，并通过默认的 JAX-WS 服务器（JDK HTTP 服务器）将其导出。

在这种情况下，端点实例被定义和管理为 Spring bean 本身。它们是使用 JAX-WS 引擎注册的，但是它们的生命周期取决于 Spring 应用程序上下文。这意味着您可以将 Spring 功能（例如显式依赖项注入）应用于端点实例。通过 `@Autowired` 进行注解驱动的注入也有效。以下示例显示了如何定义这些 bean：

```xml
<bean class="org.springframework.remoting.jaxws.SimpleJaxWsServiceExporter">
    <property name="baseAddress" value="http://localhost:8080/"/>
</bean>

<bean id="accountServiceEndpoint" class="example.AccountServiceEndpoint">
    ...
</bean>

...
```

`AccountServiceEndpoint` 可以但不必从 Spring 的 `SpringBeanAutowiringSupport` 派生，因为此示例中的端点是完全由 Spring 管理的 bean。这意味着端点实现可以如下所示（不声明任何超类-仍然使用 Spring 的 `@Autowired` 配置注解）：

```java
@WebService(serviceName="AccountService")
public class AccountServiceEndpoint {

    @Autowired
    private AccountService biz;

    @WebMethod
    public void insertAccount(Account acc) {
        biz.insertAccount(acc);
    }

    @WebMethod
    public List<Account> getAccounts(String name) {
        return biz.getAccounts(name);
    }
}
```

#### 1.4.3 使用 JAX-WS RI 的 Spring 支持导出 Web Services

Oracle 的 JAX-WS RI，作为 GlassFish 项目的一部分，将 Spring 支持作为它的 JAX-WS 通用项目的一部分。这就允许将  JAX-WS 端点定义为 Spring 管理的 beans ，类似于上一节中讨论的独立模式，不过这一次是在 Servlet 环境下。

> 这不可移植到 Java EE 环境中。它主要适用于将 JAX-WS RI 嵌入为 Web 应用程序一部分的非 EE 环境，例如 Tomcat 。

与导出基于 servlet 的端点的标准样式的不同之处在于，端点实例本身的生命周期由 Spring 管理，并且在 `web.xml` 中仅定义了一个 JAX-WS servlet 。使用标准的 Java EE 样式（如前所述），每个服务端点都有一个 servlet 定义，每个端点通常都委派给 Spring Bean（如前所述，通过使用 `@Autowired`）。

参考 https://jax-ws-commons.java.net/spring/ 获取更多有关配置和使用方式的细节。

#### 1.4.4 使用 JAX-WS 访问 Web Services

Spring 提供了两个工厂 bean 来创建 JAX-WS Web 服务代理，分别是 `LocalJaxWsServiceFactoryBean` 和 `JaxWsPortProxyFactoryBean`。前者只能返回一个 JAX-WS 服务类供我们使用。后者是完整版本，可以返回实现我们的业务服务接口的代理。在下面的示例中，我们使用 `JaxWsPortProxyFactoryBean` 为 `AccountService` 端点创建代理（同样）：

```xml
<bean id="accountWebService" class="org.springframework.remoting.jaxws.JaxWsPortProxyFactoryBean">
    <property name="serviceInterface" value="example.AccountService"/> 
    <property name="wsdlDocumentUrl" value="http://localhost:8888/AccountServiceEndpoint?WSDL"/>
    <property name="namespaceUri" value="http://example/"/>
    <property name="serviceName" value="AccountService"/>
    <property name="portName" value="AccountServiceEndpointPort"/>
</bean>
```

`wsdlDocumentUrl` 是 WSDL 文件的 URL 。Spring 在启动时需要使用它来创建 JAX-WS 服务。`namespaceUri` 对应于 `.wsdl` 文件中的 `targetNamespace`。`serviceName` 对应于 `.wsdl` 文件中的服务名称。`portName` 对应于 `.wsdl` 文件中的端口名称。

访问 Web 服务很容易，因为我们有一个供其使用的 bean 工厂，该工厂将其公开为名为 `AccountService` 的接口。以下示例显示了如何在 Spring 中进行连接：

```xml
<bean id="client" class="example.AccountClientImpl">
    ...
    <property name="service" ref="accountWebService"/>
</bean>
```

在客户端代码中，可以像访问普通类一样访问 web service ，如下面例子所示：

```java
public class AccountClientImpl {

    private AccountService service;

    public void setService(AccountService service) {
        this.service = service;
    }

    public void foo() {
        service.insertAccount(...);
    }
}
```

> 上面的内容略有简化，因为 JAX-WS 要求端点接口和实现类使用 `@WebService`，`@SOAPBinding` 等注解进行注释。这意味着您不能（轻松地）将纯 Java 接口和实现类用作 JAX-WS 端点工件。您需要先对其进行相应注解。查看 JAX-WS 文档以获取有关这些需求的详细信息。

### 1.5 通过 JMS 暴露服务

您还可以通过使用 JMS 作为基础通信协议来透明地公开服务。Spring 框架中的 JMS 远程支持非常基本。它在 `same thread` 和同一非事务性 `Session` 中发送和接收。吞吐量取决于实现。请注意，这些单线程和非事务性约束仅适用于 Spring 的 JMS 远程支持。请参阅 [JMS（Java消息服务）](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms) ，以获取有关 Spring 对基于 JMS 消息的丰富支持的信息。

下面的接口可以用在服务端和客户端：

```java
package com.foo;

public interface CheckingAccountService {

    public void cancelAccount(Long accountId);
}
```

上面接口的下面的简单实现可以用于服务端：

```java
package com.foo;

public class SimpleCheckingAccountService implements CheckingAccountService {

    public void cancelAccount(Long accountId) {
        System.out.println("Cancelling account [" + accountId + "]");
    }
}
```

以下配置文件包含在客户机和服务器上共享的 JMS 基础设施 Bean：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="connectionFactory" class="org.apache.activemq.ActiveMQConnectionFactory">
        <property name="brokerURL" value="tcp://ep-t43:61616"/>
    </bean>

    <bean id="queue" class="org.apache.activemq.command.ActiveMQQueue">
        <constructor-arg value="mmm"/>
    </bean>

</beans>
```

#### 1.5.1 服务端配置

在服务器上，您需要公开使用 `JmsInvokerServiceExporter` 的服务对象，如以下示例所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="checkingAccountService"
            class="org.springframework.jms.remoting.JmsInvokerServiceExporter">
        <property name="serviceInterface" value="com.foo.CheckingAccountService"/>
        <property name="service">
            <bean class="com.foo.SimpleCheckingAccountService"/>
        </property>
    </bean>

    <bean class="org.springframework.jms.listener.SimpleMessageListenerContainer">
        <property name="connectionFactory" ref="connectionFactory"/>
        <property name="destination" ref="queue"/>
        <property name="concurrentConsumers" value="3"/>
        <property name="messageListener" ref="checkingAccountService"/>
    </bean>

</beans>
```

````java
package com.foo;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Server {

    public static void main(String[] args) throws Exception {
        new ClassPathXmlApplicationContext("com/foo/server.xml", "com/foo/jms.xml");
    }
}
````

#### 1.5.2 客户端配置

客户端只需要创建一个客户端代理即可实现协议接口（`CheckingAccountService`）。

以下示例定义了可以注入到其他客户端对象中的 Bean（代理负责通过 JMS 将调用转发到服务器端对象）：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="checkingAccountService"
            class="org.springframework.jms.remoting.JmsInvokerProxyFactoryBean">
        <property name="serviceInterface" value="com.foo.CheckingAccountService"/>
        <property name="connectionFactory" ref="connectionFactory"/>
        <property name="queue" ref="queue"/>
    </bean>

</beans>
```

````java
package com.foo;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Client {

    public static void main(String[] args) throws Exception {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("com/foo/client.xml", "com/foo/jms.xml");
        CheckingAccountService service = (CheckingAccountService) ctx.getBean("checkingAccountService");
        service.cancelAccount(new Long(10));
    }
}
````

### 1.6 AMQP

参考 [Spring AMQP Reference Guide’s 'Spring Remoting with AMQP' section](https://docs.spring.io/spring-amqp/docs/current/reference/html/_reference.html#remoting) 获取更多信息。

>远程接口的自动探测并未实现
>
>之所以并未实现远程接口的自动探测，目的是避免开放过多的入口给远程调用者。目标对象可能实现内部回调接口，比如 `InitializingBean` 或者 `DisposableBean` ，这些接口可能并不想要暴露给调用者。
>
>为目标实现的所有接口提供代理通常在本地场景下不是问题。不过，当你暴露远程服务时，你应该暴露特定的服务接口，该接口包含可以远程使用的操作。除了内部回调接口，目标可能还会实现许多其他业务接口，这些接口也许并不希望远程暴露。基于这些原因，我们强制规定必须指定要暴露的服务接口。
>
>这是在配置便利性和内部方法的意外暴露的风险之间的权衡。始终指定要暴露的服务接口并不会增加多少工作量，但是可以保证你精确控制特定方法的暴露。

### 1.7 技术选型的考量

这里提到的每种技术都有其自身的缺陷。进行技术选型时，你应该谨慎考虑你的需要，你希望暴露的服务，以及你需要通过网络发送的对象。

当使用 RMI 时，你不能通过 HTTP 协议访问对象，除非你使用隧道技术处理 RMI 流量。RMI 是一种相当重量级的协议，它支持完整对象的序列化，当你使用的复杂数据模型需要序列化并通过网络传输时这一点非常重要。不过，RMI-JRMP 只能用于 Java 客户端。它是一种 Java-to-Java 的远程服务解决方案。

如果您既需要基于 HTTP 的远程处理，又需要依赖 Java 序列化，那么 Spring 的 HTTP 调用程序是一个不错的选择。它与 RMI 调用程序共享基本的基础设施，但使用 HTTP 作为传输。请注意，HTTP 调用程序不仅适用于 Java-Java 远程处理，也适用于客户端和服务器端的 Spring 环境。（后者也适用于非 RMI 接口的 Spring RMI 调用程序。）

在异构环境中运行时，Hessian 可能会提供重要的价值，因为它们明确允许使用非 Java 客户端。但是，非 Java 支持仍然有限。已知的问题包括 Hibernate 对象的序列化以及延迟初始化的集合。如果您有这样的数据模型，请考虑使用 RMI 或 HTTP 调用程序而不是 Hessian。

JMS 可用于提供服务集群，并使 JMS 代理负责负载平衡，发现和自动故障转移。默认情况下，Java 序列化用于 JMS 远程处理，但是 JMS 提供程序可以使用不同的机制进行序列化，例如 XStream，以使服务器可以用其他技术实现。

最后但并非最不重要的一点是，EJB 具有优于 RMI 的优势，因为它支持基于标准角色的身份验证和授权以及远程事务传播。尽管核心 Spring 并没有提供 RMI 调用程序或 HTTP 调用程序来支持安全上下文传播，但也有可能。Spring 仅提供适当的挂钩来插入第三方或自定义解决方案。

### 1.8 REST Endpoints

Spring Framework 提供了两种选择来发起对 REST endpoints 的调用：

- [使用 `RestTemplate`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#rest-resttemplate): 原生的 Spring REST 客户端，使用同步的，模版方法 API 。
- [WebClient](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-client): 非阻塞式，响应式方法，支持同步和异步及流式处理场景。

> 从 5.0 开始，非阻塞的反应式 WebClient 提供了对 RestTemplate 的现代替代方案，并有效地支持同步和异步以及流方案。`RestTemplate` 将在以后的版本中弃用，并且以后不会添加任何主要的新功能。

#### 1.8.1 使用 `RestTemplate`

`RestTemplate` 通过 HTTP 客户端库提供了更高级别的 API。它使在一行中轻松调用 REST 端点变得容易。它公开了以下几组重载方法：

| Method group      | Description                                                  |
| :---------------- | :----------------------------------------------------------- |
| `getForObject`    | 通过 GET 检索一种表示形式。                                  |
| `getForEntity`    | 通过 GET 检索一个 `ResponseEntity` (也就是，status，headers，以及 body) 。 |
| `headForHeaders`  | 使用 HEAD 检索资源的所有首部。                               |
| `postForLocation` | 使用 POST 创建一个新资源，并通过响应返回 `Location` 首部。   |
| `postForObject`   | 使用 POST 创建一个新资源，并通过响应返回对应的表示。         |
| `postForEntity`   | 使用 POST 创建一个新资源，并通过响应返回对应的表示。         |
| `put`             | 使用 PUT 创建或者更新一个资源。                              |
| `patchForObject`  | 通过使用 PATCH 更新一个资源，并通过响应返回对应的表示。注意，JDK `HttpURLConnection` 不支持 `PATCH` ，但是 Apache `HttpComponents` 及其他方案都支持。 |
| `delete`          | 使用 DELETE 删除特定 URI 上的资源。                          |
| `optionsForAllow` | 使用 ALLOW 检索资源允许的 HTTP 方法。                        |
| `exchange`        | 前述方法的通用性强（且不那么固执）版本，可在需要时提供额外的灵活性。它接受一个 `RequestEntity`（包括 HTTP 方法，URL， headers 和 body 作为输入）并返回一个 `ResponseEntity` 。这些方法允许使用 `ParametersizedTypeReference` 而不是 `Class` 来指定具有泛型的响应类型。 |
| `execute`         | 执行请求的最通用方法，完全控制通过回调接口进行的请求准备和响应提取。 |

##### 初始化

默认的构造器使用 `java.net.HttpURLConnection` 来执行请求。你可以切换到实现了 `ClientHttpRequestFactory` 的其他 HTTP 类库。内建下列支持：

- Apache HttpComponents
- Netty
- OkHttp

比如，要切换到 Apache HttpComponents，你可以这样做：

```java
RestTemplate template = new RestTemplate(new HttpComponentsClientHttpRequestFactory());
```

每个 `ClientHttpRequestFactory` 暴露配置选项特定于内部的 HTTP 客户端类库－比如，证书，连接池，或者其他细节。

> 请注意，当访问代表错误的响应状态（例如401）时，HTTP请求的 `java.net` 实现会引发异常。如果这是一个问题，请切换到另一个 HTTP 客户端库。

##### URIs

许多 `RestTmeplate` 方法接受一个 URI 模板和 URI 模板变量，一个 `String` 类型变量，或者是 `Map<String, String>` 。

下面的例子使用一个 `String` 变量参数：

```java
String result = restTemplate.getForObject(
        "https://example.com/hotels/{hotel}/bookings/{booking}", String.class, "42", "21");
```

下面的例子使用 `Map<String, String>`：

```java
Map<String, String> vars = Collections.singletonMap("hotel", "42");

String result = restTemplate.getForObject(
        "https://example.com/hotels/{hotel}/rooms/{hotel}", String.class, vars);
```

始终注意 URI 模板时自动编码的，如下面例子所示：

```java
restTemplate.getForObject("https://example.com/hotel list", String.class);

// Results in request to "https://example.com/hotel%20list"
```

您可以使用 `RestTemplate` 的 `uriTemplateHandler` 属性来自定义 URI 的编码方式。另外，您可以准备一个 `java.net.URI` 并将其传递到接受 `URI` 的 `RestTemplate` 方法之一。

有关 URI 使用和编码的更多细节，参考 [URI Links](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-uri-building) 。

##### Headers

你可以使用 `exchange()` 方法指定请求首部，如下面例子所示：

```java
String uriTemplate = "https://example.com/hotels/{hotel}";
URI uri = UriComponentsBuilder.fromUriString(uriTemplate).build(42);

RequestEntity<Void> requestEntity = RequestEntity.get(uri)
        .header(("MyRequestHeader", "MyValue")
        .build();

ResponseEntity<String> response = template.exchange(requestEntity, String.class);

String responseHeader = response.getHeaders().getFirst("MyResponseHeader");
String body = response.getBody();
```

你可以通过许多返回 `ResponseEntity` 的 `RestTemplate` 方法变体获取响应首部。

##### Body

被传入 `RestTemplate` 方法和从 `RestTemplate` 方法返回的对象都在 `HttpMessageConverter` 的帮助下与原始内容相互转化。

对于 POST，输入对象被序列化为请求体，如下面例子所示：

```java
URI location = template.postForLocation("https://example.com/people", person);
```

您无需显式设置请求的 `Content-Type` 首部。在大多数情况下，您可以找到基于源 `Object` 类型的兼容消息转换器，并且所选消息转换器会相应地设置内容类型。如有必要，可以使用 `exchange` 方法显式提供 `Content-Type` 请求首部，进而影响选择哪种消息转换器。

对于 GET，响应的主体被序列化为输出 `Object` ，如下面例子所示：

```java
Person person = restTemplate.getForObject("https://example.com/people/{id}", Person.class, 42);
```

请求的 `Accept` 首部不需要显式设定。大多数情况下，一个兼容的消息转换器能够基于期望的响应类型被找到，然后帮助填充 `Accept` 首部。如果必要，你可以使用 `exchange` 方法显式提供 `Accept` 首部。

默认地，`RestTemplate` 会注册所有的内建 [message converters](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#rest-message-conversion) ，依赖类路径检查以帮助确定存在何种可选的转换类库。你也可以显式设定要使用的消息转换器。

##### 消息转换

[Same as in Spring WebFlux](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-codecs)

`spring-web` 模块包含 `HttpMessageConverter` 契约，通过 `InputStream` 读取 HTTP 请求的请求体，通过 `OutputStream` 将数据写入 HTTP 响应体。`HttpMessageConverter` 实例可以在服务端（比如，在 SpringMVC REST 控制器里）和客户端（比如，用在 `RestTemplate` 中）使用。

框架中提供了主要媒体（MIME）类型的具体实现，默认情况下，这些实现已在客户端通过 `RestTemplate` 注册，在服务端通过 `RequestMethodHandlerAdapter` 注册（请参阅 [配置消息转换器](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-config-message-converters)）。

`HttpMessageConverter` 实现在下一节中描述。对所有的消息转换器，都有一个默认的媒体类型，不过你可以通过设定 `supportedMediaTypes` bean 属性覆盖默认值。下面的表描述了各种实现：

| MessageConverter                         | Description                                                  |
| :--------------------------------------- | :----------------------------------------------------------- |
| `StringHttpMessageConverter`             | 一个 `HttpMessageConverter` 实现，可以从 HTTP 请求实例读取 `String` 实例，向 HTTP 响应写入 `String` 实例。默认地，该转换器支持所有的文本媒体类型（`text/*`）并以 `Content-Type`  值 `text/plain` 写入。 |
| `FormHttpMessageConverter`               | 一个 `HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入表单数据。默认情况下，此转换器读取和写入 `application/x-www-form-urlencoded` 媒体类型。 表单数据是从 `MultiValueMap<String, String>` 中读取并写入的。 |
| `ByteArrayHttpMessageConverter`          | 一个 `HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入字节数组。默认情况下，此转换器支持所有媒体类型（`*/*`），并使用 `application/octet-stream` 的 `Content-Type` 进行写入。您可以通过设置 `supportedMediaTypes` 属性并覆盖 `getContentType(byte[])` 来覆盖此属性。 |
| `MarshallingHttpMessageConverter`        | 一个 `HttpMessageConverter` 实现，可以通过使用来自 `org.springframework.oxm` 包的 Spring 的 `Marshaller` 和 `Unmarshaller` 抽象来读写 XML。该转换器需要使用 `Marshaller` 和 `Unmarshaller` 才能工作。您可以通过构造函数或 bean 属性注入它们。默认情况下，此转换器支持 `text/xml` 和 `application/xml`。 |
| `MappingJackson2HttpMessageConverter`    | 一个 `HttpMessageConverter` 实现，可以通过使用 Jackson 的 `ObjectMapper` 来读取和写入 JSON。您可以根据需要使用 Jackson 提供的注解来自定义 JSON 映射。当需要进一步控制时（对于需要为特定类型提供自定义 JSON 序列化器/反序列化器的情况），可以通过 `ObjectMapper` 属性注入自定义 `ObjectMapper`。默认情况下，此转换器支持 `application/json`。 |
| `MappingJackson2XmlHttpMessageConverter` | 一个 `HttpMessageConverter` 实现，可以使用 [Jackson XML](https://github.com/FasterXML/jackson-dataformat-xml) 扩展名的 `XmlMapper` 来读写 XML。您可以根据需要使用 JAXB 或 Jackson 提供的注解来自定义 XML 映射。当需要进一步控制时（对于需要为特定类型提供自定义 XML 序列化器/反序列化器的情况），可以通过 `ObjectMapper` 属性注入自定义 `XmlMapper`。默认情况下，此转换器支持 `application/xml`。 |
| `SourceHttpMessageConverter`             | `HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入 `javax.xml.transform.Source`。仅支持 `DOMSource`，`SAXSource` 和 `StreamSource`。默认情况下，此转换器支持 `text/xml` 和 `application/xml`。 |
| `BufferedImageHttpMessageConverter`      | 一个`HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入 `java.awt.image.BufferedImage`。该转换器读取和写入 Java I/O API 支持的媒体类型。 |

##### Jackson JSON 视图

您可以指定 [Jackson JSON View](https://www.baeldung.com/jackson-json-view-annotation) 以仅序列化对象属性的一部分，如以下示例所示：

```java
MappingJacksonValue value = new MappingJacksonValue(new User("eric", "7!jd#h23"));
value.setSerializationView(User.WithoutPasswordView.class);

RequestEntity<MappingJacksonValue> requestEntity =
    RequestEntity.post(new URI("https://example.com/user")).body(value);

ResponseEntity<String> response = template.exchange(requestEntity, String.class);
```

##### Multipart

要发送多部分数据，您需要提供一个 `MultiValueMap <String, Object>`，其值可以是部分内容的 `Object`，文件部分的 `Resource` 或带首部的部分内容的 `HttpEntity`。例如：

```java
    MultiValueMap<String, Object> parts = new LinkedMultiValueMap<>();

    parts.add("fieldPart", "fieldValue");
    parts.add("filePart", new FileSystemResource("...logo.png"));
    parts.add("jsonPart", new Person("Jason"));

    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_XML);
    parts.add("xmlPart", new HttpEntity<>(myBean, headers));
```

在大多数情况下，您不必为每个部分指定 `Content-Type`。内容类型是根据要序列化的 `HttpMessageConverter` 自动确定的，对于基于文件扩展名的 `Resource` 则是自动确定的。如有必要，您可以显式地为 `MediaType` 提供一个 `HttpEntity` 包装器。

一旦 `MultiValueMap` 准备就绪，您可以将其传递给 `RestTemplate`，如下所示：

```java
    MultiValueMap<String, Object> parts = ...;
    template.postForObject("https://example.com/upload", parts, Void.class);
```

如果 `MultiValueMap` 包含至少一个非 `String` 值，则 `FormHttpMessageConverter` 将 `Content-Type` 设置为 `multipart/form-data`。如果 `MultiValueMap` 具有 `String` 值，则 `Content-Type` 默认为 `application/x-www-form-urlencoded`。如有必要，还可以显式设置 `Content-Type`。

#### 1.8.2 使用 `AsyncRestTemplate` (已废弃)

`AsyncRestTemplate` 已弃用。对于所有您可能考虑使用 `AsyncRestTemplate` 的场景，请使用 [WebClient](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-client) 代替。

## 2. Enterprise JavaBeans (EJB) 集成

EJB 好像已经被业界抛弃……

## 3. JMS (Java Message Service)

Spring 提供了一个 JMS 集成框架用来简化 JMS API 的使用，非常类似于 Spring 的 JDBC 集成对 JDBC API 使用的简化。

JMS 可以粗略分成两个部分功能，称为消息生产和消息消费。`JmsTemplate` 类被用来生产消息和同步消息接收。对于类似于 Java EE 消息驱动 bean 样式的异步接收，Spring 提供了许多消息侦听器容器，可用于创建消息驱动 POJO（MDP）。Spring 还提供了一种声明式方法来创建消息侦听器。

`org.springframework.jms.core` 软件包提供了使用 JMS 的核心功能。它包含 JMS 模板类，该 JMS 模板类通过处理资源的创建和释放来简化 JMS 的使用，就像 `JdbcTemplate` 对 JDBC 所做的那样。Spring 模板类共有的设计原则是提供辅助方法来执行常见的操作，并且对于更复杂的用法，将处理任务的核心委托给用户实现的回调接口。 JMS 模板遵循相同的设计。这些类提供了各种便利的方法，用于发送消息，同步使用消息以及向用户公开 JMS 会话和消息生成器。

`org.springframework.jms.support` 包提供了 `JMSException` 转换功能。转换将检查的 `JMSException` 层次结构转换为未检查的异常的镜像层次结构。如果已检查的 `javax.jms.JMSException` 的提供者特定的子类存在，则将此异常包装在未检查的 `UncategorizedJmsException` 中。

`org.springframework.jms.support.converter` 包提供了 `MessageConverter` 抽象，可以在 Java 对象和 JMS 消息之间进行转换。

`org.springframework.jms.support.destination` 包提供了用于管理 JMS 目的地的各种策略，例如为 JNDI 中存储的目的地提供服务定位器。

`org.springframework.jms.annotation` 包通过使用 `@JmsListener` 提供了必要的基础设施来支持注解驱动的侦听器端点。

`org.springframework.jms.config` 包为` jms` 名称空间提供了解析器实现，并提供了 Java config 支持来配置监听器容器和创建监听器端点。

最后，`org.springframework.jms.connection` 包提供了适用于独立应用程序的 `ConnectionFactory` 的实现。它还包含 Spring 用于 JMS 的 `PlatformTransactionManager` 的实现（巧妙地名为 `JmsTransactionManager`）。这样可以将 JMS 作为事务资源无缝集成到 Spring 的事务管理机制中。

> 从 Spring Framework 5 开始，Spring 的 JMS 软件包完全支持 JMS 2.0，并要求在运行时提供 JMS 2.0 API。我们建议使用 JMS 2.0 兼容的提供程序。
>
> 如果您碰巧在系统中使用了较旧的消息代理，则可以尝试升级到适用于现有代理的 JMS 2.0 兼容驱动程序。或者，您也可以尝试针对基于 JMS 1.1 的驱动程序运行，只需将 JMS 2.0 API jar 放在类路径上，而仅对驱动程序使用兼容 JMS 1.1的API。Spring 的 JMS 支持默认情况下遵守 JMS 1.1 约定，因此通过相应的配置它确实支持这种情况。但是，请仅在过渡方案中考虑这一点。

### 3.1 使用 Spring JMS

本章节描述如何使用 Spring 的 JMS 组件。

#### 3.1.1 使用 `JmsTemplate`

 `JmsTemplate` 类是 JMS 核心包的中央类。它简化了 JMS 的使用，由于当发送消息或者同步接收消息时它处理了资源的创建和释放。

使用 `JmsTemplate` 的代码只需要实现回调接口以给它们一个明确定义的高层的契约。当由 `JmsTemplate` 中的调用代码提供一个 `Session` 时，`MessageCreator` 回调接口创建一条消息。为了允许更加复杂的 JMS API 的使用，`SessionCallback` 提供 JMS 会话，同时 `ProducerCallback` 暴露一个 `Session` 和 `MessageProducer` 对。

JMS API 暴露了两种类型的发送方法，一种采用交付模式，优先级和生存时间作为服务质量（QOS）参数，另一种不采用 QOS 参数并使用默认值。由于 `JmsTemplate` 具有许多发送方法，因此设置已作为 bean 属性公开的 QOS 参数，以避免重复发送方法。类似地，通过使用 `setReceiveTimeout` 属性设置同步接收调用的超时值。

一些 JMS 提供程序允许通过 `ConnectionFactory` 的配置来管理默认的 QOS 值。这样做的结果是，调用 `MessageProducer` 实例的 `send` 方法（`send(Destination destination, Message message)`）使用的 QOS 缺省值与 JMS 规范中指定的缺省值不同。因此，为了提供对 QOS 值的一致管理，必须通过将布尔属性 `isExplicitQosEnabled` 设置为 `true`，专门启用 `JmsTemplate` 以使用其自己的 QOS 值。

为了方便，`JmsTemplate` 同时暴露了一种基本的请求－回应操作，允许发送消息并在作为操作一部分而创建的一个临时队列上等待回应。

> 一旦配置完成，`JmsTemplate` 类的实例就是线程安全的。这一点很重要，因为这意味着你可以配置 `JmsTemplate` 的单个实例然后将其共享引用安全地注入到多个协作者中。需要明确的是，`JmsTemplate` 是有状态的，因为它维护了 `ConnectionFactory` 的引用，不过这里的状态并不是会话状态。

Spring 框架 4.1中，`JmsMessagingTemplate` 建立在 `JmsTemplate` 之上，提供了一种与消息抽象的集成－也就是 `org.springframework.messaging.Message`。这就允许你可以以通用的方式创建将要发送的消息。

#### 3.1.2 连接

`JmsTemplate` 需要 `ConnectionFactory` 引用。`ConnectionFactory` 是 JMS 规范的一部分，作为使用 JMS 的入口点。它被客户端应用用来作为使用 JMS 提供者创建连接的工厂，同时包装各种配置参数，其中许多参数都是特定于提供者的，比如 SSL 配置选项。

在 EJB 中使用 JMS 时，提供者提供 JMS 接口的实现，因而它们可以参与声明式事务管理以及执行连接和会话的池化。为了使用这种实现，Java EE 容器通常需要你在 EJB 或者 servlet 部署描述符文件中声明一个 JMS 连接工厂作为 `resource-ref` 。为了确保将这些功能能够与 EJB 中的 `JmsTemplate` 一起使用，客户端应用程序应确保其引用 `ConnectionFactory` 的托管实现。

##### 缓存消息资源

标准 API 调用创建许多中间对象。为了发送一条消息，下面的 API 调用过程会执行：

```
ConnectionFactory->Connection->Session->MessageProducer->send
```

在 `ConnectionFactory` 和 `Send` 操作之间，三个中间对象被创建然后销毁。为了优化资源使用并提升性能，Spring 提供了 `ConnectionFactory` 的两种实现。

##### 使用 `SingleConnectionFactory`

Spring 提供了一个 `ConnectionFactory` 接口的实现， `SingleConnectionFactory` 。该接口在所有的  `createConnection()` 调用上返回相同的 `Connection`，而忽略对 `close()` 的调用。这对于测试环境和独立环境非常有用，因此同一连接可用于可能跨越任意数量事务的多个 `JmsTemplate` 调用。`SingleConnectionFactory` 引用了通常来自 JNDI 的标准 `ConnectionFactory`。

##### 使用 `CachingConnectionFactory`

`CachingConnectionFactory` 扩展了 `SingleConnectionFactory` 的功能，并添加了 `Session`，`MessageProducer` 和 `MessageConsumer` 实例的缓存。初始缓存大小设置为 `1`。您可以使用 `sessionCacheSize` 属性来增加缓存会话的数量。请注意，实际缓存的会话数大于该数量，因为会话是基于其确认（应答）模式缓存的，因此，当将 `sessionCacheSize` 设置为 `1` 时，最多可以有四个缓存的会话实例（每个确认模式一个）。`MessageProducer` 和 `MessageConsumer` 实例被缓存在它们自己的会话中，并且在缓存时还考虑了生产者和使用者的唯一属性。`MessageProducers` 根据其目的地进行缓存。基于由目标，选择器，noLocal 传递标志和持久订阅名称（如果创建持久使用者）组成的键来缓存 `MessageConsumers`。

#### 3.1.3 目的地管理

作为 `ConnectionFactory` 实例的目的地，是可以在 JNDI 中存储和检索的 JMS 管理的对象。在配置 Spring 应用程序上下文时，可以使用 JNDI `JndiObjectFactoryBean` 工厂类或 `<jee:jndi-lookup>` 对对象对 JMS 目的地的引用执行依赖项注入。但是，如果应用程序中有大量目的地，或者 JMS 提供程序具有独特的高级目的地管理功能，则此策略通常很麻烦。这种高级目的地管理的示例包括动态目的地的创建或对目的地的分层名称空间的支持。 `JmsTemplate` 将目的地名称的解析委托给实现 `DestinationResolver` 接口的 JMS 目的地对象。 `DynamicDestinationResolver` 是 `JmsTemplate` 所使用的默认实现，并且可以解析动态目的地。还提供了 `JndiDestinationResolver` 以充当 JNDI 中包含的目的地的服务定位器，并且可以选择降级到 `DynamicDestinationResolver` 中包含的行为。

通常，仅在运行时才知道 JMS 应用程序中使用的目的地，因此，在部署应用程序时无法通过管理方式创建。这通常是因为在交互的系统组件之间存在共享的应用程序逻辑，这些组件根据已知的命名约定在运行时创建目的地。即使创建动态目的地不属于 JMS 规范的一部分，但大多数供应商都提供了此功能。动态目的地是使用用户定义的名称创建的，该名称将它们与临时目的地区分开来，并且通常未在 JNDI 中注册。各个提供者之间用于创建动态目的地的 API 有所不同，因为与目的地关联的属性是特定于供应商的。但是，供应商有时会做出一个简单的实现选择，就是忽略 JMS 规范中的警告，并使用方法 `TopicSession` `createTopic(String topicName)` 或 `QueueSession` `createQueue(String queueName)` 方法来实现。使用默认目的地属性创建一个新目的地。然后，取决于供应商的实现，`DynamicDestinationResolver `也可以创建一个物理目的地，而不仅仅是解析一个目的地。

布尔属性 `pubSubDomain` 用于在知道正在使用哪个 `JMS` 域的情况下配置 `JmsTemplate`。默认情况下，此属性的值为 `false`，表示将使用点对点域，`Queues`。这个属性（由 `JmsTemplate` 使用）通过 `DestinationResolver` 接口的实现确定动态目的地解析的行为。

您还可以通过属性 `defaultDestination` 将 `JmsTemplate` 配置为默认目的地。默认目的地是带有不引用特定目的地的发送和接收操作。

#### 3.1.4. Message Listener Containers

在 EJB 世界中，JMS 消息最常见的用途之一就是驱动消息驱动的 bean（MDB）。Spring 提供了一种解决方案，以不将用户绑定到 EJB 容器的方式创建消息驱动的 POJO（MDP）。（有关详细信息，请参见 [异步接收：消息驱动的POJO](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async)）自 Spring Framework 4.1 以来，可以使用 `@JmsListener` 注解修释端点方法。请参阅 [注解驱动的侦听器端点](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-annotated) 以了解更多详细信息。

消息侦听器容器用于从 JMS 消息队列接收消息，并驱动注入到其中的 `MessageListener`。侦听器容器负责消息接收的所有线程，并分派到侦听器中进行处理。消息侦听器容器是 MDP 与消息传递提供程序之间的中介，并负责注册接收消息，参与事务，资源获取和释放，异常转换等。这使您可以编写与接收消息（并可能响应消息）相关的（可能很复杂的）业务逻辑，并将样板 JMS 基础设施问题委托给框架。

Spring 中包含两种标准的 JMS 消息监听器容器，各自有不同的特性集。

- [`SimpleMessageListenerContainer`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-mdp-simple)
- [`DefaultMessageListenerContainer`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-mdp-default)

##### 使用 `SimpleMessageListenerContainer`

此消息侦听器容器是两种标准样式中的简单容器。它在启动时创建固定数量的 JMS 会话和使用者，使用标准 JMS `MessageConsumer.setMessageListener()` 方法注册侦听器，并将其留给 JMS 提供者来执行侦听器回调。此变体不允许动态适应运行时需求或参与外部管理的事务。在兼容性方面，它非常符合独立 JMS 规范的精神，但通常与 Java EE 的 JMS 限制不兼容。

> 尽管 `SimpleMessageListenerContainer` 不允许参与外部管理的事务，但它确实支持本机 JMS 事务。要启用此功能，可以将 `sessionTransacted` 标志切换为 `true`，或者在 XML 名称空间中将 `acknowledge` 属性设置为 `transacted`。然后，从您的侦听器抛出的异常会导致回滚，并重新传递消息。另外，请考虑使用 `CLIENT_ACKNOWLEDGE` 模式，该模式也可以在发生异常的情况下重新交付，但不使用事务处理的 `Session` 实例，因此在该模式中不包含事务协议中任何其他 `Session` 操作（例如发送响应消息）。

> 默认的 `AUTO_ACKNOWLEDGE` 模式无法提供适当的可靠性保证。当侦听器执行失败时消息会丢失（因为提供者会在侦听器调用后自动确认每条消息，没有异常会传播到提供者），或者在侦听器容器关闭时（可以通过设置 `acceptMessagesWhileStopping` 标志进行配置） 。确保出于可靠性需求（例如，为了可靠的队列处理和持久的主题订阅）使用事务处理的会话。

##### 使用 `DefaultMessageListenerContainer`

大多数情况下使用此消息侦听器容器。 与 `SimpleMessageListenerContainer` 相反，此容器变体允许动态适应运行时需求，并能够参与外部管理的事务。当使用 `JtaTransactionManager` 进行配置时，每个接收到的消息都会在 XA 事务中注册。结果，处理可以利用 XA 事务语义。该侦听器容器在对 JMS 提供程序的低要求，高级功能（例如参与外部管理的事务）以及与 Java EE 环境的兼容性之间取得了良好的平衡。

您可以自定义容器的缓存级别。请注意，当未启用缓存时，将为每个消息接收创建一个新的连接和一个新的会话。将其与具有高负载的非持久订阅结合使用可能会导致消息丢失。在这种情况下，请确保使用适当的缓存级别。

当节点关闭时，此容器还具有可恢复的功能。默认情况下，一个简单的 `BackOff` 实现每五秒钟重试一次。您可以为更细粒度的恢复选项指定一个自定义的 `BackOff` 实现。有关示例，请参见 `ExponentialBackOff` 文档了解更多细节。

> 就像它的兄弟（[`SimpleMessageListenerContainer`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-mdp-simple)）一样，`DefaultMessageListenerContainer ` 支持本机 JMS 事务，并允许自定义确认模式。如果对您的情况可行，则强烈建议在外部管理的事务上使用此方法，也就是说，如果 JVM 死亡，您可以偶尔接收重复的消息。业务逻辑中的自定义重复消息检测步骤可以涵盖这种情况，例如以业务实体存在检查或协议表检查的形式。任何这样的安排都比替代方案更为有效：用 XA 事务包装整个处理过程（通过使用 `JtaTransactionManager` 配置 `DefaultMessageListenerContainer`）来覆盖 JMS 消息的接收以及您的消息监听器业务逻辑的执行（包括数据库操作等）。

> 默认的 `AUTO_ACKNOWLEDGE` 模式无法提供适当的可靠性保证。当侦听器执行失败时消息会丢失（因为提供者会在侦听器调用后自动确认每条消息，没有异常会传播到提供者），或者在侦听器容器关闭时（可以通过设置 `acceptMessagesWhileStopping` 标志进行配置） 消息也会丢失。确保出于可靠性需求（例如，为了可靠的队列处理和持久的主题订阅）使用事务处理的会话。

#### 3.1.5 事务管理

Spring 提供了一个 `JmsTransactionManager` 来管理单个 JMS `ConnectionFactory` 的事务。这样，JMS 应用程序就可以利用 Spring 的托管事务功能，如 [Transaction Management section of the Data Access chapter](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction) 部分所述。`JmsTransactionManager` 执行本地资源事务，将来自指定 `ConnectionFactory` 的 JMS Connection/Session 对绑定到线程。`JmsTemplate` 会自动检测此类事务资源并对其进行相应的操作。

在 Java EE 环境中，`ConnectionFactory` 汇集了 `Connection` 和 `Session` 实例，因此可以有效地在事务之间重用这些资源。在独立环境中，使用 Spring 的 `SingleConnectionFactory` 会导致共享的 JMS `Connection`，并且每个事务都有自己独立的 `Session`。另外，考虑使用提供程序专用的池适配器，例如 ActiveMQ 的 `PooledConnectionFactory` 类。

您还可以将 `JmsTemplate` 和 `JtaTransactionManager` 和具有 XA 功能的 JMS `ConnectionFactory` 一起使用来执行分布式事务。请注意，这需要使用 JTA 事务管理器以及正确的 XA 配置的 `ConnectionFactory`。（请查看您的 Java EE 服务器或 JMS 提供者的文档。）

使用 JMS API 从 `Connection` 创建 `Session` 时，在托管和非托管事务环境中重用代码可能会造成混淆。这是因为 JMS API 只有一种工厂方法可以创建 `Session`，并且它需要事务和确认模式的值。在托管环境中，设置这些值是环境的事务基础设施的责任，因此，供应商对 JMS `Connection` 的包装将忽略这些值。在非托管环境中使用 `JmsTemplate` 时，可以通过使用 `sessionTransacted` 和 `sessionAcknowledgeMode` 属性来指定这些值。当将 `PlatformTransactionManager` 与 `JmsTemplate` 一起使用时，模板总是被赋予事务性 JMS `Session`。

### 3.2 发送消息

`JmsTemplate` 包含许多方便方法来发送消息。`send` 方法通过 `javax.jms.Destination` 对象指定目的地。其他方法在 JNDI 查找中使用 `String` 来指定目的地。不是用目的地参数的 `send` 方法使用默认目的地。

下面的例子使用 `MessageCreator` 回调来从给定的 `Session` 对象创建一条文本消息：

```java
import javax.jms.ConnectionFactory;
import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.Queue;
import javax.jms.Session;

import org.springframework.jms.core.MessageCreator;
import org.springframework.jms.core.JmsTemplate;

public class JmsQueueSender {

    private JmsTemplate jmsTemplate;
    private Queue queue;

    public void setConnectionFactory(ConnectionFactory cf) {
        this.jmsTemplate = new JmsTemplate(cf);
    }

    public void setQueue(Queue queue) {
        this.queue = queue;
    }

    public void simpleSend() {
        this.jmsTemplate.send(this.queue, new MessageCreator() {
            public Message createMessage(Session session) throws JMSException {
                return session.createTextMessage("hello queue world");
            }
        });
    }
}
```

上面的例子中，`JmsTemplate` 通过传递一个引用给 `ConnectionFactory` 来构造。作为备用方案，一个无参构造器和 `connectionFactory` 可以被用来构造 JavaBean 风格（使用 `BeanFactory` 或者普通 Java 代码）的实例。另外，请考虑从 Spring 的 `JmsGatewaySupport` 便利性基类派生，该类为 JMS 配置提供了预先构建的 bean 属性。

`send(String destinationName, MessageCreator creator)` 方法允许你通过使用目的地的名称字符串发送消息。如果目的地名称被注册在 JNDI 中，你应该设置 `JndiDestinationResolver` 实例模板的 `destinationResolver` 属性。

如果你创建 `JmsTemplate` 并指定默认目的地，则 `send(MessageCreator c)` 向目的地发送消息。

#### 3.2.1 使用消息转换器

为了方便域模型对象的发送，`JmsTemplate` 具有各种发送方法，这些方法将 Java 对象作为消息数据内容的参数。`JmsTemplate` 中的重载方法 `convertAndSend()` 和 `receiveAndConvert()` 方法将转换过程委托给 `MessageConverter` 接口的一个实例。该接口定义了一个简单的协定，可以在 Java 对象和 JMS 消息之间进行转换。默认实现（ `SimpleMessageConverter` ）支持在 `String` 和 `TextMessage` ，`byte[]` 和 `BytesMesssage` 之间以及 `java.util.Map` 和 `MapMessage` 之间进行转换。通过使用转换器，您和您的应用程序代码可以专注于通过 JMS 发送或接收的业务对象，而不必担心如何将其表示为 JMS 消息。

沙箱当前包含一个 `MapMessageConverter` ，它使用反射在 JavaBean 和 `MapMessage` 之间进行转换。您可能会自己实现的其他流行实现，可以选择是使用现有 XML 编组程序包（例如 JAXB，Castor 或 XStream）创建代表该对象的 `TextMessage` 的转换器。

为了容纳消息属性，标头和正文的设置，而这些属性通常不能封装在转换器类中，`MessagePostProcessor` 接口可让您在消息转换后、但在发送之前访问消息。以下示例显示了在将 `java.util.Map` 转换为消息后如何修改消息头和属性：

```java
public void sendWithConversion() {
    Map map = new HashMap();
    map.put("Name", "Mark");
    map.put("Age", new Integer(47));
    jmsTemplate.convertAndSend("testQueue", map, new MessagePostProcessor() {
        public Message postProcessMessage(Message message) throws JMSException {
            message.setIntProperty("AccountID", 1234);
            message.setJMSCorrelationID("123-00001");
            return message;
        }
    });
}
```

这将产生以下形式的消息：

```javascript
MapMessage={
    Header={
        ... standard headers ...
        CorrelationID={123-00001}
    }
    Properties={
        AccountID={Integer:1234}
    }
    Fields={
        Name={String:Mark}
        Age={Integer:47}
    }
}
```

#### 3.2.2 使用 `SessionCallback` 和 `ProducerCallback`

尽管发送操作涵盖了许多常见的使用场景，但是您有时可能希望对 JMS `Session` 或 `MessageProducer` 执行多个操作。`SessionCallback` 和 `ProducerCallback` 分别公开了 JMS `Session` 和 `Session` / `MessageProducer` 对。`JmsTemplate` 上的 `execute()` 方法执行这些回调方法。

### 3.3 接收消息

本节介绍如何使用 Spring 中的 JMS 接收消息。

#### 3.3.1 同步接收

虽然 JMS 通常与异步处理相关联，但是您可以同步使用消息。重载的 `receive(..)` 方法提供了此功能。在同步接收期间，调用线程将阻塞，直到消息可用为止。这可能是危险的操作，因为调用线程可能会无限期地被阻塞。`receiveTimeout` 属性指定接收者在放弃等待消息之前应该等待多长时间。

#### 3.3.2 异步接收：消息驱动的 POJOs

> Spring 还通过使用 `@JmsListener` 注解来支持带注解的侦听器端点，并提供了开放的基础设施来以编程方式注册端点。到目前为止，这是设置异步接收器的最便捷方法。有关更多详细信息，请参见 [启用侦听器端点注解](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-annotated-support) 。

消息驱动 POJO（MDP）以类似于 EJB 世界中的消息驱动 Bean（MDB）的方式充当 JMS 消息的接收者。MDP 的一个限制（请参阅 [使用`MessageListenerAdapter`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async-message-listener-adapter) ）是它必须实现 `javax.jms.MessageListener `接口。请注意，如果您的 POJO 在多个线程上接收消息，则重要的是要确保您的实现是线程安全的。

下面的例子展示了一个简单的 MDP 实现：

```java
import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.MessageListener;
import javax.jms.TextMessage;

public class ExampleListener implements MessageListener {

    public void onMessage(Message message) {
        if (message instanceof TextMessage) {
            try {
                System.out.println(((TextMessage) message).getText());
            }
            catch (JMSException ex) {
                throw new RuntimeException(ex);
            }
        }
        else {
            throw new IllegalArgumentException("Message must be of type TextMessage");
        }
    }
}
```

一旦你实现了你的 `MessageListener` ，就是时候创建一个消息监听器容器了。

以下示例显示了如何定义和配置 Spring 附带的消息侦听器容器之一（在本例中为 `DefaultMessageListenerContainer` ）：

```xml
<!-- this is the Message Driven POJO (MDP) -->
<bean id="messageListener" class="jmsexample.ExampleListener"/>

<!-- and this is the message listener container -->
<bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destination" ref="destination"/>
    <property name="messageListener" ref="messageListener"/>
</bean>
```

请参阅各种消息侦听器容器的 Spring Javadoc（所有容器都实现 [MessageListenerContainer](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/MessageListenerContainer.html) ），以获取每个实现所支持功能的完整说明。

#### 3.3.3 使用 `SessionAwareMessageListener` 接口

`SessionAwareMessageListener` 接口是特定于 Spring 的接口，它提供与 JMS `MessageListener` 接口相似的协定，但也使消息处理方法可以访问从其接收 `Message` 的 JMS `Session`。以下清单显示了 `SessionAwareMessageListener` 接口的定义：

```java
package org.springframework.jms.listener;

public interface SessionAwareMessageListener {

    void onMessage(Message message, Session session) throws JMSException;
}
```

如果希望 MDP 能够响应任何接收到的消息（通过使用 `onMessage(Message, Session)` 中提供的 `Session`），则可以选择让 MDP 实现此接口（优先于标准 JMS `MessageListener` 接口）。Spring 附带的所有消息侦听器容器实现都支持实现 `MessageListener` 或 `SessionAwareMessageListener` 接口的 MDP。实现 `SessionAwareMessageListener` 的类带有警告，它们随后通过接口绑定到 Spring。是否使用它的选择完全由您作为应用程序开发人员或架构师来决定。

注意，`SessionAwareMessageListener` 接口的 `onMessage(..)` 方法抛出 `JMSException`。与标准的 JMS  `MessageListener` 接口相反，当使用 `SessionAwareMessageListener` 接口时，客户端代码负责处理任何抛出的异常。

#### 3.3.4. Using `MessageListenerAdapter`

`MessageListenerAdapter` 类是 Spring 异步消息支持中的最后一个组件。简而言之，它使您几乎可以将任何类公开为 MDP（尽管存在一些约束）。

考虑以下接口定义：

```java
public interface MessageDelegate {

    void handleMessage(String message);

    void handleMessage(Map message);

    void handleMessage(byte[] message);

    void handleMessage(Serializable message);
}
```

注意，尽管该接口既没有扩展 `MessageListener` 也没有扩展 `SessionAwareMessageListener` 接口，但是您仍然可以通过使用 `MessageListenerAdapter` 类将其用作 MDP。还请注意，如何根据各种消息处理方法可以接收和处理的各种 `Message` 类型的内容来强类型化。

现在考虑以下 `MessageDelegate` 接口的实现：

```java
public class DefaultMessageDelegate implements MessageDelegate {
    // implementation elided for clarity...
}
```

特别要注意的是，前面的 `MessageDelegate` 接口的实现（`DefaultMessageDelegate`类）完全没有 JMS 依赖性。这确实是一个 POJO，我们可以通过以下配置将其制作为 MDP：

```java
<!-- this is the Message Driven POJO (MDP) -->
<bean id="messageListener" class="org.springframework.jms.listener.adapter.MessageListenerAdapter">
    <constructor-arg>
        <bean class="jmsexample.DefaultMessageDelegate"/>
    </constructor-arg>
</bean>

<!-- and this is the message listener container... -->
<bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destination" ref="destination"/>
    <property name="messageListener" ref="messageListener"/>
</bean>
```

下一个示例展示另一个 MDP，它只能处理接收 JMS `TextMessage` 消息。请注意，实际上是如何处理消息的方法称为 `receive` （`MessageListenerAdapter` 中消息处理方法的名称默认为 `handleMessage`），但是它是可配置的（如本节后面所述）。还请注意，如何设置强类型的 `receive(..)` 方法以仅接收和响应 JMS `TextMessage` 消息。下面的清单显示了 `TextMessageDelegate` 接口的定义：

```java
public interface TextMessageDelegate {

    void receive(TextMessage message);
}
```

下面的例子展示了实现 `TextMessageDelegate` 接口的类：

```java
public class DefaultTextMessageDelegate implements TextMessageDelegate {
    // implementation elided for clarity...
}
```

相应的 `MessageListenerAdapter` 配置如下：

```xml
<bean id="messageListener" class="org.springframework.jms.listener.adapter.MessageListenerAdapter">
    <constructor-arg>
        <bean class="jmsexample.DefaultTextMessageDelegate"/>
    </constructor-arg>
    <property name="defaultListenerMethod" value="receive"/>
    <!-- we don't want automatic message context extraction -->
    <property name="messageConverter">
        <null/>
    </property>
</bean>
```

请注意，如果 `messageListener` 接收到的不是 `TextMessage` 类型的 JMS `Message`，则抛出 `IllegalStateException` 并随后将其吞下。`MessageListenerAdapter` 类的另一个功能是，如果处理程序方法返回的是非空值，则可以自动发送响应消息。考虑以下接口和类：

```java
public interface ResponsiveTextMessageDelegate {

    // notice the return type...
    String receive(TextMessage message);
}
public class DefaultResponsiveTextMessageDelegate implements ResponsiveTextMessageDelegate {
    // implementation elided for clarity...
}
```

如果您将 `DefaultResponsiveTextMessageDelegate` 与 `MessageListenerAdapter` 结合使用，则在默认配置下，执行 `receive(..)` 方法返回的所有非空值都将转换为`TextMessage。 `。然后将生成的 `TextMessage` 发送到在原始 `Message` 的 JMS `Reply-To` 属性或 `MessageListenerAdapter` 上设置的默认 `Destination` 中定义的 `Destination`（如果已配置）。如果没有找到 `Destination`，则抛出 `InvalidDestinationException`（请注意，该异常不会被吞没，并且会在调用堆栈中传播）。

#### 3.3.5 在事务中处理消息

在事务中调用消息侦听器仅需要重新配置侦听器容器。

您可以通过侦听器容器定义上的 `sessionTransacted` 标志来激活本地资源事务。然后，每个消息侦听器调用都在活动的 JMS 事务中运行，并且在侦听器执行失败的情况下回退消息接收。（通过 `SessionAwareMessageListener`）发送响应消息是同一本地事务的一部分，但是任何其他资源操作（例如数据库访问）都是独立运行的。这通常需要在侦听器实现中进行重复消息检测，以解决数据库处理已提交但消息处理未能提交的情况。

考虑以下 bean 定义：

```xml
<bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destination" ref="destination"/>
    <property name="messageListener" ref="messageListener"/>
    <property name="sessionTransacted" value="true"/>
</bean>
```

要参与外部管理的事务，您需要配置一个事务管理器并使用支持外部管理的事务的侦听器容器（通常为 `DefaultMessageListenerContainer`）。

要为 XA 事务参与配置消息侦听器容器，您需要配置一个 `JtaTransactionManager`（默认情况下，它委派给 Java EE 服务器的事务子系统）。请注意，底层的 JMS `ConnectionFactory` 必须具有 XA 功能，并已向您的 JTA 事务协调器正确注册。（检查 Java EE 服务器的 JNDI 资源配置。）这使消息接收和（例如）数据库访问成为同一事务的一部分（具有统一的提交语义，但以 XA 事务日志开销为代价）。

以下 bean 定义创建一个事务管理器：

```xml
<bean id="transactionManager" class="org.springframework.transaction.jta.JtaTransactionManager"/>
```

然后，我们需要将其添加到我们之前的容器配置中。容器负责其余的工作。以下示例显示了如何执行此操作：

```xml
<bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destination" ref="destination"/>
    <property name="messageListener" ref="messageListener"/>
    <property name="transactionManager" ref="transactionManager"/> 
</bean>
```

### 3.4. Support for JCA Message Endpoints

从 2.5 版本开始，Spring 还提供了对基于 JCA 的 `MessageListener` 容器的支持。 `JmsMessageEndpointManager` 会尝试从提供者的 `ResourceAdapter` 类名称中自动确定 `ActivationSpec` 类名称。因此，通常可以提供 Spring 的通用 `JmsActivationSpecConfig`，如以下示例所示：

```xml
<bean class="org.springframework.jms.listener.endpoint.JmsMessageEndpointManager">
    <property name="resourceAdapter" ref="resourceAdapter"/>
    <property name="activationSpecConfig">
        <bean class="org.springframework.jms.listener.endpoint.JmsActivationSpecConfig">
            <property name="destinationName" value="myQueue"/>
        </bean>
    </property>
    <property name="messageListener" ref="myMessageListener"/>
</bean>
```

或者，您可以使用给定的 `ActivationSpec` 对象设置 `JmsMessageEndpointManager`。`ActivationSpec` 对象也可以来自 JNDI 查找（使用 `<jee:jndi-lookup>`）。以下示例显示了如何执行此操作：

```xml
<bean class="org.springframework.jms.listener.endpoint.JmsMessageEndpointManager">
    <property name="resourceAdapter" ref="resourceAdapter"/>
    <property name="activationSpec">
        <bean class="org.apache.activemq.ra.ActiveMQActivationSpec">
            <property name="destination" value="myQueue"/>
            <property name="destinationType" value="javax.jms.Queue"/>
        </bean>
    </property>
    <property name="messageListener" ref="myMessageListener"/>
</bean>
```

使用 Spring 的 `ResourceAdapterFactoryBean`，你可以在本地配置目标 `ResourceAdapter` ，如下面例子所示：

```xml
<bean id="resourceAdapter" class="org.springframework.jca.support.ResourceAdapterFactoryBean">
    <property name="resourceAdapter">
        <bean class="org.apache.activemq.ra.ActiveMQResourceAdapter">
            <property name="serverUrl" value="tcp://localhost:61616"/>
        </bean>
    </property>
    <property name="workManager">
        <bean class="org.springframework.jca.work.SimpleTaskWorkManager"/>
    </property>
</bean>
```

指定的 `WorkManager` 还可以指向特定于环境的线程池-通常通过 `SimpleTaskWorkManager` 实例的 `asyncTaskExecutor` 属性来指向。如果您碰巧使用多个适配器，请考虑为所有 `ResourceAdapter` 实例定义一个共享线程池。

在某些环境（例如 WebLogic 9 或更高版本）中，您可以改为从 JNDI 获取整个 `ResourceAdapter` 对象（使用 `<jee:jndi-lookup>`）。然后，基于 Spring 的消息侦听器就可以与服务器托管的 `ResourceAdapter` 进行交互，后者也使用服务器的内置 `WorkManager`。

参考 [`JmsMessageEndpointManager`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/endpoint/JmsMessageEndpointManager.html)， [`JmsActivationSpecConfig`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/endpoint/JmsActivationSpecConfig.html)，以及 [`ResourceAdapterFactoryBean`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jca/support/ResourceAdapterFactoryBean.html) 文档获取更多细节。

Spring 还提供了与 JMS 无关的通用 JCA 消息端点管理器： `org.springframework.jca.endpoint.GenericMessageEndpointManager`。该组件允许使用任何消息侦听器类型（例如 CCI `MessageListener`）和任何提供程序特定的 `ActivationSpec` 对象。请参阅 JCA 提供者的文档以了解连接器的实际功能，并查看 [`GenericMessageEndpointManager`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jca/endpoint/GenericMessageEndpointManager.html) javadoc，以了解特定于 Spring 的配置详细信息。

> 基于 JCA 的消息端点管理与 EJB 2.1 消息驱动 Bean 非常相似。它使用相同的基础资源提供者契约。与 EJB 2.1 MDB 一样，您也可以在 Spring 上下文中使用 JCA 提供程序支持的任何消息侦听器接口。但是，由于 JMS 是与 JCA 端点管理协定一起使用的最常见的端点 API，因此 Spring 为 JMS 提供了显式的“便利”支持。

### 3.5 注解驱动的监听器端点

同步接收消息的最简单方法就是使用注解修饰的监听器端点基础设施。简而言之，它允许你暴露容器托管的 bean 的方法作为 JMS 监听器端点。下面的例子展示了如何使用：

```java
@Component
public class MyService {

    @JmsListener(destination = "myDestination")
    public void processOrder(String data) { ... }
}
```

上面例子的想法是，无论何时，只要 `javax.jms.Destinations.myDestination` 上有一条可用消息，则对应的 `processOrder` 方法就会被调用（这种情况下，使用 JMS 消息的内容，类似于 [`MessageListenerAdapter`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async-message-listener-adapter) 所提供的）。

通过使用 `JmsListenerContainerFactory` ，注解修饰的端点基础设施在幕后为每个注解修饰的方法创建一个消息监听器容器。这样的容器并不注册在应用上下文中，但是可以通过使用 `JmsListenerEndpointRegistry` bean 出于管理目的很容易地定位。

> `@JmsListener` 在 Java 8 中是一个可重复注解，因此你可以通过将额外的`@JmsListener` 注解添加到同一个方法上来声明该方法关联到多个 JMS 目的地。

#### 3.5.1 启用监听器端点注解

为了启用 `@JmsListener` 注解支持，你可以将 `@EnableJms` 添加到你的其中一个 `@Configuration` 类中，如下面例子所示：

```java
@Configuration
@EnableJms
public class AppConfig {

    @Bean
    public DefaultJmsListenerContainerFactory jmsListenerContainerFactory() {
        DefaultJmsListenerContainerFactory factory = new DefaultJmsListenerContainerFactory();
        factory.setConnectionFactory(connectionFactory());
        factory.setDestinationResolver(destinationResolver());
        factory.setSessionTransacted(true);
        factory.setConcurrency("3-10");
        return factory;
    }
}
```

默认情况下，基础设施会寻找名为 `jmsListenerContainerFactory` 的 bean 作为用来创建消息监听器容器的工厂的源。这种情况下（同时忽略了 JMS 基础设施配置），你可以使用 3 个核心线程、最多 10 个线程的线程池调用 `processOrder` 方法。

您可以自定义用于每个注解的监听器容器工厂，也可以通过实现 `JmsListenerConfigurer` 接口来显式配置默认值。仅当至少一个端点在没有特定容器工厂的情况下注册时，才需要使用默认值。请参阅实现 [`JmsListenerConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/annotation/JmsListenerConfigurer.html ) 的类的 Javadoc 以获取详细信息和示例。

如果你更喜欢 [XML configuration](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-namespace)，你可以使用 `<jms:annotation-driven>` 元素，如下面例子所示：

```xml
<jms:annotation-driven/>

<bean id="jmsListenerContainerFactory"
        class="org.springframework.jms.config.DefaultJmsListenerContainerFactory">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destinationResolver" ref="destinationResolver"/>
    <property name="sessionTransacted" value="true"/>
    <property name="concurrency" value="3-10"/>
</bean>
```

#### 3.5.2 编程式端点注册

`JmsListenerEndpoint` 提供了 JMS 端点的模型，并负责配置该模型的容器。基础设施除了通过 `JmsListener`  注解探测端点，还允许你编程式配置端点。下面的例子展示了如何做：

```java
@Configuration
@EnableJms
public class AppConfig implements JmsListenerConfigurer {

    @Override
    public void configureJmsListeners(JmsListenerEndpointRegistrar registrar) {
        SimpleJmsListenerEndpoint endpoint = new SimpleJmsListenerEndpoint();
        endpoint.setId("myJmsEndpoint");
        endpoint.setDestination("anotherQueue");
        endpoint.setMessageListener(message -> {
            // processing
        });
        registrar.registerEndpoint(endpoint);
    }
}
```

上面的例子中，我们使用 `SimpleJmsListenerEndpoint` ，它提供实际的 `MessageListener` 用于调用。不过，你也可以创建你自己的端点变体来描述自定义的调用机制。

注意，您可以完全不使用 `@JmsListener` ，而可以仅通过 `JmsListenerConfigurer` 以编程方式注册端点。

#### 3.5.3 注解的端点方法签名

目前为止，我们已经将简单的 `String` 注入你的端点，不过实际上它也可以是非常复杂的方法签名。下面的例子中，我们注入携带自定义首部字段的 `Order` ：

```java
@Component
public class MyService {

    @JmsListener(destination = "myDestination")
    public void processOrder(Order order, @Header("order_type") String orderType) {
        ...
    }
}
```

可以注入 JMS 监听器端点的主要元素如下：

- 原始的 `javax.jms.Message` 或者任何它的子类（前提是它与进入的消息类型匹配）。
- `javax.jms.Session` 用于对本地 JMS API 的可选访问（比如，为了发送自定义响应）。
- `org.springframework.messaging.Message` 表达进入的 JMS 消息。注意该消息同时包含自定义和标准首部字段（如由 `JmsHeaders` 定义的）。
- `@Header`-注解的方法参数以提取特定首部字段值，包括标准 JMS 首部字段。
- `@Headers`-注解的参数，必须还可以被分配给 `java.util.Map` 以访问所有首部字段。
- 不是支持的类型之一（`Message` 或 `Session`）的非注解元素被视为有效负载。您可以通过在 `@Payload` 中注解参数来使其明确。您还可以通过添加额外的 `@Valid` 来启用验证。

注入 Spring 的 `Message` 抽象的能力特别有用，它可以受益于存储在特定于传输的消息中的所有信息，而无需依赖于特定于传输的 API。以下示例显示了如何执行此操作：

```java
@JmsListener(destination = "myDestination")
public void processOrder(Message<Order> order) { ... }
```

方法参数的处理由 `DefaultMessageHandlerMethodFactory` 提供，您可以进一步对其进行自定义以支持其他方法参数。您也可以自定义转换和验证支持。

例如，如果我们想在处理 `Order` 之前确保其有效，则可以使用 `@Valid` 注解有效负载并配置必要的验证器，如以下示例所示：

```java
@Configuration
@EnableJms
public class AppConfig implements JmsListenerConfigurer {

    @Override
    public void configureJmsListeners(JmsListenerEndpointRegistrar registrar) {
        registrar.setMessageHandlerMethodFactory(myJmsHandlerMethodFactory());
    }

    @Bean
    public DefaultMessageHandlerMethodFactory myHandlerMethodFactory() {
        DefaultMessageHandlerMethodFactory factory = new DefaultMessageHandlerMethodFactory();
        factory.setValidator(myValidator());
        return factory;
    }
}
```

#### 3.5.4 响应管理

[`MessageListenerAdapter`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async-message-listener-adapter)  中的支持已使您的方法具有非 `void` 返回类型。在这种情况下，调用的结果将封装在一个 `javax.jms.Message` 中，该 XML 既可以向在原始消息的 `JMSReplyTo` 标头中指定的目标发送，也可以向在侦听器上配置的默认目标发送。现在，您可以使用消息传递抽象的 `@SendTo` 注解来设置默认目标。

假设我们的 `processOrder` 方法现在应该返回一个 `OrderStatus`，我们可以将其编写为自动发送响应，如以下示例所示：

```java
@JmsListener(destination = "myDestination")
@SendTo("status")
public OrderStatus processOrder(Order order) {
    // order processing
    return status;
}
```

> 如果你有几个 `@JmsListener` 注解的方法，你也可以将 `@SendTo` 注解放在类级别以在这些方法之间共享默认回应目标。

如果需要以与传输无关的方式设置其他标头，则可以使用类似于以下内容的方法来返回 `Message`：

```java
@JmsListener(destination = "myDestination")
@SendTo("status")
public Message<OrderStatus> processOrder(Order order) {
    // order processing
    return MessageBuilder
            .withPayload(status)
            .setHeader("code", 1234)
            .build();
}
```

如果需要在运行时计算响应目标，则可以将响应封装在 `JmsResponse` 实例中，该实例还提供要在运行时使用的目标。我们可以如下重写前一个示例：

```java
@JmsListener(destination = "myDestination")
public JmsResponse<Message<OrderStatus>> processOrder(Order order) {
    // order processing
    Message<OrderStatus> response = MessageBuilder
            .withPayload(status)
            .setHeader("code", 1234)
            .build();
    return JmsResponse.forQueue(response, "status");
}
```

最后，如果您需要为响应指定一些 QoS 值，例如优先级或生存时间，则可以相应地配置 `JmsListenerContainerFactory`，如以下示例所示：

```java
@Configuration
@EnableJms
public class AppConfig {

    @Bean
    public DefaultJmsListenerContainerFactory jmsListenerContainerFactory() {
        DefaultJmsListenerContainerFactory factory = new DefaultJmsListenerContainerFactory();
        factory.setConnectionFactory(connectionFactory());
        QosSettings replyQosSettings = new QosSettings();
        replyQosSettings.setPriority(2);
        replyQosSettings.setTimeToLive(10000);
        factory.setReplyQosSettings(replyQosSettings);
        return factory;
    }
}
```

### 3.6 JMS 命名空间支持

Spring 提供了 XML 命名空间支持以简化 JMS 配置。为了使用 JMS 命名空间元素，你v 要引用 JMS 规范文件。如下面例子所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:jms="http://www.springframework.org/schema/jms" 
        xsi:schemaLocation="
            http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/jms https://www.springframework.org/schema/jms/spring-jms.xsd">

    <!-- bean definitions here -->

</beans>
```

该命名空间由 3 中顶级元素组成：`<annotation-driven/>`, `<listener-container/>` 和 `<jca－listener-container/>`。`<annotation-driven/>` 启用注解驱动的监听器端点。`<listener-container/>` 和 `<jca-listener-container/>` 定义共享的监听器容器配置，同时可以包含 `<listener/>` 子元素。下面的例子展示了两个监听器的基本配置：

```xml
<jms:listener-container>

    <jms:listener destination="queue.orders" ref="orderService" method="placeOrder"/>

    <jms:listener destination="queue.confirmations" ref="confirmationLogger" method="log"/>

</jms:listener-container>
```

上面的例子等价于创建两个不同的监听器容器 bean 定义以及两个不同的 `MessageListenerAdapter` bean 定义，如  [Using `MessageListenerAdapter`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async-message-listener-adapter) 中所述。除了上面例子中展示的属性，`listener` 元素还可以包含若干可选属性。下表描述了所有可用属性：

| 属性                     | 描述                                                         |
| :----------------------- | :----------------------------------------------------------- |
| `id`                     | 托管监听器容器的 bean 名称。如果未指定，则自动生成 bean 名称。 |
| `destination` (required) | 监听器的目标名称，通过 `DestinationResolver` 策略进行解析。  |
| `ref` (required)         | 处理器对象 bean 名称。                                       |
| `method`                 | 将要调用的处理器方法名称。如果 `ref` 属性指向 `MessageListener` 或者 Spring `SessionAwareMessageListener` ，你可以忽略此属性。 |
| `response-destination`   | 向其发送响应消息的默认响应目标的名称。在请求消息中不包含 `JMSReplyTo` 字段的情况下适用。此目的地的类型由监听容器的 `response-destination-type` 属性确定。请注意，这仅适用于具有返回值的侦听器方法，为此，每个结果对象都将转换为响应消息。 |
| `subscription`           | 持久订阅的名称（如果有）。                                   |
| `selector`               | 此侦听器的可选消息选择器。                                   |
| `concurrency`            | 要启动此侦听器的并发会话或使用者的数量。该值可以是表示最大数的简单数字（例如，`5`），也可以是表示下限和上限的范围（例如，`3-5`）。请注意，指定的最小值仅是一个提示，在运行时可能会被忽略。默认值为容器提供的值。 |

`<listener-container/>` 元素也接受若干可选属性。这就允许自定义各种策略（比如，`taskExecutor` 和 `destinationResolver`）以及基本的 JMS 设定和资源引用。通过使用这些属性，你可以定义高度定制化的监听器容器，同时还能够从命名空间受益。

您可以通过指定要通过 `factory-id` 属性公开的 bean 的 `id` 来自动将此类设置公开为 `JmsListenerContainerFactory`，如以下示例所示：

```xml
<jms:listener-container connection-factory="myConnectionFactory"
        task-executor="myTaskExecutor"
        destination-resolver="myDestinationResolver"
        transaction-manager="myTransactionManager"
        concurrency="10">

    <jms:listener destination="queue.orders" ref="orderService" method="placeOrder"/>

    <jms:listener destination="queue.confirmations" ref="confirmationLogger" method="log"/>

</jms:listener-container>
```

下表描述了所有可用的属性。参考 [`AbstractMessageListenerContainer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/AbstractMessageListenerContainer.html) 类以及它的子类的文档，获取更多有关属性的细节。文档中还提供了有关事务选择以及消息重发场景的讨论。

| 属性                        | 描述                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| `container-type`            | 监听器容器的类型。可用的选择有 `default`, `simple`, `default102`, 或者 `simple102` (默认值是 `default`)。 |
| `container-class`           | 由全限定类名指定的自定义监听器容器实现类。默认是 Spring 的标准 `DefaultMessageListenerContainer` 或者 `SimpleMessageListenerContainer`， 根据 `container-type` 属性确定。 |
| `factory-id`                | 指定 `id` 暴露由作为 `JmsListenerContainerFactory` 的元素定义的设定以便它们可以被其它端点复用。 |
| `connection-factory`        | 指向 JMS `ConnectionFactory` bean 的引用（默认 bean 名称是 `connectionFactory`）。 |
| `task-executor`             | 对 JMS 侦听器调用程序的 Spring `TaskExecutor` 的引用。       |
| `destination-resolver`      | 对用于解析 JMS `Destination` 实例的 `DestinationResolver` 策略的引用。 |
| `message-converter`         | 对将 JMS 消息转换为侦听器方法参数的 `MessageConverter` 策略的引用。默认值为 `SimpleMessageConverter` 。 |
| `error-handler`             | 对用于处理在 `MessageListener` 执行期间可能发生的任何未捕获异常的 `ErrorHandler` 策略的引用。 |
| `destination-type`          | 此侦听器的 JMS 目标类型：`queue`， `topic`， `durableTopic`， `sharedTopic`，或者 `sharedDurableTopic`。这可能会启用容器的 `pubSubDomain`，`subscriptionDurable` 和 `subsubscribeShared` 属性。默认值为 `queue`（禁用这三个属性）。 |
| `response-destination-type` | 响应的 JMS 目标类型： `queue` 或者 `topic`。默认是 `destination-type` 属性的值。 |
| `client-id`                 | 此监听器容器的 JMS 客户端 ID。使用持久化订阅时你必须指定它。 |
| `cache`                     | JMS 资源的缓存级别：`none`， `connection`， `session`， `consumer`， 或者 `auto`。默认情况下（`auto`），缓存级别实际上是 `consumer`，除非已指定外部事务管理器。在这种情况下，有效的默认值为 `none`（假设 Java EE 风格的事务管理，`ConnectionFactory` 是一个 XA-感知池）。 |
| `acknowledge`               | 本地 JMS 确认模式：`auto`， `client`， `dups-ok`， 或者 `transacted`。值 `transacted` 激活了本地交易的 `Session` 。或者，您可以指定 `transaction-manager` 属性，稍后在表中进行描述。默认为 `auto`。 |
| `transaction-manager`       | 对外部 `PlatformTransactionManager`（通常是基于 XA 的事务协调器，例如 Spring 的 `JtaTransactionManager`）的引用。如果未指定，则使用本机确认（请参阅 `acknowledge` 属性）。 |
| `concurrency`               | 每个侦听器启动的并发会话或使用者的数量。它可以是表示最大值的简单数字（例如，`5`），也可以是表示上下限的范围（例如，`3-5`）。请注意，指定的最小值只是一个提示，在运行时可能会被忽略。 默认值为 `1`。如果是主题侦听器或队列顺序很重要，则应将并发限制为 `1`。考虑将其提升为一般队列。 |
| `prefetch`                  | 加载到单个会话中的最大消息数。请注意，增加此数字可能会导致并发消费者饥饿。 |
| `receive-timeout`           | 用于接受调用的超时时间（以毫秒为单位）。默认值为 `1000`（一秒）。`-1` 表示没有超时。 |
| `back-off`                  | 指定 `BackOff` 实例，用于计算两次恢复尝试之间的间隔。如果 `BackOffExecution` 实现返回 `BackOffExecution#STOP`，则侦听器容器不会进一步尝试恢复。设置此属性后，将忽略 `recovery-interval` 值。默认值为 `FixedBackOff`，间隔为 `5000` 毫秒（即 5秒）。 |
| `recovery-interval`         | 指定两次恢复尝试之间的时间间隔（以毫秒为单位）。它提供了一种方便的方法来创建具有指定间隔的 `FixedBackOff`。对于更多恢复选项，请考虑指定一个 `BackOff` 实例。缺省值为 5000 毫秒（即 5 秒）。 |
| `phase`                     | 此容器应在其中启动和停止的生命周期阶段。值越低，此容器启动越早，而其停止越晚。默认值为 `Integer.MAX_VALUE`，这意味着容器将尽可能晚地启动，并尽快停止。 |

使用 `jms` 模式支持配置基于 JCA 的侦听器容器非常相似，如以下示例所示：

```xml
<jms:jca-listener-container resource-adapter="myResourceAdapter"
        destination-resolver="myDestinationResolver"
        transaction-manager="myTransactionManager"
        concurrency="10">

    <jms:listener destination="queue.orders" ref="myMessageListener"/>

</jms:jca-listener-container>
```

下表描述了 JCA 变体的可用配置选项：

| 属性                        | 描述                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| `factory-id`                | 将此元素定义的设置公开为具有指定 ID 的 `JmsListenerContainerFactory`，以便其他端点重复使用。 |
| `resource-adapter`          | 对 JCA `ResourceAdapter` bean的引用（默认 bean 名称为 `resourceAdapter`）。 |
| `activation-spec-factory`   | `JmsActivationSpecFactory` 的引用。默认设置是自动检测 JMS 提供程序及其 `ActivationSpec` 类（参考 [`DefaultJmsActivationSpecFactory`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/endpoint/DefaultJmsActivationSpecFactory.html)）。 |
| `destination-resolver`      | 对用于解析 JMS 目标的 `DestinationResolver` 策略的引用。     |
| `message-converter`         | 对将 JMS 消息转换为侦听器方法参数的 `MessageConverter` 策略的引用。默认值为 `SimpleMessageConverter`。 |
| `destination-type`          | 此侦听器的 JMS 目标类型：`queue`， `topic`， `durableTopic`， `sharedTopic`，或者 `sharedDurableTopic`。这可能会启用容器的 `pubSubDomain`，`subscriptionDurable` 和 `subsubscribeShared` 属性。默认值为 `queue`（禁用这三个属性）。 |
| `response-destination-type` | 响应的 JMS 目标类型：`queue` 或 `topic`。默认值为 `destination-type` 属性的值。 |
| `client-id`                 | 此侦听器容器的JMS客户端ID。使用持久订阅时需要指定它。        |
| `acknowledge`               | 本地 JMS 确认模式：`auto`， `client`， `dups-ok`， 或者 `transacted`。值 `transacted` 激活了本地交易的 `Session` 。或者，您可以指定稍后描述的 `transaction-manager` 属性。默认为 `auto`。 |
| `transaction-manager`       | 对 Spring  `JtaTransactionManager` 或 `javax.transaction.TransactionManager` 的引用，用于为每个传入消息启动 XA 事务。如果未指定，则使用本机确认（请参阅 `acknowledge` 属性）。 |
| `concurrency`               | 每个侦听器启动的并发会话或使用者的数量。它可以是表示最大数的简单数字（例如， `5`），也可以是表示上下限的范围（例如，`3-5`）。请注意，指定的最小值只是一个提示，通常在运行时使用 JCA 侦听器容器时将被忽略。 预设值为 `1`。 |
| `prefetch`                  | 加载到单个会话中的最大消息数。请注意，增加此数字可能会导致并发消费者饥饿。 |

## 4. JMX



## 5. JCA CCI



## 6. Email

本章节描述如何使用 Spring 框架发送电子邮件。

> 库依赖
>
> 下面的 JAR 需要放在你的应用的类路径下以便使用 Spring 框架的电子邮件类库：
>
> -  [JavaMail](https://javaee.github.io/javamail/) 类库
>
> 此类库在网络上可以自由使用 — 比如，在 Maven 中央仓库中的 `com.sun.mail:javax.mail`。

Spring 框架提供了一个很好用的工具类库来发送邮件，将你从特定于底层邮件系统的技术细节中解脱出来，该类库同时还接管了客户端的底层资源处理。

`org.springframework.mail` 包是 Spring 框架电子邮件支持的根级别包。发送邮件的中央接口是 `MailSender` 接口。一个简单的值对象封装了简单邮件的属性，比如 `from` 和 `to` (当然还有很多别的属性)，就是 `SimpleMailMessage` 类。该包还包含受检查异常层级结构提供了低层级邮件系统异常的高层抽象，其根异常是 `MailException` 。参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/mail/MailException.html) 了解更多有关邮件异常层级结构的信息。

`org.springframework.mail.javamail.JavaMailSender` 接口添加了特定的 JavaMail 特性，比如将 MIME 消息支持添加到 `MailSender` 接口（继承该接口）。`JavaMailSender` 也提供了一个名为 `org.springframework.mail.javamail.MimeMessagePreparator` 的回调接口来准备 `MimeMessage`。

### 6.1 使用

假定我们已经有一个业务接口名为 `OrderManager`，如下面例子所示：

```java
public interface OrderManager {

    void placeOrder(Order order);

}
```

进一步假设我们有一个要求，需要生成带有订单号的电子邮件并将其发送给下订单的客户。

#### 6.1.1 基本的 `MailSender` 和 `SimpleMailMessage` 使用

下面的例子展示了如何使用 `MailSender` 和 `SimpleMailMessage` 当有人下订单时来发送邮件：

```java
import org.springframework.mail.MailException;
import org.springframework.mail.MailSender;
import org.springframework.mail.SimpleMailMessage;

public class SimpleOrderManager implements OrderManager {

    private MailSender mailSender;
    private SimpleMailMessage templateMessage;

    public void setMailSender(MailSender mailSender) {
        this.mailSender = mailSender;
    }

    public void setTemplateMessage(SimpleMailMessage templateMessage) {
        this.templateMessage = templateMessage;
    }

    public void placeOrder(Order order) {

        // Do the business calculations...

        // Call the collaborators to persist the order...

        // Create a thread safe "copy" of the template message and customize it
        SimpleMailMessage msg = new SimpleMailMessage(this.templateMessage);
        msg.setTo(order.getCustomer().getEmailAddress());
        msg.setText(
            "Dear " + order.getCustomer().getFirstName()
                + order.getCustomer().getLastName()
                + ", thank you for placing order. Your order number is "
                + order.getOrderNumber());
        try{
            this.mailSender.send(msg);
        }
        catch (MailException ex) {
            // simply log it and go on...
            System.err.println(ex.getMessage());
        }
    }

}
```

下面的例子展示了上面代码对应的 bean 定义：

```xml
<bean id="mailSender" class="org.springframework.mail.javamail.JavaMailSenderImpl">
    <property name="host" value="mail.mycompany.com"/>
</bean>

<!-- this is a template message that we can pre-load with default state -->
<bean id="templateMessage" class="org.springframework.mail.SimpleMailMessage">
    <property name="from" value="customerservice@mycompany.com"/>
    <property name="subject" value="Your order"/>
</bean>

<bean id="orderManager" class="com.mycompany.businessapp.support.SimpleOrderManager">
    <property name="mailSender" ref="mailSender"/>
    <property name="templateMessage" ref="templateMessage"/>
</bean>
```

#### 6.1.2 使用 `JavaMailSender` 和 `MimeMessagePreparator`

本节描述另一种 `OrderManager` 的实现，它使用 `MimeMessagePreparator` 回调接口。下面的例子中，`mailSender` 属性是 `JavaMailSender` 类型，因此我们可以使用 JavaMail `MimeMessage` 类：

```java
import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;

import javax.mail.internet.MimeMessage;
import org.springframework.mail.MailException;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessagePreparator;

public class SimpleOrderManager implements OrderManager {

    private JavaMailSender mailSender;

    public void setMailSender(JavaMailSender mailSender) {
        this.mailSender = mailSender;
    }

    public void placeOrder(final Order order) {
        // Do the business calculations...
        // Call the collaborators to persist the order...

        MimeMessagePreparator preparator = new MimeMessagePreparator() {
            public void prepare(MimeMessage mimeMessage) throws Exception {
                mimeMessage.setRecipient(Message.RecipientType.TO,
                        new InternetAddress(order.getCustomer().getEmailAddress()));
                mimeMessage.setFrom(new InternetAddress("mail@mycompany.com"));
                mimeMessage.setText("Dear " + order.getCustomer().getFirstName() + " " +
                        order.getCustomer().getLastName() + ", thanks for your order. " +
                        "Your order number is " + order.getOrderNumber() + ".");
            }
        };

        try {
            this.mailSender.send(preparator);
        }
        catch (MailException ex) {
            // simply log it and go on...
            System.err.println(ex.getMessage());
        }
    }

}
```

> 邮件代码是一个横切关注点，很可能是能够重构进入 [custom Spring AOP aspect](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 的候选者，随后可以在 `OrderManager` 目标上合适的连接点被执行。

Spring 框架的邮件支持包含标准 JavaMail 实现。参考相关文档获取更多信息。

### 6.2 使用 JavaMail `MimeMessageHelper`

处理 JavaMail 消息时非常方便的类是 `org.springframework.mail.javamail.MimeMessageHelper`，它使您不必使用冗长的 JavaMail API。使用 `MimeMessageHelper`，创建 `MimeMessage` 非常容易，如以下示例所示：

```java
// of course you would use DI in any real-world cases
JavaMailSenderImpl sender = new JavaMailSenderImpl();
sender.setHost("mail.host.com");

MimeMessage message = sender.createMimeMessage();
MimeMessageHelper helper = new MimeMessageHelper(message);
helper.setTo("test@host.com");
helper.setText("Thank you for ordering!");

sender.send(message);
```

#### 6.2.1 发送附件和内联资源

多部分电子邮件同时允许附件和内联资源。内联资源的示例包括您要在邮件中使用但不希望显示为附件的图像或样式表。

##### 附件

以下示例显示了如何使用 `MimeMessageHelper` 发送带有单个 JPEG 图像附件的电子邮件：

```java
JavaMailSenderImpl sender = new JavaMailSenderImpl();
sender.setHost("mail.host.com");

MimeMessage message = sender.createMimeMessage();

// use the true flag to indicate you need a multipart message
MimeMessageHelper helper = new MimeMessageHelper(message, true);
helper.setTo("test@host.com");

helper.setText("Check out this image!");

// let's attach the infamous windows Sample file (this time copied to c:/)
FileSystemResource file = new FileSystemResource(new File("c:/Sample.jpg"));
helper.addAttachment("CoolImage.jpg", file);

sender.send(message);
```

##### 內联资源

以下示例显示了如何使用 `MimeMessageHelper` 发送带有嵌入式图像的电子邮件：

```java
JavaMailSenderImpl sender = new JavaMailSenderImpl();
sender.setHost("mail.host.com");

MimeMessage message = sender.createMimeMessage();

// use the true flag to indicate you need a multipart message
MimeMessageHelper helper = new MimeMessageHelper(message, true);
helper.setTo("test@host.com");

// use the true flag to indicate the text included is HTML
helper.setText("<html><body><img src='cid:identifier1234'></body></html>", true);

// let's include the infamous windows Sample file (this time copied to c:/)
FileSystemResource res = new FileSystemResource(new File("c:/Sample.jpg"));
helper.addInline("identifier1234", res);

sender.send(message);
```

> 通过使用指定的 `Content-ID` 将内联资源添加到 `MimeMessage` 中（在上例中为 `identifier1234`）。添加文本和资源的顺序非常重要。确保首先添加文本，然后添加资源。如果您正相反进行操作，则此操作无效。

#### 6.2.2 使用模板库创建邮件内容

上一节例子中的代码通过使用诸如 `message.setText(..)` 等方法调用显式创建邮件消息内容。对简单场景来说这样没问题，在前面例子中的场景下也可以，那里是为了向你展示最基本的 API 的用法。

在典型的企业级应用中，开发者通常不会使用前面展示的方法创建邮件内容，基于以下几个原因：

- 在 Java 代码中创建基于 HTML 的邮件内容是枯燥而且容易出错的。
- 在显式逻辑和业务逻辑之间没有清晰的区隔。
- 修改邮件内容的显式结构需要修改 Java 代码，重新编译，以及重新部署。

通常，解决这些问题的方法就是使用模板类库（比如 FreeMarker）来定义邮件内容的显式结构。这样你的 Java 代码的唯一任务就是创建用于填充邮件模板的数据以及发送邮件。当你的邮件内容比较复杂时，这种方法绝对是最佳实践。同时，使用 Spring 框架的 FreeMarker 支持类，这样做也非常简单。

## 7. 任务执行和调度

Spring 框架分别通过 `TaskExecutor` 和 `TaskScheduler` 接口为任务的异步执行和调度提供了抽象。Spring 还提供了那些接口的实现，这些接口在应用程序服务器环境中支持线程池或委托给 `CommonJ`。最终，在公共接口后面使用这些实现可以抽象化 Java SE 5，Java SE 6 和 Java EE 环境之间的差异。

Spring还具有集成类，以支持使用 `Timer`（自 1.3 开始成为 JDK 的一部分）和 Quartz Scheduler（https://www.quartz-scheduler.org/）进行调度。您可以通过使用带有分别对 `Timer` 或 `Trigger` 实例的可选引用的 `FactoryBean` 来设置这两个调度程序。此外，还提供了 Quartz Scheduler 和 `Timer` 的便捷类，可用于调用现有目标对象的方法（类似于常规的 `MethodInvokingFactoryBean` 操作）。

### 7.1. Spring `TaskExecutor` 抽象

Executors 是线程池概念的JDK名称。 Executors 的命名是由于无法保证基础实现实际上是一个池。执行程序可能是单线程的，甚至是同步的。Spring 的抽象隐藏了 Java SE 和 Java EE 环境之间的实现细节。

Spring 的 `TaskExecutor` 接口与 `java.util.concurrent.Executor` 接口相同。实际上，最初，其存在的主要原因是在使用线程池时抽象出对 Java 5 的需求。该接口具有单个方法（ `execute(Runnable task)`），该方法根据线程池的语义和配置接受要执行的任务。

最初创建 `TaskExecutor` 的目的是为其他 Spring 组件提供所需的线程池抽象。诸如 `ApplicationEventMulticaster`，JMS 的 `AbstractMessageListenerContainer` 和 Quartz 集成之类的组件均使用 `TaskExecutor` 抽象来池化线程。但是，如果您的 bean 需要线程池行为，则也可以根据自己的需要使用此抽象。

#### 7.1.1. `TaskExecutor` 类型

Spring 包含若干预置的 `TaskExecutor` 实现。大多数情况下，你应该不需要自己来实现。Spring 提供如下变体：

- `SyncTaskExecutor`: 此实现不回异步执行调用。每个调用都发生在调用线程中。主要用在不需要多线程的场景，比如简单的测试用例。
- `SimpleAsyncTaskExecutor`: 此实现不会复用任何线程。它为每次调用启动一个新的线程。不过，它支持有限制的并发，超过并发度限制的调用将被阻塞直到运行中的线程结束以空出并发额度。如果你需要真正的线程池，参考此列表后面的 `ThreadPoolTaskExecutor` 。
- `ConcurrentTaskExecutor`: 此实现是 `java.util.concurrent.Executor` 实例的适配器。还有一个替代（`ThreadPoolTaskExecutor`），将 `Executor` 配置参数作为 bean 属性公开。很少需要直接使用 `ConcurrentTaskExecutor`。但是，如果 `ThreadPoolTaskExecutor` 不够灵活，无法满足您的需求，则可以选择 `ConcurrentTaskExecutor` 。
- `ThreadPoolTaskExecutor`: 此实现是最常用的。它公开了用于配置 `java.util.concurrent.ThreadPoolExecutor` 的 bean 属性，并将其包装在 `TaskExecutor` 中。如果您需要适配其他类型的 `java.util.concurrent.Executor`，我们建议您改用 `ConcurrentTaskExecutor`。
- `WorkManagerTaskExecutor`: 此实现使用 CommonJ `WorkManager` 作为其支持服务提供者，并且是在 Spring 应用程序上下文中在 WebLogic 或 WebSphere 上设置基于 CommonJ 的线程池集成的中心便利类。
- `DefaultManagedTaskExecutor`: 此实现在兼容 JSR-236 的运行时环境（例如 Java EE 7+ 应用程序服务器）中使用 JNDI 获得的 `ManagedExecutorService`，为此替换了 CommonJ `WorkManager`。

#### 7.1.2. 使用 `TaskExecutor`

Spring 的 `TaskExecutor` 实现被作为简单的 JavaBean 使用。在以下示例中，我们定义了一个 bean，使用 `ThreadPoolTaskExecutor` 来异步打印出一组消息：

```java
import org.springframework.core.task.TaskExecutor;

public class TaskExecutorExample {

    private class MessagePrinterTask implements Runnable {

        private String message;

        public MessagePrinterTask(String message) {
            this.message = message;
        }

        public void run() {
            System.out.println(message);
        }
    }

    private TaskExecutor taskExecutor;

    public TaskExecutorExample(TaskExecutor taskExecutor) {
        this.taskExecutor = taskExecutor;
    }

    public void printMessages() {
        for(int i = 0; i < 25; i++) {
            taskExecutor.execute(new MessagePrinterTask("Message" + i));
        }
    }
}
```

如你所见，你只是将你自己的 `Runnable` 添加到队列中，而不是从线程池获取线程并自己执行它。然后 `TaskExecutor` 使用它内部的规则决定任务何时执行。

为了配置 `TaskExecutor` 使用的规则，我们暴露简单的 bean 属性：

```xml
<bean id="taskExecutor" class="org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor">
    <property name="corePoolSize" value="5"/>
    <property name="maxPoolSize" value="10"/>
    <property name="queueCapacity" value="25"/>
</bean>

<bean id="taskExecutorExample" class="TaskExecutorExample">
    <constructor-arg ref="taskExecutor"/>
</bean>
```

### 7.2. Spring `TaskScheduler` 抽象

除了对 `TaskExecutor` 的抽象外，Spring 3.0 还引入了 `TaskScheduler`，其中提供了多种方法来安排任务在将来某个时刻运行。以下清单显示 `TaskScheduler` 接口定义：

```java
public interface TaskScheduler {

    ScheduledFuture schedule(Runnable task, Trigger trigger);

    ScheduledFuture schedule(Runnable task, Instant startTime);

    ScheduledFuture schedule(Runnable task, Date startTime);

    ScheduledFuture scheduleAtFixedRate(Runnable task, Instant startTime, Duration period);

    ScheduledFuture scheduleAtFixedRate(Runnable task, Date startTime, long period);

    ScheduledFuture scheduleAtFixedRate(Runnable task, Duration period);

    ScheduledFuture scheduleAtFixedRate(Runnable task, long period);

    ScheduledFuture scheduleWithFixedDelay(Runnable task, Instant startTime, Duration delay);

    ScheduledFuture scheduleWithFixedDelay(Runnable task, Date startTime, long delay);

    ScheduledFuture scheduleWithFixedDelay(Runnable task, Duration delay);

    ScheduledFuture scheduleWithFixedDelay(Runnable task, long delay);
}
```

最简单的方法是一个名为 `schedule` 的方法，该方法仅需要一个 `Runnable` 和一个 `Date`。这将导致任务在指定时间后运行一次。所有其他方法都可以安排任务重复运行。固定速率和固定延迟方法是用于简单，定期执行的，但是接受 `Trigger` 的方法则更加灵活。

#### 7.2.1. `Trigger` 接口

`Trigger` 接口本质上是受 JSR-236 的启发，该 JSR-236 自 Spring 3.0 起尚未正式实现。`Trigger` 的基本思想是执行时间可以根据过去的执行结果甚至任意条件来决定。如果这些决定确实考虑了先前执行的结果，则该信息在 `TriggerContext` 中可用。`Trigger` 接口本身非常简单，如以下清单所示：

```java
public interface Trigger {

    Date nextExecutionTime(TriggerContext triggerContext);
}
```

`TriggerContext` 是最重要的部分。它封装了所有相关数据，并在将来必要时开放以进行扩展。`TriggerContext` 是一个接口（默认情况下使用 `SimpleTriggerContext` 实现）。下面的清单展示了 `Trigger` 实现的可用方法。

```java
public interface TriggerContext {

    Date lastScheduledExecutionTime();

    Date lastActualExecutionTime();

    Date lastCompletionTime();
}
```

#### 7.2.2. `Trigger` 实现

Spring 提供了 `Trigger` 接口的两种实现。最有趣的是 `CronTrigger`。它启用了基于 cron 表达式的任务调度。例如，以下任务计划在每小时的 15 分钟后运行，但仅在工作日的上午 9 点到下午 5 点之间的“工作时间”内运行：

```java
scheduler.schedule(task, new CronTrigger("0 15 9-17 * * MON-FRI"));
```

另一个实现是 `PeriodicTrigger`，它接受一个固定的周期，一个可选的初始延迟值和一个布尔值，以指示该周期应被解释为固定速率还是固定延迟。由于 `TaskScheduler` 接口已经定义了以固定速率或固定延迟调度任务的方法，因此应尽可能直接使用这些方法。`PeriodicTrigger` 实现的价值在于您可以在依赖于 `Trigger` 抽象的组件中使用它。例如，允许周期性触发器，基于 cron 的触发器，甚至自定义触发器实现可互换使用可能很方便。这样的组件可以利用依赖注入的优势，以便您可以在外部配置此类 `Triggers` ，因此可以轻松地对其进行修改或扩展。

#### 7.2.3. `TaskScheduler` 实现

与 Spring 的 `TaskExecutor` 抽象一样，`TaskScheduler` 安排的主要好处是应用程序的调度需求与部署环境分离。在部署到不应由应用程序本身直接创建线程的应用程序服务器环境时，此抽象级别特别重要。对于这种情况，Spring 提供了一个在 WebLogic 或 WebSphere 上委派给 CommonJ `TimerManager` 的 `TimerManagerTaskScheduler`，以及一个在 Java EE 7+ 环境中委派给 JSR-236 `ManagedScheduledExecutorService` 的较新的 `DefaultManagedTaskScheduler`。两者通常都配置有 JNDI 查找。

每当不需要外部线程管理时，一个更简单的选择就是在应用程序中进行本地 `ScheduledExecutorService` 设置，可以通过 Spring 的 `ConcurrentTaskScheduler` 进行适配。为了方便起见，Spring 还提供了一个 `ThreadPoolTaskScheduler`，它在内部委托给 `ScheduledExecutorService` 以按照 `ThreadPoolTaskExecutor` 的方式提供通用的 bean 样式的配置。这些变体也适用于宽松的应用程序服务器环境中的本地嵌入式线程池设置，尤其是在 Tomcat 和 Jetty 上。

### 7.3. 对调度和异步执行的注解支持

Spring 同时提供了对调度和异步方法执行的注解支持。

#### 7.3.1. 启用调度注解

为了开启对 `@Scheduled` 和 `@Async` 注解的支持，你可以添加 `@EnableScheduling` 和 `@EnableAsync` 到你的任何一个 `@Configuration` 类中，如下面例子所示：

```java
@Configuration
@EnableAsync
@EnableScheduling
public class AppConfig {
}
```

你可以为你的应用挑选相关注解。比如，如果你只需要 `@Scheduled` 支持，你就可以省略 `@EnableAsync` 注解。为了进行更加精细的控制，你可以额外实现 `SchedulingConfigurer` 接口，或者 `AsyncConfigurer` 接口，或者同时实现两者。参考 [`SchedulingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/scheduling/annotation/SchedulingConfigurer.html) 和 [`AsyncConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/scheduling/annotation/AsyncConfigurer.html) 文档获取更多细节。

如果你更喜欢 XML 配置，你可以使用 `<task:annotation-driven>` 元素，如下面例子所示：

```xml
<task:annotation-driven executor="myExecutor" scheduler="myScheduler"/>
<task:executor id="myExecutor" pool-size="5"/>
<task:scheduler id="myScheduler" pool-size="10"/>
```

注意，在上面的 XML 中，给定一个执行器引用来处理其中对应于 `@Async` 注解修饰的方法的任务，而给定的调度器引用管理 `@Scheduled` 注解修饰的方法 。

> 处理 `@Async` 注解的默认增强模式是 `proxy`（代理），它仅允许通过代理来拦截调用。同一类内的本地调用无法以这种方式被拦截。对于更高级的拦截模式，请考虑结合编译时或加载时编织切换到 `aspectj` 模式。

#### 7.3.2.  `@Scheduled` 注解

您可以将 `@Scheduled` 注解以及触发器元数据添加到方法上。例如，以下方法每隔五秒钟以固定的延迟被调用一次，这意味着该时间段是从每个先前调用的完成时间开始计算的：

```java
@Scheduled(fixedDelay=5000)
public void doSomething() {
    // something that should execute periodically
}
```

如果需要固定速率执行，则可以更改注解中指定的属性名称。每五秒钟调用一次以下方法（在每次调用的连续开始时间之间测量时间间隔）：

```java
@Scheduled(fixedRate=5000)
public void doSomething() {
    // something that should execute periodically
}
```

对于固定延迟和固定速率的任务，可以通过指示在第一次执行该方法之前要等待的毫秒数来指定初始延迟，如下面的 `fixedRate` 示例所示：

```java
@Scheduled(initialDelay=1000, fixedRate=5000)
public void doSomething() {
    // something that should execute periodically
}
```

如果简单的周期性调度不足以满足需求，则可以提供 cron 表达式。例如，以下仅在工作日执行：

```java
@Scheduled(cron="*/5 * * * * MON-FRI")
public void doSomething() {
    // something that should execute on weekdays only
}
```

> 你还可以使用 `zone` 属性来指定 cron 表达式应该在哪个时区被解析。

请注意，要调度的方法必须具有空返回值，并且不能期望任何参数。如果该方法需要与应用程序上下文中的其他对象进行交互，则通常将通过依赖项注入来提供这些对象。

> 从 Spring Framework 4.3 开始，任何作用域范围的 bean 都支持 `@Scheduled` 方法。
>
> 确保不要在运行时初始化同一个 `@Scheduled` 注解类的多个实例，除非您确实希望为每个此类实例安排回调。与此相关的是，请确保不要在以 `@Scheduled` 注解并已在容器中注册为常规 Spring bean 的 bean 类上使用 `@ Configurable`。否则，您将获得双重初始化（一次通过容器，一次通过 `@Configurable` 切面），结果每个 `@Scheduled` 方法被调用两次。

#### 7.3.3.  `@Async` 注解

您可以在方法上提供 `@Async` 注解，以便异步调用该方法。换句话说，调用者在调用时立即返回，而方法的实际执行发生在已提交给 Spring `TaskExecutor` 的任务中。在最简单的情况下，可以将注解应用于返回 `void` 的方法，如以下示例所示：

```java
@Async
void doSomething() {
    // this will be executed asynchronously
}
```

与用 `@Scheduled` 注解注释的方法不同，这些方法可以使用参数，因为它们在运行时由调用者以“常规”方式调用，而不是从容器管理的计划任务中调用。例如，以下代码是 `@Async` 注解的合法应用程序：

```java
@Async
void doSomething(String s) {
    // this will be executed asynchronously
}
```

即使有返回值的方法也可以异步调用。但是，要求此类方法具有 `Future` 类型的返回值。这仍然提供了异步执行的好处，以便调用者可以在对该 `Future` 调用 `get()` 之前执行其他任务。以下示例说明如何在有返回值的方法上使用 `@Async`：

```java
@Async
Future<String> returnSomething(int i) {
    // this will be executed asynchronously
}
```

> `@Async` 方法不仅可以声明常规的 `java.util.concurrent.Future` 返回类型，还可以声明 Spring 的 `org.springframework.util.concurrent.ListenableFuture`，或者从 Spring 4.2 起声明 JDK 8 的 `java.util.parallel.CompletableFuture`，用于与异步任务进行更丰富的交互，并与进一步的处理步骤立即进行合成。

您不能将 `@Async` 与生命周期回调（如 `@PostConstruct` ）结合使用。要异步初始化 Spring Bean，当前必须使用单独的初始化 Spring Bean，然后在目标上调用带有 `@Async` 注解的方法，如以下示例所示：

```java
public class SampleBeanImpl implements SampleBean {

    @Async
    void doSomething() {
        // ...
    }

}

public class SampleBeanInitializer {

    private final SampleBean bean;

    public SampleBeanInitializer(SampleBean bean) {
        this.bean = bean;
    }

    @PostConstruct
    public void initialize() {
        bean.doSomething();
    }

}
```

> `@Async` 没有直接的 XML 等效项，因为此类方法应首先设计用于异步执行，而不是在外部重新声明为异步。不过，您可以结合使用自定义切入点，通过 Spring AOP 手动设置 Spring 的 `AsyncExecutionInterceptor`。

#### 7.3.4. 使用 `@Async` 的执行器资格

默认情况下，当在方法上指定 `@Async` 注解时，使用的执行器就必须是 [启用异步支持时被配置的](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#scheduling-enable-annotation-support)，比如，如果你使用 XML，执行器就应该是 `annotation-driven` 元素，或者其本身是 `AsyncConfigurer` 实现，如果存在。不过，当你需指示执行给定方法，应使用默认值以外的执行器时，你可以使用 `@Async` 注解的 `value` 属性。下面的例子展示了具体做法：

```java
@Async("otherExecutor")
void doSomething(String s) {
    // this will be executed asynchronously by "otherExecutor"
}
```

在这种情况下，`otherExecutor` 可以是 Spring 容器中任何 `Executor` bean的名称，也可以是与任何 `Executor` 相关联的限定词的名称（例如，由 `<qualifier>` 元素或 Spring 的 `@Qualifier` 注解指定的）。

#### 7.3.5. 使用 `@Async` 时的异常管理

当 `@Async` 方法的返回值类型为 `Future` 时，很容易管理在方法执行过程中引发的异常，因为在对 `Future` 结果调用 `get` 时会引发该异常。但是，对于 `void` 返回类型，该异常是未捕获的，无法传输。您可以提供一个 `AsyncUncaughtExceptionHandler` 来处理此类异常。以下示例显示了如何执行此操作：

```java
public class MyAsyncUncaughtExceptionHandler implements AsyncUncaughtExceptionHandler {

    @Override
    public void handleUncaughtException(Throwable ex, Method method, Object... params) {
        // handle exception
    }
}
```

默认情况下，仅记录异常。您可以使用 `AsyncConfigurer` 或 `<task:annotation-driven/>` XML 元素来定义自定义的 `AsyncUncaughtExceptionHandler`。

### 7.4.  `task` 命名空间

Spring 3.0 中包含了配置 `TaskExecutor` 和 `TaskScheduler` 实例的命名空间。同时提供一种方便的方式配置将要通过触发器调度的任务。

#### 7.4.1.  `scheduler` 元素

下面的元素创建一个 `ThreadPoolTaskScheduler` 实例，使用指定的线程池大小：

```xml
<task:scheduler id="scheduler" pool-size="10"/>
```

`id` 属性的值被用来作为线程池中的线程名称的前缀。`scheduler` 元素相对简单。如果你没有指定 `pool-size` 属性，默认的线程池就只会有一个线程。该元素没有其它配置选项。

#### 7.4.2.  `executor` 元素

下面的例子创建一个 `ThreadPoolTaskExecutor` 实例：

```xml
<task:executor id="executor" pool-size="10"/>
```

与 [上一部分](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#scheduling-task-namespace-scheduler) 中显示的调度器一样，为 `id` 属性提供的值用作池中线程名称的前缀。就池的大小而言， `executor` 元素比 `scheduler` 元素支持更多的配置选项。一方面，`ThreadPoolTaskExecutor` 的线程池本身更具可配置性。执行器的线程池不仅可以只包含一个线程，而且可以具有不同的核心线程数和最大线程数。如果提供单个值，则执行器具有固定大小的线程池（核心大小和最大大小相同）。但是，`executor` 元素的 `pool-size` 属性也接受 `min-max` 形式的范围。以下示例将最小值设置为 `5`，将最大值设置为 `25`：

```xml
<task:executor
        id="executorWithPoolSizeRange"
        pool-size="5-25"
        queue-capacity="100"/>
```

在前述配置中，还提供了 `queue-capacity` 值。还应根据执行器的队列容量来考虑线程池的配置。有关池大小和队列容量之间关系的完整说明，请参见 [`ThreadPoolExecutor`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html)。主要思想是，在提交任务时，如果当前活动线程数小于核心大小，则执行器首先尝试使用空闲线程。如果已达到核心大小，则只要尚未达到线程池最大容量，就将任务添加到队列中。只有当达到队列的最大容量，执行器才创建超出核心大小的新线程。如果同时还达到了线程池最大大小，那么执行器将拒绝该任务。

默认情况下，队列是无界的，但大部分情况下着并不是所需的配置，因为如果在所有池线程繁忙时将足够的任务添加到该队列中，则会导致 `OutOfMemoryErrors`。此外，如果队列是无界的，则最大大小完全无效。由于执行器总是在创建超出核心大小的新线程之前尝试队列，因此队列必须具有有限的容量，线程池才能超出核心大小（这就是为什么固定大小的池是使用无限队列时唯一明智的情况）。

如上所述，考虑拒绝任务的情况。默认情况下，当任务被拒绝时，线程池执行器将抛出 `TaskRejectedException`。但是，拒绝策略实际上是可配置的。使用默认拒绝策略（即 `AbortPolicy` 实现）时会引发异常。对于某些可以在高负载下跳过某些任务的应用程序，您可以配置 `DiscardPolicy` 或 `DiscardOldestPolicy`。对于需要在重负载下限制提交的任务的应用程序来说，另一个不错的选择是 `CallerRunsPolicy`。该策略不会引发异常或放弃任务，而是强制调用提交方法的线程运行任务本身。这样做的想法是，这样的调用者在运行该任务时很忙，无法立即提交其他任务。因此，它提供了一种在保持线程池和队列限制的同时限制传入负载的简单方法。通常，这允许执行者“赶上”它正在处理的任务，从而释放队列、池中或两者中的某些容量。您可以从 `executor` 元素上的 `rejection-policy` 属性的可用值枚举中选择任何一个。

下面的例子展示了一个 `executor` 元素，使用一系列属性指定各种行为：

```xml
<task:executor
        id="executorWithCallerRunsPolicy"
        pool-size="5-25"
        queue-capacity="100"
        rejection-policy="CALLER_RUNS"/>
```

最后，`keep-alive` 设置确定线程在终止之前可以保持空闲状态的时间限制（以秒为单位）。如果当前线程池中的线程数超过核心数，则在等待此时间而不处理任务后，多余的线程将被终止。时间值为零会导致多余的线程在执行任务后立即终止，而不会在任务队列中保留后续工作。以下示例将 `keep-alive` 值设置为两分钟：

```xml
<task:executor
        id="executorWithKeepAlive"
        pool-size="5-25"
        keep-alive="120"/>
```

#### 7.4.3. `scheduled-tasks` 元素

Spring task 命名空间最强大的功能是支持配置要在 Spring Application Context 中安排的任务。这遵循类似于 Spring 中其他“方法调用者”的方法，例如 JMS 命名空间提供的用于配置消息驱动的 POJO 的方法。基本上，`ref` 属性可以指向任何 Spring 管理的对象，而 `method` 属性提供要在该对象上调用的方法的名称。以下清单显示了一个简单的示例：

```xml
<task:scheduled-tasks scheduler="myScheduler">
    <task:scheduled ref="beanA" method="methodA" fixed-delay="5000"/>
</task:scheduled-tasks>

<task:scheduler id="myScheduler" pool-size="10"/>
```

调度程序由外部元素引用，并且每个单独的任务都包括其触发元数据的配置。在前面的示例中，该元数据定义了一个具有固定延迟的周期性触发器，该延迟指示了每个任务执行完成后要等待的毫秒数。另一个选项是 `fixed-rate`，它表示应该执行该方法的频率，而不管之前执行的时间如何。另外，对于 `fixed-delay` 和 `fixed-rate` 任务，您都可以指定 `initial-delay` 参数，指示首次执行该方法之前要等待的毫秒数。为了获得更多控制，您可以改为提供 `cron` 属性。以下示例显示了这些其他选项：

```xml
<task:scheduled-tasks scheduler="myScheduler">
    <task:scheduled ref="beanA" method="methodA" fixed-delay="5000" initial-delay="1000"/>
    <task:scheduled ref="beanB" method="methodB" fixed-rate="5000"/>
    <task:scheduled ref="beanC" method="methodC" cron="*/5 * * * * MON-FRI"/>
</task:scheduled-tasks>

<task:scheduler id="myScheduler" pool-size="10"/>
```

### 7.5. 使用 Quartz 调度器

Quartz 使用 `Trigger`，`Job` 以及 `JobDetail` 对象来实现各种任务的调度。要了解 Quartz 背后的基本概念，请参考 https://www.quartz-scheduler.org/ 。方便起见，Spring 提供了两个类来简化在基于 Spring 的引用中的 Quartz 使用。

#### 7.5.1. 使用 `JobDetailFactoryBean`

Quart `JobDetail` 对象包含运行一项任务所需的所有信息。Spring 提供了 `JobDetailFactoryBean` ，它为 XML 形式的配置提供了 bean 风格的属性。考虑下面的例子：

```xml
<bean name="exampleJob" class="org.springframework.scheduling.quartz.JobDetailFactoryBean">
    <property name="jobClass" value="example.ExampleJob"/>
    <property name="jobDataAsMap">
        <map>
            <entry key="timeout" value="5"/>
        </map>
    </property>
</bean>
```

任务细节配置包含运行任务（`ExampleJob`）所需的所有信息。超时在任务数据映射中指定。任务数据映射在 `JobExectionContext` （在任务执行期间会传递给你）中可用，但是 `JobDetail` 同样也从用于配置任务实例的任务数据映射中获取它的属性。因此，下面的例子中，`ExampleJob` 包含名为 `timeout` 的 bean 属性，`JobDetail` 自动应用该属性值：

```java
package example;

public class ExampleJob extends QuartzJobBean {

    private int timeout;

    /**
     * Setter called after the ExampleJob is instantiated
     * with the value from the JobDetailFactoryBean (5)
     */
    public void setTimeout(int timeout) {
        this.timeout = timeout;
    }

    protected void executeInternal(JobExecutionContext ctx) throws JobExecutionException {
        // do the actual work
    }

}
```

从任务数据映射中获取的额外属性对你来说同样可用。

> 通过使用 `name` 和 `group` 属性，你可以相应修改任务的名称和组。默认情况下，任务名称对应于 `JobDetailFactoryBean` bean 名称（上面例子中的 `exampleJob`）。

#### 7.5.2. 使用 `MethodInvokingJobDetailFactoryBean`

通常你很少需要调用特定对象上的方法。通过使用 `MethodInvokingJobDetailFactoryBean` ，你可以做到这一点，如下面例子所示：

```xml
<bean id="jobDetail" class="org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean">
    <property name="targetObject" ref="exampleBusinessObject"/>
    <property name="targetMethod" value="doIt"/>
</bean>
```

前面的示例导致在 `exampleBusinessObject` 方法上调用 `doIt` 方法，如以下示例所示：

```java
public class ExampleBusinessObject {

    // properties and collaborators

    public void doIt() {
        // do the actual work
    }
}
```

```xml
<bean id="exampleBusinessObject" class="examples.ExampleBusinessObject"/>
```

通过使用 `MethodInvokingJobDetailFactoryBean`，您无需创建仅调用方法的单行作业。您只需要创建实际的业务对象并连接具体对象即可。

默认情况下，Quartz Jobs 是无状态的，从而导致作业相互干扰的可能性。如果为相同的 `JobDetail` 指定两个触发器，则有可能在第一个作业完成之前启动第二个作业。如果 `JobDetail` 类实现了 `Stateful` 接口，则不会发生这种情况。在第一个作业完成之前，第二个作业不会开始。要使由 `MethodInvokingJobDetailFactoryBean` 产生的作业是非并行的，请将 `concurrent` 标记设置为 `false`，如以下示例所示：

```xml
<bean id="jobDetail" class="org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean">
    <property name="targetObject" ref="exampleBusinessObject"/>
    <property name="targetMethod" value="doIt"/>
    <property name="concurrent" value="false"/>
</bean>
```

> 默认情况下，作业将以并发方式运行。

#### 7.5.3. 通过使用触发器和 `SchedulerFactoryBean` 连接作业

我们已经创建了工作详细信息和工作。我们还回顾了便捷 bean，该 bean 使您可以在特定对象上调用方法。当然，我们仍然需要自己调度工作。这是通过使用触发器和一个 `SchedulerFactoryBean` 来完成的。Quartz 中提供了几种触发器，Spring 提供了两个具有方便的默认值的 Quartz `FactoryBean` 实现：`CronTriggerFactoryBean` 和 `SimpleTriggerFactoryBean`。

触发器需要调度。Spring提供了一个 `SchedulerFactoryBean`，它公开了要设置为属性的触发器。  `SchedulerFactoryBean` 通过这些触发器调度实际的作业。

以下清单同时使用了 `SimpleTriggerFactoryBean` 和 `CronTriggerFactoryBean`：

```xml
<bean id="simpleTrigger" class="org.springframework.scheduling.quartz.SimpleTriggerFactoryBean">
    <!-- see the example of method invoking job above -->
    <property name="jobDetail" ref="jobDetail"/>
    <!-- 10 seconds -->
    <property name="startDelay" value="10000"/>
    <!-- repeat every 50 seconds -->
    <property name="repeatInterval" value="50000"/>
</bean>

<bean id="cronTrigger" class="org.springframework.scheduling.quartz.CronTriggerFactoryBean">
    <property name="jobDetail" ref="exampleJob"/>
    <!-- run every morning at 6 AM -->
    <property name="cronExpression" value="0 0 6 * * ?"/>
</bean>
```

前面的示例设置了两个触发器，一个触发器每隔 50 秒运行一次，启动延迟为 10 秒，另一个触发器每天清晨 6 点运行。要完成所有工作，我们需要设置 `SchedulerFactoryBean`，如以下示例所示：

```xml
<bean class="org.springframework.scheduling.quartz.SchedulerFactoryBean">
    <property name="triggers">
        <list>
            <ref bean="cronTrigger"/>
            <ref bean="simpleTrigger"/>
        </list>
    </property>
</bean>
```

更多的属性可用于 `SchedulerFactoryBean`，例如工作明细所使用的日历，用于自定义 Quartz 的属性等。请参阅 [`SchedulerFactoryBean`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/scheduling/quartz/SchedulerFactoryBean.html) Javadoc了解更多信息 。

## 8. 缓存抽象

从 3.1 版开始，Spring 框架提供了对将缓存透明添加到现有 Spring 应用程序的支持。与 [transaction](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction) 支持类似，缓存抽象允许各种对现有代码影响最小的缓存解决方案的一致使用。

从 Spring 4.1 开始，通过 [JSR-107 注解](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-jsr-107) 的支持，缓存抽象得到了显着扩展。同时添加了更多自定义选项。

### 8.1. 理解缓存抽象

> 缓存 vs 缓冲
>
> 术语“缓冲”和“缓存”倾向于互换使用。但是请注意，它们代表不同的事物。传统上，缓冲区用作快速实体和慢速实体之间的数据的中间临时存储。由于一方必须等待另一方（这会影响性能），因此缓冲区允许一次移动整个数据块而不是小块数据来缓解这种情况。数据只能从缓冲区写入和读取一次。此外，缓冲区对于至少一个知道缓冲区的一方是可见的。
>
> 另一方面，根据定义，缓存是隐藏的，任何一方都不知道发生了缓存。它可以提高性能，但是也可以通过快速读取多次相同数据来实现。
>
> 您可以在 [此处](https://en.wikipedia.org/wiki/Cache_(computing)#The_difference_between_buffer_and_cache) 中找到有关缓冲区和缓存之间差异的进一步说明。

缓存抽象的核心是将缓存应用于 Java 方法，从而根据缓存中可用的信息减少执行次数。也就是说，每次调用目标方法时，抽象都会应用缓存行为，该行为检查给定参数是否已经执行了该方法。如果已执行，则返回缓存的结果，而不必执行实际的方法。如果尚未执行该方法，则将执行该方法，并将结果缓存并返回给用户，以便下次调用该方法时，将返回缓存的结果。这样，对于给定的一组参数，成本高昂的方法（无论是受 CPU 限制还是与 IO 绑定）只能执行一次，结果可以重复使用，而不必再次实际执行该方法。缓存逻辑是对应用透明的，不会对调用方造成任何干扰。

> 该方法仅适用于保证无论给定输入（或参数）执行多少次都返回相同输出（结果）的方法。

缓存抽象提供了其他与缓存相关的操作，例如更新缓存内容或删除一个或所有条目的能力。如果高速缓存处理在应用程序过程中可能更改的数据，则这些功能很有用。

与 Spring 框架中的其他服务一样，缓存服务是一种抽象（不是缓存实现），并且需要使用实际的存储来存储缓存数据。也就是说，抽象使您不必编写缓存逻辑，但是没有提供实际的数据存储。这种抽象是通过 `org.springframework.cache.Cache和org.springframework.cache.CacheManager` 接口实现的。

Spring提供了该抽象的 [一些实现](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-store-configuration) ：基于 JDK ` java.util.concurrent.ConcurrentMap` 的缓存，[Ehcache 2.x](https://www.ehcache.org/)，Gemfire 缓存，[Caffeine](https://github.com/ben-manes/caffeine/wiki) 和符合 JSR-107 的缓存（例如 Ehcache 3.x）。有关更多信息，请参见 [插入不同的后端缓存](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-plug) 插入其他缓存存储区和提供程序。

> 对于多线程和多进程环境，缓存抽象没有特殊处理，因为此类功能由缓存实现处理。

如果您具有多进程环境（即，一个应用程序部署在多个节点上），则需要相应地配置缓存提供程序。根据您的应用场景，在几个节点上复制相同数据就足够了。但是，如果在应用程序过程中更改数据，则可能需要启用其他传播机制。

高速缓存特定数据项等同于通过程序化高速缓存交互找到该数据项的典型的“如果找不到，然后继续处理并放入”代码块。没有应用锁，几个线程可能会尝试同时加载同一数据项。缓存淘汰同样如此。如果多个线程试图同时更新或逐出数据，则可以使用陈旧数据。某些缓存提供程序在该区域提供高级功能。有关更多详细信息，请参见缓存提供程序的文档。

为了使用缓存抽象，你需要注意两个方面：

- 缓存声明：确定需要缓存的方法及其策略。
- 缓存配置：数据存储和读取的后备缓存。

### 8.2. 基于注解的声明式缓存

对于缓存声明，Spring 缓存抽象提供了一系列 Java 注解：

- `@Cacheable`: 触发缓存填充。
- `@CacheEvict`: 触发缓存淘汰。
- `@CachePut`: 不影响方法调度情况下更新缓存。
- `@Caching`: 对应用于一个方法的多个缓存操作重新编组。
- `@CacheConfig`: 在类层面共享某些公用缓存相关的设置。

#### 8.2.1.  `@Cacheable` 注解

如名称所暗示的，你可以使用 `@Cacheable` 注解来标定可以被缓存的方法－也就是说，方法的结果可以被存储在缓存中，因此后续相同参数的方法调用就可以直接返回缓存中的结果，而不需要实际执行方法。最简单的形式中，注解声明之需要讲缓存名称与被注解的方法关联起来，如下面例子所示：

```java
@Cacheable("books")
public Book findBook(ISBN isbn) {...}
```

在前面的代码段中，`findBook` 方法与名为 `books` 的缓存相关联。每次调用该方法时，都会检查缓存以查看调用是否已经执行并且不必重复执行。尽管在大多数情况下，仅声明一个缓存，但注解可指定多个名称，以便使用多个缓存。在这种情况下，在执行方法之前检查每个缓存-如果命中了至少一个缓存，则返回关联的值。

> 即使未实际执行缓存的方法，所有其他不包含该值的缓存也会被更新。

下面的例子在 `findBook` 方法上使用 `@Cacheable` 注解：

```java
@Cacheable({"books", "isbns"})
public Book findBook(ISBN isbn) {...}
```

##### 默认 Key 生成

由于缓存本质上是键值存储，因此每次调用缓存方法都需要转换为适合缓存访问的键。缓存抽象使用基于以下算法的简单 `KeyGenerator`：

- 如果未提供任何参数，则返回 `SimpleKey.EMPTY`。

- 如果仅给出一个参数，则返回该实例。

- 如果给出了一个以上的参数，则返回包含所有参数的 `SimpleKey`。

只要参数具有自然键并实现有效的 `hashCode()` 和 `equals()` 方法，该方法就适用于大多数场景。如果不是这种情况，则需要更改策略。

为了提供不同的默认键生成器，你需要实现 `org.springframework.cache.interceptor.KeyGenerator` 接口。

> 随着 Spring 4.0 的发布，默认的键生成策略发生了变化。Spring 的早期版本使用了键生成策略，该策略对于多个关键参数仅考虑参数的 `hashCode()` 而不考虑 `equals()`。这可能会导致意外的键冲突（有关背景，请参见 [SPR-10237](https://jira.spring.io/browse/SPR-10237)）。新的 `SimpleKeyGenerator` 在这种情况下使用复合键。
>
> 如果您想继续使用以前的键生成策略，则可以配置已弃用的 `org.springframework.cache.interceptor.DefaultKeyGenerator` 类或创建基于哈希的自定义 `KeyGenerator` 实现。

##### 自定义 Key 生成声明

由于缓存是通用的，因此目标方法很可能具有各种签名，这些签名无法轻易映射到缓存结构顶部。当目标方法具有多个参数时，只有其中一些参数适合缓存（而其余参数仅由方法逻辑使用），这往往会变得很明显。考虑以下示例：

```java
@Cacheable("books")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

乍一看，虽然两个 `boolean` 参数会影响书的查找方式，但它们对缓存没有用处。此外，如果两者中只有一个重要而另一个不重要怎么办？

对于这种情况，可以通过`@Cacheable` 注解指定如何通过其 `key` 属性生成密钥。 您可以使用 [SpEL](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions) 选择感兴趣的参数（或其嵌套属性） ），执行操作甚至调用任意方法，而无需编写任何代码或实现任何接口。相对于 [默认生成器](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-annotations-cacheable-default-key) ，更推荐这种方式。因为随着代码库的增长，方法的签名趋向于完全不同。虽然默认策略可能适用于某些方法，但很少适用于所有方法。

下面的例子展示了各种 SpEL 声明（如果你还不熟悉 SpEL ，参考 [Spring Expression Language](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions)）：

```java
@Cacheable(cacheNames="books", key="#isbn")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)

@Cacheable(cacheNames="books", key="#isbn.rawNumber")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)

@Cacheable(cacheNames="books", key="T(someType).hash(#isbn)")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

前面的代码片段显示了选择某个参数，其属性之一甚至是任意（静态）方法是多么简单。

如果负责生成键的算法过于具体或需要共享，则可以在操作上定义一个自定义的 `keyGenerator`。为此，请指定要使用的 `KeyGenerator` bean实现的名称，如以下示例所示：

```java
@Cacheable(cacheNames="books", keyGenerator="myKeyGenerator")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

> `key` 和 `keyGenerator` 参数是互斥的，同时指定这两个参数的操作将导致异常。

##### 默认缓存解析

缓存抽象使用一个简单的 `CacheResolver`，通过使用配置的 `CacheManager` 来检索在操作级别定义的缓存。

要提供其他默认的缓存解析器，您需要实现 `org.springframework.cache.interceptor.CacheResolver` 接口。

##### 自定义缓存解析

默认的缓存解析非常适合与单个 `CacheManager` 一起使用且对复杂的缓存解析没有要求的应用程序。

对于使用多个缓存管理器的应用程序，可以将 `cacheManager` 设置为用于每个操作，如以下示例所示：

```java
@Cacheable(cacheNames="books", cacheManager="anotherCacheManager") 
public Book findBook(ISBN isbn) {...}
```

您还可以完全按照替换 [缓存 key 生成](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-annotations-cacheable-key) 的方式完全替换 `CacheResolver`。每个缓存操作都需要解析，让实现实际上可以根据运行时参数来解析要使用的缓存。以下示例显示了如何指定 `CacheResolver`：

```java
@Cacheable(cacheResolver="runtimeCacheResolver") 
public Book findBook(ISBN isbn) {...}
```

> 从Spring 4.1开始，缓存注解的 `value` 属性不再是必需的，因为 `CacheResolver` 可以提供该特定信息，而与注解的内容无关。
>
> 与 `key` 和 `keyGenerator` 类似，`cacheManager` 和 `cacheResolver` 参数是互斥的，并且同时指定这两个参数的操作将导致异常。因为自定义 `CacheManager` 被 `CacheResolver` 实现忽略。这可能不是您所期望的。

##### 同步缓存

在多线程环境中，某些操作可能被使用相同的参数并发调用（典型地在启动阶段）。默认地，缓存抽象不会锁定任何东西，同一个值可能被计算很多次，这就与缓存的目标背道而驰。

对这些特殊场景，你可以使用 `sync` 属性来构建底层缓存提供者来锁定缓存数据实体，当同一个值被重复计算时。作为结果，只有一个线程忙于计算需要缓存的值，同时其他线程都会阻塞到缓存中的该数据实体被更新。下面的例子展示了如何使用 `sync` 属性：

```java
@Cacheable(cacheNames="foos", sync=true) 
public Foo executeExpensiveOperation(String id) {...}
```

> 这是一个可选特性，你喜欢的缓存类库可能不支持。核心框架提供的所有的 `CacheManager` 实现都支持该特性。参考你的缓存提供者文档获取更多细节。

##### 条件缓存

有时候，一个方法并不是始终都适合被缓存（比如，可能依赖于给定的参数）。缓存注解通过 `condition` 参数支持该功能，携带一个 `SpEL` 表达式，该表达式可以被解析为 `true` 或者 `false` 。如果是 `true` ，该方法将被缓存。否者，该方法的行为就会如同没有被缓存一样（也就是说，该方法每次都会执行，无论结果是否被缓存或者使用何种参数）。例如，下面的方法只有当 `name` 参数长度小于 32 时才会被缓存：

```java
@Cacheable(cacheNames="book", condition="#name.length() < 32") 
public Book findBook(String name)
```

除了 `condition` 参数，你还可以使用 `unless` 参数来阻止值被添加到缓存中。与 `condition` 不同，`unless` 表达式在方法被调用之后才会被解析。扩展上面的例子，可能我们只想要缓存平装书，如下面例子所示：

```java
@Cacheable(cacheNames="book", condition="#name.length() < 32", unless="#result.hardback") 
public Book findBook(String name)
```

缓存抽象支持 `java.util.Optional` ，如果它的内容存在，就会作为被缓存的值。`#result` 始终指向业务实体，而不是任何支持的包装器，因此，上面的例子可以写成：

```java
@Cacheable(cacheNames="book", condition="#name.length() < 32", unless="#result?.hardback")
public Optional<Book> findBook(String name)
```

注意，`result` 仍然指向 `Book` 而不是 `Optional` 。因为它可能是 `null` ，我们应该使用安全的导航操作。

##### 可用的缓存 SpEL 解析上下文

每个 `SpEL` 表达式都是针对专门的 [`上下文`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions-language-ref) 解析。除了内建参数，框架提供了专门的缓存相关的元数据，比如参数名称。下面的表格描述了可用于上下文的元素，你可以使用它们进行关键或者条件计算：

| Name          | Location           | Description                                                  | Example                                                      |
| :------------ | :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `methodName`  | Root object        | 被调用方法的名称                                             | `#root.methodName`                                           |
| `method`      | Root object        | 被调用的方法                                                 | `#root.method.name`                                          |
| `target`      | Root object        | 被调用的目标对象                                             | `#root.target`                                               |
| `targetClass` | Root object        | 被调用的目标的类型                                           | `#root.targetClass`                                          |
| `args`        | Root object        | 用于调用目标的参数（作为数组）                               | `#root.args[0]`                                              |
| `caches`      | Root object        | 执行当前方法的缓存的集合                                     | `#root.caches[0].name`                                       |
| Argument name | Evaluation context | 任何方法参数的名称。如果名称不可用（可能是由于没有调试信息），则参数名称也可以在 `#a <#arg>` 下使用，其中 `#arg` 代表参数索引（从 `0` 开始）。 | `#iban` or `#a0` (you can also use `#p0` or `#p<#arg>` notation as an alias). |
| `result`      | Evaluation context | 方法调用的结果（要缓存的值）。仅在 `unless` 表达式，`cache put` 表达式（用于计算 `key`）或`cache evict`表达式（`beforeInvocation` 为 `false` 时）中可用。对于支持的包装器（例如 `Optional`），`#result` 是指实际对象，而不是包装器。 | `#result`                                                    |

#### 8.2.2.  `@CachePut` 注解

当需要在不影响方法执行的情况下更新缓存时，可以使用 `@CachePut` 注解。也就是说，该方法总是被执行，其结果被放入缓存（根据 `@CachePut` 选项）。它支持与 `@Cacheable` 相同的选项，应该用于缓存填充，而不是方法流优化。以下示例使用了 `@CachePut` 注解：

```java
@CachePut(cacheNames="book", key="#isbn")
public Book updateBook(ISBN isbn, BookDescriptor descriptor)
```

> 强烈建议不要在同一方法上使用 `@CachePut` 和 `@Cacheable` 注解，因为它们的行为不同。后者导致通过使用缓存跳过方法执行，而前者则强制执行以便执行缓存更新。这会导致意外的行为，并且，除了特定的极端情况（例如具有互斥条件的注解）外，应避免此类声明。还要注意，这样的条件不应依赖于结果对象（即 `#result` 变量），因为这些条件已预先进行验证以确认排除。

#### 8.2.3.  `@CacheEvict` 注解

缓存抽象不仅允许缓存存储的填充，还允许逐出。此过程对于从缓存中删除陈旧或未使用的数据很有用。与 `@Cacheable` 相反，`@CacheEvict` 区分执行高速缓存逐出的方法（即，用作触发从高速缓存中删除数据的触发器的方法）。与它的同级类似，`@CacheEvict` 需要指定一个或多个受操作影响的缓存，允许自定义缓存和键解析或条件，并指定一个额外的参数（`allEntries`）来指示是否 需要执行缓存范围内的逐出，而不仅仅是条目逐出（基于键）。以下示例将所有 `books` 缓存中的条目逐出：

```java
@CacheEvict(cacheNames="books", allEntries=true) 
public void loadBooks(InputStream batch)
```

当需要清除整个缓存区域时，此选项非常有用。如前面的示例所示，而不是逐出每个条目（这会花费很长时间，因为效率很低），而是一次操作删除所有条目。请注意，该框架会忽略此方案中指定的任何键，因为它不适用（整个高速缓存被驱逐，而不仅仅是一个条目）。

您还可以通过使用 `beforeInvocation` 属性指示驱逐应该发生在方法执行之后还是在方法执行之前（默认是方法执行之后）。前者提供与其余注解相同的语义：方法成功完成后，将对缓存执行操作（在这种情况下为逐出）。 如果该方法未执行（可能已被缓存）或引发了异常，则不会发生驱逐。后者（`beforeInvocation=true`）导致逐出总是在调用该方法之前发生。在不需要将逐出与方法结果联系在一起的情况下，这很有用。

注意，`void` 方法可以与 `@CacheEvict` 一起使用－因为这些方法充当触发器，所以返回值将被忽略（因为它们不与缓存交互）。这不同于 `@Cacheable` 的情况，它会向缓存中添加或更新数据，因此需要结果。

#### 8.2.4.  `@Caching` 注解

有时，需要指定相同类型的多个注解（例如，`@CacheEvict` 或 `@CachePut`），例如，因为不同缓存之间的条件或键表达式不同。`@Caching` 可以在同一方法上使用多个嵌套的 `@Cacheable`，`@CachePut` 和 `@CacheEvict` 注解。以下示例使用了两个 `@CacheEvict` 注解：

```java
@Caching(evict = { @CacheEvict("primary"), @CacheEvict(cacheNames="secondary", key="#p0") })
public Book importBooks(String deposit, Date date)
```

#### 8.2.5.  `@CacheConfig` 注解

到目前为止，我们已经看到缓存操作提供了许多自定义选项，并且您可以为每个操作设置这些选项。但是，如果某些自定义选项适用于该类的所有操作，则配置它们可能很繁琐。 、例如，指定用于类的每个高速缓存操作的高速缓存的名称可以由单个类级定义代替。这就是 `@CacheConfig` 起作用的地方。以下示例使用 `@CacheConfig` 设置缓存的名称：

```java
@CacheConfig("books") 
public class BookRepositoryImpl implements BookRepository {

    @Cacheable
    public Book findBook(ISBN isbn) {...}
}
```

`@CacheConfig` 是一个类级别的注解，它允许共享缓存名称，自定义的 `KeyGenerator`，自定义的 `CacheManager` 和自定义的 `CacheResolver`。将此注解放在类上不会打开任何缓存操作。

操作级别的自定义始终会覆盖在 `@CacheConfig` 上的设置。因此，这为每个高速缓存操作提供了三个定制级别：

- 全局配置，可用于 `CacheManager`，`KeyGenerator`。

- 在类级别，使用 `@CacheConfig`。

- 在操作级别。

#### 8.2.6. 启用缓存注解

重要的是要注意，仅仅声明缓存注解不会自动触发其动作－就像 Spring 中的许多事情一样，必须声明性地启用该功能（这意味着如果您怀疑缓存是罪魁祸首，则可以通过删除仅一个配置行来禁用它，而不是代码中的所有注解）。

要启用缓存注解，请将注解 `@EnableCaching` 添加到您的 `@Configuration` 类之一：

```java
@Configuration
@EnableCaching
public class AppConfig {
}
```

另外，对于 XML 配置，可以使用 `cache:annotation-driven` 元素：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:cache="http://www.springframework.org/schema/cache"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/cache https://www.springframework.org/schema/cache/spring-cache.xsd">

        <cache:annotation-driven/>
</beans>
```

通过 `cache:annotation-driven` 元素和 `@EnableCaching` 注解，您都可以指定各种选项，这些选项影响通过 AOP 将缓存行为添加到应用程序的方式。该配置与 [`@Transactional`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-annotation-driven-settings) 类似。

> 处理缓存注解的默认增强模式是 `proxy`，它仅允许通过代理来拦截调用。同一类内的本地调用无法以这种方式被拦截。对于更高级的拦截模式，请考虑结合编译时或加载时编织切换到 `aspectj` 模式。

> 有关实现 `CachingConfigurer` 需要的高级自定义（使用 Java 配置）的更多细节，参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) 。

| XML Attribute        | Annotation Attribute                                         | Default                                                      | Description                                                  |
| :------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `cache-manager`      | N/A (see the [`CachingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) javadoc) | `cacheManager`                                               | 要使用的缓存管理器的名称。默认的 `CacheResolver` 是在后台使用此缓存管理器初始化的（如果未设置，则初始化为 ` cacheManager`）。为了更精细地管理缓存粒度，请考虑设置 `cache-resolver` 属性。 |
| `cache-resolver`     | N/A (see the [`CachingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) javadoc) | A `SimpleCacheResolver` using the configured `cacheManager`. | 用来解析后备缓存的 `CacheResolver` 的 bean 名称。此属性不是必需的，仅需指定为 `cache-manager` 属性的替代方法。 |
| `key-generator`      | N/A (see the [`CachingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) javadoc) | `SimpleKeyGenerator`                                         | 要使用的定制 key 生成器的名称。                              |
| `error-handler`      | N/A (see the [`CachingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html) javadoc) | `SimpleCacheErrorHandler`                                    | 要使用的自定义缓存错误处理程序的名称。默认情况下，在与缓存相关的操作期间抛出的所有异常都将返回给客户端。 |
| `mode`               | `mode`                                                       | `proxy`                                                      | 默认模式（`proxy`）使用 Spring 的 AOP 框架处理带注解的 bean（要遵循的代理语义，如前所述，仅适用于通过代理传入的方法调用）。相反，替代模式（`aspectj`）使用 Spring 的 AspectJ 缓存切面来编织受影响的类，修改目标类字节码以应用于任何类型的方法调用。AspectJ 编织需要在类路径中启用 `spring-aspects.jar`，并启用加载时编织（或编译时编织）。（有关如何操作的详细信息，请参见 [Spring配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-aj-ltw-spring) 了解如何设置加载时编织。） |
| `proxy-target-class` | `proxyTargetClass`                                           | `false`                                                      | 仅适用于代理模式。控制为使用 `@Cacheable` 或 `@CacheEvict`  注解修饰的类创建哪种类型的缓存代理。如果将 `proxy-target-class` 属性设置为 `true` ，则会创建基于类的代理。如果 `proxy-target-class` 为 `false` 或省略该属性，则创建基于标准 JDK 接口的代理。 （有关不同代理类型的详细检查，请参阅 [代理机制](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-proxying) ） |
| `order`              | `order`                                                      | Ordered.LOWEST_PRECEDENCE                                    | 定义应用于用 `@Cacheable` 或 `@CacheEvict` 注解修释的 bean 的缓存增强的顺序。（有关 AOP 增强排序有关的规则的更多信息，请参阅 [Advice Ordering](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop -ataspectj-advice-ordering) 。没有指定的顺序意味着 AOP 子系统确定增强的顺序。 |

> `<cache：annotation-driven />` 仅在定义了它的相同应用程序上下文中的 bean 上查找 `@Cacheable/@CachePut/@CacheEvict/@Caching`。这意味着，如果将 `<cache:annotation-driven/>` 放在 `WebApplicationContext` 中以作为 `DispatcherServlet`，它将仅在控制器中检查 bean，而不在服务中进行检查。有关更多信息，请参见 [MVC部分](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-servlet) 。

> 方法可见性和缓存注解
>
> 使用代理时，应仅将缓存注解应用于具有公共可见性的方法。如果使用这些注解对受保护的，私有的或程序包可见的方法进行修饰，则不会引发错误，但是带注解的方法不会显示已配置的缓存设置。如果您需要注解非公共方法，请考虑使用 AspectJ（请参阅本节的其余部分），因为它会更改字节码本身。

> Spring 建议您仅使用 `@Cache*` 注解对具体类（以及具体类的方法）进行修饰，而不是对接口进行修饰。您当然可以在接口（或接口方法）上放置 `@Cache*` 注解，但这仅在您使用基于接口的代理时才可以使用。Java 注解不是从接口继承的事实意味着，如果您使用基于类的代理（`proxy-target-class="true"`）或基于编织的方面（`mode="aspectj"`），则代理和编织基础结构无法识别缓存设置，并且该对象也不会包装在缓存代理中。

> 在代理模式（默认）下，仅拦截通过代理传入的外部方法调用。这意味着即使调用的方法标记有 `@Cacheable`，自调用（实际上是目标对象中的方法调用目标对象的另一种方法）也不会导致运行时实际缓存。在这种情况下，请考虑使用 `aspectj` 模式。另外，必须完全初始化代理以提供预期的行为，因此您不应在初始化代码（即 `@PostConstruct`）中依赖此功能。

#### 8.2.7. 使用自定义注解

> 自定义注解和 AspectJ
>
> 该功能仅适用于基于代理的方法，但可以通过使用 AspectJ 进行一些额外的工作来启用。
>
> `spring-aspects` 模块仅为标准注解定义了一个方面。如果定义了自己的注解，则还需要为其定义一个方面。查看作为示例的 `AnnotationCacheAspect` 。

缓存抽象使您可以使用自己的注解来标识触发缓存填充或逐出的方法。作为模板机制，这非常方便，因为它消除了重复缓存注解声明的需求，如果指定了键或条件，或代码库中不允许外部导入（`org.springframework`），则这特别有用。与 [stereotype](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-stereotype-annotations) 注解的其余部分类似，您可以将 `@Cacheable`，`@CachePut`，`@CacheEvict` 和 `@CacheConfig` 用作 [元注解](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-meta-annotations)（即可以注释其他注解的注解）。在以下示例中，我们用自己的自定义注解替换了通用的 `@Cacheable` 声明：

```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.METHOD})
@Cacheable(cacheNames="books", key="#isbn")
public @interface SlowService {
}
```

在前面的示例中，我们定义了自己的 `SlowService` 注解，该注解本身以 `@Cacheable` 注解修饰。现在我们可以替换以下代码：

```java
@Cacheable(cacheNames="books", key="#isbn")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

以下示例显示了自定义注解，我们可以用其替换前面的代码：

```java
@SlowService
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

即使 `@SlowService` 不是 Spring 注解，容器也会在运行时自动获取其声明并理解其含义。请注意，如 [前文](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-annotation-enable) 所述，注解驱动的行为需要被启用。

### 8.3. JCache (JSR-107) 注解

从 4.1 版开始，Spring 的缓存抽象完全支持 JCache 标准注解：`@CacheResult`，`@CachePut`，`@CacheRemove` 和 `@CacheRemoveAll` 以及 `@CacheDefaults`，`@CacheKey` 和 `@CacheValue` 。您甚至可以在不将缓存存储迁移到 JSR-107 的情况下使用这些注解。内部实现使用 Spring 的缓存抽象，并提供符合规范的默认 `CacheResolver` 和 `KeyGenerator` 实现。换句话说，如果您已经在使用 Spring 的缓存抽象，则可以切换到这些标准注解，而无需更改缓存存储（或配置）。

#### 8.3.1. 特性综述

对于那些熟悉 Spring 缓存注解的人，下表描述了 Spring 注解与 JSR-107 对应体之间的主要区别：

| Spring                         | JSR-107           | Remark                                                       |
| :----------------------------- | :---------------- | :----------------------------------------------------------- |
| `@Cacheable`                   | `@CacheResult`    | 相当相似。`@CacheResult` 可以缓存特定的异常并强制执行该方法，而不管缓存的内容如何。 |
| `@CachePut`                    | `@CachePut`       | 当 Spring 使用方法调用的结果更新缓存时，JCache 要求将其作为参数传递给它，并使用 `@CacheValue` 注解。由于存在这种差异，JCache 允许在实际方法调用之前或之后更新缓存。 |
| `@CacheEvict`                  | `@CacheRemove`    | 相当相似。当方法调用导致异常时， `@CacheRemove` 支持条件驱逐。 |
| `@CacheEvict(allEntries=true)` | `@CacheRemoveAll` | 参考 `@CacheRemove`。                                        |
| `@CacheConfig`                 | `@CacheDefaults`  | 让您以类似的方式配置相同的概念。                             |

JCache 的概念是 `javax.cache.annotation.CacheResolver`，与 Spring 的 `CacheResolver` 接口相同，只是 JCache 仅支持单个缓存。默认情况下，一个简单的实现根据注解中声明的名称检索要使用的缓存。应该注意的是，如果注解中未指定缓存名称，则会自动生成一个默认值。有关更多信息，请参见 `@CacheResult#cacheName()` 的 javadoc。

`CacheResolver` 实例由 `CacheResolverFactory` 检索。可以为每个缓存操作自定义工厂，如以下示例所示：

```java
@CacheResult(cacheNames="books", cacheResolverFactory=MyCacheResolverFactory.class) 
public Book findBook(ISBN isbn)
```

> 对于所有引用的类，Spring 尝试查找具有给定类型的 bean。如果存在多个匹配项，则创建一个新实例，并可以使用常规 bean 生命周期回调，例如依赖项注入。

Key 是由 `javax.cache.annotation.CacheKeyGenerator` 生成的，其目的与 Spring 的 `KeyGenerator` 相同。默认情况下，所有方法参数都被考虑在内，除非至少一个参数用 `@CacheKey` 注解修饰。这类似于 Spring 的 [自定义 key 生成声明](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#cache-annotations-cacheable-key) 。例如，以下是相同的操作，一个使用 Spring 的抽象，另一个使用 JCache：

```java
@Cacheable(cacheNames="books", key="#isbn")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)

@CacheResult(cacheName="books")
public Book findBook(@CacheKey ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```

您也可以在操作上指定 `CacheKeyResolver`，类似于指定 `CacheResolverFactory` 的方法。

JCache 可以管理带注解的方法引发的异常。这样可以防止更新缓存，但是也可以将异常缓存为失败的指示，而不必再次调用该方法。假设如果 ISBN 的结构无效，则抛出 `InvalidIsbnNotFoundException`。这是一个永久性的失败（使用这样的参数无法检索任何书籍）。以下内容缓存了该异常，以便使用相同的无效 ISBN 进行的进一步调用直接引发该缓存的异常，而不是再次调用该方法：

```java
@CacheResult(cacheName="books", exceptionCacheName="failures"
            cachedExceptions = InvalidIsbnNotFoundException.class)
public Book findBook(ISBN isbn)
```

#### 8.3.2. 启用 JSR-107 支持

除了启用 Spring 的声明性注解支持外，您无需执行任何其他操作即可启用 JSR-107 支持。如果类路径中同时存在 JSR-107 API 和 `spring-context-support` 模块，则 `@EnableCaching` 和 `cache:annotation-driven` 元素都会自动启用 JCache 支持。

> 根据您的使用场景，选择基本上由您来做。您甚至可以通过在某些服务器上使用 JSR-107 API 并在其他服务器上使用 Spring 自己的注解来混合和匹配服务。但是，如果这些服务影响相同的缓存，则应使用一致且相同的 key 生成实现。

### 8.4. 基于 XML 的声明式缓存

如果无法使用注解（可能是由于无法访问源代码或没有外部代码），则可以使用 XML 进行声明式缓存。因此，您可以从外部指定目标方法和缓存指令，而不是注解用于缓存的方法（类似于声明式事务管理 [advice](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-first-example) ）。上一节中的示例可以转换为以下示例：

```xml
<!-- the service we want to make cacheable -->
<bean id="bookService" class="x.y.service.DefaultBookService"/>

<!-- cache definitions -->
<cache:advice id="cacheAdvice" cache-manager="cacheManager">
    <cache:caching cache="books">
        <cache:cacheable method="findBook" key="#isbn"/>
        <cache:cache-evict method="loadBooks" all-entries="true"/>
    </cache:caching>
</cache:advice>

<!-- apply the cacheable behavior to all BookService interfaces -->
<aop:config>
    <aop:advisor advice-ref="cacheAdvice" pointcut="execution(* x.y.BookService.*(..))"/>
</aop:config>

<!-- cache manager definition omitted -->
```

在前面的配置中，`bookService` 被设置为可缓存的。要应用的缓存语义封装在 `cache:advice` 定义中，这将导致使用 `findBooks` 方法将数据放入缓存，并使用 `loadBooks` 方法将数据逐出。两种定义都针对 `books` 缓存。

`aop:config` 定义通过使用 AspectJ 切入点表达式将缓存建议应用于程序中的适当点（有关更多信息，请参见[使用 Spring 进行面向方面的编程](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) ）。在前面的示例中，考虑了 `BookService` 中的所有方法，并将缓存增强应用于它们。

声明式 XML 缓存支持所有基于注解的模型，因此在两者之间切换应该相当容易。此外，两者都可以在同一应用程序内使用。基于 XML 的方法不会涉及目标代码。但是，它本质上比较冗长。当处理具有用于缓存的重载方法的类时，确定正确的方法确实需要付出额外的努力，因为 `method` 参数不是很好的判别器。在这些情况下，您可以使用 AspectJ 切入点来挑选目标方法并应用适当的缓存功能。但是，通过 XML，更容易应用程序包或组或接口范围的缓存（同样由于 AspectJ 切入点的缘故）和创建类似模板的定义（如我们在前面的示例中那样，通过 `cache:definitions` 的 `cache` 属性）。

### 8.5. 配置缓存存储

缓存抽象提供了几个存储集成选项。要使用它们，您需要声明一个适当的 `CacheManager`（一个控制和管理 `Cache` 实例的实体，可用于检索这些实例以进行存储）。

#### 8.5.1. 基于 JDK `ConcurrentMap` 的缓存

The JDK-based `Cache` implementation resides under `org.springframework.cache.concurrent` package. It lets you use `ConcurrentHashMap` as a backing `Cache` store. The following example shows how to configure two caches:

```xml
<!-- simple cache manager -->
<bean id="cacheManager" class="org.springframework.cache.support.SimpleCacheManager">
    <property name="caches">
        <set>
            <bean class="org.springframework.cache.concurrent.ConcurrentMapCacheFactoryBean" p:name="default"/>
            <bean class="org.springframework.cache.concurrent.ConcurrentMapCacheFactoryBean" p:name="books"/>
        </set>
    </property>
</bean>
```

上面的代码片段使用 `SimpleCacheManager` 为两个嵌套的名为 `default` 和 `books` 的 `ConcurrentMapCache` 实例创建 `CacheManager`。请注意，名称是直接为每个缓存配置的。

由于缓存是由应用程序创建的，因此绑定到其生命周期，使其适合于基本应用场景，测试或简单的应用程序。缓存可以很好地扩展并且非常快，但是它不提供任何管理，持久性功能或驱逐契约。

#### 8.5.2. 基于 Ehcache 的缓存

> Ehcache 3.x 完全符合 JSR-107，并且不需要专用支持。

Ehcache 2.x 实现位于 `org.springframework.cache.ehcache` 包中。同样，要使用它，您需要声明适当的 `CacheManager`。以下示例显示了如何执行此操作：

```xml
<bean id="cacheManager"
        class="org.springframework.cache.ehcache.EhCacheCacheManager" p:cache-manager-ref="ehcache"/>

<!-- EhCache library setup -->
<bean id="ehcache"
        class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean" p:config-location="ehcache.xml"/>
```

这个设置在 Spring IoC 内部引导 ehcache 库（通过 `ehcache` bean），然后将其连接到专用的 `CacheManager` 实现中。注意，整个特定于 Ehcache 的配置是从 `ehcache.xml` 中读取的。

#### 8.5.3. Caffeine 缓存

Caffeine 是 Java 8 对 Guava 缓存的重写，其实现位于 `org.springframework.cache.caffeine` 包中，并提供对 Caffeine 多个功能的访问。

以下示例配置了一个 `CacheManager`，可根据需要创建缓存：

```xml
<bean id="cacheManager"
        class="org.springframework.cache.caffeine.CaffeineCacheManager"/>
```

您还可以显式提供要使用的缓存。在这种情况下，只有那些缓存被管理器认为是可用的。以下示例显示了如何执行此操作：

```xml
<bean id="cacheManager" class="org.springframework.cache.caffeine.CaffeineCacheManager">
    <property name="caches">
        <set>
            <value>default</value>
            <value>books</value>
        </set>
    </property>
</bean>
```

Caffeine `CacheManager` 也支持自定义 `Caffeine` 和 `CacheLoader`。更多信息，参见 [Caffeine 文档](https://github.com/ben-manes/caffeine/wiki) 。

#### 8.5.4. 基于 GemFire 的缓存

GemFire 是面向内存，磁盘支持，弹性可伸缩，连续可用，活动（具有内置的基于模式的订阅通知），全局复制的数据库，并提供功能齐全的边缘缓存。有关如何将 GemFire 用作 `CacheManager`（以及更多）的更多信息，请参见 [Spring Data GemFire 参考文档](https://docs.spring.io/spring-gemfire/docs/current/reference/html/ ) 。

#### 8.5.5. JSR-107 缓存

Spring 的缓存抽象也可以使用符合 JSR-107 的缓存。JCache 实现位于 `org.springframework.cache.jcache` 包中。

同样，要使用它，您需要声明适当的 `CacheManager`。以下示例显示了如何执行此操作：

```xml
<bean id="cacheManager"
        class="org.springframework.cache.jcache.JCacheCacheManager"
        p:cache-manager-ref="jCacheManager"/>

<!-- JSR-107 cache manager setup  -->
<bean id="jCacheManager" .../>
```

#### 8.5.6. 在没有后备存储的情况下处理缓存

有时，在切换环境或进行测试时，您可能具有缓存声明而未配置实际的后备缓存。由于这是无效的配置，因此在运行时会抛出异常，因为缓存基础设施无法找到合适的存储。在这种情况下，可以连接一个简单的伪缓存，该缓存不执行任何缓存操作，而不是删除缓存声明（这可能很乏味），也就是说，它强制每次执行缓存的方法。以下示例显示了如何执行此操作：

```xml
<bean id="cacheManager" class="org.springframework.cache.support.CompositeCacheManager">
    <property name="cacheManagers">
        <list>
            <ref bean="jdkCache"/>
            <ref bean="gemfireCache"/>
        </list>
    </property>
    <property name="fallbackToNoOpCache" value="true"/>
</bean>
```

前面的 `CompositeCacheManager` 链接了多个 `CacheManager` 实例，并通过 `fallbackToNoOpCache` 标志为未配置的缓存管理器处理的所有定义添加无操作缓存。也就是说，在 `jdkCache` 或 `gemfireCache`（在示例中之前配置）中都找不到的每个缓存定义都由无操作缓存处理，该缓存不存储任何信息，导致每次执行目标方法。

### 8.6. 插入不同的后端缓存

显然，有很多缓存产品可以用作后备存储。要插入它们，您需要提供一个 `CacheManager` 和一个 `Cache` 实现，因为不幸的是，没有可用的标准可供我们使用。这听起来可能比实际要难，因为在实践中，这些类通常是简单的 [adapters](https://en.wikipedia.org/wiki/Adapter_pattern) ，它们将缓存抽象框架映射到存储 API 的顶部， 就像 `ehcache` 类一样。大多数 `CacheManager` 类都可以使用 `org.springframework.cache.support` 包中的类（例如 `AbstractCacheManager`，它负责样板代码，仅保留实际的映射）。我们希望，及时提供与 Spring 集成的库可以弥补这一小小的配置空白。

### 8.7. 如何设置 TTL / TTI /驱逐策略/ XXX 功能？

直接通过您的缓存提供程序。缓存抽象是一种抽象，而不是缓存实现。您使用的解决方案可能支持其他解决方案不支持的各种数据策略和不同的拓扑（例如，JDK `ConcurrentHashMap` －暴露在缓存抽象中将是无用的，因为没有后备支持）。此类功能应通过后备缓存（配置时）或通过其本地 API 直接控制。

