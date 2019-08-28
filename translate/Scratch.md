### 6.5 简洁的代理定义

特别是在定义事务代理时，你可以会定义很多相似的代理。父 bean 定义和子 bean 定义的使用，以及内部 bean 定义，会产生更干净和简洁的代理定义。

首先，我们为代理创建一个父，模板，bean 定义，如下：

```xml
<bean id="txProxyTemplate" abstract="true"
        class="org.springframework.transaction.interceptor.TransactionProxyFactoryBean">
    <property name="transactionManager" ref="transactionManager"/>
    <property name="transactionAttributes">
        <props>
            <prop key="*">PROPAGATION_REQUIRED</prop>
        </props>
    </property>
</bean>
```

这个定义永远不会实例化自身，因此它实际上可以并不完整。然后，每个需要被创建的代理都是一个子 bean 定义，这些子 bean 定义将代理目标包装为内部 bean 定义，因为无论如何都不会单独使用代理目标。下面的例子展示了这样一个子 bean ：

```xml
<bean id="myService" parent="txProxyTemplate">
    <property name="target">
        <bean class="org.springframework.samples.MyServiceImpl">
        </bean>
    </property>
</bean>
```

你可以覆盖来自父模板的属性。下面的例子中，我们覆盖了事务传播设定：

```xml
<bean id="mySpecialService" parent="txProxyTemplate">
    <property name="target">
        <bean class="org.springframework.samples.MySpecialServiceImpl">
        </bean>
    </property>
    <property name="transactionAttributes">
        <props>
            <prop key="get*">PROPAGATION_REQUIRED,readOnly</prop>
            <prop key="find*">PROPAGATION_REQUIRED,readOnly</prop>
            <prop key="load*">PROPAGATION_REQUIRED,readOnly</prop>
            <prop key="store*">PROPAGATION_REQUIRED</prop>
        </props>
    </property>
</bean>
```

请注意，在父 bean 示例中，我们通过将`abstract`属性设置为`true`将父 bean 定义显式标记为`abstract`，如前所述。因此，实际上可能无法实例化它。默认情况下，应用程序上下文（但不是简单的 bean 工厂）预先实例化所有单例。因此，重要的是（至少对于单例 bean），如果您有一个（父）bean 定义，您打算仅将其用作模板，并且此定义指定了一个类，则必须确保将`abstract`属性设置为`true`。否则，应用程序上下文实际上会尝试预先实例化它。

