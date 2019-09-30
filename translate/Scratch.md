## 7.8 生成超时链接

### 问题

你需要生成一个超时链接。

### 解决方案

为超时时间生成一个 Unix epoch 格式的时间戳。在 Unix 系统中，你可以通过使用类似下面例子的数据进行测试：

````
$ date -d "2020-12-31 00:00" +%s --utc
1609372800
````

接下来，你讲需要串联你的哈希字符串来匹配为 `secure_link_md5` 指令配置的字符串。这种情况下，我们要使用的字符串将是 `1293771600/resources/index.html 127.0.0.1 mySecret` 。对应的 `md5` 哈希与 16 进制摘要略有不同。`md5` 哈希是二进制格式，base64－编码，加号(+)转化为减号(-)，斜杠(/)转化为下划线(_)，等号(=)被删除。下面是 Unix 系统上的一个例子：

````
$ echo -n '1609372800/resources/index.html127.0.0.1 mySecret' \
      | openssl md5 -binary \
      | openssl base64 \
      | tr +/ -_ \
      | tr -d =
    TG6ck3OpAttQ1d7jW3JOcw
````

现在我们又饿自己的哈希，我们可以将它用作超时时间的参数：

````
/resources/index.html?md5=TG6ck3OpAttQ1d7jW3JOcw&expires=1609372
      800'
````

以下是 Python 中一个更实际的示例，该示例利用相对时间来设定超时，并将链接设置为从生成起一小时内到期。在编写本文时，此示例使用 Python 标准库在 Python 2.7 和 3.x 中工作：

````
from datetime import datetime, timedelta from base64 import b64encode
import hashlib
    # Set environment vars
    resource = b'/resources/index.html'
    remote_addr = b'127.0.0.1'
    host = b'www.example.com'
    mysecret = b'mySecret'
    # Generate expire timestamp
    now = datetime.utcnow()
    expire_dt = now + timedelta(hours=1)
    expire_epoch = str.encode(expire_dt.strftime('%s'))
    # md5 hash the string
    uncoded = expire_epoch + resource + remote_addr + mysecret
    md5hashed = hashlib.md5(uncoded).digest()
    # Base64 encode and transform the string
    b64 = b64encode(md5hashed)
    unpadded_b64url = b64.replace(b'+', b'-')\
.replace(b'/', b'_')\ 80 | Chapter 7: Security Controls
￼
.replace(b'=', b'')
    # Format and generate the link
    linkformat = "{}{}?md5={}?expires={}"
    securelink = linkformat.format(
        host.decode(),
        resource.decode(),
        unpadded_b64url.decode(),
        expire_epoch.decode()
) print(securelink)
````

### 讨论

通过这种模式，我们能够以特殊格式生成可用于 URL 的安全链接。该密钥通过使用从未发送给客户端的变量来提供安全性。您可以根据需要使用任意多个其他变量来保护某个位置。`md5` 哈希和 base64 编码是常见的，轻量级的，并且几乎在每种语言中都可用。

