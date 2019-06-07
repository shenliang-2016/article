#### `try-with-resources` 语句

`try-with-resources`语句是一个声明一个或多个资源的`try`语句。*资源*是一个在程序完成后必须关闭的对象。`try-with-resources`语句确保在语句结束时关闭每个资源。任何实现`java.lang.AutoCloseable`的对象（包括实现`java.io.Closeable`的所有对象）都可以用作资源。

以下示例从文件中读取第一行。它使用`BufferedReader`实例从文件中读取数据。`BufferedReader`是一个在程序完成后必须关闭的资源：

```java
static String readFirstLineFromFile(String path) throws IOException {
    try (BufferedReader br =
                   new BufferedReader(new FileReader(path))) {
        return br.readLine();
    }
}
```

在此示例中，在`try-with-resources`语句中声明的资源是`BufferedReader`。声明语句出现在`try`关键字后面的括号内。Java SE 7及更高版本中的类`BufferedReader`实现了接口`java.lang.AutoCloseable`。因为`BufferedReader`实例是在`try-with-resource`语句中声明的，所以无论`try`语句是正常还是意外结束（由于方法`BufferedReader.readLine`抛出一个异常`IOException`），它都会被关闭。

在Java SE 7之前，您可以使用`finally`块来确保资源被关闭，无论`try` 语句是正常还是意外结束。以下示例使用`finally`块而不是`try-with-resources`语句：

```java
static String readFirstLineFromFileWithFinallyBlock(String path)
                                                     throws IOException {
    BufferedReader br = new BufferedReader(new FileReader(path));
    try {
        return br.readLine();
    } finally {
        if (br != null) br.close();
    }
}
```

但是，在这个例子中，如果方法`readLine`和`close`都抛出异常，那么方法`readFirstLineFromFileWithFinallyBlock`会抛出`finally`块抛出的异常；而从`try`块抛出的异常被抑制。相反，在示例`readFirstLineFromFile`中，如果从`try`块和`try-with-resources`语句抛出异常，则方法`readFirstLineFromFile`抛出从`try`块抛出的异常；而从`try-with-resources`块抛出的异常被抑制。在Java SE 7及更高版本中，您可以检索已抑制的异常。有关详细信息，请参阅 [Suppressed Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html#suppressed-exceptions) 部分。

您可以在`try-with-resources`语句中声明一个或多个资源。以下示例检索`zip`文件`zipFileName`中打包的文件的名称，并创建包含这些文件名称的文本文件：

```java
public static void writeToFileZipFileContents(String zipFileName,
                                           String outputFileName)
                                           throws java.io.IOException {

    java.nio.charset.Charset charset =
         java.nio.charset.StandardCharsets.US_ASCII;
    java.nio.file.Path outputFilePath =
         java.nio.file.Paths.get(outputFileName);

    // Open zip file and create output file with 
    // try-with-resources statement

    try (
        java.util.zip.ZipFile zf =
             new java.util.zip.ZipFile(zipFileName);
        java.io.BufferedWriter writer = 
            java.nio.file.Files.newBufferedWriter(outputFilePath, charset)
    ) {
        // Enumerate each entry
        for (java.util.Enumeration entries =
                                zf.entries(); entries.hasMoreElements();) {
            // Get the entry name and write it to the output file
            String newLine = System.getProperty("line.separator");
            String zipEntryName =
                 ((java.util.zip.ZipEntry)entries.nextElement()).getName() +
                 newLine;
            writer.write(zipEntryName, 0, zipEntryName.length());
        }
    }
}
```

在这个例子中，`try-with-resources`语句包含两个由分号分隔的声明：`ZipFile`和`BufferedWriter`。当直接跟随它的代码块正常或由于异常而终止时，`BufferedWriter`和`ZipFile`对象的`close`方法将按此顺序自动调用。请注意，资源的“close”方法是在它们创建的*相反*顺序中调用的。

以下示例使用`try-with-resources`语句自动关闭`java.sql.Statement`对象：

```java
public static void viewTable(Connection con) throws SQLException {

    String query = "select COF_NAME, SUP_ID, PRICE, SALES, TOTAL from COFFEES";

    try (Statement stmt = con.createStatement()) {
        ResultSet rs = stmt.executeQuery(query);

        while (rs.next()) {
            String coffeeName = rs.getString("COF_NAME");
            int supplierID = rs.getInt("SUP_ID");
            float price = rs.getFloat("PRICE");
            int sales = rs.getInt("SALES");
            int total = rs.getInt("TOTAL");

            System.out.println(coffeeName + ", " + supplierID + ", " + 
                               price + ", " + sales + ", " + total);
        }
    } catch (SQLException e) {
        JDBCTutorialUtilities.printSQLException(e);
    }
}
```

此示例中使用的资源`java.sql.Statement`是 JDBC 4.1 及更高版本 API 的一部分。

**注意：** `try-with-resources`语句可以像普通的`try`语句一样使用`catch`和`finally`块。在`try-with-resources`语句中，任何`catch`或`finally`块在声明的资源关闭后运行。

**被抑制的异常**

可以从与`try-with-resources`语句关联的代码块中抛出异常。在示例`writeToFileZipFileContents`中，可以从`try`块抛出异常，当`try-with-resources`语句尝试关闭`ZipFile`和`BufferedWriter`时，最多可以抛出两个异常对象。 如果从`try`块抛出异常并且从`try-with-resources`语句抛出一个或多个异常，那么从`try-with-resources`语句抛出的那些异常将被抑制，并抛由`writeToFileZipFileContents`方法中的异常代码块抛出的异常。您可以通过从`try`块抛出的异常中调用`Throwable.getSuppressed`方法来检索这些被抑制的异常。

**实现`AutoCloseable`或`Closeable`接口的类**

请参阅[`AutoCloseable`](https://docs.oracle.com/javase/8/docs/api/java/lang/AutoCloseable.html) 和 [`Closeable`](https:// docs.oracle.com/javase/8/docs/api/java/io/Closeable.html) 接口的Javadoc，其中包含实现这些接口之一的类列表。`Closeable`接口扩展了`AutoCloseable`接口。 `Closeable` 接口的`close`方法抛出类型为`IOException`的异常，而`AutoCloseable`接口的`close`方法抛出类型为`Exception`的异常。因此，`AutoCloseable`接口的子类可以覆盖`close`方法的这种行为，以抛出专门的异常，例如`IOException`，或者根本没有异常。