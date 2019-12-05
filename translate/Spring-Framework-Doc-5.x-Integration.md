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
public interface AccountService {

    public void insertAccount(Account account);

    public List<Account> getAccounts(String name);
}
// the implementation doing nothing at the moment
public class AccountServiceImpl implements AccountService {

    public void insertAccount(Account acc) {
        // do something...
    }

    public List<Account> getAccounts(String name) {
        // do something...
    }
}
```

本节首先使用 RMI 将服务公开给远程客户端，然后再谈谈使用 RMI 的缺点。然后继续以使用 Hessian 作为协议的示例。

