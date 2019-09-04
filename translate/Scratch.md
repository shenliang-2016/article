### Directory 和 LDAP 包

**Directory 包**

[`javax.naming.directory`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/package-summary.html) 包扩展了 [`javax.naming`](https://docs.oracle.com/javase/8/docs/api/javax/naming/package-summary.html) 包，在命名服务基础上提供了访问目录服务的功能。此包允许应用程序存储在目录中的相关对象以及使用特定属性搜索对象。

**Directory 上下文**

[`DirContext`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html) 接口表示*目录上下文*。通过扩展 [`Context`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html) 接口，`Dircontext` 的行为就像一个名称上下文。这就意味着任何目录对象也可以提供命名上下文。它定义检查和更新目录实体的相关属性的方法。

- 属性

  你使用 [`getAttributes()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html#getAttributes-javax.naming.Name-) 方法来获取目录实体（需要你给定名称）的相关属性。属性可以使用 [`modifyAttributes()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html#modifyAttributes-javax.naming.Name-javax.naming.directory.ModificationItem:A-) 方法修改。你可以使用该操作添加、替换、或者而删除属性和/或属性值。

- 搜索

  `DirContext`包含用于执行基于内容的目录搜索的方法。在最简单和最常见的使用形式中，应用程序指定一组属性，这些属性可能具有匹配的特定值，并将此属性集提交给 [`search()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html#search-javax.naming.Name-javax.naming.directory.Attributes-) 方法。其他重载形式的 [`search()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/DirContext.html#search-javax.naming.Name-javax.naming.directory.Attributes-) 支持更复杂的搜索过滤器。

**LDAP 包**

 [`javax.naming.ldap`](https://docs.oracle.com/javase/8/docs/api/javax/naming/ldap/package-summary.html) 包中包含用于使用特定于 [LDAP v3](http://www.ietf.org/rfc/rfc2251.txt) 的功能的类和接口，这些功能尚未包含在更通用的 [`javax.naming.directory`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/package-summary.html) 包中。事实上，大多数使用LDAP的JNDI应用程序都会找到足够的`javax.naming.directory`包，根本不需要使用`javax.naming.ldap`包。此程序包主要用于需要使用“扩展”操作，控件，或未经请求的通知的应用程序。

- ”扩展“操作

  除了指定定义良好的操作（如搜索和修改）之外， [LDAP v3 (RFC 2251)](http://www.ietf.org/rfc/rfc2251.txt) 还指定了在LDAP客户端和服务器之间传输尚未定义的操作的方法。这些操作称为“扩展”操作。“扩展”操作可以由诸如因特网工程任务组（IETF）之类的标准组织或由供应商定义。

- 控件

   [LDAP v3](http://www.ietf.org/rfc/rfc2251.txt) 允许任何请求或响应通过尚未定义的修饰符（称为控件）进行扩充。与请求一起发送的控件是请求控件，而与响应一起发送的控件是响应控件。控件可以由诸如IETF的标准组织或由供应商定义。请求控件和响应控件不一定是成对的，也就是说，不需要为发送的每个请求控件都有响应控件，反之亦然。

- 未经请求的通知

  除了客户端和服务器之间正常的请求/响应交互方式之外， [LDAP v3](http://www.ietf.org/rfc/rfc2251.txt) 还指定了未经请求的通知 - 从服务器异步发送到客户端而不是响应任何客户端请求的消息。

**LDAP 上下文**

[`LdapContext`](https://docs.oracle.com/javase/8/docs/api/javax/naming/ldap/LdapContext.html) 接口表示用于执行“扩展”操作，发送请求控件和接收响应控件的上下文。JNDI教程的 [Controls and Extensions](https://docs.oracle.com/javase/jndi/tutorial/ldap/ext/index.html) 课程中介绍了如何使用这些功能的示例。