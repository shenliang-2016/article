### 使用 WebRowSet 对象

`WebRowSet`对象非常特殊，因为除了提供`CachedRowSet`对象的所有功能外，它还可以将自身编写为 XML 文档，还可以读取该 XML 文档以将其自身转换回`WebRowSet`对象。由于 XML 是不同企业可以相互通信的语言，因此它已成为 Web 服务通信的标准。因此，`WebRowSet`对象通过使 Web 服务以 XML 文档的形式从数据库发送和接收数据来满足实际需求。

本节涵盖以下主题：

- [创建并填充 WebRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#creating-and-populating-webrowset-object)
- [将 WebRowSet 对象写入 XML 以及从 XML 读取 WebRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#writing-and-reading-webrowset-object-to-xml)
- [XML 文档中有什么？](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#what-is-in-xml-document)
- [修改 WebRowSet 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#making-changes-to-webrowset-object)

Coffee Break 公司已经扩展到在线销售咖啡。用户从 Coffee Break 网站点击咖啡，通过从公司数据库获取最新信息，定期更新价目表。本节演示如何使用`WebRowSet`对象和单个方法调用将价格数据作为 XML 文档发送。

**创建并填充 WebRowSet 对象**

使用参考实现`WebRowSetImpl`中定义的默认构造函数创建一个新的`WebRowSet`对象，如以下代码行所示：

```java
WebRowSet priceList = new WebRowSetImpl();
```

尽管`priceList`对象还没有数据，但它具有`BaseRowSet`对象的默认属性。它的`SyncProvider`object首先设置为`RIOptimisticProvider`实现，这是所有断开连接的`RowSet`对象的默认设置。但是，`WebRowSet`实现将`SyncProvider`对象重置为`RIXMLProvider`实现。

您可以使用从`RowSetProvider`类创建的`RowSetFactory`实例来创建`WebRowSet`对象。请参阅 [Using JdbcRowSet Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html) 中的 [Using the RowSetFactory Interface](https://docs.oracle.com/javase/tutorial/jdbc/basics/jdbcrowset.html#rowsetfactory) 了解更多信息。

Coffee Break 总部定期向其网站发送价目表更新。有关`WebRowSet`对象的信息将显示一种可以在 XML 文档中发送最新价格表的方法。

价格表包含`COFFEES`表中`COF_NAME`和`PRICE`列中的数据。以下代码片段设置所需的属性，并使用价目表数据填充`priceList`对象：

```java
public void getPriceList(String username, String password) {
    priceList.setCommand("SELECT COF_NAME, PRICE FROM COFFEES");
    priceList.setURL("jdbc:mySubprotocol:myDatabase");
    priceList.setUsername(username);
    priceList.setPassword(password);
    priceList.execute();
    // ...
}
```

此时，除了默认属性之外，`priceList`对象还包含来自`COFFEES`表的`COF_NAME`和`PRICE`列中的数据以及有关这两列的元数据。

**将 WebRowSet 对象写入 XML 以及从 XML 读取 WebRowSet 对象**

要将`WebRowSet`对象编写为XML文档，请调用`writeXml`方法。要将XML文档的内容读入`WebRowSet`对象，请调用方法`readXml`。这两种方法都在后台完成它们的工作，这意味着除了结果之外的所有内容对您来说都是不可见的。

**使用 writeXml 方法**

方法`writeXml`编写`WebRowSet`对象，该对象将其作为表示其当前状态的XML文档调用。它将此XML文档写入您传递给它的流。流可以是`OutputStream`对象，例如`FileOutputStream`对象，或`Writer`对象，例如`FileWriter`对象。如果你传递给`writeXml`方法一个`OutputStream`对象，你将以字节为单位写入，它可以处理所有类型的数据；如果你传递一个`Writer`对象，你将用字符写入。下面的代码演示了将`WebRowSet`对象`priceList`作为XML文档写入`FileOutputStream`对象`oStream`：

```java
java.io.FileOutputStream oStream =
    new java.io.FileOutputStream("priceList.xml");
priceList.writeXml(oStream);
```

下面的代码将表示`priceList`的XML文档写入`FileWriter`对象`writer`而不是`OutputStream`对象。`FileWriter`类是用于将字符写入文件的便捷类。

```java
java.io.FileWriter writer =
    new java.io.FileWriter("priceList.xml");
priceList.writeXml(writer);
```

方法`writeXml`的另外两个版本允许你在将`ResultSet`对象的内容填充到一个`WebRowSet`对象之前将其写入流。在下面的代码行中，方法`writeXml`将`ResultSet`对象`rs`的内容读入`priceList`对象，然后将`priceList`作为XML文档写入`FileOutputStream`对象`oStream`。

```java
priceList.writeXml(rs, oStream);
```

在下一行代码中，`writeXml`方法使用`rs`的内容填充`price List`，但它将XML文档写入`FileWriter`对象而不是`OutputStream`对象：

```java
priceList.writeXml(rs, writer);
```

**使用 readXml 方法**

方法`readXml`解析XML文档，以构造XML文档描述的`WebRowSet`对象。与`writeXml`方法类似，您可以传递给`readXml`一个`InputStream`对象或一个`Reader`对象，从中读取XML文档。

```java
java.io.FileInputStream iStream =
    new java.io.FileInputStream("priceList.xml");
priceList.readXml(iStream);

java.io.FileReader reader = new
    java.io.FileReader("priceList.xml");
priceList.readXml(reader);
```

请注意，您可以将XML描述读入新的`WebRowSet`对象或读取调用`writeXml`方法的同一个`WebRowSet`对象。在从总部向 Web 站点发送价目表信息的场景中，您将使用新的`WebRowSet`对象，如以下代码行所示：

```java
WebRowSet recipient = new WebRowSetImpl();
java.io.FileReader reader =
    new java.io.FileReader("priceList.xml");
recipient.readXml(reader);
```

**XML 文档中是什么？**

`RowSet`对象不仅仅是它们包含的数据。它们还具有有关其列的属性和元数据。因此，表示`WebRowSet`对象的XML文档除了其数据之外还包括该其他信息。此外，XML文档中的数据包括当前值和原始值。（回想一下，原始值是在最近的数据更改之前存在的值。这些值是检查数据库中相应值是否已更改所必需的，从而产生了应该持久保存值的冲突： 您放入`RowSet`对象的新值或其他人放入数据库的新值。）

WebRowSet XML Schema 本身就是一个XML文档，它定义了表示`WebRowSet`对象的XML文档将包含的内容以及它必须呈现的格式。写入者和读取者都使用此模式，因为它告诉写入者如何编写XML文档（表示`WebRowSet`对象）和读取者如何解析XML文档。因为实际的写入和读取是通过方法`writeXml`和`readXml`的实现在内部完成的，所以作为用户，您不需要了解 WebRowSet XML Schema 文档中的内容。

XML文档包含分层结构中的元素和子元素。以下是描述`WebRowSet`对象的XML文档中的三个主要元素：

- [属性](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#properties-webrowset)
- [元数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#metadata-webrowset)
- [数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/webrowset.html#data-webrowset)

元素标签标示元素的开头和结尾。例如，`<properties>`标记表示 properties 元素的开头，而`</properties>`标记表示它的结束。`<map/>`标签是一种简写方式，表示 map 子元素（ properties 元素中的一个子元素）尚未赋值。以下示例XML文档使用间距和缩进来使其更易于阅读，但这些不在实际的XML文档中使用，其中间距并不意味着什么。

接下来的三节将向您展示在示例 [`WebRowSetSample.java`](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 中创建的`WebRowSet` `priceList`对象包含的三个主要元素。

**属性**

在`priceList`对象上调用`writeXml`方法会产生一个描述`priceList`的XML文档。此XML文档的属性部分如下所示：

```xml
<properties>
  <command>
    select COF_NAME, PRICE from COFFEES
  </command>
  <concurrency>1008</concurrency>
  <datasource><null/></datasource>
  <escape-processing>true</escape-processing>
  <fetch-direction>1000</fetch-direction>
  <fetch-size>0</fetch-size>
  <isolation-level>2</isolation-level>
  <key-columns>
    <column>1</column>
  </key-columns>
  <map>
  </map>
  <max-field-size>0</max-field-size>
  <max-rows>0</max-rows>
  <query-timeout>0</query-timeout>
  <read-only>true</read-only>
  <rowset-type>
    ResultSet.TYPE_SCROLL_INSENSITIVE
  </rowset-type>
  <show-deleted>false</show-deleted>
  <table-name>COFFEES</table-name>
  <url>jdbc:mysql://localhost:3306/testdb</url>
  <sync-provider>
    <sync-provider-name>
      com.sun.rowset.providers.RIOptimisticProvider
    </sync-provider-name>
    <sync-provider-vendor>
      Sun Microsystems Inc.
    </sync-provider-vendor>
    <sync-provider-version>
      1.0
    </sync-provider-version>
    <sync-provider-grade>
      2
    </sync-provider-grade>
    <data-source-lock>1</data-source-lock>
  </sync-provider>
</properties>
```

请注意，某些属性没有任何价值。例如，`datasource`属性用`<datasource/>`标记表示，这是表示`<datasource> </datasource>`的简写方式。没有给出值，因为设置了`url`属性。建立的任何连接都将使用此 JDBC URL 完成，因此不需要设置`DataSource`对象。此外，未列出`username`和`password`属性，因为它们必须保密。

**元数据**

描述`WebRowSet`对象的XML文档的元数据部分包含有关该`WebRowSet`对象中的列的信息。下面显示了`WebRowSet`对象`priceList`的这个部分。因为`priceList`对象有两列，所以描述它的XML文档有两个`<column-definition>`元素。每个`<column-definition>`元素都有子元素，提供有关所描述列的信息。

```xml
<metadata>
  <column-count>2</column-count>
  <column-definition>
    <column-index>1</column-index>
    <auto-increment>false</auto-increment>
    <case-sensitive>false</case-sensitive>
    <currency>false</currency>
    <nullable>0</nullable>
    <signed>false</signed>
    <searchable>true</searchable>
    <column-display-size>
      32
    </column-display-size>
    <column-label>COF_NAME</column-label>
    <column-name>COF_NAME</column-name>
    <schema-name></schema-name>
    <column-precision>32</column-precision>
    <column-scale>0</column-scale>
    <table-name>coffees</table-name>
    <catalog-name>testdb</catalog-name>
    <column-type>12</column-type>
    <column-type-name>
      VARCHAR
    </column-type-name>
  </column-definition>
  <column-definition>
    <column-index>2</column-index>
    <auto-increment>false</auto-increment>
    <case-sensitive>true</case-sensitive>
    <currency>false</currency>
    <nullable>0</nullable>
    <signed>true</signed>
    <searchable>true</searchable>
    <column-display-size>
      12
    </column-display-size>
    <column-label>PRICE</column-label>
    <column-name>PRICE</column-name>
    <schema-name></schema-name>
    <column-precision>10</column-precision>
    <column-scale>2</column-scale>
    <table-name>coffees</table-name>
    <catalog-name>testdb</catalog-name>
    <column-type>3</column-type>
    <column-type-name>
      DECIMAL
    </column-type-name>
  </column-definition>
</metadata>
```

从此元数据部分，您可以看到每行中有两列。第一列是`COF_NAME`，它包含类型为`VARCHAR`的值。第二列是`PRICE`，它包含`REAL`类型的值，依此类推。请注意，列类型是数据源中使用的数据类型，而不是Java编程语言中的类型。要获取或更新`COF_NAME`列中的值，可以使用`getString`或`updateString`方法，并且驱动程序会像往常那样转换为`VARCHAR`类型。

**数据**

数据部分给出了`WebRowSet`对象的每一行中每列的值。如果已填充`priceList`对象并且未对其进行任何更改，则XML文档的数据元素将如下所示。在下一节中，您将看到在修改`priceList`对象中的数据时XML文档如何更改。

对于每一行，都有一个`<currentRow>`元素，因为`priceList`有两列，每个`<currentRow>`元素包含两个`<columnValue>`元素。

```xml
<data>
  <currentRow>
    <columnValue>Colombian</columnValue>
    <columnValue>7.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>
      Colombian_Decaf
    </columnValue>
    <columnValue>8.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>Espresso</columnValue>
    <columnValue>9.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>French_Roast</columnValue>
    <columnValue>8.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>French_Roast_Decaf</columnValue>
    <columnValue>9.99</columnValue>
  </currentRow>
</data>
```

**修改 WebRowSet 对象**

您对`WebRowSet`对象进行更改的方式与对`CachedRowSet`对象的更改方式相同。然而，与`CachedRowSet`对象不同，`WebRowSet`对象跟踪更新，插入和删除，以便`writeXml`方法可以写入当前值和原始值。接下来的三个部分演示了对数据的更改，并显示了每次更改后描述`WebRowSet`对象的XML文档的样子。您不必对XML文档做任何事情; 对它的任何更改都是自动进行的，就像编写和读取XML文档一样。

**插入行**

如果 Coffee Break 连锁店的所有者想要在价目表中添加新咖啡，则代码可能如下所示：

```java
priceList.absolute(3);
priceList.moveToInsertRow();
priceList.updateString(COF_NAME, "Kona");
priceList.updateFloat(PRICE, 8.99f);
priceList.insertRow();
priceList.moveToCurrentRow();
```

在参考实现中，紧接在当前行之后进行插入。在前面的代码片段中，当前行是第三行，因此新行将在第三行之后添加并成为新的第四行。为了反映这种插入，XML文档将在`<data>`元素中的第三个`<currentRow>`元素之后添加以下`<insertRow>`元素。

`<insertRow>`元素将类似于以下内容。

```java
<insertRow>
  <columnValue>Kona</columnValue>
  <columnValue>8.99</columnValue>
</insertRow>
```

**删除行**

店主认为`Espresso`销售不足，应该从出售的咖啡中删除。因此，所有者想要从价目表中删除`Espresso`。`Espresso`位于`priceList`object的第三行，因此以下代码行将其删除：

```java
priceList.absolute(3); priceList.deleteRow();
```

以下`<deleteRow>`元素将出现在XML文档的数据部分的第二行之后，表示第三行已被删除。

```xml
<deleteRow>
  <columnValue>Espresso</columnValue>
  <columnValue>9.99</columnValue>
</deleteRow>
```

**修改行**

店主进一步认为哥伦比亚咖啡的价格过于昂贵，并希望将其降低至每磅6.99美元。以下代码将哥伦比亚咖啡的新价格设定为每磅6.99美元，这是第一行的价格：

```java
priceList.first();
priceList.updateFloat(PRICE, 6.99);
```

XML文档将在提供新值的`<updateRow>`元素中反映此更改。第一列的值没有改变，因此只有第二列的`<updateValue>`元素：

```xml
<currentRow>
  <columnValue>Colombian</columnValue>
  <columnValue>7.99</columnValue>
  <updateRow>6.99</updateRow>
</currentRow>
```

此时，通过插入行，删除行以及修改行，`priceList`对象的XML文档如下所示：

```xml
<data>
  <insertRow>
    <columnValue>Kona</columnValue>
    <columnValue>8.99</columnValue>
  </insertRow>
  <currentRow>
    <columnValue>Colombian</columnValue>
    <columnValue>7.99</columnValue>
    <updateRow>6.99</updateRow>
  </currentRow>
  <currentRow>
    <columnValue>
      Colombian_Decaf
    </columnValue>
    <columnValue>8.99</columnValue>
  </currentRow>
  <deleteRow>
    <columnValue>Espresso</columnValue>
    <columnValue>9.99</columnValue>
  </deleteRow>
  <currentRow>
    <columnValue>French_Roast</columnValue>
    <columnValue>8.99</columnValue>
  </currentRow>
  <currentRow>
    <columnValue>
      French_Roast_Decaf
    </columnValue>
    <columnValue>9.99</columnValue>
  </currentRow>
</data>
```

**WebRowSet 代码示例**

示例 `WebRowSetSample.java` 演示了此页面上描述的所有功能。