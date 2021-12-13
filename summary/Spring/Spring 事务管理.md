# [Spring事务（一）：Spring有事务吗？](https://zhuanlan.zhihu.com/p/38815840)

[![方小葱](https://pic1.zhimg.com/v2-5f10333d63d781d884f15e9fd1eb08c6_xs.jpg)](https://www.zhihu.com/people/fangxiaocong)

[方小葱](https://www.zhihu.com/people/fangxiaocong)

段子手小葱同学~

90 人赞同了该文章

很多时候去找工作，面试官会问你一些哭笑不得的问题，有的可能只是他没有表达清楚（你别指望工程师的表达能力有多强），更多的时候是他不懂，大多数开发人员水平真的很有限，他们大多数信息和知识来自于基本教程，他可能看了几本＂如何使用＂的教程，然后学着教程上的口气和思维问你问题，你要知道教程有时候的思维方式很简单，它会尽可能的从表面去讲解问题～

比如很多时候人会问你＂**Spring事务是怎样的？说说**Spring事务吧？＂这种让人摸不着头脑的问题～

当然我其实知道他想表达什么，只是很多时候这种问题真的让人摸不着头脑，不知道从哪个方面入手～

**所以以后如果有人这么问你的时候，你完全可以给他一个＂鄙视的眼神＂，然后反问他＂**Spring有事务吗？（不是抬杠，是我觉得你自己不懂还装出一副高深莫测的样子问那种问题，问问题没事，装逼就不好了，对吧？）**＂～**

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝

**首先强调一遍：Spring没有事务，Spring没有事务，Spring没有事务～**

**事务是给开发人员信心和保证的机制：**我们在说＂事务＂的时候，往往和实现层面有关，尤其是信息存储／传递系统，比如文件／数据库系统（确保文件／数据真的保存了），消息系统（确保数据真的传递了）等，这些系统为了实现＂系统可靠性保证＂向用户提供事务能力，**确保开发人员能有信心的认为系统确确实实做成了他们想做的事情．**

显然Spring没有这样的需求和能力～

严格意义上的事务需要通过undo/redo等这种机制得到保证，分布式事务还需要多个系统之间的协商来确定状态；这里不难看出，如果某个数据库没有某个功能（如redis没有回滚能力），Spring事务是实现不了的～

我们所谓的Spring事务其实是基于JDBC 事务API／JTA 对＂事务系统＂（比如数据库）的封装，他只是JDBC事务／JTA等更高层次的封装和抽象（规范和定义了事务处理的流程和API，提供了一个统一的，更高层次的事务管理模型和用户界面供用户使用，并没有提供事务能力和机制）～

说到抽象／封装必然就得映射到底层实现：Spring事务管理的核心是事务管理器（TransactionManager），他有三个核心方法:beginTransaction，commitTransaction，rollbackTransaction分别对应事务流程的开启事务，提交事务，回滚事务～

不同的实现系统实现该API定义的接口就能接入Spring事务管理～

比如JtaTransactionManager的实现是基于JTA的，DataSourceTransactionManager是基于JDBC事务接口的～HibernateTransactionManager则调用Hibernate提供的事务接口（其实也是JDBC事务的一层封装）；

你甚至可以实现一个FSTransactionManager来为文件系统提供事务功能～

所以：**以下讨论的所谓＂Spring事务＂都在说这一层事务封装（模型），这一点是你首先要搞清楚的～**

**题外话**：这种模型抽象提供统一API的思想其实很常见，比如，我们的系统要接入几个短信网关实现一个简单的发短信的功能，我们知道不同第三方短信网关提供的接口是不一样的，为了简化系统我们会抽象出一个sendSMS方法（抽象流程），然后分别实现不同公司的短信网关接入（具体实现）；这种方式就是在两个系统之间建立一个统一的＂适配器（插座，想想你家墙上的插座对你提供了一个统一的接口，他接入国家电网，但是到最后，这些电能可能来自风力发电，也可能来自水力发电）＂～

这里提一下刚说到的问题：系统有短板效应，一个系统中最差的那个部分就是那个短板，他甚至会影响整个系统～刚才说了＂事务＂只是系统为了给你信心，但他到底能给你多大的信心和保证完全取决于它自己的实现而不是spring对它的封装，如果该系统有这样的功能spring就能提供，如果他没有你也别指望spring封装能给你提供这样的功能，所以说到事务的时候，你首先考虑的是那个数据库系统的事务能力能给你多大的信心（从根本出发）～





# [Spring（八）：事务管理](https://zhuanlan.zhihu.com/p/37108469)

[![张晓康](https://pic2.zhimg.com/v2-629df415dde0575797a0040a7eb9b511_xs.jpg)](https://www.zhihu.com/people/zhang-xiao-kang-86-1)

[张晓康](https://www.zhihu.com/people/zhang-xiao-kang-86-1)

用心写文章

81 人赞同了该文章

**目录**

1、事务介绍

2、事务的四个特性（ACID）

3、Spring 事务管理的核心接口

4、 PlatformTransactionManager 事务管理器

5、TransactionStatus　事务状态

6、TransactionDefinition　基本事务属性的定义

7、Spring 编程式事务和声明式事务的区别　

8、不用事务实现转账

9、编程式事务处理实现转账（TransactionTemplate ）

10、声明式事务处理实现转账（基于AOP的 xml 配置）　　

11、声明式事务处理实现转账（基于AOP的 注解 配置）　

**正文：**

**1、事务介绍**

　　事务（Transaction），一般是指要做的或所做的事情。在计算机术语中是指访问并可能更新数据库中各种数据项的一个程序执行单元(unit)。

　　这里我们以取钱的例子来讲解：比如你去ATM机取1000块钱，大体有两个步骤：第一步输入密码金额，银行卡扣掉1000元钱；第二步从ATM出1000元钱。这两个步骤必须是要么都执行要么都不执行。如果银行卡扣除了1000块但是ATM出钱失败的话，你将会损失1000元；如果银行卡扣钱失败但是ATM却出了1000块，那么银行将损失1000元。

　　如何保证这两个步骤不会出现一个出现异常了，而另一个执行成功呢？事务就是用来解决这样的问题。事务是一系列的动作，它们综合在一起才是一个完整的工作单元，这些动作必须全部完成，如果有一个失败的话，那么事务就会回滚到最开始的状态，仿佛什么都没发生过一样。 在企业级应用程序开发中，事务管理是必不可少的技术，用来确保数据的完整性和一致性。

**2、事务的四个特性（ACID）**

　　①、原子性（Atomicity）：事务是一个原子操作，由一系列动作组成。事务的原子性确保动作要么全部完成，要么完全不起作用。

　　②、一致性（Consistency）：一旦事务完成（不管成功还是失败），系统必须确保它所建模的业务处于一致的状态，而不会是部分完成部分失败。在现实中的数据不应该被破坏。

　　③、隔离性（Isolation）：可能有许多事务会同时处理相同的数据，因此每个事务都应该与其他事务隔离开来，防止数据损坏。

　　④、持久性（Durability）：一旦事务完成，无论发生什么系统错误，它的结果都不应该受到影响，这样就能从任何系统崩溃中恢复过来。通常情况下，事务的结果被写到持久化存储器中。

**3、Spring 事务管理的核心接口**

![img](https://pic3.zhimg.com/80/v2-9026437313529f475df25a3c51dccb46_hd.jpg)

我们打开Spring的核心事务包，查看如下类：org.springframework.transaction

![img](https://pic2.zhimg.com/80/v2-0301b51b6efc002e180f574d76cf4f05_hd.jpg)

　　上面所示的三个类文件便是Spring的事务管理接口。如下图所示：下面我们分别对这三个接口进行简单的介绍

![img](https://pic4.zhimg.com/80/v2-90d3b0f6272c619a4816fb6f863512ab_hd.jpg)

**4、** **PlatformTransactionManager 事务管理器**

　　Spring事务管理器的接口是org.springframework.transaction.PlatformTransactionManager，如上图所示，Spring并不直接管理事务，通过这个接口，Spring为各个平台如JDBC、Hibernate等都提供了对应的事务管理器，也就是将事务管理的职责委托给Hibernate或者JTA等持久化机制所提供的相关平台框架的事务来实现。

　　我们进入到 PlatformTransactionManager 接口，查看源码：

![img](https://pic4.zhimg.com/80/v2-f38bb22c0b74d5fb3493fabfeb7e342b_hd.jpg)

　　①、TransactionStatus getTransaction(TransactionDefinition definition) ，事务管理器 通过TransactionDefinition，获得“事务状态”，从而管理事务。

　　②、void commit(TransactionStatus status) 根据状态提交

　　③、void rollback(TransactionStatus status) 根据状态回滚

　　也就是说Spring事务管理的为不同的事务API提供一致的编程模型，具体的事务管理机制由对应各个平台去实现。

　　比如下面我们导入实现事务管理的两种平台：JDBC和Hibernate

![img](https://pic2.zhimg.com/80/v2-7c1e3ca7f969c3040b81ebf9bdf3acc1_hd.jpg)

　　然后我们再次查看PlatformTransactionManager接口，会发现它多了几个实现类，如下：

![img](https://pic4.zhimg.com/80/v2-5a422912382e83c616c96ec94f821f27_hd.jpg)

**5、TransactionStatus　事务状态**

　　在上面 PlatformTransactionManager 接口中，有如下方法：

![img](https://pic3.zhimg.com/80/v2-15ed6d4231687400d27f6f4734bdc816_hd.jpg)

　　这个方法返回的是 TransactionStatus对象，然后程序根据返回的对象来获取事务状态，然后进行相应的操作。

　　而 TransactionStatus 这个接口的内容如下：

![img](https://pic4.zhimg.com/80/v2-cd50fb8aed2e35530a65f19a35aafebb_hd.jpg)

　　这个接口描述的是一些处理事务提供简单的控制事务执行和查询事务状态的方法，在回滚或提交的时候需要应用对应的事务状态。

**6、TransactionDefinition　基本事务属性的定义**

　　上面讲到的事务管理器接口PlatformTransactionManager通过getTransaction(TransactionDefinition definition)方法来得到事务，这个方法里面的参数是TransactionDefinition类，这个类就定义了一些基本的事务属性。

那么什么是事务属性呢？事务属性可以理解成事务的一些基本配置，描述了事务策略如何应用到方法上。事务属性包含了5个方面，如图所示：

![img](https://pic2.zhimg.com/80/v2-cd231c2885ac72a3348e9e2c7fe00749_hd.jpg)

　　TransactionDefinition 接口方法如下：

![img](https://pic4.zhimg.com/80/v2-f620c5bd30ed4578ae0f033ac1155fb7_hd.jpg)

**一、传播行为：当事务方法被另一个事务方法调用时，必须指定事务应该如何传播。**

　　　　Spring 定义了如下七中传播行为，这里以A业务和B业务之间如何传播事务为例说明：

　　①、**PROPAGATION_REQUIRED** ：required , 必须。默认值，A如果有事务，B将使用该事务；如果A没有事务，B将创建一个新的事务。

　　②、**PROPAGATION_SUPPORTS**：supports ，支持。A如果有事务，B将使用该事务；如果A没有事务，B将以非事务执行。

　　③、**PROPAGATION_MANDATORY**：mandatory ，强制。A如果有事务，B将使用该事务；如果A没有事务，B将抛异常。

　　④、**PROPAGATION_REQUIRES_NEW** ：requires_new，必须新的。如果A有事务，将A的事务挂起，B创建一个新的事务；如果A没有事务，B创建一个新的事务。

　　⑤、**PROPAGATION_NOT_SUPPORTED** ：not_supported ,不支持。如果A有事务，将A的事务挂起，B将以非事务执行；如果A没有事务，B将以非事务执行。

　　⑥、**PROPAGATION_NEVER** ：never，从不。如果A有事务，B将抛异常；如果A没有事务，B将以非事务执行。

　　⑦、**PROPAGATION_NESTED** ：nested ，嵌套。A和B底层采用保存点机制，形成嵌套事务。

**二、隔离级别：定义了一个事务可能受其他并发事务影响的程度。**

　　**并发事务引起的问题：**

在典型的应用程序中，多个事务并发运行，经常会操作相同的数据来完成各自的任务。并发虽然是必须的，但可能会导致以下的问题。


①、脏读（Dirty reads）——脏读发生在一个事务读取了另一个事务改写但尚未提交的数据时。如果改写在稍后被回滚了，那么第一个事务获取的数据就是无效的。

②、不可重复读（Nonrepeatable read）——不可重复读发生在一个事务执行相同的查询两次或两次以上，但是每次都得到不同的数据时。这通常是因为另一个并发事务在两次查询期间进行了更新。

③、幻读（Phantom read）——幻读与不可重复读类似。它发生在一个事务（T1）读取了几行数据，接着另一个并发事务（T2）插入了一些数据时。在随后的查询中，第一个事务（T1）就会发现多了一些原本不存在的记录。

**注意：不可重复读重点是修改，而幻读重点是新增或删除。**

　　在 Spring 事务管理中，为我们定义了如下的隔离级别：

　　①、ISOLATION_DEFAULT：使用后端数据库默认的隔离级别

　　②、ISOLATION_READ_UNCOMMITTED：最低的隔离级别，允许读取尚未提交的数据变更，可能会导致脏读、幻读或不可重复读

　　③、ISOLATION_READ_COMMITTED：允许读取并发事务已经提交的数据，可以阻止脏读，但是幻读或不可重复读仍有可能发生

　　④、ISOLATION_REPEATABLE_READ：对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，可以阻止脏读和不可重复读，但幻读仍有可能发生

　　⑤、ISOLATION_SERIALIZABLE：最高的隔离级别，完全服从ACID的隔离级别，确保阻止脏读、不可重复读以及幻读，也是最慢的事务隔离级别，因为它通常是通过完全锁定事务相关的数据库表来实现的

　　上面定义的隔离级别，在 Spring 的 TransactionDefinition.class 中也分别用常量 -1,0,1,2,4,8表示。比如 ISOLATION_DEFAULT 的定义：

![img](https://pic3.zhimg.com/80/v2-252462103aaba39a88726a736861f77e_hd.jpg)

**三、只读**

　　这是事务的第三个特性，是否为只读事务。如果事务只对后端的数据库进行该操作，数据库可以利用事务的只读特性来进行一些特定的优化。通过将事务设置为只读，你就可以给数据库一个机会，让它应用它认为合适的优化措施。

**四、事务超时**

为了使应用程序很好地运行，事务不能运行太长的时间。因为事务可能涉及对后端数据库的锁定，所以长时间的事务会不必要的占用数据库资源。事务超时就是事务的一个定时器，在特定时间内事务如果没有执行完毕，那么就会自动回滚，而不是一直等待其结束。

**五、回滚规则**

　　事务五边形的最后一个方面是一组规则，这些规则定义了哪些异常会导致事务回滚而哪些不会。默认情况下，事务只有遇到运行期异常时才会回滚，而在遇到检查型异常时不会回滚（这一行为与EJB的回滚行为是一致的） 。但是你可以声明事务在遇到特定的检查型异常时像遇到运行期异常那样回滚。同样，你还可以声明事务遇到特定的异常不回滚，即使这些异常是运行期异常。

**7、Spring 编程式事务和声明式事务的区别**

**编程式事务处理**：所谓编程式事务指的是通过编码方式实现事务，允许用户在代码中精确定义事务的边界。即类似于JDBC编程实现事务管理。管理使用TransactionTemplate或者直接使用底层的PlatformTransactionManager。对于编程式事务管理，spring推荐使用TransactionTemplate。

**声明式事务处理**：管理建立在AOP之上的。其本质是对方法前后进行拦截，然后在目标方法开始之前创建或者加入一个事务，在执行完目标方法之后根据执行情况提交或者回滚事务。声明式事务最大的优点就是不需要通过编程的方式管理事务，这样就不需要在业务逻辑代码中掺杂事务管理的代码，只需在配置文件中做相关的事务规则声明(或通过基于@Transactional注解的方式)，便可以将事务规则应用到业务逻辑中。

**简单地说，编程式事务侵入到了业务代码里面，但是提供了更加详细的事务管理；而声明式事务由于基于AOP，所以既能起到事务管理的作用，又可以不影响业务代码的具体实现。**

**8、不用事务实现转账**

　　我们还是以转账为实例。不用事务看如何实现转账。在数据库中有如下表 account ,内容如下：

![img](https://pic3.zhimg.com/80/v2-c509ce8f62eb0238f29f03f9209982b6_hd.jpg)

　　有两个用户 Tom 和 Marry 。他们初始账户余额都为 10000。这时候我们进行如下业务：Tom 向 Marry 转账 1000 块。那么这在程序中可以分解为两个步骤：

　　①、Tom 的账户余额 10000 减少 1000 块，剩余 9000 块。

　　②、Marry 的账户余额 10000 增加 1000 块，变为 11000块。

　　上面两个步骤要么都执行成功，要么都不执行。我们通过 TransactionTemplate 编程式事务来控制：

**第一步：创建Java工程并导入相应的 jar 包（这里不用事务其实不需要这么多jar包，为了后面的讲解需要，我们一次性导入所有的jar包）**

![img](https://pic4.zhimg.com/80/v2-7e2d0146aa62bc9b10e344a205b39713_hd.jpg)

**第二步：编写 Dao 层**

　　　　**AccountDao 接口：**

```java
package com.ys.dao;

public interface AccountDao {
    /**
     * 汇款
     * 
     * @param outer 汇款人
     * @param money 汇款金额
     */
    public void out(String outer, int money);

    /**
     * 收款
     * 
     * @param inner 收款人
     * @param money 收款金额
     */
    public void in(String inner, int money);

}
```

**AccountDaoImpl 接口实现类**

```java
package com.ys.dao.impl;

public class AccountDaoImpl extends JdbcDaoSupport implements AccountDao {

    /**
     * 根据用户名减少账户金额
     */
    @Override
    public void out(String outer, int money) {
        this.getJdbcTemplate().update("update account set money = money - ? where username = ?",
                money, outer);
    }

    /**
     * 根据用户名增加账户金额
     */
    @Override
    public void in(String inner, int money) {
        this.getJdbcTemplate().update("update account set money = money + ? where username = ?",
                money, inner);
    }

}
```

**第三步：实现 Service 层**

**AccountService 接口**

```java
package com.ys.service;

public interface AccountService {

    /**
     * 转账
     * 
     * @param outer 汇款人
     * @param inner 收款人
     * @param money 交易金额
     */
    public void transfer(String outer, String inner, int money);

}
```

**AccountServiceImpl 接口实现类**

```java
package com.ys.service.impl;

import com.ys.dao.AccountDao;
import com.ys.service.AccountService;

public class AccountServiceImpl implements AccountService {

    private AccountDao accountDao;

    public void setAccountDao(AccountDao accountDao) {
        this.accountDao = accountDao;
    }

    @Override
    public void transfer(String outer, String inner, int money) {
        accountDao.out(outer, money);
        accountDao.in(inner, money);
    }

}
```

**第四步：Spring 全局配置文件 applicationContext.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
 xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/aop
 http://www.springframework.org/schema/aop/spring-aop.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context.xsd">
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
        <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/test"></property>
        <property name="user" value="root"></property>
        <property name="password" value="root"></property>
    </bean>
    <bean id="accountDao" class="com.ys.dao.impl.AccountDaoImpl">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <bean id="accountService" class="com.ys.service.impl.AccountServiceImpl">
        <property name="accountDao" ref="accountDao"></property>
    </bean>
</beans> 
```

**第五步：测试**

```java
public class TransactionTest {

    @Test
    public void testNoTransaction() {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        AccountService account = (AccountService) context.getBean("accountService");
        // Tom 向 Marry 转账1000
        account.transfer("Tom", "Marry", 1000);
    }

}
```

**第六步：查看数据库表 account**

![img](https://pic3.zhimg.com/80/v2-67900d14d8e3ea28efca27046b9760b2_hd.jpg)

　　上面的结果和我们想的一样，Tom 账户 money 减少了1000块。而 Marry 账户金额增加了1000块。

　　这时候问题来了，比如在 Tom 账户 money 减少了1000块正常。而 Marry 账户金额增加时发生了异常，实际应用中比如断电（这里我们人为构造除数不能为0的异常），如下：

![img](https://pic2.zhimg.com/80/v2-22a316663f36130237a0c0df70955145_hd.jpg)

　　那么这时候我们执行测试程序，很显然会报错，那么数据库是什么情况呢？

![img](https://pic3.zhimg.com/80/v2-3f4bd1115cfb47e21e019304357a93e2_hd.jpg)

　　数据库account ：

![img](https://pic1.zhimg.com/80/v2-6a8ba803ce2fb7a5fb740a8af38e1ab0_hd.jpg)

　　我们发现，程序执行报错了，但是数据库 Tom 账户金额依然减少了 1000 块，但是 Marry 账户的金额却没有增加。这在实际应用中肯定是不允许的，那么如何解决呢？

**9、编程式事务处理实现转账（TransactionTemplate ）**

　　上面转账的两步操作中间发生了异常，但是第一步依然在数据库中进行了增加操作。实际应用中不会允许这样的情况发生，所以我们这里用事务来进行管理。

　　Dao 层不变，我们在 Service 层注入 TransactionTemplate 模板，因为是用模板来管理事务，所以模板需要注入事务管理器 DataSourceTransactionManager 。而事务管理器说到底还是用底层的JDBC在管理，所以我们需要在事务管理器中注入 DataSource。这几个步骤分别如下：

　　AccountServiceImpl 接口：

```java
package com.ys.service.impl;

import org.springframework.transaction.TransactionStatus;
import org.springframework.transaction.support.TransactionCallbackWithoutResult;
import org.springframework.transaction.support.TransactionTemplate;

import com.ys.dao.AccountDao;
import com.ys.service.AccountService;

public class AccountServiceImpl implements AccountService {

    private AccountDao accountDao;
    private TransactionTemplate transactionTemplate;

    public void setTransactionTemplate(TransactionTemplate transactionTemplate) {
        this.transactionTemplate = transactionTemplate;
    }

    public void setAccountDao(AccountDao accountDao) {
        this.accountDao = accountDao;
    }

    @Override
    public void transfer(final String outer, final String inner, final int money) {
        transactionTemplate.execute(new TransactionCallbackWithoutResult() {
            @Override
            protected void doInTransactionWithoutResult(TransactionStatus arg0) {
                accountDao.out(outer, money);
                // int i = 1/0;
                accountDao.in(inner, money);
            }
        });
    }

}
```

　　Spring 全局配置文件 applicationContext.xml：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
 xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/aop
 http://www.springframework.org/schema/aop/spring-aop.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context.xsd">
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
        <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/test"></property>
        <property name="user" value="root"></property>
        <property name="password" value="root"></property>
    </bean>
    <bean id="accountDao" class="com.ys.dao.impl.AccountDaoImpl">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <bean id="accountService" class="com.ys.service.impl.AccountServiceImpl">
        <property name="accountDao" ref="accountDao"></property>
        <property name="transactionTemplate" ref="transactionTemplate"></property>
    </bean>
    <!-- 创建模板 -->
    <bean id="transactionTemplate" class="org.springframework.transaction.support.TransactionTemplate">
        <property name="transactionManager" ref="txManager"></property>
    </bean>
    <!-- 配置事务管理器 ,管理器需要事务，事务从Connection获得，连接从连接池DataSource获得 -->
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
</beans> 
```

　　测试文件保持不变，可以分两次测试，第一次两次操作没有发生异常，然后数据库正常改变了。第二次操作中间发生了异常，发现数据库内容没变。

　　如果大家有兴趣也可以试试底层的PlatformTransactionManager来进行事务管理，我这里给出主要代码：

```java
        // 定义一个某个框架平台的TransactionManager，如JDBC、Hibernate
        DataSourceTransactionManager dataSourceTransactionManager =
                new DataSourceTransactionManager();
        dataSourceTransactionManager.setDataSource(this.getJdbcTemplate().getDataSource()); // 设置数据源

        DefaultTransactionDefinition transDef = new DefaultTransactionDefinition(); // 定义事务属性
        transDef.setPropagationBehavior(DefaultTransactionDefinition.PROPAGATION_REQUIRED); // 设置传播行为属性
        TransactionStatus status = dataSourceTransactionManager.getTransaction(transDef); // 获得事务状态
        try {
            // 数据库操作
            accountDao.out(outer, money);
            int i = 1 / 0;
            accountDao.in(inner, money);

            dataSourceTransactionManager.commit(status);// 提交
        } catch (Exception e) {
            dataSourceTransactionManager.rollback(status);// 回滚
        } 
```

**10、声明式事务处理实现转账（基于AOP的 xml 配置）**　

　　Dao 层和 Service 层与我们最先开始的不用事务实现转账保持不变。主要是 applicationContext.xml 文件变化了。

　　我们在 applicationContext.xml 文件中配置 aop 自动生成代理，进行事务管理：

　　①、配置管理器

　　②、配置事务详情

　　③、配置 aop

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
 xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/aop
 http://www.springframework.org/schema/aop/spring-aop.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context.xsd
 http://www.springframework.org/schema/tx
 http://www.springframework.org/schema/tx/spring-tx.xsd">
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
        <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/test"></property>
        <property name="user" value="root"></property>
        <property name="password" value="root"></property>
    </bean>
    <bean id="accountDao" class="com.ys.dao.impl.AccountDaoImpl">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <bean id="accountService" class="com.ys.service.impl.AccountServiceImpl">
        <property name="accountDao" ref="accountDao"></property>
    </bean>
    <!-- 1 事务管理器 -->
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!-- 2 事务详情（事务通知）  ， 在aop筛选基础上，比如对ABC三个确定使用什么样的事务。例如：AC读写、B只读 等
 <tx:attributes> 用于配置事务详情（属性属性）
 <tx:method name=""/> 详情具体配置
 propagation 传播行为 ， REQUIRED：必须；REQUIRES_NEW:必须是新的
 isolation 隔离级别
 -->
    <tx:advice id="txAdvice" transaction-manager="txManager">
        <tx:attributes>
            <tx:method name="transfer" propagation="REQUIRED" isolation="DEFAULT"/>
        </tx:attributes>
    </tx:advice>
    <!-- 3 AOP编程，利用切入点表达式从目标类方法中 确定增强的连接器，从而获得切入点 -->
    <aop:config>
        <aop:advisor advice-ref="txAdvice" pointcut="execution(* com.ys.service..*.*(..))"/>
    </aop:config>
</beans> 
```

　　测试类这里我们就不描述了，也是分有异常和无异常进行测试，发现与预期结果是吻合的。

**11、声明式事务处理实现转账（基于AOP的 注解 配置）**

　　分为如下两步：

　　①、在applicationContext.xml 配置事务管理器，将并事务管理器交予spring

　　②、在目标类或目标方法添加注解即可 @Transactional

　　首先在 applicationContext.xml 文件中配置如下：

```xml
<!-- 1 事务管理器 -->
<bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="dataSource" ref="dataSource"></property>
</bean>
<!-- 2 将管理器交予spring
 * transaction-manager 配置事务管理器
 * proxy-target-class
 true ： 底层强制使用cglib 代理
 -->
<tx:annotation-driven transaction-manager="txManager" proxy-target-class="true"/> 
```

　　其次在目标类或者方法添加注解@Transactional。如果在类上添加，则说明类中的所有方法都添加事务，如果在方法上添加，则只有该方法具有事务。

```java
package com.ys.service.impl;

import javax.annotation.Resource;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Isolation;
import org.springframework.transaction.annotation.Propagation;
import org.springframework.transaction.annotation.Transactional;

import com.ys.dao.AccountDao;
import com.ys.service.AccountService;

@Transactional(propagation = Propagation.REQUIRED, isolation = Isolation.DEFAULT)
@Service("accountService")
public class AccountServiceImpl implements AccountService {
    @Resource(name = "accountDao")
    private AccountDao accountDao;

    public void setAccountDao(AccountDao accountDao) {
        this.accountDao = accountDao;
    }

    @Override
    public void transfer(String outer, String inner, int money) {
        accountDao.out(outer, money);
        // int i = 1/0;
        accountDao.in(inner, money);
    }

}
```