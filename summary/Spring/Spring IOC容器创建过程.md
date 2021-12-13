# Spring IOC 容器创建过程

在测试时，经常使用这种方式来创建spring容器

```
//创建基于注解的springIOC容器
ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AopBeanConfig.class);
//创建基于配置文件的springIOC容器
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("/spring-beans.xml");
```

无论哪种方式，最终都会调用AbstractApplicationContext的一个重要方法——refresh()，首先来看这个方法的spring源码

```
    @Override
    public void refresh() throws BeansException, IllegalStateException {
        synchronized (this.startupShutdownMonitor) {
            // 1. Prepare this context for refreshing.
            prepareRefresh();

            // 2. Tell the subclass to refresh the internal bean factory. 
            ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();

            // 3. Prepare the bean factory for use in this context. 
            prepareBeanFactory(beanFactory);

            try {
                // 4. Allows post-processing of the bean factory in context subclasses.
                postProcessBeanFactory(beanFactory);

                // 5. Invoke factory processors registered as beans in the context.
                invokeBeanFactoryPostProcessors(beanFactory);

                // 6. Register bean processors that intercept bean creation.
                registerBeanPostProcessors(beanFactory);

                // 7. Initialize message source for this context.
                initMessageSource();

                // 8. Initialize event multicaster for this context.
                initApplicationEventMulticaster();

                // 9. Initialize other special beans in specific context subclasses.
                onRefresh();

                // 10. Check for listener beans and register them.
                registerListeners();

                // 11. Instantiate all remaining (non-lazy-init) singletons.
                finishBeanFactoryInitialization(beanFactory);

                // 12. Last step: publish corresponding event.
                finishRefresh();
            }

            catch (BeansException ex) {
                if (logger.isWarnEnabled()) {
                    logger.warn("Exception encountered during context initialization - " +
                            "cancelling refresh attempt: " + ex);
                }

                // Destroy already created singletons to avoid dangling resources.
                destroyBeans();

                // Reset 'active' flag.
                cancelRefresh(ex);

                // Propagate exception to caller.
                throw ex;
            }

            finally {
                // Reset common introspection caches in Spring's core, since we
                // might not ever need metadata for singleton beans anymore...
                resetCommonCaches();
            }
        }
    }
```

 

## 重点步骤简析

1. prepareRefresh 准备刷新容器

　　(1) initPropertySources() 自定义属性设置，空方法，留给子类继承

　　(2) getEnvironment.validateRequiredProperties 首先获取环境配置，然后校验必需属性

　　(3) this.earlyApplicationListeners = new LinkedHashSet<>(this.applicationListeners); 

​      初始化事件监听器

　　(4) this.earlyApplicationEvents = new LinkedHashSet<>(); 初始化早期事件

2. obtainFreshBeanFactory 获取组件工厂

　　(1) refreshBeanFactory 新建一个组件工厂，类型为DefaultListableBeanFactory，

​     然后对这个组件工厂设置了一个序列化ID

　　(2) getBeanFactory 返回刚刚创建的组件工厂

3. prepareBeanFactory 对组件工厂做各种预处理设置

　　(1) 在组件工厂中设置类加载器、属性解析器等

　　(2) 在组件工厂中添加部分组件后置处理器，例如ApplicationContextAwareProcessor、ApplicationListenerDetector

　　(3) 在组件工厂中设置忽略自动注入的接口

　　(4) 设置自动装配规则

　　(5) 在组件工厂中注册一些组件，例如环境配置ConfigurableEnvironment

4. postProcessBeanFactory 组件工厂的后置处理工作

5. invokeBeanFactoryPostProcessors 执行组件工厂后置处理器

　　这一步是在组件工厂的标准初始化(1-4)之后进行的，主要是执行BeanFactoryPostProcessor及其子接口的

　　BeanFactoryPostProcessor的子接口主要是指BeanDefinitionRegistryPostProcessor，可以向容器中注册新的组件，这个接口的特点是有两个方法，一个是自身的postProcessBeanDefinitionRegistry，另一个继承自BeanFactoryPostProcessor的postProcessBeanFactory，从源码可以看出，spring会先执行BeanDefinitionRegistryPostProcessor类型的组件的自身方法，然后执行其继承方法，最后才调用非BeanDefinitionRegistryPostProcessor的BeanFactoryPostProcessor的后置处理方法

　　(1) 从容器器中获取BeanDefinitionRegistryPostProcessor类型的组件

　　(2) 将BeanDefinitionRegistryPostProcessor类型的组件按照顺序分类并排序，即是否实现了PriorityOrdered、Ordered接口

　  (3) 依次执行实现了PriorityOrdered接口的、实现了Ordered接口的、没有实现任何顺序接口的组件的postProcessBeanDefinitionRegistry方法

　　(4) 执行所有BeanDefinitionRegistryPostProcessor组件的postProcessBeanFactory方法

　　(5) 从容器中获取其他的BeanFactoryPostProcessor类型的组件，即不是BeanDefinitionRegistryPostProcessor类型的

　　(6) 剩下的步骤跟上面类似，就是先按照实现的顺序接口分类，在每个类别下排序，然后依次执行它们的postProcessBeanFactory方法

6. registerBeanPostProcessors 注册组件后置处理器，这种处理器用于拦截bean的创建过程

beanPostProcessor有很多子接口，每种子接口的执行时机各有不同

　　|-DestructionAwareBeanPostProcessor

　　|-InstantiationAwareBeanPostProcessor　　

　　|-MergedBeanDefinitionPostProcessor

　　|-SmartInstantiationAwareBeanPostProcessor

　　(1) 获取所有的beanPostProcessor的组件名

   (2) 将所有的组件按优先顺序分为三类：

　　　 |-实现了PriorityOrdered接口的列表priorityOrderedPostProcessors

　　　 |-实现了Ordered接口的列表orderedPostProcessors

　　   |-没有实现任何顺序接口的列表nonOrderedPostProcessors

　　  还有一种特殊情况，凡是MergedBeanDefinitionPostProcessor类型的，都放在internalPostProcessors中

　  (3) 注册priorityOrderedPostProcessors

　　(4) 注册orderedPostProcessors

　　(5) 注册nonOrderedPostProcessors

　　(6) 注册internalPostProcessors

　　(7) 注册ApplicationListenerDetector，它的作用是在组件初始化之后判断其是否为

​      ApplicationListner类型，如果是，则将其添加进容器的监听器集合

7. initMessageSource 初始化消息源组件，用于消息绑定、消息解析等功能，并且提供国际化解决方案

　　(1) 获取beanFactory

　　(2) 判断beanFactory中是否包含id为messageSource的组件

　　(3) 如果已存在，则赋值给容器的messageSource属性，这种情况是我们自己在容器中注册了这个组件

　　(4) 如果不存在，则新建一个DelegatingMessageSource，并赋值给容器的messageSource属性，

​      然后在beanFactory中注册这个新组件，并设置其id为messageSource

8. initApplicationEventMulticaster 初始化事件广播器

　　(1) 获取beanFactory

　　(2) 判断beanFactory中是否存在id为applicationEventMulticaster的组件

　　(3) 如果已存在，则赋值给容器的applicationEventMulticaster属性，这种情况是我们自己在容器中注册了这个组件

　　(4) 如果不存在，则新建一个SimpleApplicationEventMulticaster，并赋值给容器的

​      applicationEventMulticaster属性，然后在beanFactory中注册这个新组件，

​      并设置其id为applicationEventMulticaster

9. onRefresh 没有任何操作，留给子类继承的，我们可以自定义子容器，在重写方法中做一些我们想要的操作

10. registerListeners 注册事件监听器

　　(1) 获取容器的属性applicationListeners，这是一个事件监听器的集合，将集合中的每个元素都添加进事件广播器

　　(2) 从容器中获取所有ApplicationListener类型的组件，将这些组件添加进事件广播器

　　(3) 发布早期事件，即容器的earlyApplicationEvents属性(参考第1(4)步)，然后清空早期事件

11. finishBeanFactoryInitialization 完成剩下的单实例bean的初始化

　　(1) 进入DefaultListableBeanFactory.preInstantiateSingletons方法，获取容器中所有的组件id列表

　　(2) 遍历组件id列表，对每个组件，获取其组件定义信息，即RootBeanDefinition

　　(3) 从组件定义信息中筛选掉抽象类、非单实例、懒加载的，这些bean在创建容器时并不初始化，

​      另外还有工厂组件，即实现了FactoryBean接口的，需要另外一套逻辑进行初始化

　　(4) 从缓存中获取单实例bean，即DefaultSingletonBeanRegistry类的singletonObjects属性，所有被创建过的

​      单实例bean都会被缓存在这个映射中；如果缓存中存在，说明这个组件之前被创建过，直接返回

　　(5) 如果缓存中不存在，则开始新建

　　　 ① 将组件标记为已创建，即将其id存入AbstractBeanFactory的alreadyCreated属性中

　　　 ② 获取组件的定义信息，即RootBeanDefinition

　　　 ③ 从定义信息中获取该组件依赖的组件，如果存在，则重新从第11(4)步开始执行，创建这些依赖的组件

　　　 ④ 创建完依赖组件(如果存在)之后，以下开始正式新建目标组件

　　　 ⑤ 给组件后置处理器一个机会用代理对象代替目标对象，即执行InstantiationAwareBeanPostProcessor

​        类型的组件后置处理器的postProcessBeforeInstantiation、postProcessAfterInitialization方法

　　   ⑥ Allow post-processors to modify the merged bean definition，即执行

​        MergedBeanDefinitionPostProcessor类型组件后置处理器的postProcessMergedBeanDefinition方法

　　　 ⑦ 执行AbstractAutowireCapableBeanFactory.populateBean方法，即属性赋值

​        在属性赋值之前，首先拿到InstantiationAwareBeanPostProcessor类型的组件后置处理器，

　　　　  并执行postProcessAfterInstantiation、postProcessProperties、postProcessPropertyValues方法；

　　　　  然后才执行该类的applyPropertyValues方法，利用反射调用组件的setter方法进行属性赋值

　　　 ⑧ 执行以下三种aware接口的方法：BeanNameAware、BeanClassLoaderAware、BeanFactoryAware

　　　 ⑨ 执行组件后置处理器的初始化前方法，即BeanPostProcessor.postProcessBeforeInitialization

​      ⑩ 执行组件的初始化方法，即InitializingBean.afterPropertiesSet，以及在容器中自定义的initMethod

 　  ⑪ 执行组件后置处理器的初始化后方法，即BeanPostProcessor.postProcessAfterInitialization

　　   ⑫ 如果需要，注册组件的销毁方法，例如DisposableBean.destroy，以及在容器中自定义的destroyMethod

​        这里只是注册，并不调用

　　(6) 通过第11(5)步，单实例bean已经创建并初始化完成，接着，会调用AbstractBeanFactory的父类方法——

　　　 DefaultSingletonBeanRegistry.getSingleton方法，将新建的bean存入singletonObjects属性中，即缓存

　　(7) 回到DefaultListableBeanFactory.preInstantiateSingletons方法(见第11(1)步)

　　   如果新建的bean实现了SmartInitializingSingleton接口，则执行afterSingletonsInstantiated回调方法

12. finishRefresh 完成容器刷新

　　(1) 初始化生命周期处理器(LifecycleProcessor)，先从BeanFactory中按类型获取，

​     如果没有就新建一个DefaultLifecycleProcessor，并注册进BeanFactory

　　(2) 获取上一步注册的生命周期处理器，回调其onRefresh方法

　　(3) 发布容器刷新事件，即ContextRefreshedEvent