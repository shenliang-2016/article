## 9.1 处理 MP4 和 FLV

### 问题

你需要流式处理数字媒体，源于 MPEG-4 (MP4) 或者 Flash Video (FLV)。

### 解决方案

将 HTTP location 块指定为 *.mp4* 或 *.flv*。NGINX 将使用渐进式下载或 HTTP 伪流式处理对媒体进行流化，同时支持查找：

````
http {
        server {
						...
            location /videos/ {
                mp4;
            }
            location ~ \.flv$ {
								flv; 
						}
				} 
}
````

该示例位置块告诉 NGINX，*videos* 目录中的文件是 MP4 格式的类型，可以通过渐进式下载支持进行流传输。第二个位置块指示 NGINX 任何以 *.flv* 结尾的文件均为 FLV 格式，并且可以使用 HTTP 伪流支持进行流式传输。

### 讨论

在 NGINX 中流式传输视频或音频文件就像一个指令一样简单。渐进式下载使客户端可以在文件下载完成之前启动媒体播放。NGINX 支持以两种格式搜索未下载的媒体部分。

