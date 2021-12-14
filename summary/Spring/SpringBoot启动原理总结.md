# [SPRINGBOOT启动原理（基于2.3.9.RELEASE版本）](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html)

- [版本](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label0)

- [总体上](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label1)

- [main方法上的注解：@SpringBootApplication](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label2)

- - [源码](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_lab2_2_0)

  - [@SpringBootConfiguration](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_lab2_2_1)

  - [@ComponentScan](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_lab2_2_2)

  - [@EnableAutoConfiguration](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_lab2_2_3)

  - - [@EnableAutoConfiguration总结](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label3_2_3_0)
    - [源码](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label3_2_3_1)
    - [@AutoConfigurationPackage](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label3_2_3_2)
    - [AutoConfigurationImportSelector](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label3_2_3_3)

- [main方法](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label3)

- - [例子](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_lab2_3_0)

  - [SpringApplication#run](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_lab2_3_1)

  - - [实例化SpringApplication对象](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label3_3_1_0)
    - [SpringApplication#run(java.lang.String...)源码解析](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label3_3_1_1)

- [SpringBoot启动事件](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label4)

- - [EventPublishingRunListener](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_lab2_4_0)

- [SpringIOC 容器初始化过程](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#_label5)



目录

- [版本](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#版本)
- [总体上](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#总体上)
- main方法上的注解：@SpringBootApplication
  - [源码](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#源码)
  - [@SpringBootConfiguration](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#springbootconfiguration)
  - [@ComponentScan](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#componentscan)
  - @EnableAutoConfiguration
    - [@EnableAutoConfiguration总结](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#enableautoconfiguration总结)
    - [源码](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#源码)
    - [@AutoConfigurationPackage](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#autoconfigurationpackage)
    - [AutoConfigurationImportSelector](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#autoconfigurationimportselector)
- main方法
  - [例子](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#例子)
  - SpringApplication#run
    - [实例化SpringApplication对象](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#实例化springapplication对象)
    - [SpringApplication#run(java.lang.String...)源码解析](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#springapplicationrunjavalangstring源码解析)
- SpringBoot启动事件
  - [EventPublishingRunListener](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#eventpublishingrunlistener)
- [SpringIOC 容器初始化过程](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#springioc-容器初始化过程)



# 版本

以下源码的 `SpringBoot` 版本：2.3.9.RELEASE。

# 总体上

分为两大步：

- **启动类上注解**：**@SpringBootApplication**
- **启动类中的main方法**：org.springframework.boot.**SpringApplication#run**(java.lang.Class<?>, java.lang.String...)

# main方法上的注解：@SpringBootApplication

## 源码

三个注解核心注解：`@SpringBootConfiguration`，`@EnableAutoConfiguration`和`@ComponentScan`。

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
```

## @SpringBootConfiguration

根据**Javadoc**可知，该注解作用就是将当前的类作为一个**JavaConfig**，然后**触发注解**`@EnableAutoConfiguration`和`@ComponentScan`的**处理**，本质上与**@Configuration**注解没有区别。

## @ComponentScan

扫描的 `Spring` 对应的组件，如 **@Componet**，**@Repository**。

我们可以通过 **basePackages** 等属性来**细粒度**的定制 `@ComponentScan` 自动**扫描的范围**，如果不指定，则**默认**Spring框架实现会从声明 `@ComponentScan` **所在类的package**进行扫描，所以 `SpringBoot` 的**启动类**最好是放在**根package**下，我们**自定义的类就放在对应的子package**下，这样就可以不指定 `basePackages`。

- - ## @EnableAutoConfiguration

    ### @EnableAutoConfiguration总结

    - **@AutoConfigurationPackage**

      - 注册**当前启动类的根 package**
      - 注册 org.springframework.boot.autoconfigure.**AutoConfigurationPackages** 的 **BeanDefinition**。

    - **@Import(AutoConfigurationImportSelector.class)**

      - 可以看到实现了 **DeferredImportSelector** 接口，该接口继承自 **ImportSelector**，根据 `Javadoc` 可知，多用于导入**被 @Conditional 注解的Bean**，之后会进行 `filter` 操作

      - AutoConfigurationImportSelector.AutoConfigurationGroup#process 方法，SpringBoot启动时会调用该方法，进行自动装配的处理，见

        SpringApplication#run(java.lang.String...)源码解析

        - **SpringApplication#run**(java.lang.String...)
        - SpringApplication#**refreshContext**（即 [Spring IOC 容器初始化的过程中](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#springioc-容器初始化过程)）
        - **ConfigurationClassParser#parse**
        - AutoConfigurationImportSelector.AutoConfigurationGroup#**process**

      - 通过**SpringFactoriesLoader**#loadFactoryNames获取应考虑的自动配置名称，例如来源于 `spring-boot-autoconfigure` jar包下的 **META-INF/spring.factories** 文件下的配置

      - 通过 **filter** 过滤掉当前环境不需要自动装配的类，各种 **@Conditional 不满足**就被过滤掉

      - 将**需要自动装配的全路径类名**注册到 `SpringIOC` 容器，**自此 SpringBoot 自动装配完成！**

### 源码

```java
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {
```

**SpringBoot 自动装配的核心注解**，在 `Spring` 框架中就提供了各种以**@Enable开头的注解**，例如： `@EnableCircuitBreaker`、`@EnableScheduling`等；

**@EnableAutoConfiguration**，**借助@Import的支持**，收集和注册特定场景相关的bean定义;

自动装配的类，通常是 `@Configuration` 类，通过 `SpringFactoriesLoader` 加载到 `Spring` 容器。

### @AutoConfigurationPackage

注册**当前启动类的根package**；

注册 org.springframework.boot.autoconfigure.**AutoConfigurationPackages** 的**BeanDefinition**。

### AutoConfigurationImportSelector

```java
public class AutoConfigurationImportSelector implements DeferredImportSelector, BeanClassLoaderAware,
  ResourceLoaderAware, BeanFactoryAware, EnvironmentAware, Ordered {
```

- 可以看到实现了 **DeferredImportSelector** 接口，该接口继承自**ImportSelector**，根据Javadoc可知，多用于导入**被@Conditional注解的Bean**

- **DeferredImportSelector**接口中有个**process**方法，SpringBoot启动时会调用该方法，进行自动装配的处理，大体流程如下：

  - **SpringApplication#run**(java.lang.String...)
  - SpringApplication#**refreshContext**
  - **ConfigurationClassParser#parse**
  - AutoConfigurationImportSelector.AutoConfigurationGroup#**process**

- **AutoConfigurationImportSelector**.**AutoConfigurationGroup**#**process**方法的源码：

  调用了AutoConfigurationImportSelector#**getAutoConfigurationEntry**方法，**获取需要自动装配类**

  ```java
  public void process(AnnotationMetadata annotationMetadata, DeferredImportSelector deferredImportSelector) {
   Assert.state(deferredImportSelector instanceof AutoConfigurationImportSelector,
     () -> String.format("Only %s implementations are supported, got %s",
       AutoConfigurationImportSelector.class.getSimpleName(),
       deferredImportSelector.getClass().getName()));
      // 获取需要自动装配类
   AutoConfigurationEntry autoConfigurationEntry = ((AutoConfigurationImportSelector) deferredImportSelector)
     .getAutoConfigurationEntry(annotationMetadata);
   this.autoConfigurationEntries.add(autoConfigurationEntry);
   for (String importClassName : autoConfigurationEntry.getConfigurations()) {
    this.entries.putIfAbsent(importClassName, annotationMetadata);
   }
  }
  ```

- AutoConfigurationImportSelector#**getAutoConfigurationEntry**大体流程如下：

  - 通过**SpringFactoriesLoader**#loadFactoryNames获取应考虑的自动配置名称，例如来源于 `spring-boot-autoconfigure` jar包下的**META-INF/spring.factories**文件下的配置

    ![img](https://img2020.cnblogs.com/blog/1158841/202104/1158841-20210430210806771-1369776051.png)

  - 通过**filter**过滤掉当前环境不需要自动装配的类，比如没有集成RabbitMQ，就不需要，或者有的条件@Conditional不满足也不需要自动装配

  - 返回**需要自动装配的全路径类名**

  - 源码如下：

  ```java
  protected AutoConfigurationEntry getAutoConfigurationEntry(AnnotationMetadata annotationMetadata) {
   if (!isEnabled(annotationMetadata)) {
    return EMPTY_ENTRY;
   }
   AnnotationAttributes attributes = getAttributes(annotationMetadata);
      // 获取预先定义的应考虑的自动配置类名称
   List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);
   configurations = removeDuplicates(configurations);
   Set<String> exclusions = getExclusions(annotationMetadata, attributes);
   checkExcludedClasses(configurations, exclusions);
   configurations.removeAll(exclusions);
      // 通过filter过滤掉当前环境不需要自动装配的类，比如没有集成RabbitMQ，就不需要，或者有的条件@Conditional不满足也不需要自动装配
   configurations = getConfigurationClassFilter().filter(configurations);
   fireAutoConfigurationImportEvents(configurations, exclusions);
      // 返回需要自动装配的全路径类名
   return new AutoConfigurationEntry(configurations, exclusions);
  }
  ```

- AutoConfigurationImportSelector#**getCandidateConfigurations**源码如下：

  ```java
  protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
   List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),
     getBeanClassLoader());
   Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you "
     + "are using a custom packaging, make sure that file is correct.");
   return configurations;
  }
  ```

- 通过**SpringFactoriesLoader**#loadFactoryNames获取应考虑的自动配置名称，通过**META-INF/spring.factories**下的配置，例如：

  ![image-20210418175725765](https://img2020.cnblogs.com/blog/1158841/202104/1158841-20210430210808113-638673023.png)

  spring-boot-autoconfigure jar包下的 `spring.factories` 文件：

  ![img](https://img2020.cnblogs.com/blog/1158841/202104/1158841-20210430210809113-165341260.png)

- 执行完`configurations = getConfigurationClassFilter().filter(configurations);`之后，各种**@Conditional不满足**就被过滤掉，剩下35个了

  ![img](https://img2020.cnblogs.com/blog/1158841/202104/1158841-20210430210811058-2100513979.png)

- 可以通过如下方法进行验证，结果没有 `RabbitAutoConfiguration` 相关的Bean，抛出异常 `NoSuchBeanDefinitionException`

  ```java
  @SpringBootApplication
  public class SpringDemosApplication implements ApplicationContextAware {
    private static ApplicationContext applicationContext;
  
    public static void main(String[] args) {
      SpringApplication.run(SpringDemosApplication.class, args);
      System.out.println(applicationContext.getBean(AopAutoConfiguration.class));
      System.out.println(applicationContext.getBean(RabbitAutoConfiguration.class));
    }
  
    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
      SpringDemosApplication.applicationContext = applicationContext;
    }
  }
  ```

# main方法

## 例子

main方法里调用org.springframework.boot.**SpringApplication**#**run**(java.lang.Class<?>, java.lang.String...)方法

```java
@SpringBootApplication
public class SpringDemosApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringDemosApplication.class, args);
    }
}
```

## SpringApplication#run

调用另外一个同名的重载方法run

```java
public static ConfigurableApplicationContext run(Class<?> primarySource, String... args) {
 return run(new Class<?>[] { primarySource }, args);
}
```

### 实例化SpringApplication对象

1. 首先会**实例化SpringApplication**一个对象
2. 在**构造方法**里初始化一些属性，比如webApplicationType，比如"SERVLET"，**初始化一些listeners**

```java
public static ConfigurableApplicationContext run(Class<?>[] primarySources, String[] args) {
 return new SpringApplication(primarySources).run(args);
}
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
 this.resourceLoader = resourceLoader;
 Assert.notNull(primarySources, "PrimarySources must not be null");
 this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
    // 初始化webApplicationType，比如"SERVLET"
 this.webApplicationType = WebApplicationType.deduceFromClasspath();
 setInitializers((Collection) getSpringFactoriesInstances(ApplicationContextInitializer.class));
    // 初始化一些listeners
 setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
 this.mainApplicationClass = deduceMainApplicationClass();
}
```

### SpringApplication#run(java.lang.String...)源码解析

[经典的观察者模式](https://github.com/iluwatar/java-design-patterns/tree/master/observer)，只要你把[事件广播的顺序](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#springboot启动事件)理解了，那**整个流程**就很容易串起来了：

1. 创建一个StopWatch实例，用来记录SpringBoot的启动时间
2. 通过SpringFactoriesLoader加载listeners：比如EventPublishingRunListener
3. 发布SprintBoot开始启动事件（EventPublishingRunListener#**starting()**）
4. 创建和配置environment（**environmentPrepared()**）
5. 打印SpringBoot的banner和版本
6. 创建对应的ApplicationContext：Web类型，Reactive类型，普通的类型(非Web)
7. prepareContext
   1. **准备ApplicationContext**，Initializers设置到ApplicationContext(**contextPrepared()**)
   2. 打印启动日志，打印profile信息(如dev, test, prod)
   3. 最终会调用到AbstractApplicationContext#refresh方法，实际上就是[Spring IOC容器的创建过程](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#springioc-容器初始化过程)，并且会进行自动装配的操作，以及发布ApplicationContext已经refresh事件，标志着ApplicationContext初始化完成(**contextLoaded()**)
8. **afterRefresh** hook方法
9. stopWatch停止计时，日志打印总共启动的时间
10. 发布SpringBoot程序已启动事件(**started()**)
11. 调用ApplicationRunner和CommandLineRunner
12. 最后发布就绪事件ApplicationReadyEvent，标志着SpringBoot可以处理就收的请求了(**running()**)

```java
public ConfigurableApplicationContext run(String... args) {
    // 创建一个StopWatch实例，用来记录SpringBoot的启动时间
 StopWatch stopWatch = new StopWatch();
 stopWatch.start();
 ConfigurableApplicationContext context = null;
 Collection<SpringBootExceptionReporter> exceptionReporters = new ArrayList<>();
 configureHeadlessProperty();
    // 通过SpringFactoriesLoader加载listeners：比如EventPublishingRunListener
 SpringApplicationRunListeners listeners = getRunListeners(args);
    // 发布SprintBoot启动事件：ApplicationStartingEvent
 listeners.starting();
 try {
  ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
     // 创建和配置environment，发布事件：SpringApplicationRunListeners#environmentPrepared
  ConfigurableEnvironment environment = prepareEnvironment(listeners, applicationArguments);
  configureIgnoreBeanInfo(environment);
     // 打印SpringBoot的banner和版本
  Banner printedBanner = printBanner(environment);
     // 创建对应的ApplicationContext：Web类型，Reactive类型，普通的类型(非Web)
  context = createApplicationContext();
  exceptionReporters = getSpringFactoriesInstances(SpringBootExceptionReporter.class,
    new Class[] { ConfigurableApplicationContext.class }, context);
     // 准备ApplicationContext，Initializers设置到ApplicationContext后发布事件：ApplicationContextInitializedEvent
     // 打印启动日志，打印profile信息(如dev, test, prod)
     // 调用EventPublishingRunListener发布ApplicationContext加载完毕事件：ApplicationPreparedEvent
  prepareContext(context, environment, listeners, applicationArguments, printedBanner);
     // 最终会调用到AbstractApplicationContext#refresh方法，实际上就是Spring IOC容器的创建过程，并且会进行自动装配的操作
     // 以及发布ApplicationContext已经refresh事件，标志着ApplicationContext初始化完成
  refreshContext(context);
     // hook方法
  afterRefresh(context, applicationArguments);
     // stopWatch停止计时，日志打印总共启动的时间
  stopWatch.stop();
  if (this.logStartupInfo) {
   new StartupInfoLogger(this.mainApplicationClass).logStarted(getApplicationLog(), stopWatch);
  }
     // 发布SpringBoot程序已启动事件ApplicationStartedEvent
  listeners.started(context);
     // 调用ApplicationRunner和CommandLineRunner
  callRunners(context, applicationArguments);
 }
 catch (Throwable ex) {
  handleRunFailure(context, ex, exceptionReporters, listeners);
  throw new IllegalStateException(ex);
 }

 try {
     // 最后发布就绪事件ApplicationReadyEvent，标志着SpringBoot可以处理就收的请求了
  listeners.running(context);
 }
 catch (Throwable ex) {
  handleRunFailure(context, ex, exceptionReporters, null);
  throw new IllegalStateException(ex);
 }
 return context;
}
```

# SpringBoot启动事件

- **SpringApplicationRunListeners**的唯一实现是**EventPublishingRunListener**;
- 整个SpringBoot的启动，流程就是各种事件的发布，调用EventPublishingRunListener中的方法。
- **只要明白了EventPublishingRunListener中事件发布的流程，也就明白了SpringBoot启动的大体流程**

## EventPublishingRunListener

方法说明如下：

```java
public class EventPublishingRunListener implements SpringApplicationRunListener, Ordered {

 private final SpringApplication application;

 private final String[] args;

 private final SimpleApplicationEventMulticaster initialMulticaster;

 public EventPublishingRunListener(SpringApplication application, String[] args) {
  this.application = application;
  this.args = args;
  this.initialMulticaster = new SimpleApplicationEventMulticaster();
  for (ApplicationListener<?> listener : application.getListeners()) {
   this.initialMulticaster.addApplicationListener(listener);
  }
 }

 @Override
 public int getOrder() {
  return 0;
 }

    // SpringBoot启动事件
 @Override
 public void starting() {
  this.initialMulticaster.multicastEvent(new ApplicationStartingEvent(this.application, this.args));
 }

    // 创建和配置环境
 @Override
 public void environmentPrepared(ConfigurableEnvironment environment) {
  this.initialMulticaster
    .multicastEvent(new ApplicationEnvironmentPreparedEvent(this.application, this.args, environment));
 }

    // 准备ApplicationContext
 @Override
 public void contextPrepared(ConfigurableApplicationContext context) {
  this.initialMulticaster
    .multicastEvent(new ApplicationContextInitializedEvent(this.application, this.args, context));
 }

    // 发布ApplicationContext已经refresh事件，标志着ApplicationContext初始化完成
 @Override
 public void contextLoaded(ConfigurableApplicationContext context) {
  for (ApplicationListener<?> listener : this.application.getListeners()) {
   if (listener instanceof ApplicationContextAware) {
    ((ApplicationContextAware) listener).setApplicationContext(context);
   }
   context.addApplicationListener(listener);
  }
  this.initialMulticaster.multicastEvent(new ApplicationPreparedEvent(this.application, this.args, context));
 }

    // SpringBoot已启动事件
 @Override
 public void started(ConfigurableApplicationContext context) {
  context.publishEvent(new ApplicationStartedEvent(this.application, this.args, context));
  AvailabilityChangeEvent.publish(context, LivenessState.CORRECT);
 }

    // "SpringBoot现在可以处理接受的请求"事件
 @Override
 public void running(ConfigurableApplicationContext context) {
  context.publishEvent(new ApplicationReadyEvent(this.application, this.args, context));
  AvailabilityChangeEvent.publish(context, ReadinessState.ACCEPTING_TRAFFIC);
 }

 @Override
 public void failed(ConfigurableApplicationContext context, Throwable exception) {
  ApplicationFailedEvent event = new ApplicationFailedEvent(this.application, this.args, context, exception);
  if (context != null && context.isActive()) {
   // Listeners have been registered to the application context so we should
   // use it at this point if we can
   context.publishEvent(event);
  }
  else {
   // An inactive context may not have a multicaster so we use our multicaster to
   // call all of the context's listeners instead
   if (context instanceof AbstractApplicationContext) {
    for (ApplicationListener<?> listener : ((AbstractApplicationContext) context)
      .getApplicationListeners()) {
     this.initialMulticaster.addApplicationListener(listener);
    }
   }
   this.initialMulticaster.setErrorHandler(new LoggingErrorHandler());
   this.initialMulticaster.multicastEvent(event);
  }
 }

 private static class LoggingErrorHandler implements ErrorHandler {

  private static final Log logger = LogFactory.getLog(EventPublishingRunListener.class);

  @Override
  public void handleError(Throwable throwable) {
   logger.warn("Error calling ApplicationEventListener", throwable);
  }

 }

}
```

# SpringIOC 容器初始化过程

由于现在大都是用**SpringBoot**开发，所以呢，`Spring IOC` 初始化的源码，就是**AnnotationConfigApplicationContext**中的源码，**IOC的初始化**就是**该类实例创建**的过程。

创建的过程（**AnnotationConfigApplicationContext的构造方法**），由于**debug过这个源码**，**我个人**把它分为两大步（暂时我先写出我的总结，后续看是否有时间能写一篇关于debug的过程）：

1. 给我们的**Bean**，创建**与之对应的BeanDefinition**，然后把他们放入**ConcurrentHashMap（key:beanName和value:beanDefinition）**中；BeanDefinition实际上包括一些**Bean的信息**，比如**BeanName**, **Scope**, 是否被**@Primary**注解修饰，是否是**@Lazy**，以及**@Description**等注解
2. **refresh()**方法： 创建IOC需要的资源

- 初始化**BeanFactory**, set一些属性，如**BeanClassLoader**，**systemEnvironment**
- 如果是SpringBoot程序，会调用方法进行**自动装配**：AutoConfigurationImportSelector.AutoConfigurationGroup#**process**，见：[@EnableAutoConfiguration的总结](https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html#enableautoconfiguration总结)
- 注册**MessageSource**，国际化相关的资源，到ApplicationContext
- 注册**ApplicationListener**到ApplicationContext
- 实例化化**lazy-init**的Bean
- **最后，publish相关的事件，ApplicationContext 就初始化完成，整个IOC容器初始化完成(IOC容器的本质就是初始化BeanFactory和ApplicationContext)，就可以从IOC容器中获取Bean自动注入了**

作者：[rhyme](https://www.cnblogs.com/theRhyme/)

出处：https://www.cnblogs.com/theRhyme/p/how-does-springboot-start.html