#### 5.5.2 声明一个切入点

你可以在`<aop:config>`元素中声明一个命名的切入点，使得该切入点在多个切面和增强器共享。

表示业务服务层中任何业务服务的执行的切入点能够被如下定义：

```xml
<aop:config>

    <aop:pointcut id="businessService"
        expression="execution(* com.xyz.myapp.service.*.*(..))"/>

</aop:config>
```

注意，切入点表达式自身使用了与 [@AspectJ support](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj) 中描述的 AspectJ 切入点表达式语言相同的语法。如果你使用基于模式的声明风格，则可以引用切入点表达式中的类型（@Aspects）中定义的命名切入点。声明上述切入点的另一种方法如下：

```xml
<aop:config>

    <aop:pointcut id="businessService"
        expression="com.xyz.myapp.SystemArchitecture.businessService()"/>

</aop:config>
```

假定你拥有一个 `SystemArchitecture` 切面，如 [Sharing Common Pointcut Definitions](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-common-pointcuts) 中所述。

则在一个切面内部声明一个切入点非常类似于声明一个顶级切入点，如下面例子所示：

```xml
<aop:config>

    <aop:aspect id="myAspect" ref="aBean">

        <aop:pointcut id="businessService"
            expression="execution(* com.xyz.myapp.service.*.*(..))"/>

        ...

    </aop:aspect>

</aop:config>
```

与 @AspectJ 切面大致相同，使用基于模式的定义样式声明的切入点可以收集连接点上下文。例如，以下切入点将`this`对象收集为连接点上下文并将其传递给增强：

```xml
<aop:config>

    <aop:aspect id="myAspect" ref="aBean">

        <aop:pointcut id="businessService"
            expression="execution(* com.xyz.myapp.service.*.*(..)) &amp;&amp; this(service)"/>

        <aop:before pointcut-ref="businessService" method="monitor"/>

        ...

    </aop:aspect>

</aop:config>
```

必须通过包含匹配名称的参数来声明增强以接收收集的连接点上下文，如下所示：

```java
public void monitor(Object service) {
    ...
}
```

当需要组合切入点子表达式时，XML 文件中的`&&`很难处理，所以你可以使用`and`，`or`以及`not`关键字相应替换`&&`，`||`，和`!`。比如，上面的切入点可以优化为：

```xml
<aop:config>

    <aop:aspect id="myAspect" ref="aBean">

        <aop:pointcut id="businessService"
            expression="execution(* com.xyz.myapp.service.*.*(..)) and this(service)"/>

        <aop:before pointcut-ref="businessService" method="monitor"/>

        ...
    </aop:aspect>
</aop:config>
```

请注意，以这种方式定义的切入点由其XML `id`引用，不能用作命名切入点来形成复合切入点。因此，基于模式的定义样式中的命名切入点支持比@AspectJ样式提供的支持更有限。

