##### 自动配置的 Data LDAP 测试

你可以使用 `@DataLdapTest` 来测试 LDAP 应用程序。默认情况下，它配置内存嵌入式 LDAP（如果可用），配置 `LdapTemplate`，扫描 `@Entry` 类，并配置 Spring Data LDAP 存储库。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。（有关将 LDAP 与 Spring Boot 结合使用的更多信息，请参阅 [LDAP](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#boot-features-ldap) ）

>  由 `@DataLdapTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

下面的例子展示了 `@DataLdapTest` 注解的使用：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.data.ldap.DataLdapTest;
import org.springframework.ldap.core.LdapTemplate;

@DataLdapTest
class ExampleDataLdapTests {

    @Autowired
    private LdapTemplate ldapTemplate;

    //
}
```

内存嵌入式 LDAP 通常非常适合测试，因为它速度快并且不需要安装任何开发人员。但是，如果您希望针对真实的 LDAP 服务器运行测试，则应排除嵌入式 LDAP 自动配置，如以下示例所示：

```java
import org.springframework.boot.autoconfigure.ldap.embedded.EmbeddedLdapAutoConfiguration;
import org.springframework.boot.test.autoconfigure.data.ldap.DataLdapTest;

@DataLdapTest(excludeAutoConfiguration = EmbeddedLdapAutoConfiguration.class)
class ExampleDataLdapNonEmbeddedTests {

}
```