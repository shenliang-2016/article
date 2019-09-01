### 使用 FilteredRowSet 对象

使用`FilteredRowSet`对象可以减少`RowSet`对象中可见的行数，这样您就可以只处理与您正在执行的操作相关的数据。您可以决定要对数据设置的限制（如何“过滤”数据）并将该过滤器应用于`FilteredRowSet`对象。换句话说，`FilteredRowSet`对象仅显示符合您设置的限制的数据行。`JdbcRowSet`对象始终与其数据源有连接，可以使用对数据源的查询进行此筛选，该数据源仅选择要查看的列和行。查询的`WHERE`子句定义了过滤条件。`FilteredRowSet`对象为断开连接的`RowSet`对象提供了一种方法来进行此过滤，而无需对数据源执行查询，从而避免必须连接到数据源并向其发送查询。

例如，假设咖啡馆 Coffee Break 连锁店已经发展到美国各地的数百家商店，并且所有商店都列在名为`COFFEE_HOUSES`的表中。老板希望仅通过咖啡馆比较应用来衡量加利福尼亚州商店的成功与否，该应用不需要与数据库系统的持久连接。这种比较将考察销售商品与销售咖啡饮料的盈利能力以及各种其他成功衡量标准，并将根据咖啡饮料销售，商品销售和总销售额对加州商店进行排名。因为表`COFFEE_HOUSES`有数百行，所以如果搜索的数据量减少到`STORE_ID`列中的值表示加利福尼亚的那些行，这些比较将更快更容易。

这正是`FilteredRowSet`对象通过提供以下功能解决的问题：

 - 能够根据设定的标准限制可见的行
 - 能够选择哪些数据可见而无需连接到数据源

本节涵盖以下主题：

- [在 Predicate 对象中定义过滤准则](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#defining-filtering-criteria-in-predicate-object)
- [创建 FilteredRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#creating-filteredrowset-object)
- [创建并设置 Predicate 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#creating-and-setting-predicate-object)
- [使用新的 Predicate 对象设置 FilteredRowSet 对象以进一步过滤数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#filter-data-further)
- [更新 FilteredRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#updating-filteredrowset-object)
- [插入或者更新行](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#inserting-or-updating-row)
- [删除所有过滤器使所有行可见](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#removing-all-filters)
- [删除行](https://docs.oracle.com/javase/tutorial/jdbc/basics/filteredrowset.html#deleting-row)

**在 Predicate 对象中定义过滤准则**

要设置`FilteredRowSet`对象中哪些行可见的条件，您可以定义一个实现`Predicate`接口的类。使用此类创建的对象使用以下内容进行初始化：

 - 值必须落在的范围的高端
 - 值必须落在的范围的低端
 - 列的列名或列号，其值必须位于由高和低边界设置的值范围内

请注意，值的范围是闭区间，这意味着边界处的值包含在范围内。例如，如果范围具有100的上限值和50的下限值，则认为值50在该范围内，值49不是。同样，100在范围内，但101不在。

根据老板想要比较加利福尼亚商店的情况，必须编写`Predicate`接口的实现，该接口用于过滤位于加利福尼亚州的 Coffee Break 咖啡馆。没有一种正确的方法可以做到这一点，这意味着在编写实现方面存在很大的自由度。例如，您可以根据需要为类及其成员命名，并以任何方式实现构造函数和三个计算方法，以实现所需的结果。

列出所有咖啡馆的表格名为`COFFEE_HOUSES`，有几百行。为了使事情更易于管理，本示例使用行少得多的表，这足以说明如何完成过滤。

`STORE_ID`列中的值是`int`值，其中指示咖啡馆所处的状态等。例如，以`10`开头的值表示该州是加利福尼亚州。以`32`开头的`STORE_ID`值表示俄勒冈州，以`33`开头的那些表示华盛顿州。

以下类 [`StateFilter`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 实现了`Predicate`接口：

```java
public class StateFilter implements Predicate {

    private int lo;
    private int hi;
    private String colName = null;
    private int colNumber = -1;

    public StateFilter(int lo, int hi, int colNumber) {
        this.lo = lo;
        this.hi = hi;
        this.colNumber = colNumber;
    }

    public StateFilter(int lo, int hi, String colName) {
        this.lo = lo;
        this.hi = hi;
        this.colName = colName;
    }

    public boolean evaluate(Object value, String columnName) {
        boolean evaluation = true;
        if (columnName.equalsIgnoreCase(this.colName)) {
            int columnValue = ((Integer)value).intValue();
            if ((columnValue >= this.lo)
                &&
                (columnValue <= this.hi)) {
                evaluation = true;
            } else {
                evaluation = false;
            }
        }
        return evaluation;
    }

    public boolean evaluate(Object value, int columnNumber) {

        boolean evaluation = true;

        if (this.colNumber == columnNumber) {
            int columnValue = ((Integer)value).intValue();
            if ((columnValue >= this.lo)
                &&
                (columnValue <= this.hi)) {
                evaluation = true;
            } else {
                evaluation = false;
            }
        }
        return evaluation;
    }


    public boolean evaluate(RowSet rs) {
    
        CachedRowSet frs = (CachedRowSet)rs;
        boolean evaluation = false;

        try {
            int columnValue = -1;

            if (this.colNumber > 0) {
                columnValue = frs.getInt(this.colNumber);
            } else if (this.colName != null) {
                columnValue = frs.getInt(this.colName);
            } else {
                return false;
            }

            if ((columnValue >= this.lo)
                &&
                (columnValue <= this.hi)) {
                evaluation = true;
            }
        } catch (SQLException e) {
            JDBCTutorialUtilities.printSQLException(e);
            return false;
        } catch (NullPointerException npe) {
            System.err.println("NullPointerException caught");
            return false;
        }
        return evaluation;
    }
}
```

这是一个非常简单的实现，它检查由`colName`或`colNumber`指定的列中的值，以查看它是否在`lo`到`hi`的范围内。来自 [`FilteredRowSetSample`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 的以下代码行创建了一个过滤器，该过滤器仅允许`STORE_ID`列所在的行值表示介于10000和10999之间的值，表示加利福尼亚州的位置：

```
StateFilter myStateFilter = new StateFilter(10000, 10999, 1);
```

请注意，刚定义的`StateFilter`类适用于一列。通过使用参数数组而不是单个值，可以将它应用于两个或更多列。例如，`Filter`对象的构造函数可能如下所示：

```java
public Filter2(Object [] lo, Object [] hi, Object [] colNumber) {
    this.lo = lo;
    this.hi = hi;
    this.colNumber = colNumber;
}
```

`colNumber`对象中的第一个元素给出第一列，其中将根据`lo`中的第一个元素和`hi`中的第一个元素检查该值。将使用`lo`和`hi`中的第二个元素检查由`colNumber`指示的第二列中的值，依此类推。因此，三个数组中的元素数应该相同。下面的代码是`evaluate(RowSet rs)`方法的实现可能看起来像`Filter2`对象，其中参数是数组：

```java
public boolean evaluate(RowSet rs) {
    CachedRowSet crs = (CachedRowSet)rs;
    boolean bool1;
    boolean bool2;
    for (int i = 0; i < colNumber.length; i++) {

        if ((rs.getObject(colNumber[i] >= lo [i]) &&
            (rs.getObject(colNumber[i] <= hi[i]) {
            bool1 = true;
        } else {
            bool2 = true;
        }

        if (bool2) {
            return false;
        } else {
            return true;
        }
    }
}
```

使用`Filter2`实现的优点是你可以使用任何`Object`类型的参数，并且可以检查一列或多列而无需编写另一个实现。但是，您必须传递一个`Object`类型，这意味着您必须将基本类型转换为其`Object`类型。例如，如果对`lo`和`hi`使用`int`值，则必须将`int`值转换为`Integer`对象，然后再将其传递给构造函数。`String`对象已经是`Object`类型，所以你不必转换它们。

**创建 FilteredRowSet 对象**

`FilteredRowSet`接口的参考实现，`FilteredRowSetImpl`，包括一个默认构造函数，在下面的代码行中使用它来创建空的`FilteredRowSet`对象`frs`：

```
FilteredRowSet frs = new FilteredRowSetImpl();
```

该实现扩展了`BaseRowSet`抽象类，因此`frs`对象具有在`BaseRowSet`中定义的默认属性。这意味着`frs`是可滚动的，可更新的，不显示已删除的行，已启用转义处理，等等。另外，因为`FilteredRowSet`接口是`CachedRowSet`，`Joinable`和`WebRowSet`的子接口，所以`frs`对象具有每个接口的能力。它可以作为断开连接的`RowSet`对象运行，可以是`JoinRowSet`对象的一部分，并且可以以 XML 格式读写自己。

**注意**：或者，您可以使用JDBC驱动程序的`WebRowSet`实现中的构造函数。但是，`RowSet`接口的实现将与参考实现不同。这些实现将具有不同的名称和构造函数。例如，Oracle JDBC 驱动程序的`WebRowSet`接口的实现名为`oracle.jdbc.rowset.OracleWebRowSet`。

您可以使用从RowSetProvider类创建的`RowSetFactory`实例来创建`FilteredRowSet`对象。请参阅 [Using JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html) 中的 [Using the RowSetFactory Interface](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#rowsetfactory) 了解更多信息。

与其他断开连接的`RowSet`对象一样，`frs`对象必须填充来自表格数据源的数据，表格数据源是参考实现中的关系数据库。来自 [`FilteredRowSetSample`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 的以下代码片段设置连接到数据库以执行其命令所需的属性。请注意，此代码使用`DriverManager`类进行连接，这样做是为了方便起见。通常，最好使用已向实现 Java 命名和目录接口 (JNDI) 的命名服务注册的`DataSource`对象：

```java
frs.setCommand("SELECT * FROM COFFEE_HOUSES");
frs.setUsername(settings.userName);
frs.setPassword(settings.password);
frs.setUrl(settings.urlString);
```

以下代码行使用存储在`COFFEE_HOUSE`表中的数据填充`frs`对象：

```java
frs.execute();
```

方法`execute`通过调用`frs`的`RowSetReader`对象来执行各种事情，它创建一个连接，执行`frs`的命令，用`ResultSet`中的数据填充`frs` 生成的对象，并关闭连接。 请注意，如果表`COFFEE_HOUSES`的行数多于`frs`对象一次可以保存在内存中，则会使用`CachedRowSet`分页方法。

在该场景中，Coffee Break 所有者将在办公室中完成上述任务，然后将存储在`frs`对象中的信息导入或下载到咖啡馆比较应用程序中。从现在开始，`frs`对象将独立运行，而无需连接到数据源。

**创建并设置 Predicate 对象**

既然`FilteredRowSet`对象`frs`包含了 Coffee Break 位置的列表，你可以设置选择标准来缩小`frs`对象中可见的行数。

下面的代码行使用先前定义的`StateFilter`类来创建对象`myStateFilter`，该对象检查列`STORE_ID`以确定哪些商店在加利福尼亚（如果商店的ID号介于10000和10999之间，则商店在加利福尼亚州）：

```java
StateFilter myStateFilter = new StateFilter(10000, 10999, 1);
```

以下行将`myStateFilter`设置为`frs`的过滤器。

```java
frs.setFilter(myStateFilter);
```

要进行实际过滤，可以调用方法`next`，它在参考实现中调用之前已实现的`Predicate.evaluate`方法的相应版本。

如果返回值为`true`，则该行将可见；如果返回值为`false`，则该行将不可见。

**使用新的 Predicate 对象设置 FilteredRowSet 对象以进一步过滤数据**

您可以串行设置多个过滤器。第一次调用方法`setFilter`并将其传递给`Predicate`对象时，您已在该过滤器中应用了过滤条件。在每行调用方法`next`后，只显示那些满足过滤器的行，你可以再次调用`setFilter`，传递一个不同的`Predicate`对象。即使一次只设置一个过滤器，效果是两个过滤器都累积应用。

例如，所有者通过将`stateFilter`设置为`frs`的`Predicate`对象来检索加利福尼亚州的 Coffee Break 商店列表。现在，店主希望比较加利福尼亚州的两个城市，旧金山（表格中为`COFFEE_HOUSES`表中的`SF`）和洛杉矶（表格中的`LA`）中的商店。首先要做的是编写一个`Predicate`实现，用于过滤`SF`或`LA`中的商店：

```java
public class CityFilter implements Predicate {

    private String[] cities;
    private String colName = null;
    private int colNumber = -1;

    public CityFilter(String[] citiesArg, String colNameArg) {
        this.cities = citiesArg;
        this.colNumber = -1;
        this.colName = colNameArg;
    }

    public CityFilter(String[] citiesArg, int colNumberArg) {
        this.cities = citiesArg;
        this.colNumber = colNumberArg;
        this.colName = null;
    }

    public boolean evaluate Object valueArg, String colNameArg) {

        if (colNameArg.equalsIgnoreCase(this.colName)) {
            for (int i = 0; i < this.cities.length; i++) {
                if (this.cities[i].equalsIgnoreCase((String)valueArg)) {
                    return true;
                }
            }
        }
        return false;
    }

    public boolean evaluate(Object valueArg, int colNumberArg) {

        if (colNumberArg == this.colNumber) {
            for (int i = 0; i < this.cities.length; i++) {
                if (this.cities[i].equalsIgnoreCase((String)valueArg)) {
                    return true;
                }
            }
        }
        return false;
    }


    public boolean evaluate(RowSet rs) {

        if (rs == null) return false;

        try {
            for (int i = 0; i < this.cities.length; i++) {

                String cityName = null;

                if (this.colNumber > 0) {
                    cityName = (String)rs.getObject(this.colNumber);
                } else if (this.colName != null) {
                    cityName = (String)rs.getObject(this.colName);
                } else {
                    return false;
                }

                if (cityName.equalsIgnoreCase(cities[i])) {
                    return true;
                }
            }
        } catch (SQLException e) {
            return false;
        }
        return false;
    }
}
```

来自 [`FilteredRowSetSample`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 的以下代码片段设置新过滤器并遍历`frs`中的行，打印出来 `CITY`列包含`SF`或`LA`的行。请注意，`frs`目前只包含商店在加利福尼亚州的行，因此当过滤器更改为另一个`Predicate`对象时，`Predicate`对象`state`的条件仍然有效。下面的代码将过滤器设置为`CityFilter`对象`city`。`CityFilter`实现使用数组作为构造函数的参数来说明如何完成：

```java
public void testFilteredRowSet() {

    FilteredRowSet frs = null;
    StateFilter myStateFilter = new StateFilter(10000, 10999, 1);
    String[] cityArray = { "SF", "LA" };

    CityFilter myCityFilter = new CityFilter(cityArray, 2);

    try {
        frs = new FilteredRowSetImpl();

        frs.setCommand("SELECT * FROM COFFEE_HOUSES");
        frs.setUsername(settings.userName);
        frs.setPassword(settings.password);
        frs.setUrl(settings.urlString);
        frs.execute();

        System.out.println("\nBefore filter:");
        FilteredRowSetSample.viewTable(this.con);

        System.out.println("\nSetting state filter:");
        frs.beforeFirst();
        frs.setFilter(myStateFilter);
        this.viewFilteredRowSet(frs);

        System.out.println("\nSetting city filter:");
        frs.beforeFirst();
        frs.setFilter(myCityFilter);
        this.viewFilteredRowSet(frs);
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    }
}
```

对于位于加利福尼亚州旧金山或加利福尼亚州洛杉矶的每个商店，输出应包含一行。如果有一行，其中`CITY`列包含`LA`而`STORE_ID`列包含40003，则它不会包含在列表中，因为当过滤器设置为`state`时它已经被过滤掉了。（40003不在10000到10999的范围内。）

**更新 FilteredRowSet 对象**

您可以对`FilteredRowSet`对象进行更改，但前提是该更改不违反当前有效的任何过滤条件。例如，如果新值或值在过滤条件内，则可以插入新行或更改现有行中的一个或多个值。

**插入或者更新行**

假设两个新的咖啡休息咖啡馆刚刚开业，店主想将它们添加到所有咖啡馆的名单中。如果要插入的行不符合有效的累积过滤条件，则将阻止添加该行。

`frs`对象的当前状态是设置了`StateFilter`对象，然后设置了`CityFilter`对象。因此，`frs`目前只显示那些满足两个过滤器条件的行。同样重要的是，除非满足两个过滤器的条件，否则不能向`frs`对象添加行。下面的代码片段试图在`frs`对象中插入两个新行，一行中`STORE_ID`和`CITY`列中的值都满足条件，一行中`STORE_ID`中的值无法通过过滤器，但`CITY`列中的值可以通过过滤器：

```java
frs.moveToInsertRow();
frs.updateInt("STORE_ID", 10101);
frs.updateString("CITY", "SF");
frs.updateLong("COF_SALES", 0);
frs.updateLong("MERCH_SALES", 0);
frs.updateLong("TOTAL_SALES", 0);
frs.insertRow();

frs.updateInt("STORE_ID", 33101);
frs.updateString("CITY", "SF");
frs.updateLong("COF_SALES", 0);
frs.updateLong("MERCH_SALES", 0);
frs.updateLong("TOTAL_SALES", 0);
frs.insertRow();
frs.moveToCurrentRow();
```

如果你使用`next`方法遍历`frs`对象，你会发现加利福尼亚州旧金山的新咖啡馆有一行数据，但华盛顿旧金山的商店没有。

**删除所有过滤器使所有行可见**

店主可以通过使过滤器无效来在华盛顿添加商店。如果没有设置过滤器，`frs`对象中的所有行都会再次可见，并且任何位置的商店都可以添加到商店列表中。下面的代码行取消了当前的过滤器，有效地消除了之前在`frs`对象上设置的两个`Predicate`实现。

```java
frs.setFilter(null);
```

**删除行**

如果店主决定关闭或出售其中一个咖啡馆，店主将希望将其从`COFFEE_HOUSES`表中删除。只要行可见，店主就可以删除表现不佳的咖啡馆的行。

例如，假设刚刚使用参数`null`调用方法`setFilter`，则`frs`对象上没有设置过滤器。这意味着所有行都是可见的，因此可以删除。但是，在设置`StateFilter`对象`myStateFilter`之后，过滤掉加利福尼亚以外的任何州，只能删除位于加利福尼亚州的店。当`CityFilter`对象`myCityFilter`被设置为`frs`对象时，只有加利福尼亚州旧金山或加利福尼亚州洛杉矶的咖啡馆才能被删除，因为它们只在可见的行中。

