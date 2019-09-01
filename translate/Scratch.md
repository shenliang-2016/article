### 使用 SQLXML 对象

`Connection`接口使用`createSQLXML`方法为创建`SQLXML`对象提供支持。创建的对象不包含任何数据。可以通过在`SQLXML`接口上调用`setString`，`setBinaryStream`，`setCharacterStream`或`setResult`方法将数据添加到对象中。

本章节涵盖以下主题：

- [创建 SQLXML 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#creating_sqlxml)
- [在 ResultSet 中查询 SQLXML 值](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#retrieving_sqlxml)
- [访问 SQLXML 对象数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#accessing_sqlxml)
- [存储 SQLXML 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#storing_sqlxml)
- [初始化 SQLXML 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#initializing_sqlxml)
- [释放 SQLXML 资源](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#releasing_sqlxml)
- [示例代码](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#sample_code)

**创建 SQLXML 对象**

在下面的代码摘录中，方法`Connection.createSQLXML`用于创建一个空的`SQLXML`对象。`SQLXML.setString`方法用于将数据写入创建的`SQLXML`对象。

```java
Connection con = DriverManager.getConnection(url, props);
SQLXML xmlVal = con.createSQLXML();
xmlVal.setString(val);
```

**在 ResultSet 中查询 SQLXML 值**

`SQLXML`数据类型的处理方式与更原始的内置类型相似。可以通过调用`ResultSet`或`CallableStatement`接口中的`getSQLXML`方法来检索`SQLXML`值。

例如，以下代码摘录从`ResultSet` *rs*的第一列检索`SQLXML`值：

```java
SQLXML xmlVar = rs.getSQLXML(1);
```

`SQLXML`对象至少在创建它们的事务期间保持有效，除非调用它们的`free`方法。

**访问 SQLXML 对象数据**

`SQLXML`接口提供`getString`，`getBinaryStream`，`getCharacterStream`和`getSource`方法来访问其内部内容。以下代码摘录使用`getString`方法检索`SQLXML`对象的内容：

```java
SQLXML xmlVal= rs.getSQLXML(1);
String val = xmlVal.getString();
```

`getBinaryStream`或`getCharacterStream`方法可用于获取可以直接传递给XML解析器的`InputStream`或`Reader`对象。以下代码摘录从`SQLXML`对象获取`InputStream`对象，然后使用DOM（文档对象模型）解析器处理流：

```java
SQLXML sqlxml = rs.getSQLXML(column);
InputStream binaryStream = sqlxml.getBinaryStream();
DocumentBuilder parser = 
    DocumentBuilderFactory.newInstance().newDocumentBuilder();
Document result = parser.parse(binaryStream);
```

`getSource`方法返回一个`javax.xml.transform.Source`对象。源用作XML解析器和XSLT转换器的输入。

以下摘录使用通过调用`getSource`方法返回的`SAXSource`对象从`SQLXML`对象检索和解析数据：

```java
SQLXML xmlVal= rs.getSQLXML(1);
SAXSource saxSource = sqlxml.getSource(SAXSource.class);
XMLReader xmlReader = saxSource.getXMLReader();
xmlReader.setContentHandler(myHandler);
xmlReader.parse(saxSource.getInputSource());
```

**存储 SQLXML 对象**

与其他数据类型一样，`SQLXML`对象可以作为输入参数传递给`PreparedStatement`对象。方法`setSQLXML`用`SQLXML`对象设置指定的`PreparedStatement`参数。

在下面的摘录中，`authorData`是`java.sql.SQLXML`接口的一个实例，其数据先前已初始化。

```java
PreparedStatement pstmt = conn.prepareStatement("INSERT INTO bio " +
                              "(xmlData, authId) VALUES (?, ?)");
pstmt.setSQLXML(1, authorData);
pstmt.setInt(2, authorId);
```

`updateSQLXML`方法可用于更新可更新结果集中的列值。

如果在调用`setSQLXML`或`updateSQLXML`之前，`SQLXML`对象的`java.xml.transform.Result`，`Writer`或`OutputStream`对象尚未关闭，则抛出`SQLException`。

**初始化 SQLXML 对象**

`SQLXML`接口提供方法`setString`，`setBinaryStream`，`setCharacterStream`或`setResult`来初始化通过调用`Connection.createSQLXML`方法创建的`SQLXML`对象的内容。

以下摘录使用方法`setResult`返回一个`SAXResult`对象来填充新创建的`SQLXML`对象：

```java
SQLXML sqlxml = con.createSQLXML();
SAXResult saxResult = sqlxml.setResult(SAXResult.class);
ContentHandler contentHandler = saxResult.getXMLReader().getContentHandler();
contentHandler.startDocument();
    
// set the XML elements and
// attributes into the result
contentHandler.endDocument();
```

以下摘录使用`setCharacterStream`方法获取`java.io.Writer`对象以初始化`SQLXML`对象：

```java
SQLXML sqlxml = con.createSQLXML();
Writer out= sqlxml.setCharacterStream();
BufferedReader in = new BufferedReader(new FileReader("xml/foo.xml"));
String line = null;
while((line = in.readLine() != null) {
    out.write(line);
}
```

类似地，`SQLXML` `setString`方法可用于初始化`SQLXML`对象。

如果尝试在先前已初始化的`SQLXML`对象上调用`setString`，`setBinaryStream`，`setCharacterStream`和`setResult`方法，则将抛出`SQLException`。如果对同一个`SQLXML`对象发生多次调用方法`setBinaryStream`，`setCharacterStream`和`setResult`，则抛出一个`SQLException`并返回先前返回的`javax.xml.transform.Result`，` Writer`或`OutputStream`对象不受影响。

**释放 SQLXML 资源**

`SQLXML`对象至少在创建它们的事务期间保持有效。这可能导致应用程序在长时间运行的事务期间耗尽资源。应用程序可以通过调用`free`方法释放`SQLXML`资源。

在下面的摘录中，调用`方法SQLXML.free`来释放为先前创建的`SQLXML`对象保存的资源。

```java
SQLXML xmlVar = con.createSQLXML();
xmlVar.setString(val);
xmlVar.free();
```

**示例代码**

MySQL和Java DB及其各自的JDBC驱动程序不完全支持本节所述的`SQLXML` JDBC数据类型。但是，示例`RSSFeedsTable`演示了如何使用MySQL和Java DB处理XML数据。

The Coffee Break的老板关注来自各种网站的多个RSS源，其中包括餐馆和饮料行业的新闻。RSS（Really Simple Syndication或Rich Site Summary）源是一个XML文档，其中包含一系列文章和相关元数据，例如每篇文章的发布日期和作者。老板希望将这些RSS提要存储到数据库表中，包括来自The Coffee Break博客的RSS提要。

文件`rss-the-coffee-break-blog.xml`是来自The Coffee Break博客的示例RSS源。

**在MySQL中使用XML数据**

示例`RSSFeedsTable`将RSS提要存储在表`RSS_FEEDS`中，该表是使用以下命令创建的：

```sql
create table RSS_FEEDS
    (RSS_NAME varchar(32) NOT NULL,
    RSS_FEED_XML longtext NOT NULL,
    PRIMARY KEY (RSS_NAME));
```

MySQL不支持XML数据类型。相反，此示例将XML数据存储在类型为`LONGTEXT`的列中，该列是`CLOB`SQL数据类型。MySQL有四种`CLOB`数据类型；`LONGTEXT`数据类型在四个中保存最多的字符。

方法`RSSFeedsTable.addRSSFeed`将RSS提要添加到`RSS_FEEDS`表。此方法的第一个语句将RSS提要（由此示例中的XML文件表示）转换为类型为`org.w3c.dom.Document`的对象，该对象表示DOM（文档对象模型）文档。该类以及包`javax.xml`中包含的类和接口包含使您能够操作XML数据内容的方法。例如，以下语句使用 XPath 表达式从`Document`对象检索RSS提要的标题：

```java
Node titleElement =
    (Node)xPath.evaluate("/rss/channel/title[1]",
        doc, XPathConstants.NODE);
```

XPath表达式`/rss/channel/title[1]`检索第一个`<title>`元素的内容。对于文件`rss-the-coffee-break-blog.xml`，这是字符串`The Coffee Break Blog`。

以下语句将RSS提要添加到表`RSS_FEEDS`：

```java
// For databases that support the SQLXML
// data type, this creates a
// SQLXML object from
// org.w3c.dom.Document.

System.out.println("Adding XML file " + fileName);
String insertRowQuery =
    "insert into RSS_FEEDS " +
    "(RSS_NAME, RSS_FEED_XML) values " +
    "(?, ?)";
insertRow = con.prepareStatement(insertRowQuery);
insertRow.setString(1, titleString);

System.out.println("Creating SQLXML object with MySQL");
rssData = con.createSQLXML();
System.out.println("Creating DOMResult object");
DOMResult dom = (DOMResult)rssData.setResult(DOMResult.class);
dom.setNode(doc);

insertRow.setSQLXML(2, rssData);
System.out.println("Running executeUpdate()");
insertRow.executeUpdate();
```

`RSSFeedsTable.viewTable`方法检索`RSS_FEEDS`的内容。对于每一行，该方法创建一个名为`doc`的类型为`org.w3c.dom.Document`的对象，其中将XML内容存储在列`RSS_FEED_XML`中。该方法检索XML内容并将其存储在名为`rssFeedXML`的`SQLXML`类型的对象中。`rssFeedXML`的内容被解析并存储在`doc`对象中。

**在Java DB中使用XML数据**

**注意**：有关在Java DB中使用XML数据的更多信息，请参阅 [*Java DB Developer's Guide*](http://docs.oracle.com/javadb/index_jdk8.html) 中的“XML数据类型和运算符”部分。

示例`RSSFeedsTable`将RSS提要存储在表`RSS_FEEDS`中，该表是使用以下命令创建的：

```sql
create table RSS_FEEDS
    (RSS_NAME varchar(32) NOT NULL,
    RSS_FEED_XML xml NOT NULL,
    PRIMARY KEY (RSS_NAME));
```

Java DB支持XML数据类型，但它不支持`SQLXML` JDBC数据类型。因此，您必须将任何XML数据转换为字符格式，然后使用Java DB运算符`XMLPARSE`将其转换为XML数据类型。

`RSSFeedsTable.addRSSFeed`方法将RSS提要添加到`RSS_FEEDS`表。此方法的第一个语句将RSS提要（由此示例中的XML文件表示）转换为`org.w3c.dom.Document`类型的对象。这在 [使用MySQL中的XML数据](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlxml.html#working-with-xml-data-in-mysql) 中进行了描述。

`RSSFeedsTable.addRSSFeed`方法使用方法`JDBCTutorialUtilities.convertDocumentToString`将RSS提要转换为`String`对象。

Java DB有一个名为`XMLPARSE`的运算符，它将字符串表示形式解析为Java DB XML值，如以下摘录所示：

```java
String insertRowQuery =
    "insert into RSS_FEEDS " +
    "(RSS_NAME, RSS_FEED_XML) values " +
    "(?, xmlparse(document cast " +
    "(? as clob) preserve whitespace))";
```

`XMLPARSE`运算符要求您将XML文档的字符表示转换为Java DB识别的字符串数据类型。在此示例中，它将其转换为`CLOB`数据类型。有关Apache Xalan和Java DB要求的更多信息，请参见 [入门](https://docs.oracle.com/javase/tutorial/jdbc/basics/gettingstarted.html) 和Java DB文档。

方法`RSSFeedsTable.viewTable`检索`RSS_FEEDS`的内容。由于Java DB不支持JDBC数据类型`SQLXML`，因此必须将XML内容检索为字符串。Java DB有一个名为`XMLSERIALIZE`的运算符，它将XML类型转换为字符类型：

```java
String query =
    "select RSS_NAME, " +
    "xmlserialize " +
    "(RSS_FEED_XML as clob) " +
    "from RSS_FEEDS";
```

与`XMLPARSE`运算符一样，`XMLSERIALIZE`运算符要求Apache Xalan列在Java类路径中。

