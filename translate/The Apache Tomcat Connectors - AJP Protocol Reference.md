# The Apache Tomcat Connectors - AJP Protocol Reference

## 介绍

Apache Tomcat Connectors 项目作为 Tomcat 项目的一部分，提供 web 服务器插件用以连接 web 服务器和 Tomcat 及其它后端组件。

支持的 web 服务器包括：

* Apache HTTP 服务器，包含名为 mod_jk 的插件（模块）。
* 微软 IIS ，包含名为 ISAPI redirector 的插件（扩展）。
* iPlanet web 服务器，包含名为 NSAPI redirector 的插件。

所有情况下，这些插件都使用一种特定协议来连接后端，名为 Apache JServ Protocol ，或者简称为 AJP。众所周知的支持 AJP 的后端有 Apache Tomcat、Jettey 和 JBoss。尽管该协议存在3个版本：ajp12、ajp13 和 ajp14，大多数服务器使用都只是使用 ajp13。老版本 ajp12 不使用持久化连接，已经过时。新版本 ajp14 还处于实验研究阶段。有时，ajp13 会被称为 AJP 1.3 或者 AJPv13，不过我们就只使用 ajp13 这个名字。

## ajp13 介绍

此文档最初是由 Dan Milstein danmil@shore.net 在2000年12月编写。目前此文档由 xml 文件产生，以便于集成到 Tomcat 文档中。

此文档描述 Apache JServProtocol 版本 1.3，下面称为 ajp13。很明显，目前并没有其它文献说明该协议如何工作。此文档试图填补此空白。希望可以帮到协议的维护者和潜在的协议移植者。

## 关于作者

我并不是协议的设计者之一，我认为 Gal Shachor 是最初的协议设计者。此文档中的所有内容都是由我在 tomcat 3.x 版本代码中看到的具体实现衍生而来，但是我并不能保证绝对准确。我也不清楚某些设计决策的动机。尽我所能，我尝试给出了一些选择的合理解释，但是也是仅仅基于我的猜测。总之，Shachor 写的 C 代码非常整洁易读，即使完全没有文档。我整理了 Java 文档，我认为已经足够清晰易懂了。

## 设计目标

基于 Gal Shachor 在 jakarta-dev 邮件列表中的邮件，此版本协议关于 JK （ajp13）的最初目标是扩展 mod_jserv 和 ajp12（我仅仅包含了关于 web 服务器和 servlet 容器之间通信的部分目标），通过以下方式：

* 改善性能，特别是速度。
* 增加对 SSL 的支持，从而````isSecure()````和````getScheme()````将可以在 servlet 容器中正常工作。客户端证书和加密套件将可以作为请求属性被用于 servlets 。

## 协议概览

ajp13 是一个面向数据包的协议。基于性能考虑该协议选择了二进制格式数据，而不是可读性更好的普通文本。web 服务器通过 TCP 连接与 servlet 容器通信。为了减少昂贵的 socket 创建过程，web 服务器将试图保持与 servlet 容器的持久化 TCP 连接，同时在多个请求响应周期内重用同一个连接。

一旦一个连接分配到一个特定的请求，它在该请求处理周期终结之前都不能被其它请求使用。换句话说，请求并不能多路复用连接。这就使得连接两端的代码非常简单，然而也导致同时会有更多连接被创建。

一旦 web 服务器已经打开一个到 servlet 容器的连接，该连接可能处于下列某个状态中的一个：

* 空闲

  没有请求通过该连接被处理

* 已分配

  该连接正在处理一个特定请求

一旦一个连接被分配给一个特定的请求，基本的请求信息（比如 HTTP 首部）将以高度浓缩的形式（比如，通常是将字符串编码为整数）通过连接被发送。该格式的细节在下面的请求数据包结构中详述。如果请求存在请求体（content-length > 0），则请求体将紧随其后以单独的数据包被发送。

此刻，servlet 容器应该已经预先准备好了开始请求处理。如果是，则接下来它将会发送下列消息给 web 服务器：

* SEND_HEADERS

  回送一个首部集合给浏览器。

* SEND_BODY_CHUNK

  回送一个消息体数据分片给浏览器。

* GET_BODY_CHUNK

  从请求获取更多数据，如果它还没有传输完成。这是有必要的，因为数据包由固定的最大尺寸，同时请求所包含的数据的数量却并不是确定的（比如文件上传的场景）。（注意：这个与 HTTP 的分片传输无关。）

* END_RESPONSE

  结束请求处理周期。

每条消息都伴随着不同格式的数据包。参见下文响应数据包结构获取更多细节。

## 基本数据包结构

此协议从外部数据表示法 XDR 规范中继承了一些东西，但是又有很大不同，比如没有 4 字节组合。

ajp13 对所有数据类型使用网络字节顺序。

此协议中包含 4 种数据类型：字节、布尔、整型和字符串类型。

**Byte**

​	一个单独的字节。

**Boolean**

​	一个单独的字节，1 = true，0 = false。使用其它非 0 值表示 true 是 C 语言风格，但是并不一定总是有效的。

**Integer**

​	取值范围在 0 到 2^16 (32768) 之间的数字。2 字节存储，高位字节优先顺序（高字节保存在内存的低地址中，所谓的大端模式）。

**String**

​	可变长度字符串，长度最大 2^16。首先将长度打包进两个字节之后编码，随后是字符串，包括作为字符串结束符号的````\0````。注意，编码之后的长度并不包括作为结束符的````\0````，就像````strlen````返回值。这一点在 Java 端看来可能会造成某些混乱，因为 Java 中充斥着各种自增操作来跳过这些终结符。我猜测这么做的目的是为了保证 C 代码额外的效率，C 代码在读取 servlet 容器发送回来的携带该终结符的字符串时效率更高，C 代码能够直接将字符串引用传递到一个单独的缓冲区中，而不需要复制。如果没有终结符````\0````，则 C 代码就必须将内容拷贝出来以获取它作为一个字符串的证据。注意长度值为 -1（65535）表示一个````null````字符串，也就是长度数据之后并没有什么数据。

### 数据包尺寸

根据大量代码分析得到，数据包最大尺寸是 8*1024 (8k)。数据包的实际长度被编码在首部中。

### 数据包首部

从 web 服务器向容器发送的数据包以````0x1234````。从容器向 web 服务器发送的数据包以````AB````开头（这是字符 A 和 B 的 ASCII 码表示）。这些两个字节之后，是表示载荷长度的整数（已编码）。尽管看起啦最大载荷长度可以达到 2^16 字节，事实上，相关实现代码已经将载荷最大程度限制为 8k 字节。

**数据包格式（web 服务器 -> 容器）**

````xml
字节		0		1		2		3		4...(n+3)
内容		0x12	0x34	Data Length(n)	Data
````

**数据包格式（容器 -> web 服务器）**

````xml
字节		0		1		2		3		4...(n+3)
内容		A		B		Data Length(n)	Data
````

对大多数数据包来说，载荷中的第一个字节编码了消息的类型。例外的情况是从 web 服务器向容器发送的请求体数据包，它们携带一个标准的数据包首部，````0x1234```` 然后是数据包的长度，但是随后并没有任何前缀类型代码（看起来是我的错误）。

web 服务器可以将下列消息发送给 servlet 容器：

| 类型代码 | 数据包类型           | 含义                       |
| ---- | --------------- | ------------------------ |
| 2    | Forward Request | 基于接下来的数据开始请求处理周期         |
| 7    | Shutdown        | web 服务器要求容器关闭            |
| 8    | Ping            | web 服务器要求容器接管控制权（安全登录阶段） |
| 10   | CPing           | web 服务器要求容器尽快响应一个 CPong  |
| none | Data            | 尺寸（2字节）和相应的消息体数据         |

为了保证基本的安全性，容器实际上只能接受来自它自己所运行的机器的````Shutdown````请求。

第一个````Data````数据包在````Forward Request````之后会立即被 web 服务器发送。

servlet 容器可以发送下列类型的消息给 web 服务器：

| 类型代码 | 数据包类型           | 含义                                       |
| ---- | --------------- | ---------------------------------------- |
| 3    | Send Body Chunk | 从 servlet 容器发送一个消息体分片到 web 服务器（推测，应该是发送给浏览器） |
| 4    | Send Headers    | 从 servlet 容器发送响应首部到 web 服务器（推测，应该是发送给浏览器） |
| 5    | End Response    | 标识响应的结束（也就是请求处理周期的结束）                    |
| 6    | Get Body Chunk  | 从请求中获取更多数据，如果请求尚未被全部传输                   |
| 9    | CPong Reply     | 对 CPing 请求的响应                            |

上述每种消息都有不同的内部结构，下面详述。

## 请求数据包结构

从 web 服务器到容器的````Forward Request````类型消息结构：

````xml
AJP13_FORWARD_REQUEST :=
	prefix_code			(byte) 0x02 = JK_AJP13_FORWARD_REQUEST
	method				(byte)
	protocol			(String)
	req_uri				(String)
	remote_addr			(String)
	remote_host			(String)
	server_name			(String)
	server_port			(integer)
	is_ssl				(boolean)
	num_headers			(String)
	request_headers		*(req_header_name req_header_value)
	attributes			*(attribute_name attribute_value)
	request_teminator	(byte) 0xFF
````

````request_headers````结构：

````xml
req_header_name :=
	sc_req_header_name | (String) [see below for how this is parsed]

sc_req_header_name := 0xA0xx (integer)

req_header_value := (String)
````

可选的````attributes````具有以下结构：

````xml
attribute_name := sc_a_name | (sc_a_req_attribute string)

attribute_value := (string)
````

注意，最重要的首部字段就是````content-length````，因为它决定了容器是否应该立即寻找下一个数据包。

下面是关于````Forward Request````的详细描述。

### 请求前缀

对所有的请求，请求前缀都是 2。

### 方法

HTTP 方法，被编码为一个单独的字节：

| 方法名              | 编码   |
| ---------------- | ---- |
| OPTIONS          | 1    |
| GET              | 2    |
| HEAD             | 3    |
| POST             | 4    |
| PUT              | 5    |
| DELETE           | 6    |
| TRACE            | 7    |
| PROPFIND         | 8    |
| PROPPATCH        | 9    |
| MKCOL            | 10   |
| COPY             | 11   |
| MOVE             | 12   |
| LOCK             | 13   |
| UNLOCK           | 14   |
| ACL              | 15   |
| REPORT           | 16   |
| VERSION-CONTROL  | 17   |
| CHECKIN          | 18   |
| CHECKOUT         | 19   |
| UNCHECKOUT       | 20   |
| SEARCH           | 21   |
| MKWORKSPACE      | 22   |
| UPDATE           | 23   |
| LABEL            | 24   |
| MERGE            | 25   |
| BASELINE_CONTROL | 26   |
| MKACTIVITY       | 27   |

ajp13 版本之后，使用 mod_jk2 时，即使不在上述列表中的额外方法也会被传输。

### protocol, req_uri, remote_addr, remote_host, server_name, server_port, is_ssl

这些字段都具有很好的自解释性，所有这些字段都是必须的，每个请求都需要包含。

### 首部

````request_headers````的结构如下：首先时编码之后的首部字段数目````num_headers````。然后是一系列的````req_header_name/req_header_value````对。为了节省空间，基本首部字段名都被编码为整数。如果首部字段名不在基本首部字段列表中，则其会被规范化编码（作为一个字符串，前缀长度）。基本首部字段名称````sc_req_header_name````和对应的编码如下：

| 名称              | 编码值    | 编码名称                   |
| --------------- | ------ | ---------------------- |
| accept          | 0xA001 | SC_REQ_ACCEPT          |
| accept-charset  | 0xA002 | SC_REQ_ACCEPT_CHARSET  |
| accept-encoding | 0xA003 | SC_REQ_ACCEPT_ENCODING |
| accept-language | 0xA004 | SC_REQ_ACCEPT_LANGUAGE |
| authorization   | 0xA005 | SC_REQ_TUTHORIZATION   |
| connection      | 0xA006 | SC_REQ_CONNECTION      |
| content-type    | 0xA007 | SC_REQ_CONTENT_TYPE    |
| content-length  | 0xA008 | SC_REQ_CONTENT_LENGTH  |
| cookie          | 0xA009 | SC_REQ_COOKIE          |
| cookie2         | 0xA00A | SC_REQ_COOKIE2         |
| host            | 0xA00B | SC_REQ_HOST            |
| pragma          | 0xA00C | SC_REQ_PRAGMA          |
| referer         | 0xA00D | SC_REQ_REFERER         |
| user-agent      | 0xA00E | SC_REQ_USER_AGENT      |

Java 代码在读取数据包时获取开头两个字节的整数，如果它的高位字节看起来是````0xA0````，则该 Java 代码将使用该整数的第二个字节内容作为首部字段名数组的下标。如果它的第一个字节不是````0xA0````，则代码会假定这开头两个字节的整数是接下来将要读入的字符串的长度。

以上逻辑的基础是假定所有首部字段名称的长度都不超过````0x9FFF(==0xA000 - 1)````。这个当然是完全合理的，虽然多少有些专断。如果你像我一样，此时想到了 cookie 规范，其中的首部字段长度可以有多长，但是并不是一个问题，这里的长度限制是关于首部字段名，而不是值。看起来在 HTTP 规范里也不太可能很快出现不受管控的巨大首部字段名。

注意：````content-length````首部字段是非常重要的。如果该字段存在且非0，容器就会假定请求包含请求体（比如一个 POST 请求），从而立即回尝试从输入流中读取下一个单独的数据包以获取该请求体。

### 属性

名称以````?````开头的属性都是可选的。每个属性都有对应的一个字节的编码来表示其类型，还有一个字符串来表示其值。它们可以被以任何顺序发送（虽然 C 代码永远会以以下顺序发送它们）。一个特殊的终结编码被发送用以表示可选属性列表的结束。该字节编码列表如下：

| 属性名            | 编码   | 说明           |
| -------------- | ---- | ------------ |
| ?context       | 0x01 | 尚未实现         |
| ?servlet_path  | 0x02 | 尚未实现         |
| ?remote_user   | 0x03 |              |
| ?auth_type     | 0x04 |              |
| ?query_string  | 0x05 |              |
| ?route         | 0x06 |              |
| ?ssl_cert      | 0x07 |              |
| ?ssl_cipher    | 0x08 |              |
| ?ssl_session   | 0x09 |              |
| ?req_attribute | 0x0A | 名称（后面的属性的名称） |
| ?ssl_key_size  | 0x0B |              |
| ?secret        | 0x0C |              |
| ?stored_method | 0x0D |              |
| are_done       | 0xFF | 请求终结符        |

````context````和````servlet_path````目前并不是由 C 代码设置，而且大多数 Java 代码都会忽略这两个字段（某些代码实际上会在这些编码之后携带字符串的情况下直接跳出）。我不确定这究竟是个缺陷还是一个尚未实现的特性，或者根本就只是一些残留代码。但是这两个属性在连接的两端都会丢失。

````remote_user````和````auth_type````大概是关于 HTTP 层面的身份认证，用来传递远程用户的用户名和用来建立他们的身份标识的认证机制类型（比如 Basic、Digest）。我不清楚为什么密码没有一起被发送。同时我也完全不了解 HTTP 身份认证。

````query_string````、````ssl_cert````、````ssl_cipher````和````ssl_session````关于相应的 HTTP 和 HTTPS 内容。

````route````属性字段，按照我的理解，用来支持粘性会话，将一个用户会话关联到一个特定的 Tomcat 实例，在多个实例的负载均衡的服务器集群环境中。我不了解其中细节。

除了上述基本属性列表，任何数量的其它属性都可以通过````req_attribute````编码（0x0A）。表示该属性名和值的一对字符串会立即被发送。环境变量值可以通过这种方式传递。

最终，当所有属性都已经发送完毕，终结符````0xFF````就会被发送。该信号出现在属性列表的结尾，同时也出现在请求数据包的结尾。

## 响应数据包结构

容器可以发送给 web 服务器的消息结构：

````xml
AJP13_SEND_BODY_CHUNK :=
	prefix_code		3
	chunk_length	(integer)
	chunk			*(byte)

AJP13_SEND_HEADERS :=
	prefix_code			4
	http_status_code	(integer)
	http_status_msg		(string)
	num_headers			(integer)
	response_headers	*(res_header_name header_value)

res_header_name :=
	sc_res_header_name | (string) [see below for how this is parsed]

sc_res_header_name := 0xA0 (byte)

header_value := (string)

AJP13_END_RESPONSE :=
	prefix_code		5
	reuse			(boolean)

AJP13_GET_BODY_CHUNK :=
	prefix_code			6
	requested_length	(integer)
````

### 发送消息体分片

消息体分片是基本的二进制数据，直接被发送回浏览器。

### 发送首部

状态码和状态描述是 HTTP 的正常内容（比如````200````和````OK````）。响应首部字段名称会像请求首部字段名称相同的方式被编码。通用首部字段编码如下：

| 名称               | 编码     |
| ---------------- | ------ |
| Content-Type     | 0xA001 |
| Content-Language | 0xA002 |
| Content-Length   | 0xA003 |
| Date             | 0xA004 |
| Last-Modified    | 0xA005 |
| Location         | 0xA006 |
| Set-Cookie       | 0xA007 |
| Set-Cookie2      | 0xA008 |
| Servlet-Engine   | 0xA009 |
| Status           | 0xA00A |
| WWW-Authenticate | 0xA00B |

字符串首部字段名被编码后，字段值立即就会被编码。

### 响应结束

请求处理周期结束信号。如果````reuse````标识是````true````（对 C 代码来说是非0的任何值），该 TCP 连接可以被新到来的请求再次使用。如果````reuse```` 标识是````false````（==0）则连接应该被关闭。

### 获取消息体分片

容器从请求获取更多数据（如果请求体太大以至于无法装入第一个数据包，或者请求经过了分片）。web 服务器将发送一个消息体数据包给容器，其中包含的数据的最小数量是````request_length````，最大数量是可发送的消息体的最大值 8186（8k  - 6）字节，实际的数据就是请求体尚未发送的数据。

如果消息体已经没有更多数据（比如，容器实体跨越消息体结尾读取数据），web 服务器将回送一个````empty````数据包，其消息体数据包中有效载荷长度是0。（0x12, 0x34, 0x00, 0x00）

## 我的疑问

如果请求首部大小超过了最大的数据包长度时会发生什么？并没有找到当请求首部长度超过8k字节时发送第二个数据包的规范。我猜这个问题在响应发送逻辑中进行了处理，但是并不确定。我不知道是否存在方法可以将8k字节以上的数据放入请求首部字段中，但是我敢打赌存在这种情况（比如包含大量 ssl 信息和环境变量的 cookies 数据很容易就会超过8k字节）。我认为这种情况下连接器将会在尝试发送任何首部字段之前就失败，但是我并不确定。

身份认证呢？看起来在 web 服务器和 servlet 容器之间的连接上不存在任何身份认证。我认为这是一个潜在的风险。