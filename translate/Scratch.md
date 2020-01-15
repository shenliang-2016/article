#### 4.9.4. SAML 2.0

##### Relying Party

如果您在类路径中具有 `spring-security-saml2-service-provider`，则可以利用一些自动配置功能来轻松设置 SAML 2.0 Relying Party。该配置利用了 `Saml2RelyingPartyProperties` 下的属性。

Relying Party 注册代表身份提供商 IDP 和服务提供商 SP 之间的配对配置。您可以在 `spring.security.saml2.relyingparty` 前缀下注册多个 Relying Party，如以下示例所示：

```properties
spring.security.saml2.relyingparty.registration.my-relying-party1.signing.credentials[0].private-key-location=path-to-private-key
spring.security.saml2.relyingparty.registration.my-relying-party1.signing.credentials[0].certificate-location=path-to-certificate
spring.security.saml2.relyingparty.registration.my-relying-party1.identityprovider.verification.credentials[0].certificate-location=path-to-verification-cert
spring.security.saml2.relyingparty.registration.my-relying-party1.identityprovider.entity-id=remote-idp-entity-id1
spring.security.saml2.relyingparty.registration.my-relying-party1.identityprovider.sso-url=https://remoteidp1.sso.url

spring.security.saml2.relyingparty.registration.my-relying-party2.signing.credentials[0].private-key-location=path-to-private-key
spring.security.saml2.relyingparty.registration.my-relying-party2.signing.credentials[0].certificate-location=path-to-certificate
spring.security.saml2.relyingparty.registration.my-relying-party2.identityprovider.verification.credentials[0].certificate-location=path-to-other-verification-cert
spring.security.saml2.relyingparty.registration.my-relying-party2.identityprovider.entity-id=remote-idp-entity-id2
spring.security.saml2.relyingparty.registration.my-relying-party2.identityprovider.sso-url=https://remoteidp2.sso.url
```

#### 4.9.5. Actuator 安全

为了安全起见，默认情况下禁用除 `/health` 和 `/info` 外的所有执行器。`management.endpoints.web.exposure.include` 属性可用于启用执行器。

如果 Spring Security 在类路径上，并且不存在其他 `WebSecurityConfigurerAdapter`，则通过 Spring Boot 自动配置保护除 `/health` 和 `/info` 以外的所有执行器。如果您定义了一个自定义的 `WebSecurityConfigurerAdapter`，Spring Boot 的自动配置将退出，您将完全控制执行器访问规则。

> 在设置 `management.endpoints.web.exposure.include` 之前，请确保裸露的执行器不包含敏感信息和/或通过将它们放置在防火墙后面或通过诸如 Spring Security 之类的东西进行保护。

##### 跨站点请求伪造保护

由于 Spring Boot 依赖于 Spring Security 的默认设置，因此 CSRF 保护默认情况下处于启用状态。这意味着，在使用默认安全配置时，需要 `POST`（关闭和记录器端点），`PUT` 或 `DELETE` 的执行器端点将收到 `403` 禁止错误。

> 我们建议仅在创建非浏览器客户端使用的服务时完全禁用 CSRF 保护。

关于 CSRF 保护的其他信息可以在 [Spring Security参考指南](https://docs.spring.io/spring-security/site/docs/5.2.1.RELEASE/reference/htmlsingle/#csrf) 中找到。

