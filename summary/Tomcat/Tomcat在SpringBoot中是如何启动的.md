## Tomcat在SpringBoot中是如何启动的

https://my.oschina.net/luozhou/blog/3088908

## 前言

我们知道SpringBoot给我们带来了一个全新的开发体验，我们可以直接把web程序打成jar包，直接启动，这就得益于SpringBoot内置了容器，可以直接启动。本文将以Tomcat为例，来看看SpringBoot是如何启动Tomcat的，同时也将展开学习下Tomcat的源码，了解Tomcat的设计。

## 从 Main 方法说起

用过SpringBoot的人都知道，首先要写一个main方法来启动

```java
@SpringBootApplication
public class TomcatdebugApplication {

    public static void main(String[] args) {
        SpringApplication.run(TomcatdebugApplication.class, args);
    }

}
```

我们直接点击run方法的源码，跟踪下来，发下最终 的`run`方法是调用`ConfigurableApplicationContext`方法，源码如下：

```java
public ConfigurableApplicationContext run(String... args) {
		StopWatch stopWatch = new StopWatch();
		stopWatch.start();
		ConfigurableApplicationContext context = null;
		Collection<springbootexceptionreporter> exceptionReporters = new ArrayList&lt;&gt;();
		//设置系统属性『java.awt.headless』，为true则启用headless模式支持
		configureHeadlessProperty();
		//通过*SpringFactoriesLoader*检索*META-INF/spring.factories*，
       //找到声明的所有SpringApplicationRunListener的实现类并将其实例化，
       //之后逐个调用其started()方法，广播SpringBoot要开始执行了
		SpringApplicationRunListeners listeners = getRunListeners(args);
		//发布应用开始启动事件
		listeners.starting();
		try {
		//初始化参数
			ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
			//创建并配置当前SpringBoot应用将要使用的Environment（包括配置要使用的PropertySource以及Profile）,
        //并遍历调用所有的SpringApplicationRunListener的environmentPrepared()方法，广播Environment准备完毕。
			ConfigurableEnvironment environment = prepareEnvironment(listeners, applicationArguments);
			configureIgnoreBeanInfo(environment);
			//打印banner
			Banner printedBanner = printBanner(environment);
			//创建应用上下文
			context = createApplicationContext();
			//通过*SpringFactoriesLoader*检索*META-INF/spring.factories*，获取并实例化异常分析器
			exceptionReporters = getSpringFactoriesInstances(SpringBootExceptionReporter.class,
					new Class[] { ConfigurableApplicationContext.class }, context);
			//为ApplicationContext加载environment，之后逐个执行ApplicationContextInitializer的initialize()方法来进一步封装ApplicationContext，
        //并调用所有的SpringApplicationRunListener的contextPrepared()方法，【EventPublishingRunListener只提供了一个空的contextPrepared()方法】，
        //之后初始化IoC容器，并调用SpringApplicationRunListener的contextLoaded()方法，广播ApplicationContext的IoC加载完成，
        //这里就包括通过**@EnableAutoConfiguration**导入的各种自动配置类。
			prepareContext(context, environment, listeners, applicationArguments, printedBanner);
			//刷新上下文
			refreshContext(context);
			//再一次刷新上下文,其实是空方法，可能是为了后续扩展。
			afterRefresh(context, applicationArguments);
			stopWatch.stop();
			if (this.logStartupInfo) {
				new StartupInfoLogger(this.mainApplicationClass).logStarted(getApplicationLog(), stopWatch);
			}
			//发布应用已经启动的事件
			listeners.started(context);
			//遍历所有注册的ApplicationRunner和CommandLineRunner，并执行其run()方法。
      //我们可以实现自己的ApplicationRunner或者CommandLineRunner，来对SpringBoot的启动过程进行扩展。
			callRunners(context, applicationArguments);
		}
		catch (Throwable ex) {
			handleRunFailure(context, ex, exceptionReporters, listeners);
			throw new IllegalStateException(ex);
		}

		try {
		//应用已经启动完成的监听事件
			listeners.running(context);
		}
		catch (Throwable ex) {
			handleRunFailure(context, ex, exceptionReporters, null);
			throw new IllegalStateException(ex);
		}
		return context;
	}
```

其实这个方法我们可以简单的总结下步骤为 > 1. 配置属性 > 2. 获取监听器，发布应用开始启动事件 > 3. 初始化输入参数 > 4. 配置环境，输出banner > 5. 创建上下文 > 6. 预处理上下文 > 7. 刷新上下文 > 8. 再刷新上下文 > 9. 发布应用已经启动事件 > 10. 发布应用启动完成事件。

其实上面这段代码，如果只要分析tomcat内容的话，只需要关注两个内容即可，上下文是如何创建的，上下文是如何刷新的，分别对应的方法就是`createApplicationContext()` 和`refreshContext(context)`，接下来我们来看看这两个方法做了什么。

```java
protected ConfigurableApplicationContext createApplicationContext() {
		Class<!--?--> contextClass = this.applicationContextClass;
		if (contextClass == null) {
			try {
				switch (this.webApplicationType) {
				case SERVLET:
					contextClass = Class.forName(DEFAULT_SERVLET_WEB_CONTEXT_CLASS);
					break;
				case REACTIVE:
					contextClass = Class.forName(DEFAULT_REACTIVE_WEB_CONTEXT_CLASS);
					break;
				default:
					contextClass = Class.forName(DEFAULT_CONTEXT_CLASS);
				}
			}
			catch (ClassNotFoundException ex) {
				throw new IllegalStateException(
						"Unable create a default ApplicationContext, " + "please specify an ApplicationContextClass",
						ex);
			}
		}
		return (ConfigurableApplicationContext) BeanUtils.instantiateClass(contextClass);
	}
```

这里就是根据我们的`webApplicationType` 来判断创建哪种类型的Servlet，代码中分别对应着Web类型(SERVLET)，响应式Web类型（REACTIVE)，非Web类型（default)。我们建立的是Web类型，所以肯定实例化 `DEFAULT_SERVLET_WEB_CONTEXT_CLASS`指定的类，也就是`AnnotationConfigServletWebServerApplicationContext`类。我们来用图来说明下这个类的关系

![img](https://oscimg.oschina.net/oscnet/ddfa51d6e2de3d57c7422625e51f6250314.jpg)

通过这个类图我们可以知道，这个类继承的是`ServletWebServerApplicationContext`，这就是我们真正的主角，而这个类最终是继承了`AbstractApplicationContext`。了解完创建上下文的情况后，我们再来看看刷新上下文，相关代码如下：

```java
//类：SpringApplication.java

private void refreshContext(ConfigurableApplicationContext context) {
    //直接调用刷新方法
		refresh(context);
		if (this.registerShutdownHook) {
			try {
				context.registerShutdownHook();
			}
			catch (AccessControlException ex) {
				// Not allowed in some environments.
			}
		}
	}
//类：SpringApplication.java

protected void refresh(ApplicationContext applicationContext) {
		Assert.isInstanceOf(AbstractApplicationContext.class, applicationContext);
		((AbstractApplicationContext) applicationContext).refresh();
	}
```

这里还是直接传递调用本类的`refresh(context)`方法，最后是强转成父类`AbstractApplicationContext`调用其`refresh()`方法，该代码如下：

```java
// 类：AbstractApplicationContext	
public void refresh() throws BeansException, IllegalStateException {
		synchronized (this.startupShutdownMonitor) {
			// Prepare this context for refreshing.
			prepareRefresh();

			// Tell the subclass to refresh the internal bean factory.
			ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();

			// Prepare the bean factory for use in this context.
			prepareBeanFactory(beanFactory);

			try {
				// Allows post-processing of the bean factory in context subclasses.
				postProcessBeanFactory(beanFactory);

				// Invoke factory processors registered as beans in the context.
				invokeBeanFactoryPostProcessors(beanFactory);

				// Register bean processors that intercept bean creation.
				registerBeanPostProcessors(beanFactory);

				// Initialize message source for this context.
				initMessageSource();

				// Initialize event multicaster for this context.
				initApplicationEventMulticaster();

				// Initialize other special beans in specific context subclasses.这里的意思就是调用各个子类的onRefresh()
				onRefresh();

				// Check for listener beans and register them.
				registerListeners();

				// Instantiate all remaining (non-lazy-init) singletons.
				finishBeanFactoryInitialization(beanFactory);

				// Last step: publish corresponding event.
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

这里我们看到`onRefresh()`方法是调用其子类的实现，根据我们上文的分析，我们这里的子类是`ServletWebServerApplicationContext`。

```java
//类：ServletWebServerApplicationContext
protected void onRefresh() {
		super.onRefresh();
		try {
			createWebServer();
		}
		catch (Throwable ex) {
			throw new ApplicationContextException("Unable to start web server", ex);
		}
	}
	
private void createWebServer() {
		WebServer webServer = this.webServer;
		ServletContext servletContext = getServletContext();
		if (webServer == null &amp;&amp; servletContext == null) {
			ServletWebServerFactory factory = getWebServerFactory();
			this.webServer = factory.getWebServer(getSelfInitializer());
		}
		else if (servletContext != null) {
			try {
				getSelfInitializer().onStartup(servletContext);
			}
			catch (ServletException ex) {
				throw new ApplicationContextException("Cannot initialize servlet context", ex);
			}
		}
		initPropertySources();
	}
```

到这里，其实庐山真面目已经出来了，`createWebServer()`就是启动web服务，但是还没有真正启动Tomcat。既然`webServer`是通过`ServletWebServerFactory`来获取的，我们就来看看这个工厂的真面目。

![img](https://oscimg.oschina.net/oscnet/32105bd09038062130bae500d6717f223f8.jpg)

## 走进Tomcat内部

根据上图我们发现，工厂类是一个接口，各个具体服务的实现是由各个子类来实现的，所以我们就去看看`TomcatServletWebServerFactory.getWebServer()`的实现。

```java
	@Override
	public WebServer getWebServer(ServletContextInitializer... initializers) {
		Tomcat tomcat = new Tomcat();
		File baseDir = (this.baseDirectory != null) ? this.baseDirectory : createTempDir("tomcat");
		tomcat.setBaseDir(baseDir.getAbsolutePath());
		Connector connector = new Connector(this.protocol);
		tomcat.getService().addConnector(connector);
		customizeConnector(connector);
		tomcat.setConnector(connector);
		tomcat.getHost().setAutoDeploy(false);
		configureEngine(tomcat.getEngine());
		for (Connector additionalConnector : this.additionalTomcatConnectors) {
			tomcat.getService().addConnector(additionalConnector);
		}
		prepareContext(tomcat.getHost(), initializers);
		return getTomcatWebServer(tomcat);
	}
```

根据上面的代码，我们发现其主要做了两件事情，第一件事就是把Connnctor(我们称之为连接器)对象添加到Tomcat中，第二件事就是`configureEngine`，这连接器我们勉强能理解（不理解后面会述说），那这个`Engine`是什么呢？我们查看`tomcat.getEngine()`的源码：

```java
    public Engine getEngine() {
        Service service = getServer().findServices()[0];
        if (service.getContainer() != null) {
            return service.getContainer();
        }
        Engine engine = new StandardEngine();
        engine.setName( "Tomcat" );
        engine.setDefaultHost(hostname);
        engine.setRealm(createDefaultRealm());
        service.setContainer(engine);
        return engine;
    }
```

根据上面的源码，我们发现，原来这个Engine是容器，我们继续跟踪源码，找到`Container`接口

![img](https://oscimg.oschina.net/oscnet/d46479019a9158e06e887998d303487e90e.jpg)

上图中，我们看到了4个子接口，分别是Engine，Host，Context，Wrapper。我们从继承关系上可以知道他们都是容器，那么他们到底有啥区别呢？我看看他们的注释是怎么说的。

```java
 /**
 If used, an Engine is always the top level Container in a Catalina
 * hierarchy. Therefore, the implementation's <code>setParent()</code> method
 * should throw <code>IllegalArgumentException</code>.
 *
 * @author Craig R. McClanahan
 */
public interface Engine extends Container {
    //省略代码
}
/**
 * <p>
 * The parent Container attached to a Host is generally an Engine, but may
 * be some other implementation, or may be omitted if it is not necessary.
 * </p><p>
 * The child containers attached to a Host are generally implementations
 * of Context (representing an individual servlet context).
 *
 * @author Craig R. McClanahan
 */
public interface Host extends Container {
//省略代码
    
}
/*** </p><p>
 * The parent Container attached to a Context is generally a Host, but may
 * be some other implementation, or may be omitted if it is not necessary.
 * </p><p>
 * The child containers attached to a Context are generally implementations
 * of Wrapper (representing individual servlet definitions).
 * </p><p>
 *
 * @author Craig R. McClanahan
 */
public interface Context extends Container, ContextBind {
    //省略代码
}
/**</p><p>
 * The parent Container attached to a Wrapper will generally be an
 * implementation of Context, representing the servlet context (and
 * therefore the web application) within which this servlet executes.
 * </p><p>
 * Child Containers are not allowed on Wrapper implementations, so the
 * <code>addChild()</code> method should throw an
 * <code>IllegalArgumentException</code>.
 *
 * @author Craig R. McClanahan
 */
public interface Wrapper extends Container {

    //省略代码
}
```

上面的注释翻译过来就是，`Engine`是最高级别的容器，其子容器是`Host`，`Host`的子容器是`Context`，`Wrapper`是`Context`的子容器，所以这4个容器的关系就是父子关系，也就是`Engine`>`Host`>`Context`>`Wrapper`。 我们再看看`Tomcat`类的源码:

```java
//部分源码，其余部分省略。
public class Tomcat {
//设置连接器
     public void setConnector(Connector connector) {
        Service service = getService();
        boolean found = false;
        for (Connector serviceConnector : service.findConnectors()) {
            if (connector == serviceConnector) {
                found = true;
            }
        }
        if (!found) {
            service.addConnector(connector);
        }
    }
    //获取service
       public Service getService() {
        return getServer().findServices()[0];
    }
    //设置Host容器
     public void setHost(Host host) {
        Engine engine = getEngine();
        boolean found = false;
        for (Container engineHost : engine.findChildren()) {
            if (engineHost == host) {
                found = true;
            }
        }
        if (!found) {
            engine.addChild(host);
        }
    }
    //获取Engine容器
     public Engine getEngine() {
        Service service = getServer().findServices()[0];
        if (service.getContainer() != null) {
            return service.getContainer();
        }
        Engine engine = new StandardEngine();
        engine.setName( "Tomcat" );
        engine.setDefaultHost(hostname);
        engine.setRealm(createDefaultRealm());
        service.setContainer(engine);
        return engine;
    }
    //获取server
       public Server getServer() {

        if (server != null) {
            return server;
        }

        System.setProperty("catalina.useNaming", "false");

        server = new StandardServer();

        initBaseDir();

        // Set configuration source
        ConfigFileLoader.setSource(new CatalinaBaseConfigurationSource(new File(basedir), null));

        server.setPort( -1 );

        Service service = new StandardService();
        service.setName("Tomcat");
        server.addService(service);
        return server;
    }
    
    //添加Context容器
      public Context addContext(Host host, String contextPath, String contextName,
            String dir) {
        silence(host, contextName);
        Context ctx = createContext(host, contextPath);
        ctx.setName(contextName);
        ctx.setPath(contextPath);
        ctx.setDocBase(dir);
        ctx.addLifecycleListener(new FixContextListener());

        if (host == null) {
            getHost().addChild(ctx);
        } else {
            host.addChild(ctx);
        }
        
    //添加Wrapper容器
         public static Wrapper addServlet(Context ctx,
                                      String servletName,
                                      Servlet servlet) {
        // will do class for name and set init params
        Wrapper sw = new ExistingStandardWrapper(servlet);
        sw.setName(servletName);
        ctx.addChild(sw);

        return sw;
    }
    
}
```

阅读`Tomcat`的`getServer()`我们可以知道，`Tomcat`的最顶层是`Server`,Server就是`Tomcat`的实例，一个`Tomcat`一个`Server`;通过`getEngine()`我们可以了解到Server下面是Service，而且是多个，一个Service代表我们部署的一个应用，而且我们还可以知道，`Engine`容器，一个`service`只有一个；根据父子关系，我们看`setHost()`源码可以知道，`host`容器有多个；同理，我们发现`addContext()`源码下，`Context`也是多个；`addServlet()`表明`Wrapper`容器也是多个，而且这段代码也暗示了，其实`Wrapper`和`Servlet`是一层意思。另外我们根据`setConnector`源码可以知道，连接器(`Connector`)是设置在`service`下的，而且是可以设置多个连接器(`Connector`)。

根据上面分析，我们可以小结下： Tomcat主要包含了2个核心组件，连接器(Connector)和容器(Container),用图表示如下：

![img](https://oscimg.oschina.net/oscnet/f5163f6d4c2cf52cc41c757356896693782.jpg)

一个`Tomcat`是一个`Server`，一个`Server`下有多个`service`，也就是我们部署的多个应用，一个应用下有多个连接器(`Connector`)和一个容器（`Container`）,容器下有多个子容器，关系用图表示如下：

![img](https://oscimg.oschina.net/oscnet/a98162cf99f8098dd76d307551593266ce0.jpg)

`Engine`下有多个`Host`子容器，`Host`下有多个`Context`子容器，`Context`下有多个`Wrapper`子容器。

## 总结

SpringBoot的启动是通过`new SpringApplication()`实例来启动的，启动过程主要做如下几件事情： > 1. 配置属性 > 2. 获取监听器，发布应用开始启动事件 > 3. 初始化输入参数 > 4. 配置环境，输出banner > 5. 创建上下文 > 6. 预处理上下文 > 7. 刷新上下文 > 8. 再刷新上下文 > 9. 发布应用已经启动事件 > 10. 发布应用启动完成事件。

而启动Tomcat就是在第7步中“刷新上下文”；Tomcat的启动主要是初始化2个核心组件，连接器(Connector)和容器（Container），一个Tomcat实例就是一个Server，一个Server包含多个Service，也就是多个应用程序，每个Service包含多个连接器（Connetor）和一个容器（Container),而容器下又有多个子容器，按照父子关系分别为：Engine，Host，Context，Wrapper。其中除了Engine外，其余的容器都是可以有多个。