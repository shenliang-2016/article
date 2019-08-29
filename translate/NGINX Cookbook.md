# NGINX Cookbook

高性能负载均衡先进方案

Derek Dejonghe

# 目录

（完成后自动生成）

# 序

欢迎来到 NGINX Cookbook 的最新升级版本。距离 O'Reilly 发布这个手册的最初版本已经过去将近两年。过去的两年里很多事情都发生了变化，除了一件事：全世界每天都有越来越多的网站开始运行在 NGINX 之上。如今这个数字大概是 3 亿，大约是本手册最初版本发布时的两倍。

大量的理由可以支持这个事实：从最初版本至今已经过去 14 年，NGINX 仍然在不断成长。它是一把瑞士军刀：NGINX 可以是一个 web 服务器，负载均衡器，内容缓存，或者是 API 网关。不过可能更重要的原因是，它是可靠的。

NGINX Cookbook 向你展示如何从 NGINX 开放源代码和 NGINX Plus 中得到这一切。你将看到超过 150 页的简单的介绍，涵盖了包括如何正确安装 NGINX，如何配置所有主要特性，调试以及常见错误等等内容。

此升级版本还包含了诸如 gRPC 支持、HTTP/2 服务端推送、以及为了在集群环境中进行负载均衡的随机二选一算法等新的开源特性。同时还包括新的 NGINX Plus 特性诸如支持状态共享、新的 NGINX Plus API 以及一个键值对存储。本手册几乎涵盖了所有你需要知道的有关 NGINX 的信息。

希望你会喜欢本手册，同时也希望它可以在你创建和部署应用时提供有效的帮助。

— Faisal Memon

Product Marketing Manager, NGINX, Inc.

# 前言

NGINX Cookbook 的目标是提供一系列简单易懂的例子，来说明真实世界中应用交付过程中可能遇到的问题。贯穿本书，你将获取到 NGINX 的许多特性以及如何使用它们。本手册相当全面，涉及到 NGINX 的绝大部分主要能力。

贯穿本书，会出现对免费且开源的 NGINX 软件的引用，也会出现对许多 NGINX 公司相关商业产品的引用，比如 NGINX Plus。作为付费版本组成部分的 NGINX Plus 的特性和指令只能付费使用。由于 NGINX Plus 是应用程序交付控制器，同时提供了许多高级特性，重视这些特性对全面了解 NGINX 平台是很重要的。

本书将从 NGINX 和 NGINX Plus 的安装过程开始，连同一些基本的新手上路步骤等。然后，第二部分介绍各种形式的负载均衡，以及有关流量控制、缓存以及自动化的章节。认证和安全控制章节涵盖大量内容，其重要性在于 NGINX 通常都是网络流量进入你的应用的第一个入口，也就是应用层的第一道防线。还有若干章节涵盖大量前沿主题，诸如 HTTP/2，媒体流，云及容器环境等。同样也包括更传统一些的可选主题，诸如监控，调试，性能等等。

我自己将 NGINX 作为一个多用途工具，我相信本书可以指引您也做到这一点。它是我信赖并乐于使用的软件。很高兴与你分享这些只是，同时希望通过阅读本书，你可以将其中的方案联系到你遇到的真实世界的应用场景，并采用这些解决方案。

# 1 基础

## 1.0 介绍

想要了解 NGINX 开源代码或者 NGINX Plus，你需要首先安装它们并学习一些基础知识。本章节你将学到如何安装 NGINX，它的主配置文件的位置以及管理员命令等。同时还有如何验证你的安装，以及如何发送请求到默认服务器。

## 1.1 在 Debian/Ubuntu 上安装

### 问题

你需要安装 NGINX 开源代码到 Debian 或者 Ubuntu 机器上。

### 解决方案

创建名为`/etc/apt/sources.list.d/nginx.list`，包含以下内容：

````shell
deb http://nginx.org/packages/mainline/OS/ CODENAME nginx
deb-src http://nginx.org/packages/mainline/OS CODENAME nginx
````

修改文件，将其中 URL 末尾的`OS`替换为`ubuntu`或者`debian`，取决于你采用哪种发行版。同时，以你的发行版编码名称替换其中的`CODENAME`，Debian上是`jessie`或者`stretch` ，Ubuntu上是`trusty`，`xenial`，`artful`，或者`bionic` 。然后，运行下面的命令：

````shell
wget http://nginx.org/keys/nginx_signing.key
apt-key add nginx_signing.key
apt-get update
apt-get install -y nginx
/etc/init.d/nginx start
````

### 讨论

你刚刚创建的文件指示`apt`包管理系统使用 NGINX 官方代码仓库。下载命令之后的命令下载 NGINX GPG 包签名密钥并将其导入`apt` 。提供签名给`apt`系统就使得后者可以验证来自远程仓库的包。`apt-get-update`命令指示`apt`系统根据它所知道的仓库刷新它的包列表。刷新包列表之后，你可以从 NGINX 官方仓库安装 NGINX 开源代码。安装之后，最后一条命令启动 NGINX 。

## 1.2 在 RedHat/CentOS 上安装

### 问题

你需要在 RedHat 或者 CentOS 上安装 NGINX 开源代码。

### 解决方案

创建一个名为`/etc/yum.repos.d/nginx.repo`的文件包含以下内容：

````shell
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/mainline/OS/OSRELEASE/$basearch/
gpgcheck=0
enabled=1
````

修改文件，将其中 URL 末尾的`OS`替换为`rhel`或者`centos`，取决于你采用哪种发行版。同时，以你的发行版版本替换其中的`OSRELEASE`，版本 6.x 对应于`6`，版本 7.x 对应于`7` 。然后，运行下面的命令：

````shell
yum -y install nginx
systemctl enable nginx
systemctl start nginx
firewall-cmd --permanent --zone=public --add-port=80/tcp
firewall-cmd --reload
````

### 讨论

你刚刚创建的文件指示`yum`包管理系统利用官方 NGINX 开源代码包仓库。接下来的命令从官方仓库安装 NGINX 开源代码，并指示`systemd`在系统启动时启动 NGINX，然后告诉它现在启动 NGINX。防火墙民工为 TCP 协议开放`80`端口，这是 HTTP 协议的默认端口。最后的命令重新加载防火墙以使设置生效。

## 1.3 安装 NGINX Plus

### 问题

你需要安装 NGINX Plus。

### 解决方案

访问 http://cs.nginx.com/repo_setup 。从下拉菜单中选择你的操作系统，然后跟着安装向导操作。安装过程类似于安装开源代码。不过你还需要安装一个证书以认证身份来访问 NGINX Plus 仓库。

### 讨论

NGINX 确保此仓库中的安装向导始终最新。根据你的操作系统和版本不同，这些向导略有不同，但是其共同之处是：你需要登录 NGINX 门户下载提供给您的证书和密钥才能通过身份认证访问 NGINX Plus 仓库。

## 1.4 验证安装

### 问题

你希望验证 NGINX 安装并确认版本。

### 解决方案

你可以验证已经安装的 NGINX 并确认它的版本，通过下面的命令：

````shell
$ nginx -v
nginx version: nginx/1.15.3
````

如这个例子所示，响应展示了版本。

你可以确认 NGINX 正在运行，通过使用以下命令：

````shell
$ ps -ef | grep nginx
root	1738	1		0	19:54	?	00:00:00	nginx: master process
nginx	1739	1738	0	19:54	?	00:00:00	nginx: worker process
````

`ps`命令列出运行中的进程。将结果通过管道传递给`grep`命令，你可以在输出中搜索特定的单词。这个例子使用`grep`搜索`nginx`。结果显示有两个运行中的进程，一个`master`和一个`worker`。如果 NGINX 正在运行，你将始终都能看到一个`master`进程和一个或者多个`worker`进程。有关启动 NGINX 的指引请看下一章节。要将 NGINX 作为守护进程启动，请使用 `init.d`或者`systemd`方法。

为了验证 NGINX 可以正确响应请求，使用你的浏览器向你的机器发出请求，或者使用`curl`：

````shell
$ curl localhost
````

你将看到 NGINX 默认的欢迎页面。

### 讨论

`nginx`命令允许你与 NGINX 二进制包交互以确认版本、列出已安装模块、测试配置以及向`master`进程发送信号等。NGINX 必须保持运行以服务请求。`ps`命令是确定 NGINX 当前是作为守护进程还是前台程序在运行的万全之策。随着 NGINX 默认提供的配置使得 NGINX 运行一个端口`80`上的静态站点 HTTP 服务器。你可以通过创建一个 HTTP 请求到`localhost`地址上的机器来测试这个默认站点，当然请求主机的 IP 或者主机名也可以。

## 1.5 关键文件，命令，和名录

### 问题

你需要理解重要的 NGINX 目录和命令。

### 解决方案

#### NGINX 文件和目录

*/etc/nginx/*

​	此目录是 NGINX 服务器的默认配置根目录。在这里你将发现决定 NGINX 行为的配置文件。

*/etc/nginx/nginx.conf*

​	此文件是 NGINX 服务使用的默认配置的入口点。该配置文件设置全局设定，诸如`worker`进程、新能调优、日志、模块动态加载、以及对其它 NGINX 配置文件的引用。在默认配置中，此文件包含顶级`http`块，其中包括下面描述的目录中所有的配置文件。

*/etc/nginx/conf.d/*

​	此目录包含默认 HTTP 服务器配置文件。此目录中以`.conf`结尾的文件都包含在*/etc/nginx/nginx.conf*文件中的顶级`http`块中。这是使用`include`语句来组织你的配置文件以降低配置复杂度的最佳实践。在某些包仓库中，此目录被命名为*sites-enabled*，同时配置文件链接自名为*sites-available*的目录，不过这个传统已经过时了。

*/var/log/nginx/*

​	此目录是默认的 NGINX 日志文件位置。此目录中你可以发现一个*access.log*文件和一个*error.log*文件。前者包含对应于每个达到 NGINX 的请求的数据实体。如果调试模块启用，后者包含错误事件和相关的调试信息。

#### NGINX 命令

`nginx -h`

​	展示 NGINX 帮助菜单。

`nginx -v`

​	展示 NGINX 版本。

`nginx -V`

​	展示 NGINX 版本，构建信息以及配置参数，其中展示构建进入 NGINX 二进制包的模块。

`nginx -t`

​	测试 NGINX 配置。

`nginx -T`

​	测试 NGINX 配置并打印验证过的配置到屏幕。此命令在寻求支持时非常有用。

`nginx -s signal`

​	`-s`标记发送一个信号给 NGINX `master`进程。你可以发送信号诸如`stop`，`quit`，`reload`，以及`reopen`。其中`stop`信号立即停止 NGINX 进程。`quit`信号在 NGINX 进程处理完当前请求之后才会停止它。`reload`信号重新加载配置。`reopen`信号指示 NGINX 重新打开日志文件。

### 讨论

理解和这些关键文件、目录以及命令之后，你就已经准备好了开始使用 NGINX 。有了这些认识，你可以修改默认配置文件同时测试你的修改通过使用`nginx -t`命令。如果你测试通过，你也将知道如何指示 NGINX 来重新加载配置文件，使用`nginx -s reload`命令。

## 1.6 提供静态内容服务

### 问题

你需要使用 NGINX 提供静态内容服务。

### 解决方案

重写*/etc/nginx/conf.d/default.conf*文件中的默认 HTTP 服务器配置，改为下面的 NGINX 配置：

````
server {
	listen 80 default_server;
	server_name www.example.com;

	location / {
		root /usr/share/nginx/html;
		# alias /usr/share/nginx/html;
		index index.html index.htm;
	}
}
````

### 讨论

此配置通过 HTTP 协议在`80`端口上提供来自目录*/usr/share/nginx/html/*的静态文件服务。此配置的第一行定义了一个新的`server`块。这定义了一个新的上下文由 NGINX 来监听。第二行指示 NGINX 监听`80`端口，同时`default_server`参数指示 NGINX 使用该服务器作为端口`80`的默认上下文。`server_name`指令定义主机名，或者请求应该直接发送到此服务器的名称。如果此配置没有定义作为`default_server`的上下文，当 HTTP 主机首部匹配到`server_name`指令提供的值时，NGINX 将直接请求此服务器。

`location`块基于 URI 上的路径定义一个配置。该路径，或者 URL 中域名之后的部分，被作为 URI。NGINX 将最佳匹配该 URI 请求到一个`location`块。上面例子中使用`/`来匹配所有请求。`root`指令指示 NGINX 到哪里去寻找为给定上下文提供服务内容的静态文件。请求的 URI 被附加到这个`root`指令值后面，然后用来寻找请求的文件。如果我们已经为`location`指令体哦国内了一个 URI 前缀，这就将被包含到连接之后的路径中，除非为我们使用`alias`目录而不是`root`目录。最后，`index`指令为 NGINX 提供了一个默认文件，或者一个文件列表，当 URI 中没有提供进一步的路径时使用。

## 1.7 优雅地重新加载

### 问题

你需要在不丢包的情况下重新加载你的配置。

### 解决方案

使用 NGINX 的`reload`方法来实现无需停止服务器的优雅的配置重新加载：

````shell
$ nginx -s reload
````

这个例子重新加载 NGINX 系统，实际上是使用 NGINX 二进制程序向`master`进程发送了一个信号。

### 讨论

不停机重新加载 NGINX 配置提供了运行时不丢包热更新配置的能力。在高实时、动态环境中，你将需要在某些时候改变你的负载均衡配置。NGINX 允许你在保持负载均衡器在线的情况下做到这一点。此特性开启了无穷的可能性，比如在生产环境中的重新运行配置管理，或者构建一个应用 - 以及集群敏感的模块来动态配置和重新加载 NGINX 以应对环境需求。

# 2 高性能负载均衡

## 2.0 介绍

今天的因特网用户体验要求性能和实时性。为了获得这种效果，一个系统通常会有多个副本同时运行，负载被分布到这些副本之上。当负载增加时，另外的系统副本可以随时上线，这种架构技术被称为*水平扩展*。基于软件的基础设施由于其弹性愈发流行，打开了一个无限可能的巨大世界。无论是小到为了保证高可用的两个节点组成的集合，还是大到遍布全世界的互联网，都需要一种动态负载均衡解决方案基础设施。NGINX 以多种方法满足了这种需求，比如 HTTP，TCP，以及 UDP 负载均衡，本章中我们将会介绍。

当负载被均衡时，对客户端来说只有积极影响。很多现在 web 架构采用无状态的应用层，将状态存储在共享内存或者数据库中。不过，这也不是全部事实。会话状态非常有价值而且广泛存在于交互应用中。这种状态数据可能会被存储在应用服务器本地，这样做有很多理由。比如，在处理大量数据的应用程序中，当网络负载超过了承载能力时，如果会话状态时本地存储在应用服务器上，这就对用户体验至关重要，因为这样一来，该用户的后续请求将会继续被分发到同一个服务器。另外一个作用就是当会话尚未结束时服务器不应该被释放。大规模使用有状态的应用需要只能的负载均衡器。NGINX Plus 通过跟踪 cookies 或者路由提供了多种方法来解决此问题。本章节涵盖了会话持久化，因为它与 NGINX 和 NGINX Plus 的负载均衡有关。

确保 NGINX 正在服务的应用的健康状况同样重要。基于某些原因，应用失效了。可能是因为网络连通性问题、服务器失效、或者应用失效等等。代理服务器和负载均衡器必须足够聪明来探测到上游服务器的这种失效并停止将流量发送给它们。否则，客户端将需要等待，最终也只是得到一个超时。服务器发生故障时缓解服务质量下降的方法是让代理检查上游服务器的运行状况。NGINX 提供两种不同类型的健康检查：被动方式，可用于开源版；主动方式，仅在 NGINX Plus 中可用。积极的健康检查定期进行建立连接或请求上游服务器，并验证响应是否正确。被动健康检查在客户端发出请求或建立连接时会监控连接或上游服务器的响应。您可能希望使用被动健康检查来减少您的上游服务器负载，也可能希望使用主动健康状况检查以在客户端发现服务失败之前确定上游服务器故障。本章的末尾介绍了监控您正在负载均衡的上游应用程序服务器的运行健康状况。

## 2.1 HTTP 负载均衡

### 问题

你需要在两个或者多个 HTTP 服务器之间分发负载。

### 解决方案

使用 NGINX HTTP 模块实现 HTTP 服务器之间的负载均衡，使用`upstream`块：

````
upstream backend {
  server 10.10.12.45:80			weight=1;
  server app.example.com:80		weight=2;
}
server {
  location / {
    proxy_pass http://backend;
  }
}
````

此配置在两个端口`80`上的 HTTP 服务器之间均衡负载。`weight`参数指示 NGINX 传递两倍于连接数的请求给第二台服务器，同时，`weight`参数的默认值是`1`。

### 讨论

HTTP `upstream`模块控制 HTTP 的负载均衡。这个模块定义目的地的池 - 任何 Unix sockets，IP 地址以及 DNS 记录的组合。`upstream`模块也定义了所有单独的请求应该如何分配到所有上游服务器上。

每个上游目的地都由`server`指令定义在上游服务器池中。`server`指令提供了一个 Unix socket，IP 地址，或者一个 FQDN，连同一系列的可选参数。这些参数对请求路由进行更多控制。这些参数包括负载均衡算法中服务器的权重，服务器是否处于待机模式，服务器是否可用，以及如何确定服务器不可用等。NGINX Plus 提供了一系列的其他参数，诸如服务器的连接限制，高级 DNS 解析控制，以及在服务器启动后缓慢增加到它的连接的能力。

## 2.2 TCP 负载均衡

### 问题

你需要将负载分布到两台或者多台 TCP 服务器上。

### 解决方案

使用 NGINX `stream`模块在 TCP 服务器之间进行负载均衡，使用`upstream`块：

````
stream {
	upstream mysql_read {
		server read1.example.com:3306	weight=5;
		server read2.example.com:3306;
		server 10.10.12.34:3306			backup;
	}
	
	server {
		listen 3306;
		proxy_pass mysql_read;
	}
}
````

例子中的`server`块指示 NGINX 在 TCP 端口 3306 上监听，同时在两个 MySQL 数据库读副本之间进行负载均衡，同时列出了另外一个作为后备，如果主服务器不可用时流量将被转发到后备服务器。这个配置不会被加入`conf.d`文件夹，因为该文件夹包含在一个`http`块内部。相反，你应该创建另外一个文件夹，名为`stream.conf.d`，在`nginx.conf`文件中打开`stream`块，然后将这个新建的文件夹包含在其中。

### 讨论

TCP 负载均衡通过 NGINX `stream`模块定义。该`stream`模块，类似于`HTTP`模块，允许你定义上游服务器池，同时位置一个监听服务器。当配置一个服务器在指定端口上监听时，你必须定义该端口，或者可选地，定义一个主机地址和端口。在那里，必须配置一个目的地服务器，无论它是别的地址的直接反向代理或者资源的上游池。

TCP 负载均衡的上游非常类似于 HTTP 的上游，它在其中上游资源服务器，配置了 Unix socket，IP，或者全限定域名（FQDN），连同服务器权重，最大连接数，DNS 解析服务器，以及连接增加周期，还有服务器是否活动，关闭，或者处于后备模式。

NGINX Plus 提供了更多特性用于 TCP 负载均衡。这些高级特性可以在本手册中找到。本章节稍后将会介绍用于所有负载均衡的健康检测。

## 2.3 UDP 负载均衡

### 问题

你需要在两个或者多个 UDP 服务器之间分布负载。

### 解决方案

使用 NGINX `stream`模块在 UDP 服务器之间进行负载均衡，使用定义为`udp`的`upstream`块：

````
stream {
	upstream ntp {
		server ntp1.example.com:123		weight=2;
		server ntp2.example.com:123;
	}
	
	server {
		listen 123 udp;
		proxy_pass ntp;
	}
}
````

本章节在两个上游网络时间协议（NTP）服务器之间使用 UDP 协议配置负载均衡。指定UDP负载均衡就像在`listen`指令中使用`udp`参数一样简单。

如果你正在均衡负载的服务需要在客户端和服务器之间来回传输多个包，你可以指定`reuseport`参数。这种服务的例子是 OpenVPN，Voice over Internet Protocol (VoIP)，虚拟桌面解决方案，以及报文传输层安全(DTLS)。下面的例子使用 NGINX 处理 OpenVPN 连接并将它们代理到本地运行的 OpenVPN 服务上：

````
stream {
	server {
		listen 1195 udp reuseport;
		proxy_pass 127.0.0.1:1194;
	}
}
````

### 讨论

你可能会问，当我可以在 DNS A 或者 SRV 记录中拥有多个主机时，为什么还需要负载均衡器？答案是，我们不仅可以使用各种负载均衡算法来均衡负载，还可以在 DNS 服务器之间进行负载均衡。UDP 服务狗蹭了我们的互联网系统依赖的大量服务，比如 DNS，NTP，以及 VoIP。UDP 负载均衡可能对大家来说不太常用，但是实际上在世界范围内都是至关重要的。

你可以在`stream`模块中发现 UDP 负载均衡，就像 TCP 那样，同时配置也是一样的方式。两者的主要区别在于`listen`指令指定打开的 socket 是用于处理数据报的。当处理数据报时，一些其他指令可能会用到，比如`proxy_response`指令，指示 NGINX 上游服务器可以发送多少个期望中的响应。默认情况下，这个值在`proxy_timeout`达到之前是无限的。

`reuseport`参数指示 NGINX 为每个工作进程创建一个单独的监听 socket 。这就允许系统内核将连入的连接在工作进程之间分配来处理客户端和服务器之间传输的多个数据报文。`reuseport`特性只能工作在 Linux kernels 3.9 或者更高，DragonFly BSD，以及FreeBSD 12 或更高版本上。

## 2.4 负载均衡方法

### 问题

轮询负载均衡不适用于你的使用场景，因为你需要应对异质负载或者你拥有服务器资源池。

### 解决方案

使用某种 NGINX 负载均衡防范，比如最少连接，最少时间，通用散列，IP 散列，或者随机分配：

````
upstream backend {
	least_conn;
	server backend.example.com;
	server backend1.example.com;
}
````

这个例子为后端上游服务器池设定了负载均衡算法为最少连接算法。所有负载均衡算法，通用散列，随机和最小时间除外，都是独立的指令，例如前面的示例。以下讨论中解释了这些指令的参数。

### 讨论

并不是所有的请求或者数据包都携带相同的权重，基于此，轮询或者加权轮询都不适用于所有应用或者流量。NGINX 提供了多种负载均衡算法来应对各种应用场景。除了可以选择这些负载均衡算法或者方法，你还可以配置它们。下面的负载均衡方法适用于上游 HTTP，TCP 和 UDP 池。

*轮询*

​	默认负载均衡方法，按照上游服务器资源池中的服务器列表顺序将请求以此转发给各个服务器。你也可以引入权重，变成加权轮询方法，这样你就可以根据上游服务器的不同容量分配负载。权重 weight 整数值越大，轮询中该服务器优先级越高。权重背后的算法只是加权平均的统计概率。

*最少连接*

​	此方法将当前请求代理到目前打开状态的连接最少的上游服务器。最少连接，类似于轮询，同样可以引入权重考虑来确定与哪个服务器建立连接。指令名称是`least_conn`。

*最短时间*

​	仅 NGINX Plus 可用。最短时间类似于最少连接，因为它代理具有最少数量的当前连接的上游服务器，但优先选择具有最低平均响应时间的服务器。这种方法是最复杂的负载均衡算法之一，适用于高性能 web 应用。此算法相对于最少连接算法更加合理，因为最少的连接并不等价于最快的响应。必须为此指令指定`header`或者`last_byte`参数。当指定`header`时，会使用接收到响应头的时间。当指定`last_byte`时，会使用接收到全部响应的时间。此指令的名称是`least_time`。

*通用散列*

​	管理员定义以给定的文本、请求或者运行时的变量来定义一个散列。NGINX 将负载在服务器之间分发，通过为当前请求生成一个散列并基于该散列选择上游服务器。此方法在你需要对请求应该发送给谁或者为了确定哪台上游服务器最可能将拥有数据缓存进行更多控制的情况下非常有用。注意，当一个服务器被添加进资源池或者从资源池中删除时，被散列的请求将被重新分发。此算法拥有一个可选参数，`consistent`，用来最小化重新分发的影响。该指令名为`hash`。

*随机*

​	此方法用来指示 NGINX 从服务器组中随机选择一个，同时可以考虑引入服务器权重。可选的`tow [method]`参数指示 NGINX 随机选择两个服务器并使用给定的负载均衡方法在两者之间分配负载。默认会使用`least_conn`方法，如果`two`参数传递没有另外携带方法名。随机负载均衡的指令名是`random`。

*IP 散列*

​	此方法仅用于 HTTP 。IP 散列使用客户端 IP 地址来散列。略微不同于使用远程变量的通用散列，此算法使用 IPv4 地址的前三个元组或者完整的 IPv6 地址。此方法确保同一个客户端始终被代理至同一个上游服务器，只要该服务器是可用的，当会话状态数据非常关键而又没有由应用的共享存储处理时，这一点极端重要。此方法在分布散列时还考虑了`weight`参数。指令名称为`ip_hash`。

## 2.5 粘性 Cookie

### 问题

你需要使用 NGINX Plus 将一个下游客户端绑定到一个上游服务器。

### 解决方案

使用`sticky cookie`指令来指示 NGINX Plus 创建和跟踪一个 cookie：

````
upstream backend {
	server backend1.example.com;
	server backend2.example.com;
	stick cookie
		affinity
		expires=1h
		domain=.example.com
		httponly
		secure
		path=/;
}
````

此配置创建并追踪 cookie 以将一个下游客户端绑定到一个上游服务器。在这个例子中，cookie 名为`affinity`，作用域被设置为`.example.com`，超时时间是 1 小时，不能被客户端消费，只能使用 HTTPS 发送，对所有请求资源路径都可用。

### 讨论

在`sticky`指令上使用`cookie`参数会在首次请求时创建一个 cookie，它包含有关上游服务器的信息。NGINX Plus 追踪此 cookie，确保后续的请求也会被发送到同一个上游服务器。`cookie`参数的第一个位置参数是要创建和跟踪的 cookie 的名称。其他参数提供额外的控制，通知浏览器适当的使用，例如到期时间，域，路径，以及 cookie 是否可以在客户端使用，或者是否可以通过不安全的协议传递。

## 2.6 粘性学习

### 问题

你需要通过使用已有的 cookie 和 NGINX Plus 将一个下游客户端绑定到一个上游服务器。

### 解决方案

使用`sticky learn`指令来发现并跟踪由上游应用创建额 cookies：

````
upstream backend {
	server backend1.example.com:8080;
	server backend2.example.com:8081;
	
	sticky learn
			create=$upstream_cookie_cookiename
			lookup=$cookie_cookiename
			zone=client_session:2m;
}
````

这个例子指示 NGINX 通过在响应头中寻找名为`COOKIENAME`的 cookie 寻找并追踪会话，同时通过在请求头中寻找相同 cookie 以探查现有的会话。会话`affinity`被存储在一个共享存储区域，该区域大小为 2 MB，大约可以跟踪 16000 个会话。cookie 的名称将始终都是特定于应用的。通用的 cookie 名称，比如`jsessionid`或者`phpsessionid`，通常会默认设置在应用或者应用服务器配置中。

### 讨论

当应用创建它们自己的会话状态 cookies 时，NGINX Plus 在请求响应中发现并追踪它们。当`sticky`指令被提供`learn`参数时，这种类型的 cookie 跟踪被执行。用于 cookies 跟踪的共享存储随着`zone`参数指定，包括名称和大小。NGINX Plus 被指示在来自上游服务器的响应中寻找 cookies，通过指定`create`参数，同时搜索事先注册的服务器`affinity`使用`lookup`参数。这些参数的值就是由 HTTP 模块暴露出来的变量。

## 2.7 粘性路由

### 问题

你需要对持久的会话被 NGINX Plus 路由到上游服务器的过程进行细粒度控制。

### 解决方案

使用携带`route`参数的`sticky`指令以使用有关请求路由的变量：

````
map $cookie_jsessionid $route_cookie {
	~.+\.(?P<route>\w+)$ $route;
}

map $request_uri $route_uri {
	~jsessionid=.+\.(?P<route>\w+)$ $route;
}

upstream backend {
	server backend1.example.com route=a;
	server backend2.example.com route=b;
	
	sticky route $route_cookie $route_uri;
}
````

此示例尝试提取Java会话ID，方法是首先从cookie中通过将Java会话ID cookie的值映射到具有第一个`map`块的变量，然后通过在请求URI中查看名为`jsessionid`的参数来将值映射到使用第二个`map`块的变量。带有`route`参数的`sticky`指令被传入任意数量的变量。第一个非零或非空值用于路由。如果使用`jsessionid` cookie，请求将被路由到`backend1`；如果使用URI参数，请求将路由到`backend2`。虽然此示例基于Java通用会话ID，但同样适用于其他会话技术（如`phpsessionid`）或应用程序为会话ID生成的任何保证唯一的标识符。

### 讨论

有时候，你可以会想要将流量直接转发到特定的服务器来实现一点更细粒度的控制。`sticky`指令的`route`参数就是为了实现此目的。粘性路由给与你更好的控制，实际的追踪以及粘性，不同于通用散列负载均衡算法。客户端首先会被基于路由指定被路由到上游服务器，然后后续的请求将在 cookie 或者 URI 中携带路由信息。粘性路由需要评估一系列的位置参数。第一个非空变量被用来路由到一个服务器。map 块可以被用于选择转换变量并将它们保存为其它用于路由的变量。基本上，`sticky route`指令在 NGINX Plus 的共享存储区中创建一个会话来追踪你指定到上游服务器的任何客户端会话 ID，然后将携带此会话 ID 的后续请求分发到同一个上游服务器，如它的最初那个请求一样。

## 2.8 连接排空

### 问题

你需要优雅地将服务器移除为了维护或者其它原因，同时还要保证通过 NGINX Plus 不间断提供服务。

### 解决方案

通过 NGINX Plus API 使用`drain`参数，如第五章中描述的那样，指示 NGINX 停止发送尚未被追踪的新的连接：

````
$ curl -X POST -d '{"drain":true}' \
	'http://nginx.local/api/3/http/upstreams/backend/servers/0'

{
  "id":0,
  "server":"172.17.0.3:80",
  "weight":1,
  "max_conns":0,
  "max_fails":1,
  "fail_timeout":"10s",
  "slow_start":"0s",
  "route":"",
  "backup":false,
  "down":false,
  "drain":true
}
````

### 讨论

当会话状态被本地存储到服务器上时，在被从资源池中移除之前，连接和持久会话必须被排空。排空连接就这样一个过程：在从上游服务器池中移除该服务器之前，让有关该服务器的会话原地超时。你可以在`server`指令中添加`drain`参数来为特定的服务器配置连接排空。当`drain`参数被设置之后，NGINX Plus 停止发送新的会话给该服务器，但是允许当前会话继续被服务完成。你也可以通过将`drain`参数添加到上游服务器指令来切换此配置。

## 2.9 被动健康检测

### 问题

你需要被动地检查上游服务器的健康状况。

### 解决方案

使用 NGINX 健康检测以及负载均衡来保证只有健康的上游服务器被使用：

````
upstream backend {
  server backend1.example.com:1234 max_fails=3 fail_timeout=3s;
  server backend2.example.com:1234 max_fails=3 fail_timeout=3s;
}
````

此配置被动地监控上游服务器监控状况，设定`max_fails`指令为 3，`fail_timeout`为 3 秒。这些指令参数对 stream 和 HTTP 服务器的效果是一样的。

### 讨论

被动健康检测在 NGINX 的开源版本中是可用的。被动监控器观测当客户端请求通过 NGINX 时的连接的失败或者超时。被动健康监测默认开启，这里提到的参数允许你改变它们的行为。对所有类型的负载均衡来说，健康状况健康都是重要的，不仅仅是站在用户体验角度来看，也关系到业务连续性。NGINX 被动监控上游 HTTP，TCP以及UDP服务器来确保它们正在运行并且是健康的。

## 2.10 主动健康检测

### 问题

你需要通过 NGINX Plus 主动检测上游服务器的健康状况。

### 解决方案

对 HTTP 服务器，在`location`块中使用`health_check`指令：

````
http {
  server {
    ...
    location / {
      proxy_pass http://backend;
      health_check interval=2s
      	fails=2
      	passes=5
      	uri=/
      	match=welcom;
    }
  }
  # status is 200, content type is "text/html",
  # and body contains "Welcome to nginx!"
  match welcome {
    status 200;
    header Content-Type = text/html;
    body ~ "Welcome to nginx!";
  }
}
````

对 HTTP 服务器进行健康检测的配置通过每隔两秒向 URI '/' 发送一个 HTTP 请求来检测上游服务器的健康状况。上游服务器必须连续通过 5 次健康监测才会被认为是健康的。如果连续两次健康检测失败则服务器就会被认为不健康。来自上游服务器的响应必须匹配配置中已经定义好的匹配块。该匹配块定义了状态码为`200`，响应头`Content-Type`值是`text/html`，响应体中内容是`Welcome to nginx!`。HTTP `match`块包含三个指令：`status`，`header`，以及`body`。这三个指令都有比较标识。

TCP/UDP服务的 stream 健康检测非常类似：

````
stream {
  ...
  server {
    listen 1234;
    proxy_pass stream_backend;
    health_check interval=10s
    	passes=2
    	fails=3;
    health_check_timeout 5s;
  }
  ...
}
````

这个例子中，TCP 服务器被配置为在端口`1234`上监听，同时代理到一个上游服务器集合，并主动检测其健康状况。stream `health_check`指令携带与 HTTP 健康检测指令相同的参数，除了`uri`，同时 stream 版本拥有一个参数用来将检测协议切换为`udp`。在这个例子中，检测时间间隔被设定为 10 秒，连续两次检测通过就会被认为是健康的，连续三次失败则会被认为不健康的。主动 stream 健康检测也可以被用来验证上游服务器的响应。`match`块只包含两个指令：`send`和`expect`。`send`指令是将要发送的原始数据，`expect`是一个精确的响应或者用于匹配的正则表达式。

### 讨论

NGINX Plus 中的主动健康检测不断发送请求到源服务器来检测它们的健康状况。这些健康检测能够评估的不仅仅只有响应状态码。在 NGINX Plus 中，主动 HTTP 健康监测监控基于上游服务器的响应的一系列可接受约束条件。你可以配置主动健康监测监控上游服务器检测的频率，通过多少次检测会被认为是健康的，检测失败多少次会被认为是不健康的，记忆期望的结果应该是什么。`match`参数指向一个匹配块，该匹配块定义了响应的可接受约束条件。匹配块还定义了发送给上游服务器的数据，当用在 TCP/UDP 服务器的 stream 上下文中时。这些特性使得 NGINX 可以确保上游服务器始终是健康的。

## 2.11 慢开始

### 问题

你的应用需要在承载全部的生产负载之前逐步提升。

### 解决方案

在`server`指令中使用`slow_start`参数来在指定时间内逐步增加特定数量的连接，逐步将新的服务器加入上游服务器负载均衡池中。

````
upstream {
  zone backend 64k;
  
  server server1.example.com slow_start=20s;
  server server2.example.com slow_start=15s;
}
````

`server`指令配置将缓慢提升流量到刚刚重新被加入服务器资源池中的上游服务器。`server1`将每隔 20 秒提升连接数，`server2`每隔 15 秒增加连接数。

### 讨论

*slow start*是一个概念，表示每隔一段时间逐步缓慢增加被代理到一个服务器上的请求数量。慢开始允许应用通过使用缓存进行预热，初始化数据库连接以避免在启动瞬间超负荷。这种特性在服务器健康检测从失败到恢复健康时起作用，或者在服务器重新进入负载均衡池中时刻生效。

## 2.12 TCP 健康检测

### 问题

你需要检测你的上游 TCP 服务器，使用健康状态的服务器，并将不健康的服务器从服务器资源池中移除。

### 解决方案

在`server`块中使用`health_check`指令以进行主动健康监测：

````
stream {
  server {
    listen			3306;
    proxy_pass		read_backend;
    health_check	interval=10 passes=2 fails=3;
  }
}
````

这个例子主动监测上游服务器。如果上游服务器不能响应三次或者更多由 NGINX 初始化的 TCP 连接就会被认为不健康。NGINX 每隔 10 秒执行这种检测。只有当服务器通过两次健康检测之后才会被认为是健康的。

### 讨论

TCP 健康状态可以被 NGINX Plus 通过主动或者被动检测验证。被动健康监控不需要任何客户端和上游服务器之间的额外通信。如果上游服务器超时或者拒绝连接，被动健康检测将认为该服务器不健康。主动健康检测将初始化它们自己的可配置检测来确定健康状况。捉到那个健康检测不仅检测与上游服务器的连接，同时还期望得到给定的响应。

# 3 流量控制

## 3.0 介绍

NGINX 和 NGINX Plus 都可以归类为 web 流量控制器范畴。你可以使用 NGINX 基于许多属性进行智能流量路由和流量控制。本章介绍 NGINX 基于百分比分割客户端请求，利用客户端的地理位置以及以速率，连接和带宽限制的形式控制流量的能力。在阅读本章时，请记住，您可以混合使用这些功能以实现无数可能性。

## 3.1 A/B 测试

### 问题

你需要在两个或者多个版本的文件或者应用之间分配客户端以测试接受性。

### 解决方案

使用`split_clients`模块来给出一个百分比，你的客户端请求将按照这个百分比在不同的上游服务器池中的服务器之间分配：

````
split_clients "${remote_addr}AAA" $variant {
  20.0%		"backendv2";
  *			"backendv1";
}
````

`split_clients`指令散列你提供来作为第一个参数的字符串，并且将该散列结果乘以你给出的那个百分比，将其映射到你提供来作为第二个参数的变量。第三个参数时一个对象，包含一个键值对，其中键是百分比权重，值是应该分配到其上的值。键可以实百分比或者一个星号。星号表示除了明确的百分比之外剩余的全部流量。上面例子中，对于20％的客户端IP地址，`$variant`变量的值为`backendv2`，对于剩余的80％，变量值为`backendv1`。

上面例子中，`backendv1`和`backendv2`表示上游服务器资源池，因而也可以被用在`proxy_pass`指令中：

````
location / {
  proxy_pass http://$variant
}
````

使用变量`$variant`，我们的流量将在两个不同的应用服务器池之间分配。

### 讨论

此类 A/B 测试在商业网站用来测试不同类型的市场和前端特性的转化率的场景下非常有用。应用程序普遍使用一种名为“金丝雀发布”的部署策略。在这种部署策略中，流量被缓慢切换到新版本应用服务。在不同服务版本之间分配你的客户端请求当你退出新版本代码时很有用，可以在发生错误时明确限制影响范围。无论基于何种考虑在不同应用集合之间分配流量，NGINX 都可以通过`split_client`模块很简单地实现。

### 参考

[split_client Documentation](http://nginx.org/en/docs/http/ngx_http_split_clients_module.html)

## 3.2 使用 GeoIP 模块和数据库

### 问题

你需要安装 GeoIP 数据库并开启 NGINX 的内置变量来记录日志并将你的客户端的位置告诉你的应用。

### 解决方案

NGINX 官方开源代码包仓库，第一章中安装 NGINX 时配置的那个，提供了一个名为`nginx-module-geoip`的包。当使用 NGINX Plus 包仓库时，该包名为`nginx-plus-module-geoip`。这些包安装 GeoIP 模块的动态版本。

RHEL/CentOS NGINX 开源代码：

````
# yum install nginx-module-geoup
````

Debian/Ubuntu NGINX 开源代码：

````
# apt-get install nginx-module-geoip
````

RHEL/CentOS NGINX Plus：

````
# yum install nginx-plus-module-geoip
````

Debian/Ubuntu NGINX Plus：

````
# apt-get install nginx-plus-module-geoip
````

下载 GeoIP 国家城市数据库并解压：

````bash
# mkdir /etc/nginx/geoip
# cd /etc/nginx/geoip
# wget "http://geolite.maxmind.com/\download/geoip/database/GeoLiteCountry/GeoIP.dat.gz"
# gunzip GeoIP.dat.gz
# wget "http://geolite.maxmind.com/\download/geoip/database/GeoLiteCity.dat.gz"
# gunzip GeoLiteCity.dat.gz
````

这一系列命令在 */etc/nginx* 目录下创建一个 *geoip* 目录，移动到这个新的目录，下载并解压包。

本地磁盘上建立了国家城市 GeoIP 数据库，现在你就可以构建 NGINX GeoIP 模块来使用它们基于客户端 IP 地址来暴露内置变量：

````
load_module "/usr/lib64/nginx/modules/ngx_http_geoip_module.so";

http {
  geoip_country /etc/nginx/geoip/GeoIP.dat;
  geoip_city /etc/nginx/geoip/GeoLiteCity.dat;
}
````

`load_module`指令从它的文件系统路径下动态加载模块。`load_module`指令只在主上下文中有效。`geoip_country`指令使用文件`GeoIP.dat`文件的路径，该文件包含 IP 地址和国家编码之间映射的数据库，仅在 HTTP 上下文中可用。

### 讨论

`geoip_country`和`geoip_city`指令暴露本模块中内置的一系列可用变量。`geoip_country`指令启用的变量允许你区分你的客户端的国家和地区。这些变量包括`$geoip_country_code`，`$geoip_country_code3`，以及`$geoip_country_name`。国家编码变量返回两个字母组成的国家编码。第二个变量返回三个字母组成的国家编码。国家名称变量返回完整的国家名称。

`geoip_city`指令启用了很多变量。`geoip_city`指令启用与`geoip_country`指令相同的所有变量，只使用不同的名称，例如`$geoip_city_country_code`，`$geoip_city_country_code3`和`$geoip_city_country_name`。其他变量包括`$geoip_city`，`$geoip_city_continent_code`，`$geoip_latitude`，`$geoip_longitude`和`$geoip_postal_code`，所有这些都描述了它们返回的值。`$geoip_region`和`$geoip_region_name`描述区域，地区，州，省，联邦属地等。区域是双字母代码，其中`region name`是全名。`$geoip_area_code`（仅在美国有效）返回三位数的电话区号。

利用这些变量，你可以记录有关你的客户端的信息。你可以有选择地将这些信息作为请求头或者变量传递给你的服务端应用，或者使用 NGINX 以特殊方法来路由你的流量。

### 参考

[GeoIP Update](https://github.com/maxmind/geoipupdate)

## 3.3 基于国家限制访问

### 问题

你需要限制来自特定国家的访问来满足商业合同或者应用需求。

### 解决方案

将你希望阻止或者放行的国家编码映射到一个变量：

````
load_module
	"/usr/lib64/nginx/modules/ngx_http_geoip_module.so";
	
http {
  map $geoip_country_code $country_access {
    "US"	0;
    "RU"	0;
    default	1;
  }
  ...
}
````

这个映射将设置一个新的变量`$country_access`为`1`或者`0`。如果客户端 IP 地址来自 US 或者 Russia，该变量将被设置为`0`。对所有其它国家，该变量将被设置为`1`。

现在，在你的`server`块中，我们将使用`if`语句来拒绝所有不是来自 US 或者 Russia 的访问：

````
server {
  if($country_access = '1'){
    retrurn 403;
  }
  ...
}
````

如果`$country_access`变量被设置为`1`则这个`if`语句将得到`True`。此时，服务器将返回 403 unauthorized 响应。否者，服务器正常操作来响应请求。因此，这个`if`块的作用就是阻止所有不是来自 US 或者 Russia 的人的访问。

### 讨论

这是一个简短的例子，展示了如何只允许来自两个国家的访问。这个例子可以被扩展到适应你的实际生产需求。你可以使用相同的方法来基于任何由 GeoIP 模块启用的其它内置变量允许或者阻止特定的访问。

## 3.4 寻找初始客户端

### 问题

因为 NGINX 前面存在其它代理，你需要寻找初始客户端 IP 地址

### 解决方案

使用`geoip_proxy`指令定义你的代理 IP 地址范围，使用`geoip_proxy_recursive`指令寻找初始 IP：

````
load_module "/usr/lib64/nginx/modules/ngx_http_geoip_module.so";

http {
  geoip_country /etc/nginx/geoip/GeoIP.dat;
  geoip_city /etc/nginx/geoip/GeoLiteCity.dat;
  geoip_proxy 10.0.16.0/26;
  geoip_proxy_recursive on;
  ...
}
````

`geoip_proxy`指令定义了一个 CIDR(ClasslessInter-DomainRouting 无类别域间路由) 范围，我们的代理服务器运行其中，同时指示 NGINX 使用`X-Forwarded-For`头部来发现客户端 IP 地址。`geoip_proxy_recursive`指令指示 NGINX 递归遍历`X-Forwarded-For`头部来寻找已知的最后客户端 IP 。

### 讨论

如果你在 NGINX 前面使用其它的代理，你将发现 NGINX 会提取该代理的 IP 地址而不是客户端的。你可以使用`geoip_proxy`指令指示 NGINX 使用`X-Forwarded-For`头部，当来自给定 IP 范围的连接被打开。`geoip_proxy`指令使用一个地址或者一个 CIDR 范围。当 NGINX 前面存在多个代理来转发流量时，你可以使用`geoip_proxy_recursive`指令在`X-Forwarded-For`中递归查找地址来寻找初始客户端地址。你可能会想要在 NGINX 前面使用某些有用的负载均衡机制，比如 AWS ELB，Google 负载均衡器，或者 Azure 负载均衡器等。

## 3.5 限制连接

### 问题

你需要基于预定义的键限制连接数量，比如客户端 IP 地址。

### 解决方案

创建一个共享存储区域来保存连接度量，同时使用`limit_conn`指令来限制打开连接：

````
http {
  limit_conn_zone $binary_remote_addr zone=limitbyaddr:10m;
  limit_conn_status 429;
  ...
  server {
    ...
    	limit_conn limitbyaddr 40;
    ...
  }
}
````

此配置创建了一个名为`limit_byaddr`的共享存储区。使用的预定义的键是客户端 IP 地址的二进制形式。该共享存储区的大小被设置为10MB。`limit_conn`指令携带两个参数：`limit_conn_zone`名称和允许的连接数量。`limit_conn_status`设定当连接被限制时返回的响应状态码是 429，表示请求太多。`limit_conn`和`limit_conn_status`指令在 HTTP 、服务器以及位置上下文中可用，

### 讨论

基于键限制连接的数量能够被用于防御服务资源被滥用，以及保证为所有客户端公平的服务。需要注意的是，预定义的键意义重大。如我们在上面例子中那样，使用 IP 地址，可能会有风险，如果很多用户处在同一个子网中，共享同一个边界网关 IP 地址，比如当他们处于一个网络地址转换（NAT）后面时。这种情况下整个客户端组都会被限制。`limit_conn_zone`指令只在 HTTP 上下文中有效。你可以在 HTTP 上下文中使用任意数量的对 NGINX 可用的变量以便创建限制规则。使用能够在应用层面标识用户的的变量，比如会话 cookie，对于某些使用场景可能时更好的解决方案。`limit_conn_status`默认为`503`，服务不可用。你可能会更倾向于使用`429`，因为服务实际上是可用的，同时`500-level`响应标识服务端错误，而`400-level`响应表示客户端错误。

## 3.6 限制速率

### 问题

你需要限制请求速率，通过预定义的键，比如客户端 IP 地址。

### 解决方案

使用速率限制模块来限制请求比率：

````
http {
  limit_req_zone $binary_remote_addr
  	zone=limitbyaddr:10m rate=1r/s;
  limit_req_status 429;
  ...
  server {
    ...
    	limit_req zone=limitbyaddr burst=10 nodelay;
    ...
  }
}
````

此例子配置创建了一个名为`limitbyaddr`的共享存储区域。使用的预定义的键是客户端的 IP 地址的二进制形式。该共享存储区的大小设定为 10 MB。该区域使用关键字参数设定速率。`limit_req`指令携带两个可选的关键词参数：`zone`和`burst`。`zone`用来指示指令使用哪个共享存储区域来限制请求。当一个给定区域的请求速率达到阈值时，请求就会被延迟，直到达到它们的最大崩溃阈值，该阈值由`burst`关键字参数确定。`burst`关键字参数默认是`0`。`limit_req`同时携带了第三个可选参数，`nodelay`。这个参数允许客户端在被限制之前无延迟地使用它的`burst`。`limit_req_status`设定返回给客户端的状态为一个特定的 HTTP 状态码，默认是`503`。`limit_req_status`和`limit_req`在 HTTP、服务器以及位置上下文中都可用。`limit_req_zone`仅在 HTTP 上下文中可用。NGINX Plus v R16 中的速率限制是集群敏感的。

### 讨论

速率限制模块非常强大，可以在保证对所有人的服务质量的同时防御大量请求。限制请求速率有很多原因，其中之一就是安全。你可以通过对你的登录页面施加非常严格的限制来防御蛮力攻击。你可以对所有请求施加何时的限制，以粉碎某些恶意用户对你的应用进行拒绝服务攻击或者浪费资源的图谋。速率限制模块的配置类似于前面一节中介绍的连接限制模块配置，因为两个概念本身就很类似。你可以指定请求速率将请求限制为每秒钟多少个请求或者每分钟多少个请求。当达到速率限制时，此事件就会被记录进入日志。这里还存在一个例子中没有出现的指令`limit_req_log_level`，默认为`error`，不过可以被设置为`info`，`notice`或者`warn`。NGINX Plus v R16 中的速率限制是集群敏感的。

## 3.7 带宽限制

### 问题

你需要限制每个客户端下载资源的带宽。

### 解决方案

使用 NGINX 的 `limit_rate`和`limit_rate_after`指令来限制发送给客户端的响应的速率。

````
location /download/ {
	limit_rate_after 10m;
	limit_rate 1m;
}
````

此`location`块配置指定了对于前缀为`download` 的 URI，发送给客户端的响应的数量将在 10MB 之后开始被限制为每秒 1MB 的速率。带宽限制是对每个连接而言，所以你可能会希望在连接限制基础上再为每个连接使用带宽限制。

### 讨论

限制特定连接的带宽使 NGINX 能够以您指定的方式在所有客户端之间共享其上载带宽。这两个指令可以完成所有操作：`limit_rate_after`和`limit_rate`。`limit_rate_after`指令几乎可以在任何上下文中设置：HTTP，服务器，`location`，以及当`if`位于某个 `location`中时。`limit_rate`指令适用于与`limit_rate_after`相同的上下文。但是，也可以通过设置名为`$limit_rate`的变量来设置它。`limit_rate_after`指令指定在传输指定数量的数据之前，不应对连接进行速率限制。`limit_rate`指令默认指定给定上下文的速率限制，以每秒字节数为单位。但是，您可以指定`m`表示兆字节或`g`表示千兆字节。两个指令默认值为`0`。值`0`表示根本不限制下载速率。此模块允许您以编程方式更改客户端的速率限制。

# 4 大规模可扩展内容缓存

## 4.0 介绍

通过存储在将来会被用于提供服务的请求的响应，缓存可以加速内容服务。内容缓存减少上游服务器的负载，缓存完整的响应而不是为相同的请求执行计算和查询。缓存提升性能并降低负载，意味着你可以用更少的资源提供更快的服务。位于战略位置的可扩展的分布式缓存服务器对用户的体验产生巨大影响。让主机内容尽可能靠近消费者以或者最佳性能是一种优化。你也可以尽可能靠近你的用户缓存你的内容。这就是内容分发网络模式，CDNs。使用 NGINX 你可以在任何运行 NGINX 服务器的地方缓存你的服务内容，有效保证你创建自己的 CDN。使用 NGINX 缓存，你也可以被动缓存内容并在上游服务器失效时刻使用缓存的响应提供服务。

## 4.1 缓存区域

### 问题

你需要缓存内容，同时需要定义缓存应该存储在什么地方。

### 解决方案

使用`proxy_cache_path`指令定义共享存储缓存区域以及缓存内容的位置：

````
proxy_cache_path /var/nginx/cache
				keys_zone=CACHE:60m
				levels=1:2
				inactive=3h
				max_size=20g;
proxy_cache CACHE;
````

此缓存定义例子在文件系统中创建了 `/var/nginx/cache/cache`目录用来缓存响应。同时创建了一个共享存储空间，名为`CACHE`，具有 60MB 存储空间。这个例子设定目录结构层次，定义了当缓存的响应经过 3 小时仍然没有被再次请求时就会被释放。同时定义了缓存的最大尺寸是 20GB。`proxy_cache`指令声明一个特定的上下文来使用该缓存区域。`proxy_cache_path`在 HTTP 上下文中有效，`proxy_cache`指令在 HTTP ，服务器，以及`location`上下文中都有效。

### 讨论

为了在 NGINX 中配置缓存，声明一个路径和区域来使用是必需的。NGINX 中的缓存区域使用`proxy_cache_path`指令创建。`proxy_cache_path`指令分配一个位置用来存储缓存的信息，以及一个共享存储空间来存储活动的键和响应元数据。此指令的可选参数对缓存的维护和访问提供了更多的控制。`levels`参数定义如何创建文件结构。该参数的值是一个分号分隔的值，声明了子目录名称的长度，同时最大层级为 3 层。NGINX 缓存基于缓存键，该键是一个缓存的值。然后 NGINX 会将结果存储在提供的文件结构中，使用缓存键作为文件路径，同时基于`levels`值拆分目录。`inactive`参数允许控制缓存元素在它最近一次被使用后能够存在于缓存中的时间长度。缓存的大小也使用`max_size`参数配置。其他参数与缓存加载过程有关，缓存加载过程是将缓存在磁盘文件中的缓存键加载到共享存储区域中的过程。

## 4.2 缓存散列键

### 问题

你需要控制你的内容的缓存和查找方式。

### 解决方案

使用`proxy_cache_key`指令和相关变量来定义缓存是否命中的标准：

````
proxy_cache_key "$host$request_uri $cookie_user";
````

缓存散列键将指示 NGINX 基于被请求的主机和 URI 缓存页面，同时 cookie 定义了用户。基于此你就可以缓存动态页面而不包含为不同用户生成的服务内容。

### 讨论

默认`proxy_cache_key`，适用于大多数应用场景，是`"$scheme$proxy_host$request_uri"`。使用的变量包括模式、HTTP 或者 HTTPS，`proxy_host`，请求被发送到的目的地，以及请求 URI。所有这些都会影响 NGINX 将请求代理到的目标 URL。你会发现存在许多其他因素会为每个应用定义一个唯一的请求，比如请求参数，请求头，会话标识符，等等，你可能会希望使用它们创建你自己的散列键。

选择一个好的散列键是非常重要的，所以需要基于对应用的透彻理解。为静态内容选择缓存键通常很直接，使用主机名和 URI 就足够了。为类似于应用仪表盘的页面的动态内容选择缓存键就需要更多有关用户与应用的交互方式以及用户体验的差异程度等方面的了解。处于安全考量，在没有充分理解上下文的情况下，你可能不希望将一个用户的缓存数据暴露给其他用户。`proxy_cache_key`指令配置将被散列到缓存键的字符串。`proxy_cache_key`可在 HTTP，服务器，以及`location`块中被设定，提供请求缓存方式的灵活控制。

## 4.3 缓存旁路

### 问题

你需要绕过缓存的能力。

### 解决方案

使用`proxy_cache_bypass`指令的一个非空或者非零的值。一种做法是在`location`块中设定一个你不想缓存的变量等于`1`：

````
proxy_cache_bypass $ http_cache_bypass;
````

此配置指示 NGINX 在名为`cache_bypass`的 HTTP 请求头被设置为非`0`的任何值时绕过缓存。

### 讨论

很多场景下不允许请求被缓存。为此，NGINX  暴露了`proxy_cache_bypass`指令，当该指令值为非空或者非零时，请求将被发送给上游服务器而不会从缓存拉取结果。不同的需求和场景下的缓存旁路将由你的应用使用情况决定。缓存旁路技术可以和使用请求或响应头一样简单，也能像多个`map`块协同工作那样复杂。

基于多种原因，你可能会希望绕过缓存。一个重要原因就是排查问题和调试。如果你反复拉取缓存的页面或者你的缓存键是特定于用户标识符的，则复现问题会非常困难。拥有绕过缓存的能力就尤其重要。选项包括但不限于在设置特定cookie，请求头或请求参数时绕过缓存。您还可以通过设置`proxy_cache off`来完全关闭给定上下文（例如`location`块）的缓存。

## 4.4 缓存性能

### 问题

你需要通过在客户端的缓存提成性能。

### 解决方案

使用客户端缓存控制头部：

````
location ~* \.(css|js)$ {
 expires 1y;
 add_header Cache-Control "public";
}
````

这个`location`块指定客户端可以缓存 CSS 和 JavaScript 内容。其中的`expires`指令指示客户端它们缓存的资源将在一年之后过期失效。`add_header`指令添加 HTTP 响应头`Cache-Control`到响应中，值为`public`，以允许所有的缓存服务器以这种方式缓存资源。如果你指定该值为`private`，则只允许客户端缓存资源值。

### 讨论

很多因素可以影响缓存性能，磁盘速度是重要因素。NGINX 配置中的很多内容可以帮助你调整缓存性能。一种选择是以这样一种方式设置响应的头部：即客户端实际缓存响应并且根本不向NGINX发出请求，而只是从其自己的缓存中提供请求的资源。

## 4.5 缓存清理

### 问题

你需要从缓存中清除一个对象。

### 解决方案

使用 NGINX Plus 的清理特性，`proxy_cache_purge`指令，以及一个非空或者`0`值得变量：

````
map $request_method $purge_method {
	PURGE 1;
	default 0;
}
server {
	...
	location / {
		proxy_cache_purge $purge_method;
	}
}
````

这个例子中，特定对象的缓存将被清理，如果它被方法`PURGE`请求访问。下面是一个`curl`命令的例子，它可以清理名为`main.js`的缓存文件：

````
$ curl -XPURGE localhost/main.js
````

### 讨论

处理静态文件的常用方法是将文件的哈希值放在文件名中。这可确保在您推出新代码和内容时，您的CDN会将其识别为新文件，因为URI已更改。但是，这并不适用于您设置了不适合此模型的缓存键的动态内容。在每个缓存方案中，您都必须有一种清除缓存的方法。NGINX Plus提供了一种清除缓存响应的简单方法。`proxy_cache_purge`指令在传递非零或非空值时将清除与请求匹配的缓存项。设置清除的一种简单方法是通过映射`PURGE`的请求方法。但是，您可能希望将其与`geo_ip`模块或简单身份认证结合使用，以确保没有人可以清除您珍贵的缓存项目。NGINX还允许使用`*`，它将清除与公共 URI 前缀匹配的缓存项。要使用通配符，您需要使用`purger=on`参数配置`proxy_cache_path`指令。

## 4.6 缓存切片

### 问题

你需要通过将文件分段来提升缓存效率。

### 解决方案

使用 NGINX `slice`指令以及它的内置参数来将缓存结果切分成片段：

````
proxy_cache_path /tmp/mycache keys_zone=mycache:10m;
server {
	...
	proxy_cache mycache;
	slice 1m;
	proxy_cache_key $host$uri$is_args$args$slice_range;
	proxy_set_header Range $slice_range;
	proxy_http_version 1.1;
	proxy_cache_valid 200 206 1h;
	
	location / {
		proxy_path http://origin:80;
	}
}
````

### 讨论

此配置定义了一个缓存区域并对服务器可用。`slice`指令然后被用来指示 NGINX 将响应切分为 1MB 的文件片段。缓存文件根据`proxy_cache_key`指令存储。注意名为`slice_range`的内置变量的使用。当向初始服务器发出请求时，相同的变量被用作请求头，同时请求的 HTTP 版本升级为 HTTP/1.1，因为 HTTP/1.0 不支持字节范围请求。为一个小时内的缓存验证设置响应状态码为`200`或者`206`，然后定义`location`和初始服务器。

缓存切片模块我 HTML5 视频分发而开发，该场景使用了字节范围请求向浏览器传输伪流内容。默认地，NGINX 能够从它的缓存提供字节范围请求服务。如果一个请求的字节范围包含尚未缓存的内容，NGINX 将向初始服务器请求完整的文件。当你使用缓存切片模块时，NGINX 将会仅仅向初始服务器请求必需的文件片段。范围超过单个分片的范围请求，包括整个文件的请求，将会触发对每个需要片段的子请求，然后所有的片段都会被缓存起来。当所有的片段都被缓存之后，就会组装响应并发送到客户端，这就使得 NGINX 缓存和服务范围请求内容更加高效。缓存切片模块只应该用在不会改变的大文件的情况。NGINX 每次接收到来自初始服务器的片段后都会验证 ETag 。如果初始服务器上的 ETag 发生了变化，NGINX 就会取消该事务，因为缓存已经不可用了。如果内容没有变化同时文件更小，或者初始服务器能够处理缓存填充过程中的负载尖峰，那么更好的办法是使用下面参考资料中提到的文章中描述的缓存锁定模块。

### 参考

[Smart and Efficient Byte-Range Caching with NGINX & NGINX Plus](http://bit.ly/2DxGo1M)

# 5 可编程性和自动化

## 5.0 介绍

可编程性指的是可以通过编程方式与其它系统交互的能力。NGINX Plus 的 API 提供了如下特性：通过 HTTP 接口与 NGINX Plus 的配置和行为交互的能力。此 API 提供了通过 HTTP 请求添加或者移除上游服务器来重新配置 NGINX Plus 的能力。NGINX Plus 中的键值存储功能支持另一层面的动态配置 - 您可以利用 HTTP 调用注入 NGINX Plus 可用于动态路由或控制流量的信息。本章将介绍通过同一 API 公开的 NGINX Plus API 和键值存储模块。

配置管理工具自动化服务器的按照和配置过程，这在云计算时代是无价之宝。大规模 web 应用的工程师不再需要手动配置服务器，现在他们可以选用任何一种可用的配置管理工具。使用这些工具，工程师可以以一种可重复、可测试而且模块化的风格编写配置和代码，一次产生许多相同配置的服务器。本章节涵盖几种可用的配置管理工具，介绍如何使用它们安装 NGINX 并提供一个基本配置文件模板。这些例子非常基本但是仍然可以展示如何在每个平台上启动 NGINX 服务器。

## 5.1 NGINX Plus API

### 问题

你有一个动态环境，同时需要在运行中重新配置 NGINX Plus。

### 解决方案

配置 NGINX Plus API 来允许通过 API 调用添加或者移除服务器：

````
upstream backend {
	zone http_backend 64k;
}
server {
	# ...
	location /api {
		api [write=on];
		# Directives limiting access to the API
		# See chapter 7
	}
	
	location = /dashboard.html {
		root	/usr/shar/nginx/html;
	}
}
````

这个 NGINX Plus 配置创建一个拥有一个共享存储区域的上游服务器，在`/api`的`location`块中启用 API ，同时为 NGINX Plus 的仪表盘提供一个`location`。

你可以使用该 API 在服务器上线后将它们添加到服务器池中：

````
$ curl -X POST -d '{"server":"172.17.0.3"}' \
	'http://nginx.local/api/3/http/upstreams/backend/servers/'

{
	"id":0,
	"server":"172.17.0.3:80",
	"weight":1,
	"max_conns":0,
	"max_fails":1,
	"fail_timeout":"10s",
	"slow_start":"0s",
	"route":"",
	"backup":false,
	"down":false
}
````

此`curl`调用向 NGINX Plus 发出一个请求，将一个新的服务器添加到后端上游服务器配置中。HTTP 方法是`POST`，请求体是一个 JSON 对象。NGINX Plus API 是 RESTful 的，因此，请求 URI 中包含若干参数。URI 格式如下：

````
/api/{version}/http/upstreams/{httpUpstreamName}/servers/
````

你可以通过 NGINX Plus API 列出上游服务器池中的服务器：

````
$ curl 'http://nginx.local/api/3/http/upstreams/backend/servers/'
[
  {
    "id":0,
 	"server":"172.17.0.3:80",
 	"weight":1,
 	"max_conns":0,
 	"max_fails":1,
 	"fail_timeout":"10s",
 	"slow_start":"0s",
 	"route":"",
 	"backup":false,
 	"down":false
  }
]
````

这个例子中的`curl`调用向 NGINX Plus 发出了一个请求来列出名为`backend`的上游服务器池中的所有服务器。目前，我们只有在前一个`curl`调用中添加的那一台服务器。这个请求将返回一个上游服务器对象，包含服务器的所有可配置选项。

使用 NGINX Plus API 排空来自某个上游服务器的连接，准备将该服务器优雅地从上游服务器资源池中移除。你可以在 2.8 章节中看到有关连接排空的更多细节。

````
$ curl -X PATCH -d '{"drain":true}' \
	'http://nginx.local/api/3/http/upstreams/backend/servers/0'
{
 	"id":0,
 	"server":"172.17.0.3:80",
 	"weight":1,
 	"max_conns":0,
 	"max_fails":1,
 	"fail_timeout":
 	"10s","slow_start":
 	"0s",
 	"route":"",
 	"backup":false,
 	"down":false,
 	"drain":true
}
````

这个`curl`中，我们指定请求方法为`PATCH`，传递一个 JSON 体来指示它为某个服务器排空连接，同时将服务器 ID 附加在 URI 之后来指定服务器。我们可以发现列出的服务器中包含前面`curl`命令添加的那台服务器 ID。

NGINX Plus 将开始排空连接。此过程可能持续到应用的会话关闭。为了确定你开始排空的服务器上目前还有多少活动的连接正在被服务，使用下面的调用查看正在被排空的服务器的`active`属性：

````
$ curl 'http://nginx.local/api/3/http/upstreams/backend'
{
 	"zone" : "http_backend",
 	"keepalive" : 0,
 	"peers" : 
 	[
 		{
			"backup" : false,
 			"id" : 0,
 			"unavail" : 0,
 			"name" : "172.17.0.3",
 			"requests" : 0,
 			"received" : 0,
 			"state" : "draining",
 			"server" : "172.17.0.3:80",
 			"active" : 0,
 			"weight" : 1,
 			"fails" : 0,
			"sent" : 0,
 			"responses" : {
 				"4xx" : 0,
 				"total" : 0,
 				"3xx" : 0,
 				"5xx" : 0,
 				"2xx" : 0,
 				"1xx" : 0
 			},
 			"health_checks" : {
 				"checks" : 0,
 				"unhealthy" : 0,
 				"fails" : 0
 			},
 			"downtime" : 0
 		}
 	],
 	"zombies" : 0
}
````

当所有连接都被排空后，使用 NGINX Plus API 将该服务器从上游服务器资源池中移除：

````
$ curl -X DELETE \
	'http://nginx.local/api/3/http/upstreams/backend/servers/0'
[]
````

此`curl`命令向同一个 URI 发出一个`DELETE`方法请求来更新服务器状态。该`DELETE`方法指示 NGINX 移除该服务器。此 API 调用返回所有仍然留在服务器池中的的服务器和它们的 ID。因为我们是从一个空的服务器池开始，然后只通过 API 添加了一个服务器，接着排空连接，最后又移除了该服务器，现在我们重新拥有了一个空的服务器池。

### 讨论

NGINX Plus 独占 API 允许动态应用服务器在运行时将它们自己添加到 NGINX 配置中、或者从其中移除。当服务器上线时，它们可以将自己注册到服务器池中，NGINX 将开始向它们发送请求。当一个服务器需要被移除，它可以请求 NGINX Plus 排空它的连接，然后再它关闭之前将它从上游服务器池中移除。这就允许基础设施通过某些自动化机制动态扩容或者减配，而不需要人类参与。

### 参考

[NGINX Plus API Swagger Documentation](https://demo.nginx.com/swagger-ui/)

## 5.2 键值对存储

### 问题

你需要 NGINX Plus 基于来自应用的输入来进行动态流量管理决策。

### 解决方案

建立集群敏感的键值对存储和 API ，然后添加键值对：

````
keyval_zone zone=blacklist:1M;
keyval $remote_addr $num_failures zone=blacklist;

server {
  # ...
  location / {
    if($num_failures){
      return 403 'Forbidden';
    }
    return 200 'OK';
  }
}
server {
  # ...
  # Directives limiting access to the API
  # See chapter 6
  location /api {
    api write=on;
  }
}
````

此 NGINX Plus 配置使用`keyval_zone`目录来构建一个名为`blacklist`的键值对存储共享存储区域，同时设定其大小上限为 1 MB。然后`keyval`指令将第一个参数`$remote_addr`的值映射到该区域中的一个新的名为`$num_failures`的变量。这个新的变量接下来会被用于确定 NGINX Plus 是否应该为请求返回 403 `Forbidden`状态码响应。

使用此配置启动 NGINX Plus 服务器之后，你可以`curl`本地主机并期待接收到 200 `OK`响应：

````
$ curl 'http://127.0.0.1/'
OK
````

现在将本地机器的 IP 地址添加到该键值对存储中，对应的值为`1`：

````
$ curl -X POST -d '{"127.0.0.1":"1"}' \
	'http://127.0.0.1/api/3/httop/keyvals/blacklist'
````

此`curl`命令提交一个 HTTP POST 请求，携带一个包含一个键值对对象的 JSON 对象作为请求体，该键值对将被提交到`blacklist`共享存储区。键值对存储 API URI 的格式如下：

````
/api/{version}/http/keyvals/{httpKeyvalZoneName}
````

现在本地机器的 IP 地址已经被添加到名为`blacklist`的键值对区域中，对应值`1`。在下一个请求中，NGINX Plus 在该键值对区域内寻找`$remote_addr`，找到该条目，并将其值映射到变量`$num_failures`。此变量接下来在`if`语句中被评估。当变量拥有一个值时，`if` 语句评估结果为`true`，同时 NGINX Plus 返回 403 `Forbidden`状态码响应。

````
$ curl 'http://127.0.0.1'
Forbidden
````

你可以更新或者删除该键，通过发出`PATCH`方法请求：

````
$ curl -X PATCH -d '{"127.0.0.1":null}' \
	'http://127.0.0.1/api/3/http/keyvals/blacklist'
````

如果值为`null`则 NGINX Plus 将删除该键，同时请求将再次返回 200 `OK`。

### 讨论

键值对存储，作为 NGINX Plus 的独占特性，允许应用向 NGINX Plus 注入信息。在上面例子中，`$remote_addr`变量被用来创建动态黑名单。你可以已任何 NGINX Plus 可能拥有的变量来填充该键值对存储，比如会话 cookie，同时提供给 NGINX Plus 一个外部的值。在 NGINX Plus R16 中，该键值对存储是集群敏感的，也就是说，你只需要将你的键值对更新到一台 NGINX Plus 服务器上，所有集群中的服务器都会接收到这个信息。

### 参考

[Dynamic Bandwidth Limits](https://www.nginx.com/blog/dynamic-bandwidth-limits-nginx-plus-key-value-store/)

## 5.3 与 Puppet 一起安装

### 问题

你需要使用 Puppet 安装配置 NGINX 来管理 NGINX 配置，NGINX 配置被作为代码，并配合其它的 Puppet 配置。

### 解决方案

创建一个模块来安装 NGINX，管理你需要的文件，并确保 NGINX 正在运行：

````
class nginx {
  package {"nginx": ensure => 'installed',}
  service {"nginx":
  	ensure => 'true',
  	hasrestart => 'true',
  	restart => '/etc/init.d/nginx reload',
  }
  file { "nginx.conf":
    path => '/etc/nginx/nginx.conf',
    require => Package['nginx'],
    notify => Service['nginx'],
    content => template('nginx/templates/nginx.conf.erb'),
    user => 'root',
    group => 'root',
    mode => '0644';
  }
}
````

此模块使用包管理工具来确保 NGINX 包被安装。也保证 NGINX 正在运行而且在启动时 NGINX 是可用的。此配置使用`hasrestart`指令通知 Puppet 服务拥有一个重启命令，同时我们可以使用 NGINX reload 覆盖该`restart`命令。文件资源将管理并使用 Embedded Ruby(ERB) 模板语言模板化`nginx.conf`文件。由于`require`指令，该文件的模板化将在 NGINX 包被安装之后发生。不过，由于`notify`指令，文件资源将通知 NGINX 服务来重新加载。模板化的配置文件不包含在内。不过，它可以是简单地安装一个默认的 NGINX 配置文件，也可以是非常复杂地使用 ERB 或者 EPP 模板语言循环和变量替换。

### 讨论

Puppet 是基于 Ruby 编程语言的配置管理工具。模块由领域特定语言构建并通过为给定服务器定义配置的清单文件调用。Puppet 可以使用主从配置或者无主配置运行。使用 Puppet，清单运行在主服务器上，然后发送给从服务器。这一点很重要，因为它保证了从服务器仅仅被分发跟它有关的配置，而不会得到其它服务器的额外配置。有大量额高级公共模块对 Puppet 可用。从这些模块开始，将帮助你对配置文件的理解。来自 GitHub 的 voxpupuli 项目的一个公共 NGINX 模块将为你模板化配置文件。

### 参考

[Puppet Documentation](https://puppet.com/docs)

[Puppet Package Documentation](https://puppet.com/docs/puppet/6.7/types/package.html)

[Puppet Service Documentation](https://puppet.com/docs/puppet/6.7/types/service.html)

[Puppet File Documentation](https://puppet.com/docs/puppet/6.7/types/file.html)

[Puppet Templating Documentation](https://puppet.com/docs/puppet/6.7/lang_template.html)

[Voxpupuli NGINX Module](https://github.com/voxpupuli/puppet-nginx)

## 5.4 与 Chef 一起安装

### 问题

你需要使用 Chef 安装配置 NGINX 来管理 NGINX 配置，NGINX 配置被作为代码，并配合其它的 Chef 配置。

### 解决方案

使用配方创建一个菜谱来安装NGINX并通过模板配置配置文件，并确保在配置到位后重新加载NGINX。以下是一个示例配方：

````
package 'nginx' do
 action :install
end
service 'nginx' do
 supports :status => true, :restart => true, :reload => true
 action [ :start, :enable ]
end
template 'nginx.conf' do
 path "/etc/nginx.conf"
 source "nginx.conf.erb"
 owner 'root'
 group 'root'
 mode '0644'
 notifies :reload, 'service[nginx]', :delayed
end
````

`package`块安装 NGINX。`service`块确保 NGINX 被启动并且在系统启动时启动，然后向 Chef 的其它部分声明 NGINX 服务支持的操作。`template`模块模板化一个 ERB 文件并将其放在`/etc/nginx.conf`中，其中包含文件所有者和`root`组。`template`块还会设定`mode`为`644`并通知`nginx`服务`reload`，但会一直等到由`:delayed`语句声明的 Chef 运行结束。模板化配置文件不包括在内。但是，它可以像默认的 NGINX 配置文件一样简单，也可以使用 ERB 模板语言循环和变量替换而变得非常复杂。

### 讨论

Chef 是一个基于 Ruby 的配置管理工具。Chef 可以在 master-slave 或 solo 配置中运行，现在称为 Chef Zero。Chef 有一个非常大的社区，有许多名为超市的公共食谱。可以通过名为 Berkshelf 的命令行实用程序安装和维护超市的公共食谱。Chef 非常有强大，我们所展示的只是一个小样本。超市中的公共 NGINX 食谱非常灵活，提供了从包管理器或从源轻松安装 NGINX 的选项，以及编译和安装许多不同模块以及模板化基本配置的能力。

### 参考

[Chef documentation](https://docs.chef.io/)

[Chef Package](https://docs.chef.io/resource_package.html)

[Chef Service](https://docs.chef.io/resource_service.html)

[Chef Template](https://docs.chef.io/resource_template.html)

[Chef Supermarket for NGINX](https://supermarket.chef.io/cookbooks/nginx)

## 5.5 与 Ansible 一起安装

### 问题

你需要使用 Ansible 安装配置 NGINX 来管理 NGINX 配置，NGINX 配置被作为代码，并配合其它的 Ansible 配置。

### 解决方案

创建一个 Ansible 运行文件来安装 NGINX 并管理`nginx.conf`文件。下面是用来安装 NGINX 的剧本的例子。确保它正在运行并模板和配置文件：

````
- name: NGINX | Installing NGINX
  package: name=nginx state=present
- name: NGINX | Starting NGINX
  service:
 	name: nginx
 	state: started
 	enabled: yes
- name: Copy nginx configuration in place.
  template:
 	src: nginx.conf.j2
 	dest: "/etc/nginx/nginx.conf"
 	owner: root
 	group: root
 	mode: 0644
  notify:
 	- reload nginx
````

`package`块安装 NGINX。`service`块确保 NGINX 被启动并且在系统启动时启动。`template`模块模板化一个 `Jinja2` 文件并将结果放在`/etc/nginx.conf`中，其中包含文件所有者和`root`组。`template`块还会设定`mode`为`644`并通知`nginx`服务`reload`。模板化配置文件不包括在内。但是，它可以像默认的 NGINX 配置文件一样简单，也可以使用 Jinja2 模板语言循环和变量替换而变得非常复杂。

### 讨论

Ansible 是一个应用广泛的强大的配置管理工具，基于 Python。任务配置放在 YAML 文件中，同时你使用 Jinja2 模板语言来进行文件模板化。Ansible 在订阅模型上提供名为 Ansible Tower 的主机。但是，它通常用于本地计算机或直接构建服务器到客户端或无主模型。Ansible 批量 SSH 到其服务器并运行配置。与其他配置管理工具非常相似，有一个庞大的公共角色社区。Ansible 称之为 Ansible Galaxy。您可以找到非常复杂的角色用于你的剧本。

### 参考

[Ansible Documentation](https://docs.ansible.com/)

[Ansible Packages](https://docs.ansible.com/ansible/latest/modules/package_module.html)

[Ansible Service](https://docs.ansible.com/ansible/latest/modules/service_module.html)

[Ansible Template](https://docs.ansible.com/ansible/latest/modules/template_module.html)

[Ansible Galaxy](https://galaxy.ansible.com/)

## 5.6 与 SaltStack 一起安装

### 问题

你需要使用 SaltStack 安装配置 NGINX 来管理 NGINX 配置，NGINX 配置被作为代码，并配合其它的 SaltStack 配置。

### 解决方案

安装 NGINX 通过包管理模块同时管理你需要的配置文件。下面是一个 state 文件（*sls*）的例子，它将安装`nginx`包并确保服务运行，在系统启动时开启，当配置文件发生变化时重新加载：

````
nginx:
 pkg:
 - installed
 service:
 - name: nginx
 - running
 - enable: True
 - reload: True
 - watch:
 - file: /etc/nginx/nginx.conf
/etc/nginx/nginx.conf:
 file:
 - managed
 - source: salt://path/to/nginx.conf
 - user: root
 - group: root
 - template: jinja
 - mode: 644
 - require:
 	- pkg: nginx
````

这是通过包管理实用程序安装 NGINX 并管理*nginx.conf*文件的基本示例。NGINX 软件包被安装，并且该服务正在运行并在系统引导时启用。使用 SaltStack，您可以声明由 Salt 管理的文件，如示例中所示，并由许多不同的模板语言模板化。模板化配置文件不包括在内。但是，它可以像默认的 NGINX 配置文件一样简单，也可以与 Jinja2 模板语言循环和变量替换共同使用而非常复杂。此配置还指定必须在管理文件之前安装 NGINX，因为`require`语句。文件到位后，由于服务上的`watch`指令重新加载 NGINX 而重新加载，而不是重新启动，因为`reload`指令设置为`True`。

### 讨论

SaltStack 是一个功能强大的配置管理工具，用于在 YAML 中定义服务器状态。SaltStack 的模块可以用 Python 编写。Salt 为状态和文件暴露了 Jinja2 模板语言。但是，对于文件，还有许多其他选项，例如 Mako，Python 本身等。Salt 工作在主从配置和无主配置。奴隶被称为 minions。然而，主从传输通信与其他通信不同，这使得 SaltStack 与众不同。使用 Salt，您可以选择 ZeroMQ，TCP 或可靠的异步事件传输（RAET）来传输到 Salt 代理；或者如果你不能使用代理，则 master 主机可以改为使用 SSH。由于传输层默认是异步的，因此构建 SaltStack 是为了能够使用较低的主服务器负载将其消息传递给大量minions。

### 参考

[SaltStack](https://docs.saltstack.com/en/latest/)

[Installed Packages](https://docs.saltstack.com/en/latest/ref/states/all/salt.states.pkg.html#salt.states.pkg.installed)

[Managed Files](https://docs.saltstack.com/en/latest/ref/states/all/salt.states.file.html#salt.states.file.managed)

[Templating with Jinja](https://docs.saltstack.com/en/latest/topics/jinja/index.html)

## 5.7 使用 Consul 模板化进行自动化配置

### 问题

您需要自动化 NGINX 配置，以通过使用 Consul 来响应您环境中的变化。

### 解决方案

使用`consul-template`守护进程和一个模板文件来模板化你选择的 NGINX 配置文件：

````
upstream backend { {{range service "app.backend"}}
  server {{.Address}};{{end}}
}
````

这个例子时一个 Consul 模板文件，用来模板化一个上游配置块。此模板将遍历 Consul 中标识为`app.backend`的节点。对于 Consul 中的每个节点，模板将生成携带该节点的IP地址的服务器指令。

`consul-template`守护进程通过命令行运行，并且能够被用来在每次模板化的配置文件发生变化时重新加载 NGINX：

````
# consul-template -consul consul.example.internal -template \
	template:/etc/nginx/conf.d/upstream.conf:"nginx -s reload"
````

此命令指示`consul-template`守护程序连接到`consul.example.internal`地址的 Consul 集群，并使用当前工作目录中名为*template*的文件对模板进行模板化并将生成的内容输出到*/etc/nginx/conf.d/upstream.conf*，然后每次模板文件更改时重新加载 NGINX。`-template`标志采用模板文件的字符串、输出位置和模板化过程发生后运行的命令。这三个变量用冒号分隔。如果正在运行的命令有空格，请确保将其用双引号括起来。 `-consul`标志告诉守护进程要连接的 Consul 集群。

### 讨论

Consul 是一个功能强大的服务发现工具和配置存储。Consul 在类似目录的结构中存储有关节点和键值对的信息，并允许进行 RESTful API交互。Consul 还在每个客户端上提供 DNS 接口，允许对连接到群集的节点进行域名查找。利用 Consul 集群的单独项目是`consul-template`守护程序。此工具模板化文件以响应 Consul 节点，服务或键值对中的更改。这使得 Consul 成为 NGINX 自动化的强大选择。使用`consul-template`，您还可以指示守护程序在更改模板后运行命令。有了这个，我们可以重新加载 NGINX 配置，让您的 NGINX 配置与您的环境一起活跃起来。使用 Consul，您可以在每个客户端上设置运行状况检查，以检查预期服务的运行状况。通过此故障检测，您可以相应地模拟 NGINX 配置，仅将流量发送到健康主机。

###  参考

[Consul Home Page](https://www.consul.io/)

[Introduction to Consul Template](https://www.hashicorp.com/blog/introducing-consul-template.html)

[Consul Template GitHub](https://github.com/hashicorp/consul-template)

# 6 身份认证

## 6.0 介绍

NGINX 能够认证客户端。使用 NGINX 来承担认证客户端请求的工作，这样可以提供阻止未经身份认证的请求到达你的应用服务器的能力。NGINX 开源版本可用模块中包含了基本的身份认证和认证子请求。NGINX Plus 扩展模块可以验证 JSON Web Tokens (JWT) 可以与使用标准 OpenID Connect 认证的第三方身份认证提供者集成。

## 6.1 HTTP 基本身份认证

### 问题

你需要通过 HTTP 基本身份认证保护你的应用或者内容。

### 解决方案

生成一个如下格式的文件，其中的密码使用以下几种允许的格式之一加密或者哈希：

````
# comment
name1:password1
name2:password2:comment
name3:password3
````

用户名是第一个字段，密码是第二个字段，分隔符是分号。第三个字段是可选的，你可以用它来为每个用户添加注释。NGINX 可以理解几种密码格式，其中之一就是是否密码使用了 C 函数`crypt()`进行了加密。该函数通过`openssl passwd` 命令暴露给命令行。安装 `openssl` 之后，你就可以通过下面的命令创建加密密码字符串：

````shell
$ openssl passwd MyPassword1234
````

输出将是一个字符串，NGINX 可以将其用于你的密码文件中。

在你的 NGING 配置文件中使用 `auth_basic` 和 `auth_basic_user_file` 指令来启用基本身份认证：

````
location / {
  auth_basic				"Private site";
  auth_basic_user_file		conf.d/passwd;
}
````

你可以在 HTTP，服务器，或者 location 上下文中使用 `auth_basic` 指令。该指令携带一个字符串参数，当一个未经身份认证的用户到来时，该字符串将出现在基本身份认证弹出窗口上。`auth_basic_user_file` 指定了用户文件的路径。

### 讨论

按照不同的安全级别，你可以通过几种方式生成基本身份认证的密码，并使用几种不同的格式。来自 Apache 的 `htpasswd` 命令也可以生成密码。`openssl` 和 `htpasswd` 命令都使用 `apr1` 算法生成密码，NGINX 都可以理解。密码也可以是 Lightweight Directory Access Protocol (LDAP) 和 Dovecot 使用的加盐的 SHA-1格式。NGINX 支持更多格式和哈希算法，不过，其中很多都被认为是不安全的，因为它们很容易被暴力破解。

你可以使用基本身份认证保护你的整个 NGINX 主机的内容、特定的虚拟服务器、或者甚至是特定 location 块。借本身份认证不会替代web应用的用户身份认证，不过它可以协助保持私密信息的安全。在幕后，基本身份认证通过服务器返回 `401 unauthorized` HTTP 状态码以及响应头 `WWW-Authenticate` 来完成。该响应头将拥有值 `Basic realm="your string"`。该响应将导致浏览器提示需要用户名和密码。用户名和密码使用分号分隔，使用 base64 编码，然后通过请求头 `Authorization` 发送。该请求头将指定一个 `Basic` 以及 `user:password` 编码字符串。服务器解码该请求头并根据给定的 `auth_basic_user_file` 对其中的信息进行验证。由于用户名密码字符串仅仅只是 base64 编码，推荐使用 HTTPS 进行基本身份认证。

## 6.2 身份认证子请求

### 问题

你拥有一个第三方身份认证系统，你想使用它进行请求身份认证。

### 解决方案

使用 `http_auth_request_module` 向身份认证服务发送一个请求在为原始请求提供服务之前验证身份标识：

````
location /private/ {
  auth_request				/auth;
  auth_request_set			$auth_status $upstream_status;
}

location = /auth {
  internal;
  proxy_pass				http://auth-server;
  proxy_pass_request_body	off;
  proxy_set_header			Content-Length "";
  proxy_set_header			X-Original-URI $request_uri;
}
````

`auth_request` 指令携带一个 URI 参数，该参数必须是一个本地内部 location 。`auth_request_set` 指令允许你设定来自认证子请求的变量。

### 讨论

`http_auth_request_module` 在所有被 NGINX 服务器处理的请求上开启身份认证。该模块在为原始请求提供服务之前发起一个身份认证子请求来确定该请求是否能够访问它请求的资源。整个原始请求被代理到该子请求 location。该身份认证 location 作为子请求的典型代理工作，并发送原始请求，包括原始请求体和请求头。子请求的响应的状态码用来确定原始请求是否可以访问资源。如果子请求返回 HTTP 200 状态码，则身份认证成功，原始请求被满足。如果子请求返回 HTTP 401 或者 403 状态码，则原始请求也会返回同样的状态码。

如果你的身份认证服务不需要请求体，你可以使用`proxy_pass_request_body`指令丢弃请求体，如例子中所示。这样做可以减少请求大小和事件。由于响应体被忽略，`Content-Length` 响应头必须被设定为一个空字符串。如果你的身份认证服务需要了解请求访问的 URI，你将希望将该值放在一个自定义首部中，你的认证服务可以检查并校验它。如果还有其它的你不希望通过认证子请求发送到认证服务的数据，比如响应头等等，你可以使用 `auth_request_set` 指令来从响应数据中排除它们。

## 6.3 验证 JWTs

### 问题

你需要在请求被 NGINX Plus 处理之前验证一个 JWT 。

### 解决方案

NGINX Plus 的 HTTP JWT 身份认证模块用来验证 token 签名并将 JWT 声明和请求头嵌入为 NGINX 变量：

````
location /api/ {
  auth_jwt				"api";
  auth_jwt_key_file		conf/keys.json
}
````

此配置为此 location 启用 JWT 验证。`auth_jwt` 指令被传入一个字符串，被作为认证域。`auth_jwt` 携带一个可选的 token 参数，是携带该 JWT 的变量。默认情况下，根据 JWT 标准使用 `Authentication` 头。`auth_jwt`指令还可用于从继承的配置中取消所需 JWT 身份认证的影响。要关闭身份认证，请将关键字`off`传递给`auth_jwt`指令，不带任何其他内容。要取消继承的身份认证需求，请将`off`关键字传递给`auth_jwt`指令，不带任何其他内容。`auth_jwt_key_file`采用单个参数。此参数是标准 JSON Web Key 格式的密钥文件的路径。

### 讨论

NGINX Plus 能够验证 JSON web 签名类型的 token ，而不是 JSON web 加密类型，其中整个 token 都是加密的。NGINX Plus 能够验证使用 HS256、RS256、以及 ES256 算法签名的签名。使用 NGINX Plus 验证 token 能够节省时间和资源，因为不再需要发送子请求到认证服务。NGINX Plus 解密 JWT 请求头和有效负载，并捕获标准请求头和声明到嵌入变量中供你使用。

### 参考

[RFC Standard Documentation of JSON Web Signature](https://tools.ietf.org/html/rfc7515)

[RFC Standard Documentation of JSON Web Algorithms](https://tools.ietf.org/html/rfc7518)

[RFC Standard Documentation of JSON Web Token](https://tools.ietf.org/html/rfc7519)

[NGINX Embedded Variables](http://nginx.org/en/docs/http/ngx_http_auth_jwt_module.html#variables)

[Detailed NGINX Blog](https://www.nginx.com/blog/authenticating-api-clients-jwt-nginx-plus/)

## 6.4 创建 JSON Web Keys

### 问题

你需要一个 JSON Web Keys 供 NGINX Plus 使用。

### 解决方案

NGINX Plus 使用 JSON Web Key (JWK) 格式如 RFC 标准中所述。此标准允许 JWK 文件中包含密钥对象数组。

下面是密钥文件的例子：

````
{"keys":
[
  {
    "kty":"oct",
    "kid":"0001",
    "k":"OctetSequenceKeyValue"
  },
  {
	"kty":"EC",
	"kid":"0002"
	"crv":"P-256",
	"x": "XCoordinateValue",
	"y": "YCoordinateValue",
	"d": "PrivateExponent",
	"use": "sig"
  },
  {
	"kty":"RSA",
	"kid":"0003"
	"n": "Modulus",
	"e": "Exponent",
	"d": "PrivateExponent"
  }
]
}
````

上面的 JWK 文件展示了 RFC 标准中提到的3种初始密钥类型。这些密钥的格式也是 RFC 标准的一部分。`kty`属性是密钥类型。此文件展示了3种密钥类型：字节序列（`oct`），椭圆曲线（`EC`），以及 `RSA` 类型。`kid` 属性是密钥 ID。标准中指定这些密钥的其它属性。参考 RFC 文档获取更多信息。

### 讨论

在许多不同的语言中已经有大量的用于产生 JSON Web Key 的类库可用。推荐创建一个密钥服务作为中央 JWK 认证中心，负责创建并定器更新你的 JWK。对应更强的安全需求，推荐将你的 JWK 提升到 SSL/TLS 认证相同的安全级别。使用适当的用户和组权限保护您的密钥文件。将它们保存在主机内存中是最佳做法。您可以通过创建像 ramfs 这样的内存中文件系统来实现。定期更新密钥也很重要；您可以选择创建一个创建公钥和私钥的密钥服务，并通过 API 将它们提供给应用程序和 NGINX。

### 参考

[RFC standardization documentation of JSON Web Key](https://tools.ietf.org/html/rfc7517)