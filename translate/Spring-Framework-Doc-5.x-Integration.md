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

