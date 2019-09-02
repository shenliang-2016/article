### 使用 Datalink 对象

`DATALINK`值通过URL引用基础数据源外部的资源。URL，统一资源定位符，是指向万维网上的资源的指针。资源可以是文件或目录这样简单的东西，也可以是对更复杂的对象的引用，例如对数据库或搜索引擎的查询。

本章节涵盖以下主题：

- [存储外部数据的引用](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatalink.html#storing_datalink)
- [检索外部数据的引用](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatalink.html#retrieving_datalink)

**存储外部数据的引用**

使用`PreparedStatement.setURL`方法将`java.net.URL`对象指定为预准备语句。如果Java平台不支持所设置的URL类型，请使用`setString`方法存储URL。

例如，假设 The Coffee Break 的所有者想要在数据库表中存储重要URL列表。以下示例`DatalinkSample.addURLRow`将一行数据添加到表`DATA_REPOSITORY`。该行包含一个标识URL的字符串，`DOCUMENT_NAME`和URL本身，`URL`：

```java
public void addURLRow(String description, String url)
    throws SQLException {

    PreparedStatement pstmt = null;

    try {
        pstmt = this.con.prepareStatement(
            "INSERT INTO data_repository" +
            "(document_name,url) VALUES (?,?)");

        pstmt.setString(1, description);
        pstmt.setURL(2,new URL(url));
        pstmt.execute();
    } catch (SQLException sqlex) {
        JDBCTutorialUtilities.printSQLException(sqlex);
    } catch (Exception ex) {
        System.out.println("Unexpected exception");
        ex.printStackTrace();
    } finally {
        if (pstmt != null) {
            pstmt.close();
        }
    }
}
```

**检索外部数据引用**

使用`ResultSet.getURL`方法将对外部数据的引用检索为`java.net.URL`对象。如果Java平台不支持方法`getObject`或`getURL`返回的URL类型，则通过调用方法`getString`将URL检索为`String`对象。

以下示例`DatalinkSample.viewTable`显示存储在表`DATA_REPOSITORY`中的所有URL的内容：

```java
public static void viewTable(Connection con, Proxy proxy)
    throws SQLException, IOException {

    Statement stmt = null;
    String query =
      "SELECT document_name, url " +
      "FROM data_repository";

    try {
        stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery(query);

        if ( rs.next() )  {
            String documentName = null;
            java.net.URL url = null;

            documentName = rs.getString(1);

            // Retrieve the value as a URL object.
            url = rs.getURL(2);

            if (url != null) {

                // Retrieve the contents
                // from the URL
          
                URLConnection myURLConnection =
                    url.openConnection(proxy);
                BufferedReader bReader =
                    new BufferedReader(
                        new InputStreamReader(
                            myURLConnection.
                                getInputStream()));

                System.out.println("Document name: " + documentName);

                String pageContent = null;

                while ((pageContent = bReader.readLine()) != null ) {
                    // Print the URL contents
                    System.out.println(pageContent);
                }
            } else {
                System.out.println("URL is null");
            }
        }
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    } catch(IOException ioEx) {
        System.out.println("IOException caught: " + ioEx.toString());
    } catch (Exception ex) {
        System.out.println("Unexpected exception");
        ex.printStackTrace();
    } finally {
        if (stmt != null) { stmt.close(); }
    }
}
```

示例`DatalinkSample`将Oracle URL http://www.oracle.com 存储在表`DATA_REPOSITORY`中。之后，它显示存储在`DATA_REPOSITORY`中的URL引用的所有文档的内容，其中包括Oracle主页 http://www.oracle.com 。

该示例使用以下语句从结果集中检索URL作为`java.net.URL`对象：

```java
url = rs.getURL(2);
```

该示例使用以下语句访问URL对象引用的数据：

```java
URLConnection myURLConnection = url.openConnection(proxy);
BufferedReader bReader = new BufferedReader(
    new InputStreamReader(
        myURLConnection.getInputStream()));

System.out.println("Document name: " + documentName);

String pageContent = null;

while ((pageContent = bReader.readLine()) != null ) {
    // Print the URL contents
    System.out.println(pageContent);
}
```

`URLConnection.openConnection`方法不带参数，这意味着`URLConnection`表示与 Internet 的直接连接。如果需要代理服务器连接到 Internet，则`openConnection`方法接受`java.net.Proxy`对象作为参数。以下语句演示了如何使用服务器名称`www-proxy.example.com`和端口号`80`创建 HTTP 代理：

```
Proxy myProxy;
InetSocketAddress myProxyServer;
myProxyServer = new InetSocketAddress("www-proxy.example.com", 80);
myProxy = new Proxy(Proxy.Type.HTTP, myProxyServer);
```

### 使用 RowId 对象

**注意：**MySQL和Java DB当前不支持`RowId` JDBC接口。因此，没有JDBC教程示例可用于演示本节中描述的功能。

`RowId`对象表示数据库表中行的地址。但请注意，`ROWID`类型不是标准SQL类型。`ROWID`值非常有用，因为它们通常是访问单行的最快方式，并且是表中行的唯一标识。但是，不应将`ROWID`值用作表的主键。例如，如果从表中删除特定行，则数据库可能会将其`ROWID`值重新分配给稍后插入的行。

本章节涵盖以下主题：

- [检索 RowId 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlrowid.html#retrieving_rowid_objects)
- [使用 RowId 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlrowid.html#using_rowid_objects)
- [RowId 的有效期](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqlrowid.html#lifetime_rowid_validity)

**检索 RowId 对象**

通过调用接口`ResultSet`和`CallableStatement`中定义的`getter`方法来检索`java.sql.RowId`对象。返回的`RowId`对象是一个不可变对象，您可以将其用作后续引用作为行的唯一标识符。以下是调用`ResultSet.getRowId`方法的示例：

```java
java.sql.RowId rowId_1 = rs.getRowId(1);
```

**使用 RowId 对象**

您可以将`RowId`对象设置为参数化`PreparedStatement`对象中的参数：

```java
Connection conn = ds.getConnection(username, password);
PreparedStatement ps = conn.prepareStatement(
    "INSERT INTO BOOKLIST" +
    "(ID, AUTHOR, TITLE, ISBN) " +
    "VALUES (?, ?, ?, ?)");
ps.setRowId(1, rowId_1);
```

您还可以在可更新的`ResultSet`对象中更新具有特定`RowId`对象的列：

```java
ResultSet rs = ...
rs.next();
rs.updateRowId(1, rowId_1);
```

`RowId`对象值通常在数据源之间不可移植，并且在`PreparedStatement`和`ResultSet`对象中分别使用`set`或`update`方法时应被视为特定于数据源。因此，不建议从连接到一个数据源的`ResultSet`对象获取`RowId`对象，然后尝试在连接到不同的数据源的不相关的`ResultSet`对象中使用该`RowId`对象。

**RowId 的有效期**

只要未删除标识的行并且`RowId`对象的生存期在`RowId`的数据源指定的生存期的范围内，`RowId`对象就是有效的。

要确定数据库或数据源的`RowId`对象的生存期，请调用方法`DatabaseMetaData.getRowIdLifetime`。它返回`RowIdLifetime`枚举数据类型的值。以下方法`JDBCTutorialUtilities.rowIdLifeTime`返回`RowId`对象的生存期：

```java
public static void rowIdLifetime(Connection conn)
    throws SQLException {

    DatabaseMetaData dbMetaData = conn.getMetaData();
    RowIdLifetime lifetime = dbMetaData.getRowIdLifetime();

    switch (lifetime) {
        case ROWID_UNSUPPORTED:
            System.out.println("ROWID type not supported");
            break;

        case ROWID_VALID_FOREVER:
            System.out.println("ROWID has unlimited lifetime");
            break;

        case ROWID_VALID_OTHER:
            System.out.println("ROWID has indeterminate lifetime");
            break;

        case ROWID_VALID_SESSION:
            System.out.println(
                "ROWID type has lifetime that " +
                "is valid for at least the " +
                "containing session");
            break;

        case ROWID_VALID_TRANSACTION:
            System.out.println(
                "ROWID type has lifetime that " +
                "is valid for at least the " +
                "containing transaction");
            break;
    }
}
```

