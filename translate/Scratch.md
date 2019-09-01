### 使用大对象

`Blob`，`Clob`和`NClob` Java对象的一个重要特性是，您可以操作它们，而无需将所有数据从数据库服务器带到客户端计算机。某些实现表示这些类型的实例，其中包含实例所代表的数据库中对象的定位符（逻辑指针）。因为`BLOB`，`CLOB`或`NCLOB` SQL对象可能非常大，所以使用定位器可以显着提高性能。但是，其他实现完全实现了客户端计算机上的大对象。

如果要将`BLOB`，`CLOB`或`NCLOB`SQL值的数据带到客户端计算机，请使用为此目的提供的`Blob`，`Clob`和`NClob`Java接口中的方法。这些大对象类型对象将它们表示的对象的数据实现为流。

本章节涵盖以下主题：

- [添加大对象类型对象到数据库](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html#add_lob)
- [查询 CLOB 值](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html#retrieve_clob)
- [添加和查询 BLOB 对象](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html#add_retrieve_blob)
- [释放大对象持有的资源](https://docs.oracle.com/javase/tutorial/jdbc/basics/blob.html#release_large_objects)

**添加大对象类型对象到数据库**

以下来自`ClobSample.addRowToCoffeeDescriptions`的摘录将`CLOB`SQL值添加到表`COFFEE_DESCRIPTIONS`中。`Clob` Java对象`myClob`包含`fileName`指定的文件的内容。

```java
public void addRowToCoffeeDescriptions(
    String coffeeName, String fileName)
    throws SQLException {

    PreparedStatement pstmt = null;
    try {
        Clob myClob = this.con.createClob();
        Writer clobWriter = myClob.setCharacterStream(1);
        String str = this.readFile(fileName, clobWriter);
        System.out.println("Wrote the following: " +
            clobWriter.toString());

        if (this.settings.dbms.equals("mysql")) {
            System.out.println(
                "MySQL, setting String in Clob " +
                "object with setString method");
            myClob.setString(1, str);
        }
        System.out.println("Length of Clob: " + myClob.length());

        String sql = "INSERT INTO COFFEE_DESCRIPTIONS " +
                     "VALUES(?,?)";

        pstmt = this.con.prepareStatement(sql);
        pstmt.setString(1, coffeeName);
        pstmt.setClob(2, myClob);
        pstmt.executeUpdate();
    } catch (SQLException sqlex) {
        JDBCTutorialUtilities.printSQLException(sqlex);
    } catch (Exception ex) {
      System.out.println("Unexpected exception: " + ex.toString());
    } finally {
        if (pstmt != null)pstmt.close();
    }
}
```

以下行创建一个`Clob` Java对象：

```java
Clob myClob = this.con.createClob();
```

以下代码行检索一个流（在本例中是一个名为`clobWriter`的`Writer`对象），用于将字符流写入`Clob` Java对象`myClob`。方法`ClobSample.readFile`写入这个字符流；流来自`String` `fileName`指定的文件。方法参数`1`表示`Writer`对象将开始在`Clob`值的开头写入字符流：

```java
Writer clobWriter = myClob.setCharacterStream(1);
```

`ClobSample.readFile`方法逐行读取文件`fileName`指定的文件，并将其写入`writerArg`指定的`Writer`对象：

```java
private String readFile(String fileName, Writer writerArg)
        throws FileNotFoundException, IOException {

    BufferedReader br = new BufferedReader(new FileReader(fileName));
    String nextLine = "";
    StringBuffer sb = new StringBuffer();
    while ((nextLine = br.readLine()) != null) {
        System.out.println("Writing: " + nextLine);
        writerArg.write(nextLine);
        sb.append(nextLine);
    }
    // Convert the content into to a string
    String clobData = sb.toString();

    // Return the data.
    return clobData;
}
```

以下摘录创建了一个`PreparedStatement`对象`pstmt`，它将`Clob` Java对象`myClob`插入到`COFFEE_DESCRIPTIONS`中：

```java
PreparedStatement pstmt = null;
// ...
String sql = "INSERT INTO COFFEE_DESCRIPTIONS VALUES(?,?)";
pstmt = this.con.prepareStatement(sql);
pstmt.setString(1, coffeeName);
pstmt.setClob(2, myClob);
pstmt.executeUpdate();
```

**查询 CLOB 值**

方法`ClobSample.retrieveExcerpt`从列值`COF_NAME`等于`coffeeName`参数指定的`String`值的行中检索存储在`COFFEE_DESCRIPTIONS`的`COF_DESC`列中的`CLOB` SQL值：

```java
public String retrieveExcerpt(String coffeeName, int numChar)
    throws SQLException {

    String description = null;
    Clob myClob = null;
    PreparedStatement pstmt = null;

    try {
        String sql =
            "select COF_DESC " +
            "from COFFEE_DESCRIPTIONS " +
            "where COF_NAME = ?";

        pstmt = this.con.prepareStatement(sql);
        pstmt.setString(1, coffeeName);
        ResultSet rs = pstmt.executeQuery();

        if (rs.next()) {
            myClob = rs.getClob(1);
            System.out.println("Length of retrieved Clob: " +
                myClob.length());
        }
        description = myClob.getSubString(1, numChar);
    } catch (SQLException sqlex) {
        JDBCTutorialUtilities.printSQLException(sqlex);
    } catch (Exception ex) {
        System.out.println("Unexpected exception: " + ex.toString());
    } finally {
        if (pstmt != null) pstmt.close();
    }
    return description;
}
```

以下行从`ResultSet`对象`rs`中检索`Clob` Java值：

```java
myClob = rs.getClob(1);
```

以下行从`myClob`对象中检索子字符串。子字符串从`myClob`值的第一个字符开始，最多包含`numChar`中指定的个数的连续字符数，其中`numChar`是一个整数。

```java
description = myClob.getSubString(1, numChar);
```

**添加和查询 BLOB 对象**

添加和检索`BLOB` SQL对象类似于添加和检索`CLOB` SQL对象。使用`Blob.setBinaryStream`方法检索`OutputStream`对象，以编写`Blob` Java对象（调用该方法使用的对象）表示的`BLOB` SQL值。

**释放大对象持有的资源**

`Blob`，`Clob`和`NClob` Java对象至少在创建它们的事务期间保持有效。这可能导致应用程序在长时间运行的事务期间耗尽资源。应用程序可以通过调用`free`方法释放`Blob`，`Clob`和`NClob`资源。

在下面的代码片段中，调用方法`Clob.free`来释放为先前创建的`Clob`对象保存的资源：

```java
Clob aClob = con.createClob();
int numWritten = aClob.setString(1, val);
aClob.free();
```

