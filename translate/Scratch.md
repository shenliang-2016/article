### 3.2 解析错误码为错误信息

上面介绍了数据绑定和验证。本章节涵盖对应于验证失败的输出信息。在上一章节中的例子中，我们拒绝了`name`和`age`字段。如果我们希望使用`MessageSource`来输出错误消息，则可以在拒绝字段（例子中是`name`和`age`）时使用错误编码。当我们调用（直接或者间接调用，比如使用`ValidationUtils`类）`rejectValue`或者`Errors`接口中的任何一个其它的`reject`方法。底层实现不仅注册你传入的错误编码，同时还注册了大量额外的错误编码。`MessgeCodesResolver`确定`Errors`接口注册的错误编码。默认地，使用`DefaultMessageCodesResolver`，它不仅注册你给出的错误编码和相应的错误消息，同时还注册包含你传入该`reject`方法的字段名称的消息。因此，如果你通过使用`rejectValue("age", "too.darn.old")`来拒绝字段，除了`too.darn.old`编码，Spring 同时注册了`too.darn.old.age`和`too.darn.old.age.int`（前者包含字段名称而后者包含字段类型）。这样做是为了方便在定位错误消息时帮助开发人员。

有关`MessageCodesResolver`和默认策略的更多细节参见 [`MessageCodesResolver`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/validation/MessageCodesResolver.html) 和 [`DefaultMessageCodesResolver`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/validation/DefaultMessageCodesResolver.html) 文档。

### 3.3 Bean 操纵和 `BeanWrapper`

`org.springframework.beans`包遵循 JavaBeans 标准。所谓的 JavaBean 是这样的类：拥有默认的无参构造器，遵行如下字段命名约定，名为`bingoMadness`的字段有相应的 setter 方法`setBingoMadness(...)`和 getter 方法`getBingoMadness()`。更多信息参考 [javabeans](https://docs.oracle.com/javase/8/docs/api/java/beans/package-summary.html) 。

beans 包中一个相当重要的类是`BeanWrapper`接口和它相应的实现`BeanWrapperImpl` 。从官方文档可知，`BeanWrapper`提供了设置和获取属性值（单个或者批量）、获取属性描述符、查询属性以确定它们是否可读或者可写等功能。同时，`BeanWrapper`提供了嵌套属性支持，开启了任意深度的子属性设置功能。`BeanWrapper`还支持添加标准 JavaBeans `PropertyChangeListeners`和`VetoableChangeListeners`的能力，而且不需要目标类中提供支持代码。最后，`BeanWrapper`提供了设定索引属性的支持。`BeanWrapper`通常不会直接由应用代码使用，而是通常由`DataBinder`和`BeanFactory`使用。

`BeanWrapper`的工作方式部分如其名称表示：它包装 bean 以对该 bean 执行操作，例如设置和检索属性。

#### 3.3.1 设定和获取基本属性和嵌套属性

设置和获取属性是通过使用`setPropertyValue`，`setPropertyValues`，`getPropertyValue`和`getPropertyValues`方法完成的，这些方法带有几个重载变体。Springs javadoc更详细地描述了它们。JavaBeans规范具有指示对象属性的约定。下表显示了这些约定的一些示例：

| 表达式                    | 解释                                       |
| ---------------------- | ---------------------------------------- |
| `name`                 | 指示对应于 `getName()` 或者 `isName()` 和 `setName(..)` 方法的属性 `name` 。 |
| `account.name`         | 指示属性 `account`上的对应于 `getAccount().setName()` 或者 `getAccount().getName()`方法的嵌套属性 `name` 。 |
| `account[2]`           | 只是索引属性 `account` 的第三个元素。索引属性可以是类型 `array`, `list`, 或者其它自然有序集合。 |
| `account[COMPANYNAME]` | 指示由`account` Map属性的`COMPANYNAME`键索引的映射条目的值。 |

（如果您不打算直接使用`BeanWrapper`，那么下一部分对您来说并不重要。如果您只使用`DataBinder`和`BeanFactory`及其默认实现，那么您应该跳到 [PropertyEditors](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-beans-conversion) 部分。）

以下两个示例类使用`BeanWrapper`来获取和设置属性：

```java
public class Company {

    private String name;
    private Employee managingDirector;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Employee getManagingDirector() {
        return this.managingDirector;
    }

    public void setManagingDirector(Employee managingDirector) {
        this.managingDirector = managingDirector;
    }
}
```

```java
public class Employee {

    private String name;

    private float salary;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public float getSalary() {
        return salary;
    }

    public void setSalary(float salary) {
        this.salary = salary;
    }
}
```

以下代码片段显示了如何检索和操作实例化的 `Companies` 和 `Employees`的某些属性的一些示例：

```java
BeanWrapper company = new BeanWrapperImpl(new Company());
// setting the company name..
company.setPropertyValue("name", "Some Company Inc.");
// ... can also be done like this:
PropertyValue value = new PropertyValue("name", "Some Company Inc.");
company.setPropertyValue(value);

// ok, let's create the director and tie it to the company:
BeanWrapper jim = new BeanWrapperImpl(new Employee());
jim.setPropertyValue("name", "Jim Stravinsky");
company.setPropertyValue("managingDirector", jim.getWrappedInstance());

// retrieving the salary of the managingDirector through the company
Float salary = (Float) company.getPropertyValue("managingDirector.salary");
```

