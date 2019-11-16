被用在类级别时，此注解表示被声明的类（以及它的子类）的所有方法默认都是事务性的。或者，每个方法可以被分别注解。注意，一个类级别的注解不会作用到类集成体系中的祖先，这种场景下，方法需要呗局部重新声明以便成为子类级别的注解的参与者。

当一个 POJO 类，比如上面定义为 Spring 上下文中的  bean 的类，你可以通过在 `@Configuration` 类中使用 `@EnableTransactionManagement` 注解来将该 bean 实例标记为事务性的。参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/transaction/annotation/EnableTransactionManagement.html) 获取更多细节。

在 XML 配置文件中，`<tx:annotation-driven/>` 标签提供了类似的便利性：

````xml
<!-- from the file 'context.xml' -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx
        https://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- this is the service object that we want to make transactional -->
    <bean id="fooService" class="x.y.service.DefaultFooService"/>

    <!-- enable the configuration of transactional behavior based on annotations -->
    <tx:annotation-driven transaction-manager="txManager"/><!-- a PlatformTransactionManager is still required --> 

    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!-- (this dependency is defined somewhere else) -->
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!-- other <bean/> definitions here -->

</beans>
````

> 你可以忽略 `<tx:annotation-driven/>` 标签中的 `transaction-manager` 属性，如果你希望写入其中的 `PlatformTransactionManager` 的名字就是 `transactionManager` 。如果你希望注入的 `PlatformTransactionManager` bean 是任何其他名字，你就必须像上面例子那样显式使用 `transaction-manager` 属性。

> 方法可见性和 `@Transactional` 
>
> 当你使用代理时，你应该仅仅将 `@Transactional` 注解应用于可见性为 public 的方法。如果你使用 `@Transactional` 注解了 protected、private 或者包可见方法，不会发生错误，但是被注解的方法并不会展示出配置的事务性设定。如果你需要注解非 public 方法，考虑使用 AspectJ (后面介绍)。

