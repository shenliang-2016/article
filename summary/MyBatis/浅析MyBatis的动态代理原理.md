# [浅析MyBatis的动态代理原理](https://segmentfault.com/a/1190000019130222)

[![img](https://avatar-static.segmentfault.com/101/086/1010865114-5e781b5513762_huge128)**pjmike**](https://segmentfault.com/u/pjmike)发布于 2019-05-09

![img](https://sponsor.segmentfault.com/lg.php?bannerid=0&campaignid=0&zoneid=25&loc=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000019130222&referer=https%3A%2F%2Fwww.baidu.com%2Flink%3Furl%3D4g5aYxJyzqdSte7yiIZHm9S6wbnfVkmJfI0tCW1DORc0JOATp0lJOptd8YgyCsCqJ7G9jZtrvv-B-eLrGyTkMa%26wd%3D%26eqid%3Df20fc782000476e70000000661b04bf0&cb=afc11e2292)

## 前言

一直以来都在使用MyBatis做持久化框架，也知道当我们定义XXXMapper接口类并利用它来做CRUD操作时，Mybatis是利用了动态代理的技术帮我们生成代理类。那么动态代理内部的实现细节到底是怎么的呀？XXXMapper.java类和XXXMapper.xml到底是如何关联起来的呀？本篇文章就来详细剖析下MyBatis的动态代理的具体实现机制。

## MyBatis的核心组件及应用

在详细探究MyBatis中动态代理机制之前，先来补充一下基础知识，认识一下MyBatis的核心组件。

- **SqlSessionFactoryBuilder(构造器)**： 它可以从XML、注解或者手动配置Java代码来创建SqlSessionFactory。
- **SqlSessionFactory**: 用于创建SqlSession (会话) 的工厂
- **SqlSession**: SqlSession是Mybatis最核心的类，可以用于执行语句、提交或回滚事务以及获取映射器Mapper的接口
- **SQL Mapper**： 它是由一个Java接口和XML文件（或注解）构成的，需要给出对应的SQL和映射规则，它负责发送SQL去执行，并返回结果

> 注意： 现在我们使用Mybatis，一般都是和Spring框架整合在一起使用，这种情况下，SqlSession将被Spring框架所创建，所以往往不需要我们使用SqlSessionFactoryBuilder或者SqlSessionFactory去创建SqlSession

下面展示一下如何使用MyBatis的这些组件，或者如何快速使用MyBatis：

1. 数据库表

```sql
CREATE TABLE  user(
  id int,
  name VARCHAR(255) not NULL ,
  age int ,
  PRIMARY KEY (id)
)ENGINE =INNODB DEFAULT CHARSET=utf8;
```

1. 声明一个User类

```java
@Data
public class User {
    private int id;
    private int age;
    private String name;

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

1. 定义一个全局配置文件mybatis-config.xml (关于配置文件中具体属性标签解释参阅官方文档)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--全局配置文件的根元素-->
<configuration>
    <!--enviroments表示环境配置，可以配置成开发环境(development)、测试环境(test)、生产环境(production)等-->
    <environments default="development">
        <environment id="development">
            <!--transactionManager： 事务管理器，属性type只有两个取值：JDBC和MANAGED-->
            <transactionManager type="MANAGED" />
            <!--dataSource: 数据源配置-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver" />
                <property name="url" value="jdbc:mysql://localhost:3306/test"/>
                <property name="username" value="root" />
                <property name="password" value="root" />
            </dataSource>
        </environment>
    </environments>
    <!--mappers文件路径配置-->
    <mappers>
        <mapper resource="mapper/UserMapper.xml"/>
    </mappers>
</configuration>
```

1. UserMapper接口

```java
public interface UserMapper {
    User selectById(int id);
}
```

1. UserMapper文件

```xml
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace属性表示命令空间，不同xml映射文件namespace必须不同-->
<mapper namespace="com.pjmike.mybatis.UserMapper">
    <select id="selectById" parameterType="int"
            resultType="com.pjmike.mybatis.User">
             SELECT id,name,age FROM user where id= #{id}
       </select>
</mapper>
```

1. 测试类

```java
public class MybatisTest {
    private static SqlSessionFactory sqlSessionFactory;
    static {
        try {
            sqlSessionFactory = new SqlSessionFactoryBuilder()
                    .build(Resources.getResourceAsStream("mybatis-config.xml"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    public static void main(String[] args) {
        try (SqlSession sqlSession = sqlSessionFactory.openSession()) {
            UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
            User user = userMapper.selectById(1);
            System.out.println("User : " + user);
        }
    }
}
// 结果：
User : User{id=1, age=21, name='pjmike'}
```

上面的例子简单的展示了如何使用MyBatis，与此同时，我也将用这个例子来进一步探究MyBatis动态原理的实现。

## MyBatis动态代理的实现

```java
public static void main(String[] args) {
    try (SqlSession sqlSession = sqlSessionFactory.openSession()) {
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);// <1>
        User user = userMapper.selectById(1);
        System.out.println("User : " + user);
    }
}
```

在前面的例子中，我们使用sqlSession.getMapper()方法获取UserMapper对象，实际上这里我们是获取了UserMapper接口的代理类，然后再由代理类执行方法。那么这个代理类是如何生成的呢？在探究动态代理类如何生成之前，我们先来看下SqlSessionFactory工厂的创建过程做了哪些准备工作，比如说mybatis-config配置文件是如何读取的，映射器文件是如何读取的？

### mybatis全局配置文件解析

```java
private static SqlSessionFactory sqlSessionFactory;
static {
    try {
        sqlSessionFactory = new SqlSessionFactoryBuilder()
                .build(Resources.getResourceAsStream("mybatis-config.xml"));
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

我们使用new SqlSessionFactoryBuilder().build()的方式创建SqlSessionFactory工厂，走进build方法

```java
 public SqlSessionFactory build(InputStream inputStream, Properties properties) {
    return build(inputStream, null, properties);
  }

  public SqlSessionFactory build(InputStream inputStream, String environment, Properties properties) {
    try {
      XMLConfigBuilder parser = new XMLConfigBuilder(inputStream, environment, properties);
      return build(parser.parse());
    } catch (Exception e) {
      throw ExceptionFactory.wrapException("Error building SqlSession.", e);
    } finally {
      ErrorContext.instance().reset();
      try {
        inputStream.close();
      } catch (IOException e) {
        // Intentionally ignore. Prefer previous error.
      }
    }
  }
```

**对于mybatis的全局配置文件的解析，相关解析代码位于XMLConfigBuilder的parse()方法**中：

```java
 public Configuration parse() {
    if (parsed) {
      throw new BuilderException("Each XMLConfigBuilder can only be used once.");
    }
    parsed = true;
    //解析全局配置文件
    parseConfiguration(parser.evalNode("/configuration"));
    return configuration;
  }

  private void parseConfiguration(XNode root) {
    try {
      //issue #117 read properties first
      propertiesElement(root.evalNode("properties"));
      Properties settings = settingsAsProperties(root.evalNode("settings"));
      loadCustomVfs(settings);
      loadCustomLogImpl(settings);
      typeAliasesElement(root.evalNode("typeAliases"));
      pluginElement(root.evalNode("plugins"));
      objectFactoryElement(root.evalNode("objectFactory"));
      objectWrapperFactoryElement(root.evalNode("objectWrapperFactory"));
      reflectorFactoryElement(root.evalNode("reflectorFactory"));
      settingsElement(settings);
      // read it after objectFactory and objectWrapperFactory issue #631
      environmentsElement(root.evalNode("environments"));
      databaseIdProviderElement(root.evalNode("databaseIdProvider"));
      typeHandlerElement(root.evalNode("typeHandlers"));
      //解析mapper映射器文件
      mapperElement(root.evalNode("mappers"));
    } catch (Exception e) {
      throw new BuilderException("Error parsing SQL Mapper Configuration. Cause: " + e, e);
    }
  }
```

从parseConfiguration方法的源代码中很容易就可以看出它对mybatis全局配置文件中各个元素属性的解析。当然最终解析后返回一个Configuration对象，Configuration是一个很重要的类，它包含了Mybatis的所有配置信息，它是通过XMLConfigBuilder取钱构建的，Mybatis通过XMLConfigBuilder读取mybatis-config.xml中配置的信息，然后将这些信息保存到Configuration中

### 映射器Mapper文件的解析

```java
  //解析mapper映射器文件
  mapperElement(root.evalNode("mappers"));
```

该方法是对全局配置文件中mappers属性的解析，走进去：

![mapper xml](https://segmentfault.com/img/remote/1460000019130225?w=1271&h=528)

`mapperParser.parse()`方法就是XMLMapperBuilder对Mapper映射器文件进行解析，可与XMLConfigBuilder进行类比

```java
  public void parse() {
    if (!configuration.isResourceLoaded(resource)) {
      configurationElement(parser.evalNode("/mapper")); //解析映射文件的根节点mapper元素
      configuration.addLoadedResource(resource);  
      bindMapperForNamespace(); //重点方法，这个方法内部会根据namespace属性值，生成动态代理类
    }
    parsePendingResultMaps();
    parsePendingCacheRefs();
    parsePendingStatements();
  }
```

- **configurationElement(XNode context)方法**

该方法主要用于将mapper文件中的元素信息，比如`insert`、`select`这等信息解析到MappedStatement对象，并保存到Configuration类中的mappedStatements属性中，以便于后续动态代理类执行CRUD操作时能够获取真正的Sql语句信息

![configurationElement](https://segmentfault.com/img/remote/1460000019130226)

buildStatementFromContext方法就用于解析`insert、select`这类元素信息，并将其封装成MappedStatement对象，具体的实现细节这里就不细说了。

- **bindMapperForNamespace()方法**

该方法是核心方法，它会根据mapper文件中的namespace属性值，为接口生成动态代理类，这就来到了我们的主题内容——动态代理类是如何生成的。

### 动态代理类的生成

bindMapperForNamespace方法源码如下所示：

```java
 private void bindMapperForNamespace() {
    //获取mapper元素的namespace属性值
    String namespace = builderAssistant.getCurrentNamespace();
    if (namespace != null) {
      Class<?> boundType = null;
      try {
        // 获取namespace属性值对应的Class对象
        boundType = Resources.classForName(namespace);
      } catch (ClassNotFoundException e) {
        //如果没有这个类，则直接忽略，这是因为namespace属性值只需要唯一即可，并不一定对应一个XXXMapper接口
        //没有XXXMapper接口的时候，我们可以直接使用SqlSession来进行增删改查
      }
      if (boundType != null) {
        if (!configuration.hasMapper(boundType)) {
          // Spring may not know the real resource name so we set a flag
          // to prevent loading again this resource from the mapper interface
          // look at MapperAnnotationBuilder#loadXmlResource
          configuration.addLoadedResource("namespace:" + namespace);
          //如果namespace属性值有对应的Java类，调用Configuration的addMapper方法，将其添加到MapperRegistry中
          configuration.addMapper(boundType);
        }
      }
    }
  }
```

这里提到了Configuration的addMapper方法，实际上Configuration类里面通过MapperRegistry对象维护了所有要生成动态代理类的XxxMapper接口信息，可见Configuration类确实是相当重要一类

```java
public class Configuration {
    ...
    protected MapperRegistry mapperRegistry = new MapperRegistry(this);
    ...
    public <T> void addMapper(Class<T> type) {
      mapperRegistry.addMapper(type);
    }
    public <T> T getMapper(Class<T> type, SqlSession sqlSession) {
      return mapperRegistry.getMapper(type, sqlSession);
    }
    ...
}
```

其中两个重要的方法：getMapper()和addMapper()

- getMapper(): 用于创建接口的动态类
- addMapper(): mybatis在解析配置文件时，会将需要生成动态代理类的接口注册到其中

#### 1. Configuration#addMappper()

Configuration将addMapper方法委托给MapperRegistry的addMapper进行的，源码如下：

```java
  public <T> void addMapper(Class<T> type) {
    // 这个class必须是一个接口，因为是使用JDK动态代理，所以需要是接口，否则不会针对其生成动态代理
    if (type.isInterface()) {
      if (hasMapper(type)) {
        throw new BindingException("Type " + type + " is already known to the MapperRegistry.");
      }
      boolean loadCompleted = false;
      try {
        // 生成一个MapperProxyFactory，用于之后生成动态代理类
        knownMappers.put(type, new MapperProxyFactory<>(type));
        //以下代码片段用于解析我们定义的XxxMapper接口里面使用的注解，这主要是处理不使用xml映射文件的情况
        MapperAnnotationBuilder parser = new MapperAnnotationBuilder(config, type);
        parser.parse();
        loadCompleted = true;
      } finally {
        if (!loadCompleted) {
          knownMappers.remove(type);
        }
      }
    }
  }
```

MapperRegistry内部维护一个映射关系，每个接口对应一个MapperProxyFactory（生成动态代理工厂类）

```java
  private final Map<Class<?>, MapperProxyFactory<?>> knownMappers = new HashMap<>();
```

这样便于在后面调用MapperRegistry的getMapper()时，直接从Map中获取某个接口对应的动态代理工厂类，然后再利用工厂类针对其接口生成真正的动态代理类。

#### 2. Configuration#getMapper()

Configuration的getMapper()方法内部就是调用MapperRegistry的getMapper()方法，源代码如下：

```java
  public <T> T getMapper(Class<T> type, SqlSession sqlSession) {
    //根据Class对象获取创建动态代理的工厂对象MapperProxyFactory
    final MapperProxyFactory<T> mapperProxyFactory = (MapperProxyFactory<T>) knownMappers.get(type);
    if (mapperProxyFactory == null) {
      throw new BindingException("Type " + type + " is not known to the MapperRegistry.");
    }
    try {
      //这里可以看到每次调用都会创建一个新的代理对象返回
      return mapperProxyFactory.newInstance(sqlSession);
    } catch (Exception e) {
      throw new BindingException("Error getting mapper instance. Cause: " + e, e);
    }
  }
```

从上面可以看出，创建动态代理类的核心代码就是在MapperProxyFactory.newInstance方法中，源码如下：

```java
  protected T newInstance(MapperProxy<T> mapperProxy) {
    //这里使用JDK动态代理，通过Proxy.newProxyInstance生成动态代理类
    // newProxyInstance的参数：类加载器、接口类、InvocationHandler接口实现类
    // 动态代理可以将所有接口的调用重定向到调用处理器InvocationHandler，调用它的invoke方法
    return (T) Proxy.newProxyInstance(mapperInterface.getClassLoader(), new Class[] { mapperInterface }, mapperProxy);
  }

  public T newInstance(SqlSession sqlSession) {
    final MapperProxy<T> mapperProxy = new MapperProxy<>(sqlSession, mapperInterface, methodCache);
    return newInstance(mapperProxy);
  }
```

> PS: 关于JDK动态代理的详细介绍这里就不再细说了，有兴趣的可以参阅我之前写的文章：[动态代理的原理及其应用](https://link.segmentfault.com/?enc=%2Bi%2BwiHCZ1lEXC6gNvbmvhA%3D%3D.oWJaM%2FvwKj2yguQBXsbG130M7qrsbN0A5OebqPGKSLU5g8sBMuogPqJ8mgdez0wElBuXsmeeq%2Faea1TCcIjMTbuiX%2FljC7ASB8eLRgK5t4yDPc6n%2B4a5gAmLLSIF9vrdxlN0UbNH16MMmE0yW%2Fow5vMeUKUNnyniLHO805mq0M%2B1LsqQwcFRy6vsJ2NjHBUh)

这里的InvocationHandler接口的实现类是MapperProxy，其源码如下：

```java
public class MapperProxy<T> implements InvocationHandler, Serializable {

  private static final long serialVersionUID = -6424540398559729838L;
  private final SqlSession sqlSession;
  private final Class<T> mapperInterface;
  private final Map<Method, MapperMethod> methodCache;

  public MapperProxy(SqlSession sqlSession, Class<T> mapperInterface, Map<Method, MapperMethod> methodCache) {
    this.sqlSession = sqlSession;
    this.mapperInterface = mapperInterface;
    this.methodCache = methodCache;
  }

  @Override
  public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
    
    try {
      //如果调用的是Object类中定义的方法，直接通过反射调用即可
      if (Object.class.equals(method.getDeclaringClass())) {
        return method.invoke(this, args);
      } else if (isDefaultMethod(method)) {
        return invokeDefaultMethod(proxy, method, args);
      }
    } catch (Throwable t) {
      throw ExceptionUtil.unwrapThrowable(t);
    }
    //调用XxxMapper接口自定义的方法，进行代理
    //首先将当前被调用的方法Method构造成一个MapperMethod对象，然后掉用其execute方法真正的开始执行。
    final MapperMethod mapperMethod = cachedMapperMethod(method);
    return mapperMethod.execute(sqlSession, args);
  }
  private MapperMethod cachedMapperMethod(Method method) {
    return methodCache.computeIfAbsent(method, k -> new MapperMethod(mapperInterface, method, sqlSession.getConfiguration()));
  }
  ...
}
```

最终的执行逻辑在于MapperMethod类的execute方法，源码如下：

```java
public class MapperMethod {

  private final SqlCommand command;
  private final MethodSignature method;

  public MapperMethod(Class<?> mapperInterface, Method method, Configuration config) {
    this.command = new SqlCommand(config, mapperInterface, method);
    this.method = new MethodSignature(config, mapperInterface, method);
  }
  public Object execute(SqlSession sqlSession, Object[] args) {
    Object result;
    switch (command.getType()) {
      //insert语句的处理逻辑
      case INSERT: {
        Object param = method.convertArgsToSqlCommandParam(args);
        result = rowCountResult(sqlSession.insert(command.getName(), param));
        break;
      }
      //update语句的处理逻辑
      case UPDATE: {
        Object param = method.convertArgsToSqlCommandParam(args);
        result = rowCountResult(sqlSession.update(command.getName(), param));
        break;
      }
      //delete语句的处理逻辑
      case DELETE: {
        Object param = method.convertArgsToSqlCommandParam(args);
        result = rowCountResult(sqlSession.delete(command.getName(), param));
        break;
      }
      //select语句的处理逻辑
      case SELECT:
        if (method.returnsVoid() && method.hasResultHandler()) {
          executeWithResultHandler(sqlSession, args);
          result = null;
        } else if (method.returnsMany()) {
          result = executeForMany(sqlSession, args);
        } else if (method.returnsMap()) {
          result = executeForMap(sqlSession, args);
        } else if (method.returnsCursor()) {
          result = executeForCursor(sqlSession, args);
        } else {
          Object param = method.convertArgsToSqlCommandParam(args);
          //调用sqlSession的selectOne方法
          result = sqlSession.selectOne(command.getName(), param);
          if (method.returnsOptional()
              && (result == null || !method.getReturnType().equals(result.getClass()))) {
            result = Optional.ofNullable(result);
          }
        }
        break;
      case FLUSH:
        result = sqlSession.flushStatements();
        break;
      default:
        throw new BindingException("Unknown execution method for: " + command.getName());
    }
    if (result == null && method.getReturnType().isPrimitive() && !method.returnsVoid()) {
      throw new BindingException("Mapper method '" + command.getName()
          + " attempted to return null from a method with a primitive return type (" + method.getReturnType() + ").");
    }
    return result;
  }
  ...
}
```

在MapperMethod中还有两个内部类，SqlCommand和MethodSignature类，在execute方法中首先用switch case语句根据SqlCommand的getType()方法，判断要执行的sql类型，比如INSET、UPDATE、DELETE、SELECT和FLUSH，然后分别调用SqlSession的增删改查等方法。

慢着，说了这么多，那么这个getMapper()方法什么时候被调用呀？实际是一开始我们调用SqlSession的getMapper()方法：

```java
UserMapper userMapper = sqlSession.getMapper(UserMapper.class);

public class DefaultSqlSession implements SqlSession {

  private final Configuration configuration;
  private final Executor executor;
  @Override
  public <T> T getMapper(Class<T> type) {
    return configuration.getMapper(type, this);
  }
  ...
}
```

所以getMapper方法的大致调用逻辑链是：
SqlSession#getMapper() ——> Configuration#getMapper() ——> MapperRegistry#getMapper() ——> MapperProxyFactory#newInstance() ——> Proxy#newProxyInstance()

还有一点我们需要注意：**我们通过SqlSession的getMapper方法获得接口代理来进行CRUD操作，其底层还是依靠的是SqlSession的使用方法**。

## 小结

根据上面的探究过程，简单画了一个逻辑图（不一定准确）：

![Mybatis动态代理](https://segmentfault.com/img/remote/1460000019130227?w=1074&h=421)

本篇文章主要介绍了MyBatis的动态原理，回过头来，我们需要知道我们使用UserMapper的动态代理类进行CRUD操作，本质上还是通过SqlSession这个关键类执行增删改查操作，但是对于SqlSession如何具体执行CRUD的操作并没有仔细阐述，有兴趣的同学可以查阅相关资料。

## 参考资料 & 鸣谢

- [http://www.tianshouzhi.com/ap...](https://link.segmentfault.com/?enc=zQCHiygygSKoDfhAQv%2BV%2BQ%3D%3D.6sXX0dz7Yb4IJzsBGiXnsWvvg3h3EA17L9KbFc4Pxc7pBT9YSeS8qvlwO2D8T3HjYlYgo6zi0lEJ7YiRL9wrEQ%3D%3D)
- [http://www.mybatis.org/mybati...](https://link.segmentfault.com/?enc=AihwzlQ%2FlJM1IuEID%2B5qpw%3D%3D.cfMKfOlPTYazbvVA5AdqUf3cbuml4VXZ69oskppSAqgkacDCWY71LWzjt6THzIm3)











