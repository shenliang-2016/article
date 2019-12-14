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

## 2 Enterprise JavaBeans (EJB) 集成

EJB 好像已经被业界抛弃……

## 3 JMS (Java Message Service)

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
