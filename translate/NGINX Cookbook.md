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