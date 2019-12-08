# Integration

Version 5.1.9.RELEASE

----

本参考文档涵盖 Spring 框架与大量 Java EE 以及相关技术的集成技术。

## 1 Spring 的 Remoting 和 Web Services

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

