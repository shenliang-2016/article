# [Spring-三级缓存和循环依赖](https://segmentfault.com/a/1190000023712597)



[![img](https://avatar-static.segmentfault.com/281/956/2819560278-5b6c538137484_huge128)**KerryWu**](https://segmentfault.com/u/kerrywu)发布于 2020-08-21

![img](https://sponsor.segmentfault.com/lg.php?bannerid=0&campaignid=0&zoneid=25&loc=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000023712597&referer=https%3A%2F%2Fwww.baidu.com%2Flink%3Furl%3DT2C8ad3aVCM6x5rxxzjWkV96CSc_Q2v7pE0CoWjrJ3JxedQJiNFqU-2IetdjqnKGZuBEM7R5CVnCBmHhGD0o2q%26wd%3D%26eqid%3D86699e13000275ce0000000661addd0a&cb=2bfa0dfd4b)

## 1. 循环依赖

什么是依赖注入？假设有两个类A和B，A在实例化的时候需要B的实例，而B在实例化时又需要A的实例，在类的实例化过程就陷入死循环。这也就是传统逻辑上的，“到底是先有鸡，还是先有蛋”的问题？
下面举一个例子,定义了两个类Type和Org：

```java
// Org.java
@Data
@Component
public class Org {
    private final Role role;

    public Org(Role role) {
        this.role = role;
    }
}

// Role.java
@Data
@Component
public class Role {
    private final Org org;

    public Role(Org org) {
        this.org = org;
    }
}
```

这是spring中典型的构造器注入方式，其实也代表了普通非spring bean之间，相互依赖时的实例化过程，但结果在运行的时候直接报循环依赖的错误：

```gradle
***************************
APPLICATION FAILED TO START
***************************

Description:

The dependencies of some of the beans in the application context form a cycle:

   demoController (field private pers.kerry.exercise.springexercise.pojo.Org pers.kerry.exercise.springexercise.controller.DemoController.org)
┌─────┐
|  org defined in file [/Users/kerry/code/idea/spring-exercise/target/classes/pers/kerry/exercise/springexercise/pojo/Org.class]
↑     ↓
|  role defined in file [/Users/kerry/code/idea/spring-exercise/target/classes/pers/kerry/exercise/springexercise/pojo/Role.class]
└─────┘
```

而如果我们改一下代码，把构造器注入方式改成基于属性的注入（@Autowired、@Resouce），奇怪的是不报错了，而且相互依赖的两个bean 都实例化成功了。说明spring框架有解决循环依赖的问题，我们了解spring解决循环依赖的过程，其实有助于进一步了解spring 中 bean的活动过程。

## 2. 三级缓存

我们在之前介绍Bean的生命周期时说过，spring 中 bean的实例化过程，并非只是调用构造方法。除去spring框架本身提供的一些钩子或扩展方法，简单分成下面三个核心方法：

Spring在创建Bean的过程中分为三步

1. 实例化，对应方法：AbstractAutowireCapableBeanFactory中的createBeanInstance方法，简单理解就是new了一个对象。
2. 属性注入，对应方法：AbstractAutowireCapableBeanFactory的populateBean方法，为实例化中new出来的对象填充属性和注入依赖。
3. 初始化，对应方法：AbstractAutowireCapableBeanFactory的initializeBean，执行aware接口中的方法，初始化方法，完成AOP代理。

从单例Bean的初始化来看，主要可能发生循环依赖的环节就在第二步`populate`。值得注意的是，`基于构造方法注入`的方式，其实是将第一步和第二步同时进行，因此马上就抛出错误。而spring通过`基于属性注入`的方式，是否有其他特殊的处理呢，我们这时候就要提到spring的三级缓存：

- private final Map<String, Object> singletonObjects = new ConcurrentHashMap<>(256);
- private final Map<String, Object> earlySingletonObjects = new HashMap<>(16);
- private final Map<String, ObjectFactory<?>> singletonFactories = new HashMap<>(16);

| 缓存                  | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| singletonObjects      | 第一级缓存，存放可用的完全初始化，成品的Bean。               |
| earlySingletonObjects | 第二级缓存，存放半成品的Bean，半成品的Bean是已创建对象，但是未注入属性和初始化。用以解决循环依赖。 |
| singletonFactories    | 第三级缓存，存的是Bean工厂对象，用来生成半成品的Bean并放入到二级缓存中。用以解决循环依赖。如果Bean存在AOP的话，返回的是AOP的代理对象。 |

## 3. 核心方法：getSingleton

我们在获取bean实例的时候，其实是先从三级缓存中获取，`getBean` 方法的逻辑如下：

```java
Object sharedInstance = getSingleton(beanName);

public Object getSingleton(String beanName) {
    return getSingleton(beanName, true);
}

protected Object getSingleton(String beanName, boolean allowEarlyReference) {
    // 查询缓存中是否有创建好的单例
    Object singletonObject = this.singletonObjects.get(beanName);
    // 如果缓存不存在，判断是否正在创建中
    if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
        // 加锁防止并发
        synchronized (this.singletonObjects) {
            // 从earlySingletonObjects中查询是否有early缓存
            singletonObject = this.earlySingletonObjects.get(beanName);
            // early缓存也不存在，且允许early引用
            if (singletonObject == null && allowEarlyReference) {
                // 从单例工厂Map里查询beanName
                ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
                if (singletonFactory != null) {
                    // singletonFactory存在，则调用getObject方法拿到单例对象
                    singletonObject = singletonFactory.getObject();
                    // 将单例对象添加到early缓存中
                    this.earlySingletonObjects.put(beanName, singletonObject);
                    // 移除单例工厂中对应的singletonFactory
                    this.singletonFactories.remove(beanName);
                }
            }
        }
    }
    return (singletonObject != NULL_OBJECT ? singletonObject : null);
}
```

1. 只针对单例的bean，多例的后面讨论
2. 默认的singletonObjects缓存不存在要get的beanName时，判断beanName是否正在创建中
3. 从early缓存earlySingletonObjects中再查询，early缓存是用来缓存已实例化但未组装完成的bean
4. 如果early缓存也不存在，从singletonFactories中查找是否有beanName对应的ObjectFactory对象工厂
5. 如果对象工厂存在，则调用getObject方法拿到bean对象
6. 将bean对象加入early缓存，并移除singletonFactories的对象工厂

这是 `getBean`的逻辑，三级缓存中一级一级地找匹配的Bean，直到最后一级缓存，通过匹配beanName 的 ObjectFactory 来获取Bean。那么singletonFactories何时放入了可以通过getObject获得bean对象的ObjectFactory呢？

## 4. 核心方法：doCreateBean

Bean的实例化，实际执行的源码是AbstractAutowireCapableBeanFactory类的doCreateBean方法：

```java
 protected Object doCreateBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args) throws BeanCreationException {
        // 1、创建一个对bean原始对象的包装对象-BeanWrapper，执行createBeanInstance，即构造方法或工厂方法，给BeanWrapper赋值
        BeanWrapper instanceWrapper = null;
        if (mbd.isSingleton()) {
            instanceWrapper = (BeanWrapper)this.factoryBeanInstanceCache.remove(beanName);
        }
        if (instanceWrapper == null) {
            instanceWrapper = this.createBeanInstance(beanName, mbd, args);
        }

        Object bean = instanceWrapper.getWrappedInstance();
        Class<?> beanType = instanceWrapper.getWrappedClass();
        if (beanType != NullBean.class) {
            mbd.resolvedTargetType = beanType;
        }
        // 2、允许其他修改beanDefinition，如使用Annotation增强Bean定义等，这通过类MergedBeanDefinitionPostProcessor来完成
        synchronized(mbd.postProcessingLock) {
            if (!mbd.postProcessed) {
                try {
                    this.applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
                } catch (Throwable var17) {
                    throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Post-processing of merged bean definition failed", var17);
                }

                mbd.postProcessed = true;
            }
        }
        // 3、将当前bean 的 ObjetFactory放入singletonFactories中， 
        boolean earlySingletonExposure = mbd.isSingleton() && this.allowCircularReferences && this.isSingletonCurrentlyInCreation(beanName);
        if (earlySingletonExposure) {
            if (this.logger.isTraceEnabled()) {
                this.logger.trace("Eagerly caching bean '" + beanName + "' to allow for resolving potential circular references");
            }

            this.addSingletonFactory(beanName, () -> {
                return this.getEarlyBeanReference(beanName, mbd, bean);
            });
        }

        Object exposedObject = bean;
        // 4、执行 populateBean，设置属性值
        // 5、执行 initializeBean，调用 Bean的初始化方法
        try {
            this.populateBean(beanName, mbd, instanceWrapper);
            exposedObject = this.initializeBean(beanName, exposedObject, mbd);
        } catch (Throwable var18) {
            if (var18 instanceof BeanCreationException && beanName.equals(((BeanCreationException)var18).getBeanName())) {
                throw (BeanCreationException)var18;
            }

            throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Initialization of bean failed", var18);
        }
        // 6、再次处理循环依赖问题
        if (earlySingletonExposure) {
            Object earlySingletonReference = this.getSingleton(beanName, false);
            if (earlySingletonReference != null) {
                if (exposedObject == bean) {
                    exposedObject = earlySingletonReference;
                } else if (!this.allowRawInjectionDespiteWrapping && this.hasDependentBean(beanName)) {
                    String[] dependentBeans = this.getDependentBeans(beanName);
                    Set<String> actualDependentBeans = new LinkedHashSet(dependentBeans.length);
                    String[] var12 = dependentBeans;
                    int var13 = dependentBeans.length;

                    for(int var14 = 0; var14 < var13; ++var14) {
                        String dependentBean = var12[var14];
                        if (!this.removeSingletonIfCreatedForTypeCheckOnly(dependentBean)) {
                            actualDependentBeans.add(dependentBean);
                        }
                    }

                    if (!actualDependentBeans.isEmpty()) {
                        throw new BeanCurrentlyInCreationException(beanName, "Bean with name '" + beanName + "' has been injected into other beans [" + StringUtils.collectionToCommaDelimitedString(actualDependentBeans) + "] in its raw version as part of a circular reference, but has eventually been wrapped. This means that said other beans do not use the final version of the bean. This is often the result of over-eager type matching - consider using 'getBeanNamesForType' with the 'allowEagerInit' flag turned off, for example.");
                    }
                }
            }
        }
        // 7、注册bean的销毁回调方法，在beanFactory中注册销毁通知，以便在容器销毁时，能够做一些后续处理工作
        try {
            this.registerDisposableBeanIfNecessary(beanName, bean, mbd);
            return exposedObject;
        } catch (BeanDefinitionValidationException var16) {
            throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Invalid destruction signature", var16);
        }
    }
```

> BeanWrapper

BeanWrapper接口，作为spring内部的一个核心接口，正如其名，它是bean的包裹类，即在内部中将会保存该bean的实例，提供其它一些扩展功能。同时，BeanWrapper接口还继承了PropertyAccessor, propertyEditorRegistry, TypeConverter、ConfigurablePropertyAccessor接口，所以它还提供了访问bean的属性值、属性编辑器注册、类型转换等功能。

我们回顾一下bean的实例化过程：

1. ResourceLoader加载配置信息
2. BeanDefinitionReader读取并解析<bean>标签，并将<bean>标签的属性转换为BeanDefinition对应的属性，并注册到BeanDefinitionRegistry注册表中。
3. 容器扫描BeanDefinitionRegistry注册表，通过反射机制获取BeanFactoryPostProcessor类型的工厂后处理器，并用这个工厂后处理器对BeanDefinition进行加工。
4. 根据处理过的BeanDefinition，实例化bean。然后BeanWrapper结合BeanDefinitionRegistry和PropertyEditorRegistry对Bean的属性赋值。

## 4. 思考和总结

### 4.1. 问题：多例的循环依赖可以解决吗

单例bean的循环引用是因为每个对象都是固定的，只是提前暴露对象的引用，最终这个引用对应的对象是创建完成的。但是多例的情况下，每次getBean都会创建一个新的对象，那么应该引用哪一个对象呢，这本身就已经是矛盾的了。多实例Bean是每次创建都会调用doGetBean方法，根本没有使用一二三级缓存，肯定不能解决循环依赖。因而spring中对于多例之间相互引用是会提示错误的。

```java
Error creating bean with name 'beanA': Requested bean is currently in creation: Is there an unresolvable circular reference?
```

可见spring会认为多例之间的循环引用是无法解决的。

### 4.2. 问题：构造器、setter注入方式的循环依赖可以解决吗

这里还是拿A和B两个Bean举例说明：

| 注入方式                                           | 是否解决循环依赖 |
| -------------------------------------------------- | ---------------- |
| 均采用setter方法注入                               | 是               |
| 均采用构造器注入                                   | 否               |
| A中注入B的方式为setter方法，B中注入A的方式为构造器 | 是               |
| B中注入A的方式为setter方法，A中注入B的方式为构造器 | 否               |

### 4.3. 问题：为什么是三级缓存，二级不行吗？

我们再整理一下spring解决循环依赖的过程：一级缓存singletonObject存储成品的Bean，二级缓存earlySingletonObject存储半成品的Bean，当出现循环依赖时可以先注入earlySingletonObject中的Bean实例。那三级缓存singletonFactory存在的意义何在？

singletonFactory 存储的对象工厂是 ObjectFactory，这是一个函数式接口，唯一抽象方法是getObject。在doCreateBean方法的第三步addSingletonFactory，往singletonFactory添加ObjectFactory的匿名内部类中，返回对象的方法是getEarlyBeanReference。

```java
this.addSingletonFactory(beanName, () -> {
                return this.getEarlyBeanReference(beanName, mbd, bean);
            });
```

我们再看看 getEarlyBeanReference 的方法实现：

```java
protected Object getEarlyBeanReference(String beanName, RootBeanDefinition mbd, Object bean) {
    Object exposedObject = bean;
    if (bean != null && !mbd.isSynthetic() && hasInstantiationAwareBeanPostProcessors()) {
        for (BeanPostProcessor bp : getBeanPostProcessors()) {
            if (bp instanceof SmartInstantiationAwareBeanPostProcessor) {
                SmartInstantiationAwareBeanPostProcessor ibp = (SmartInstantiationAwareBeanPostProcessor) bp;
                exposedObject = ibp.getEarlyBeanReference(exposedObject, beanName);
                if (exposedObject == null) {
                    return exposedObject;
                }
            }
        }
    }
    return exposedObject;
}
```

这里也设置了一个InstantiationAwareBeanPostProcessor后置处理器的扩展点，允许在对象返回之前修改甚至替换bean，总的来说，这是某一AOP方法的实现步骤。因此如果存在 AOP的定义，singletonFactory返回的不是原始的Bean实例，而是实现AOP方法的代理类。

那么如果在doCreateBean方法中，直接生成Bean基于AOP的代理对象，将代理对象存入二级缓存earlySingleton，是不是还是可以不需要三级缓存singletonFactory呢？

如果这么做了，就把AOP中创建代理对象的时机提前了，不管是否发生循环依赖，都在doCreateBean方法中完成了AOP的代理。不仅没有必要，而且违背了Spring在结合AOP跟Bean的生命周期的设计！Spring结合AOP跟Bean的生命周期本身就是通过AnnotationAwareAspectJAutoProxyCreator这个后置处理器来完成的，在这个后置处理的postProcessAfterInitialization方法中对初始化后的Bean完成AOP代理。**如果出现了循环依赖，那没有办法，只有给Bean先创建代理，但是没有出现循环依赖的情况下，设计之初就是让Bean在生命周期的最后一步完成代理而不是在实例化后就立马完成代理。**

> **1. 一级缓存：singletonObjects 单例池**

单例 Bean 创建完成后就放在 singletonObjects 这个 Map 里面，这就是一级缓存。

> **2. 二级缓存：earlySingletonObjects**

earlySingletonObjects 这个 Map 存放提前暴露 Bean 的引用，实例化以后，就把对象放入到这个 Map 中。

`b.setA(getBean("a"))` 在加载 b 的过程中，可以在 earlySingletonObjects 拿到 a 的引用，此时 a 仅仅经过了实例化，并没有设置属性。

getEarlyBeanReference(beanName, mbd, bean)有可能会进行 AOP 的增强，创建代理类，因此二级缓存 earlySingletonObjects 存放的有可能是经过 AOP 增强的代理对像。

> **3. 三级缓存：singletonFactories**

为了解决二级缓存中 AOP 生成新对象的问题，Spring 中的解决方案就是提前 AOP。

在加载 b 的流程中，如果发生了循环依赖，就是说 b 又依赖了 a，我们就要对 a 执行 AOP，提前获取增强以后的 a 对象，这样 b 对象依赖的 a 对象就是增强以后的 a 了。

三级缓存的 key 是 beanName，value 是一个 lambda 表达式，这个 lambda 表达式的作用就是进行提前 AOP。

![image](https://segmentfault.com/img/bVcOKJD)

### 4.4. 总结

我们再回顾spring中循环依赖的解决流程，网上看到一个流程图很能清晰的说明其中过程。

![image](https://segmentfault.com/img/bVbLETo)

Spring通过三级缓存解决了循环依赖。一级缓存为单例池，二级缓存为早期曝光对象，三级缓存为早期曝光对象工厂。当A、B两类发生循环引用，在A实例化之后，将自己提早曝光(即加入三级缓存)，如果A初始AOP代理，该工厂对象返回的是被代理的对象，若未被代理，返回对象本身。当A进行属性注入时，经过之前实例化步骤，此时轮到B属性注入，调用getBean(a)获取A对象，由于A处理正在创建集合中，此时也发了循环依赖，所以可以从三级缓存获取对象工厂(如果A被AOP代理，此时返回就是代理对象)，并把对象放到二级缓存中，这样保证A只经过一次AOP代理。接下来，B走完Spring生命周期流程，并放入单例池中。当B创建完后，会将B注入A，A走完Spring生命周期流程。到此，循环依赖结束。











