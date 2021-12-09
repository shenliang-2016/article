# [MyBatis之分页插件(PageHelper)工作原理](https://www.cnblogs.com/dengpengbo/p/10579631.html)

 数据分页功能是我们软件系统中必备的功能，在持久层使用mybatis的情况下，pageHelper来实现后台分页则是我们常用的一个选择，所以本文专门类介绍下。

# PageHelper原理

相关依赖

```xml
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis</artifactId>
	<version>3.2.8</version>
</dependency>
<dependency>
	<groupId>com.github.pagehelper</groupId>
	<artifactId>pagehelper</artifactId>
	<version>1.2.15</version>
</dependency>
```

## 1.添加plugin

  要使用PageHelper首先在mybatis的全局配置文件中配置。如下:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
		PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
		"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

	<plugins>
		<!-- com.github.pagehelper为PageHelper类所在包名 -->
		<plugin interceptor="com.github.pagehelper.PageHelper">
			<property name="dialect" value="mysql" />
			<!-- 该参数默认为false -->
			<!-- 设置为true时，会将RowBounds第一个参数offset当成pageNum页码使用 -->
			<!-- 和startPage中的pageNum效果一样 -->
			<property name="offsetAsPageNum" value="true" />
			<!-- 该参数默认为false -->
			<!-- 设置为true时，使用RowBounds分页会进行count查询 -->
			<property name="rowBoundsWithCount" value="true" />
			<!-- 设置为true时，如果pageSize=0或者RowBounds.limit = 0就会查询出全部的结果 -->
			<!-- （相当于没有执行分页查询，但是返回结果仍然是Page类型） -->
			<property name="pageSizeZero" value="true" />
			<!-- 3.3.0版本可用 - 分页参数合理化，默认false禁用 -->
			<!-- 启用合理化时，如果pageNum<1会查询第一页，如果pageNum>pages会查询最后一页 -->
			<!-- 禁用合理化时，如果pageNum<1或pageNum>pages会返回空数据 -->
			<property name="reasonable" value="false" />
			<!-- 3.5.0版本可用 - 为了支持startPage(Object params)方法 -->
			<!-- 增加了一个`params`参数来配置参数映射，用于从Map或ServletRequest中取值 -->
			<!-- 可以配置pageNum,pageSize,count,pageSizeZero,reasonable,不配置映射的用默认值 -->
			<!-- 不理解该含义的前提下，不要随便复制该配置 -->
			<property name="params" value="pageNum=start;pageSize=limit;" />
			<!-- always总是返回PageInfo类型,check检查返回类型是否为PageInfo,none返回Page -->
			<property name="returnPageInfo" value="check" />
		</plugin>
	</plugins>
</configuration>
```

## 2.加载过程

  我们通过如下几行代码来演示过程

```java
// 获取配置文件
InputStream inputStream = Resources.getResourceAsStream("mybatis/mybatis-config.xml");
// 通过加载配置文件获取SqlSessionFactory对象
SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(inputStream);
// 获取SqlSession对象
SqlSession session = factory.openSession();
PageHelper.startPage(1, 5);
session.selectList("com.bobo.UserMapper.query");
```

加载配置文件我们从这行代码开始

```java
new SqlSessionFactoryBuilder().build(inputStream);
 public SqlSessionFactory build(InputStream inputStream) {
   return build(inputStream, null, null);
 }
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322152947419.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322153016724.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322153044143.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)

```java
private void pluginElement(XNode parent) throws Exception {
  if (parent != null) {
    for (XNode child : parent.getChildren()) {
      // 获取到内容:com.github.pagehelper.PageHelper
      String interceptor = child.getStringAttribute("interceptor");
      // 获取配置的属性信息
      Properties properties = child.getChildrenAsProperties();
      // 创建的拦截器实例
      Interceptor interceptorInstance = (Interceptor) resolveClass(interceptor).newInstance();
      // 将属性和拦截器绑定
      interceptorInstance.setProperties(properties);
      // 这个方法需要进入查看
      configuration.addInterceptor(interceptorInstance);
    }
  }
}
  public void addInterceptor(Interceptor interceptor) {
  	// 将拦截器添加到了 拦截器链中 而拦截器链本质上就是一个List有序集合
    interceptorChain.addInterceptor(interceptor);
  }
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322153357145.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)

**小结**:通过SqlSessionFactory对象的获取，我们加载了全局配置文件及映射文件同时还将配置的拦截器添加到了拦截器链中。

## 3.PageHelper定义的拦截信息

  我们来看下PageHelper的源代码的头部定义

```java
@SuppressWarnings("rawtypes")
@Intercepts(
	@Signature(
		type = Executor.class, 
		method = "query", 
		args = {MappedStatement.class
				, Object.class
				, RowBounds.class
				, ResultHandler.class
			}))
public class PageHelper implements Interceptor {
    //sql工具类
    private SqlUtil sqlUtil;
    //属性参数信息
    private Properties properties;
    //配置对象方式
    private SqlUtilConfig sqlUtilConfig;
    //自动获取dialect,如果没有setProperties或setSqlUtilConfig，也可以正常进行
    private boolean autoDialect = true;
    //运行时自动获取dialect
    private boolean autoRuntimeDialect;
    //多数据源时，获取jdbcurl后是否关闭数据源
    private boolean closeConn = true;
// 定义的是拦截 Executor对象中的
// query(MappedStatement ms,Object o,RowBounds ob ResultHandler rh)
// 这个方法
type = Executor.class, 
method = "query", 
args = {MappedStatement.class
		, Object.class
		, RowBounds.class
		, ResultHandler.class
	}))
```

PageHelper中已经定义了该拦截器拦截的方法是什么。

## 4.Executor

  接下来我们需要分析下SqlSession的实例化过程中Executor发生了什么。我们需要从这行代码开始跟踪

```java
SqlSession session = factory.openSession();
public SqlSession openSession() {
  return openSessionFromDataSource(configuration.getDefaultExecutorType(), null, false);
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019032215422628.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322154317345.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322154354773.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322154502409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)

增强Executor
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322154539962.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322154708810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)

  到此我们明白了,Executor对象其实被我们生存的代理类增强了。invoke的代码为

```java
public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
  try {
    Set<Method> methods = signatureMap.get(method.getDeclaringClass());
    // 如果是定义的拦截的方法 就执行intercept方法
    if (methods != null && methods.contains(method)) {
      // 进入查看 该方法增强
      return interceptor.intercept(new Invocation(target, method, args));
    }
    // 不是需要拦截的方法 直接执行
    return method.invoke(target, args);
  } catch (Exception e) {
    throw ExceptionUtil.unwrapThrowable(e);
  }
}
/**
 * Mybatis拦截器方法
 *
 * @param invocation 拦截器入参
 * @return 返回执行结果
 * @throws Throwable 抛出异常
 */
public Object intercept(Invocation invocation) throws Throwable {
    if (autoRuntimeDialect) {
        SqlUtil sqlUtil = getSqlUtil(invocation);
        return sqlUtil.processPage(invocation);
    } else {
        if (autoDialect) {
            initSqlUtil(invocation);
        }
        return sqlUtil.processPage(invocation);
    }
}
```

该方法中的内容我们后面再分析。Executor的分析我们到此，接下来看下PageHelper实现分页的具体过程。

## 5.分页过程

  接下来我们通过代码跟踪来看下具体的分页流程，我们需要分别从两行代码开始:

### 5.1 startPage

```java
PageHelper.startPage(1, 5);
/**
 * 开始分页
 *
 * @param params
 */
public static <E> Page<E> startPage(Object params) {
    Page<E> page = SqlUtil.getPageFromObject(params);
    //当已经执行过orderBy的时候
    Page<E> oldPage = SqlUtil.getLocalPage();
    if (oldPage != null && oldPage.isOrderByOnly()) {
        page.setOrderBy(oldPage.getOrderBy());
    }
    SqlUtil.setLocalPage(page);
    return page;
}
/**
 * 开始分页
 *
 * @param pageNum    页码
 * @param pageSize   每页显示数量
 * @param count      是否进行count查询
 * @param reasonable 分页合理化,null时用默认配置
 */
public static <E> Page<E> startPage(int pageNum, int pageSize, boolean count, Boolean reasonable) {
    return startPage(pageNum, pageSize, count, reasonable, null);
}
/**
 * 开始分页
 *
 * @param offset 页码
 * @param limit  每页显示数量
 * @param count  是否进行count查询
 */
public static <E> Page<E> offsetPage(int offset, int limit, boolean count) {
    Page<E> page = new Page<E>(new int[]{offset, limit}, count);
    //当已经执行过orderBy的时候
    Page<E> oldPage = SqlUtil.getLocalPage();
    if (oldPage != null && oldPage.isOrderByOnly()) {
        page.setOrderBy(oldPage.getOrderBy());
    }
    // 这是重点！！！
    SqlUtil.setLocalPage(page);
    return page;
}
private static final ThreadLocal<Page> LOCAL_PAGE = new ThreadLocal<Page>();
// 将分页信息保存在ThreadLocal中 线程安全！
public static void setLocalPage(Page page) {
    LOCAL_PAGE.set(page);
}
```

### 5.2selectList方法

```java
session.selectList("com.bobo.UserMapper.query");
public <E> List<E> selectList(String statement) {
  return this.selectList(statement, null);
}

public <E> List<E> selectList(String statement, Object parameter) {
  return this.selectList(statement, parameter, RowBounds.DEFAULT);
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322160044903.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)
我们需要回到invoke方法中继续看

```java
/**
 * Mybatis拦截器方法
 *
 * @param invocation 拦截器入参
 * @return 返回执行结果
 * @throws Throwable 抛出异常
 */
public Object intercept(Invocation invocation) throws Throwable {
    if (autoRuntimeDialect) {
        SqlUtil sqlUtil = getSqlUtil(invocation);
        return sqlUtil.processPage(invocation);
    } else {
        if (autoDialect) {
            initSqlUtil(invocation);
        }
        return sqlUtil.processPage(invocation);
    }
}
```

进入sqlUtil.processPage(invocation);方法

```java
/**
 * Mybatis拦截器方法
 *
 * @param invocation 拦截器入参
 * @return 返回执行结果
 * @throws Throwable 抛出异常
 */
private Object _processPage(Invocation invocation) throws Throwable {
    final Object[] args = invocation.getArgs();
    Page page = null;
    //支持方法参数时，会先尝试获取Page
    if (supportMethodsArguments) {
    	// 从线程本地变量中获取Page信息，就是我们刚刚设置的
        page = getPage(args);
    }
    //分页信息
    RowBounds rowBounds = (RowBounds) args[2];
    //支持方法参数时，如果page == null就说明没有分页条件，不需要分页查询
    if ((supportMethodsArguments && page == null)
            //当不支持分页参数时，判断LocalPage和RowBounds判断是否需要分页
            || (!supportMethodsArguments && SqlUtil.getLocalPage() == null && rowBounds == RowBounds.DEFAULT)) {
        return invocation.proceed();
    } else {
        //不支持分页参数时，page==null，这里需要获取
        if (!supportMethodsArguments && page == null) {
            page = getPage(args);
        }
        // 进入查看
        return doProcessPage(invocation, page, args);
    }
}
/**
  * Mybatis拦截器方法
  *
  * @param invocation 拦截器入参
  * @return 返回执行结果
  * @throws Throwable 抛出异常
  */
 private Page doProcessPage(Invocation invocation, Page page, Object[] args) throws Throwable {
     //保存RowBounds状态
     RowBounds rowBounds = (RowBounds) args[2];
     //获取原始的ms
     MappedStatement ms = (MappedStatement) args[0];
     //判断并处理为PageSqlSource
     if (!isPageSqlSource(ms)) {
         processMappedStatement(ms);
     }
     //设置当前的parser，后面每次使用前都会set，ThreadLocal的值不会产生不良影响
     ((PageSqlSource)ms.getSqlSource()).setParser(parser);
     try {
         //忽略RowBounds-否则会进行Mybatis自带的内存分页
         args[2] = RowBounds.DEFAULT;
         //如果只进行排序 或 pageSizeZero的判断
         if (isQueryOnly(page)) {
             return doQueryOnly(page, invocation);
         }

         //简单的通过total的值来判断是否进行count查询
         if (page.isCount()) {
             page.setCountSignal(Boolean.TRUE);
             //替换MS
             args[0] = msCountMap.get(ms.getId());
             //查询总数
             Object result = invocation.proceed();
             //还原ms
             args[0] = ms;
             //设置总数
             page.setTotal((Integer) ((List) result).get(0));
             if (page.getTotal() == 0) {
                 return page;
             }
         } else {
             page.setTotal(-1l);
         }
         //pageSize>0的时候执行分页查询，pageSize<=0的时候不执行相当于可能只返回了一个count
         if (page.getPageSize() > 0 &&
                 ((rowBounds == RowBounds.DEFAULT && page.getPageNum() > 0)
                         || rowBounds != RowBounds.DEFAULT)) {
             //将参数中的MappedStatement替换为新的qs
             page.setCountSignal(null);
             // 重点是查看该方法
             BoundSql boundSql = ms.getBoundSql(args[1]);
             args[1] = parser.setPageParameter(ms, args[1], boundSql, page);
             page.setCountSignal(Boolean.FALSE);
             //执行分页查询
             Object result = invocation.proceed();
             //得到处理结果
             page.addAll((List) result);
         }
     } finally {
         ((PageSqlSource)ms.getSqlSource()).removeParser();
     }

     //返回结果
     return page;
 }
```

进入 BoundSql boundSql = ms.getBoundSql(args[1])方法跟踪到PageStaticSqlSource类中的

```java
@Override
protected BoundSql getPageBoundSql(Object parameterObject) {
    String tempSql = sql;
    String orderBy = PageHelper.getOrderBy();
    if (orderBy != null) {
        tempSql = OrderByParser.converToOrderBySql(sql, orderBy);
    }
    tempSql = localParser.get().getPageSql(tempSql);
    return new BoundSql(configuration, tempSql, localParser.get().getPageParameterMapping(configuration, original.getBoundSql(parameterObject)), parameterObject);
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322162541526.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322162608772.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)

也可以看Oracle的分页实现
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190322162640212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kcGItYm9ib2thb3lhLXNtLmJsb2cuY3Nkbi5uZXQ=,size_16,color_FFFFFF,t_70)

至此我们发现PageHelper分页的实现原来是在我们执行SQL语句之前动态的将SQL语句拼接了分页的语句，从而实现了从数据库中分页获取的过程。





