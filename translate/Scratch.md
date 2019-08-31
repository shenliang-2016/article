## 7.2 允许跨域资源共享

### 问题

你从另外一个域名提供资源服务，需要允许跨域资源共享(CORS)以允许浏览器使用这些资源。

### 解决方案

修改基于`request` 方法的首部以启用 CORS ：

````
map $request_method $cors_method {
	OPTIONS 11;
	GET  1;
	POST 1;
	default 0;
}
server {
	...
	location / {
		if ($cors_method ~ '1') {
			add_header 'Access-Control-Allow-Methods'
				'GET,POST,OPTIONS';
			add_header 'Access-Control-Allow-Origin'
        '*.example.com';
      add_header 'Access-Control-Allow-Headers'
        'DNT,
         Keep-Alive,
         User-Agent,
         X-Requested-With,
         If-Modified-Since,
         Cache-Control,
         Content-Type';
		}
		if ($cors_method = '11') {
			add_header 'Access-Control-Max-Age' 1728000;
      add_header 'Content-Type' 'text/plain; charset=UTF-8';
      add_header 'Content-Length' 0;
      return 204;
		}
	}
}
````

在这个例子中有很多内容，通过使用`map`将`GET`和`POST`方法组合在一起来浓缩。`OPTIONS`请求方法向客户端返回有关此服务器的`CORS`规则的*preflight*请求。CORS 允许使用`OPTIONS`，`GET`和`POST`方法。设置`Access-Control-Allow-Origin`首部允许从此服务器提供的内容也可用于`origins`与此首部匹配的页面。该*preflight*请求可以缓存在客户端上 1,728,000 秒或20天。

### 讨论

当请求的资源属于非自己的域时，JavaScript 等资源会生成 CORS。当请求被视为跨域时，浏览器必须遵守 CORS 规则。如果资源没有专门允许其使用的首部，则浏览器不会使用该资源。为了允许我们的资源被其他子域使用，我们必须设置 CORS 首部，这可以使用`add_header`指令完成。如果请求是具有标准内容类型的`GET`，`HEAD`或`POST`，并且请求没有特殊首部，则浏览器将发出请求并仅检查`origin`。其他请求方法将使浏览器发出*preflight*请求以检查它将遵循该资源的服务器的条款。如果您没有正确设置这些首部，浏览器在尝试使用该资源时会出错。

