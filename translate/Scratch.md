### 4.5. 国际化

Spring Boot 支持本地化消息，因此您的应用程序可以迎合不同语言首选项的用户。默认情况下，Spring Boot 在类路径的根目录下查找 `messages` 资源包的存在。

> 当配置的资源包的默认属性文件可用时（即默认情况下为 `messages.properties`），将应用自动配置。如果您的资源包仅包含特定于语言的属性文件，则需要添加默认资源文件。如果找不到与任何配置的基本名称匹配的属性文件，则不会有自动配置的 `MessageSource`。

可以使用 `spring.messages` 名称空间配置资源包的基本名称以及其他几个属性，如以下示例所示：

```properties
spring.messages.basename=messages,config.i18n.messages
spring.messages.fallback-to-system-locale=false
```

> `spring.messages.basename` 支持逗号分隔的位置列表，可以是包限定符，也可以是从类路径根目录解析的资源。

参考 [`MessageSourceProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/context/MessageSourceProperties.java) 获取更多支持的选项。

