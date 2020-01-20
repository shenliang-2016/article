#### 4.11.8. LDAP

[LDAP](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol) （轻量级目录访问协议）是一种开源的，与供应商无关的行业标准应用协议，用于通过 IP 网络访问和维护分布式目录信息服务。Spring Boot 从 [UnboundID](https://www.ldap.com/unboundid-ldap-sdk-for-java) 为任何兼容的 LDAP 服务器提供自动配置，并支持嵌入式内存 LDAP 服务器。

LDAP 抽象由 [Spring Data LDAP](https://github.com/spring-projects/spring-data-ldap) 提供。有一个 `spring-boot-starter-data-ldap` “Starter”，用于以方便的方式收集依赖项。

##### 连接 LDAP 服务器

要连接到 LDAP 服务器，请确保您声明对 `spring-boot-starter-data-ldap` “Starter” 或 `spring-ldap-core` 的依赖，然后在 `application.properties` 中声明服务器的 URL，如以下示例所示：

```properties
spring.ldap.urls=ldap://myserver:1235
spring.ldap.username=admin
spring.ldap.password=secret
```

如果您需要自定义连接设置，则可以使用 `spring.ldap.base` 和 `spring.ldap.base-environment` 属性。

将基于这些设置自动配置 `LdapContextSource`。如果您需要对其进行自定义（例如使用 `PooledContextSource`），则仍可以注入自动配置的 `LdapContextSource`。确保将自定义的 `ContextSource` 标记为 `@Primary`，以便自动配置的 `LdapTemplate` 使用它。

##### Spring Data LDAP Repositories

Spring Data 包括对 LDAP 的存储库支持。有关 Spring Data LDAP 的完整详细信息，请参考 [参考文档](https://docs.spring.io/spring-data/ldap/docs/1.0.x/reference/html/)。

您还可以像使用其他任何 Spring Bean 一样注入自动配置的 `LdapTemplate` 实例，如以下示例所示：

```java
@Component
public class MyBean {

    private final LdapTemplate template;

    @Autowired
    public MyBean(LdapTemplate template) {
        this.template = template;
    }

    // ...

}
```

##### 嵌入式内存 LDAP 服务器

出于测试目的，Spring Boot 支持从 [UnboundID](https://www.ldap.com/unboundid-ldap-sdk-for-java) 自动配置内存中的 LDAP 服务器。要配置服务器，请向 `com.unboundid：unboundid-ldapsdk` 添加一个依赖项，并声明一个 `spring.ldap.embedded.base-dn` 属性，如下所示：

```properties
spring.ldap.embedded.base-dn=dc=spring,dc=io
```

> 可以定义多个 base-dn 值，但是，由于专有名称通常包含逗号，因此必须使用正确的符号进行定义。在 yaml 文件中，可以使用 yaml 列表符号：
>
> ````yaml
> spring.ldap.embedded.base-dn:
> 	- dc=spring,dc=io
> 	- dc=pivotal,dc=io
> ````
>
> 在 properties 文件中，您必须将索引作为属性名称的一部分包括在内：
>
> ````properties
> spring.ldap.embedded.base-dn[0]=dc=spring,dc=io
> spring.ldap.embedded.base-dn[1]=dc=pivotal,dc=io
> ````

默认情况下，服务器在随机端口上启动并触发常规 LDAP 支持。无需指定 `spring.ldap.urls` 属性。

如果您的类路径中有一个 `schema.ldif` 文件，则该文件用于初始化服务器。如果您想从其他资源加载初始化脚本，也可以使用 `spring.ldap.embedded.ldif` 属性。

默认情况下，使用标准架构来验证 `LDIF` 文件。您可以通过设置 `spring.ldap.embedded.validation.enabled` 属性来完全关闭验证。如果您具有自定义属性，则可以使用 `spring.ldap.embedded.validation.schema` 来定义您的自定义属性类型或对象类。

