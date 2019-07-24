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

