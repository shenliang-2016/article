## 3.8 参数和数值处理的一般问题

参数和数值处理存在的一般问题存在于由 Spring 框架的 JDBC 支持提供的各种不同方法中。本节介绍如何解决这些问题。

### 3.8.1 为参数提供 SQL 类型信息

通常，Spring 基于传入参数的类型来确定参数的 SQL 类型。在设定参数值时显式提供其 SQL 类型是可能的。有时候正确设定 `NULL` 值是有必要的。

你可以通过以下几种方法提供 SQL 类型信息：

- `JdbcTemplate` 的许多更新和查询方法携带一个 `int` 数组形式的附加参数。该数组被用来表示相应参数的 SQL 类型，使用来自 `java.sql.Types` 类的常量值。为每个参数提供一个实体。
- 你可以使用 `SqlParameterValue` 类包装需要附加信息的参数值。为了做到这一点，为每个类创建一个新的实例并在构造方法中传入 SQL 类型和参数值。你还可以为数值提供可选的尺度参数。
- 对于使用命名参数的方法，你可以使用 `SqlParameterSource`，`BeanPropertySqlParameterSource` 或者 `MapSqlParameterSource` 类。它们都有为所有命名参数值注册 SQL 类型的方法。

### 3.8.2 处理 BLOB 和 CLOB 对象

您可以在数据库中存储图像，其他二进制数据和大块文本。这些大对象称为二进制数据的 BLOB（二进制大型对象），而字符数据称为 CLOB（字符大型对象）。在 Spring 中，您可以直接使用 `JdbcTemplate` 以及使用 RDBMS Objects 和 `SimpleJdbc` 类提供的更高抽象来处理这些大对象。所有这些方法都使用 `LobHandler` 接口的实现来实际管理 LOB（大对象）数据。`LobHandler` 通过 `getLobCreator` 方法提供对 `LobCreator` 类的访问，该方法用于创建要插入的新 LOB 对象。

`LobCreator` 和 `LobHandler` 为 LOB 输入输出提供下面的支持：

- BLOB
  - `byte[]`: `getBlobAsBytes` 和 `setBlobAsBytes`
  - `InputStream`: `getBlobAsBinaryStream` 和 `setBlobAsBinaryStream`
- CLOB
  - `String`: `getClobAsString` 和 `setClobAsString`
  - `InputStream`: `getClobAsAsciiStream` 和 `setClobAsAsciiStream`
  - `Reader`: `getClobAsCharacterStream` 和 `setClobAsCharacterStream`

下个例子展示了如何创建并插入一个 BLOB。随后我们展示如何从数据库中读取它。

本例子使用了 `JdbcTemplate` 和 `AbstractLobCreatingPreparedStatementCallback` 实现。它实现了 `setValues` 方法。该方法提供了一个 `LobCreator` ，我们用来设定你的 SQL 插入语句中的 LOB 列字段值。

这个例子中，我们假设存在一个变量，`lobHandler` ，已经设定为一个 `DefaultLobHandler` 实例。你通常可以通过依赖注入设置该值。

下面的例子展示了如何创建和插入一个 BLOB：

```java
final File blobIn = new File("spring2004.jpg");
final InputStream blobIs = new FileInputStream(blobIn);
final File clobIn = new File("large.txt");
final InputStream clobIs = new FileInputStream(clobIn);
final InputStreamReader clobReader = new InputStreamReader(clobIs);

jdbcTemplate.execute(
    "INSERT INTO lob_table (id, a_clob, a_blob) VALUES (?, ?, ?)",
    new AbstractLobCreatingPreparedStatementCallback(lobHandler) {  
        protected void setValues(PreparedStatement ps, LobCreator lobCreator) throws SQLException {
            ps.setLong(1, 1L);
            lobCreator.setClobAsCharacterStream(ps, 2, clobReader, (int)clobIn.length());  
            lobCreator.setBlobAsBinaryStream(ps, 3, blobIs, (int)blobIn.length());  
        }
    }
);

blobIs.close();
clobReader.close();
```

> 如果您在从 `DefaultLobHandler.getLobCreator()` 返回的 `LobCreator` 上调用 `setBlobAsBinaryStream`，`setClobAsAsciiStream` 或 `setClobAsCharacterStream` 方法，则可以为 `contentLength` 参数指定一个负值。如果指定的内容长度为负数，则 `DefaultLobHandler` 将使用 set-stream 方法的 JDBC 4.0 变体，而没有 `length` 参数。否则，它将指定的长度传递给驱动程序。
>
> 请参阅有关 JDBC 驱动程序的文档，以用于验证它是否支持流式 LOB 而无需提供内容长度。

现在是时候从数据库中读取 LOB 数据了。再次，您要使用具有相同实例变量 `lobHandler` 的 `JdbcTemplate` 以及对 `DefaultLobHandler` 的引用。以下示例显示了如何执行此操作：

```java
List<Map<String, Object>> l = jdbcTemplate.query("select id, a_clob, a_blob from lob_table",
    new RowMapper<Map<String, Object>>() {
        public Map<String, Object> mapRow(ResultSet rs, int i) throws SQLException {
            Map<String, Object> results = new HashMap<String, Object>();
            String clobText = lobHandler.getClobAsString(rs, "a_clob");  
            results.put("CLOB", clobText);
            byte[] blobBytes = lobHandler.getBlobAsBytes(rs, "a_blob");  
            results.put("BLOB", blobBytes);
            return results;
        }
    });
```