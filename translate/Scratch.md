## 9.3 使用 HDS 的流

### 问题

你需要支持 Adobe's HTTP Dynamic Streaming (HDS) ，该数据流已经分段并与元数据分离。

### 解决方案

使用 NGINX Plus 的分段 FLV 文件 (F4F) 支持模块向你的用户提供 Adobe Adaptive Streaming：

````
location /video/ {
        alias /var/www/transformed_video;
        f4f;
        f4f_buffer_size 512k;
}
````

该示例指示 NGINX Plus 使用 NGINX Plus F4F 模块从磁盘上的某个位置向客户端提供已经分段的媒体。索引文件（*.f4x*）的缓冲区大小设置为512 KB。

### 讨论

NGINX Plus F4F 模块使 NGINX 能够将预先分段的媒体提供给最终用户。此类的配置与在 HTTP 位置块内使用 `f4f` 处理程序一样简单。`f4f_buffer_size` 指令为这种类型的媒体的索引文件配置缓冲区大小。

## 9.4 带宽限制

### 问题

你需要在不影响观看体验的前提下限制流媒体客户端下行带宽。

### 解决方案

使用 NGINX Plus 为 MP4 媒体文件提供的比特率限制支持：

````
location /video/ {
        mp4;
        mp4_limit_rate_after 15s;
        mp4_limit_rate       1.2;
}
````

此配置允许下游客户端在应用比特率限制之前下载15秒。15秒后，允许客户端以比特率的120％的速率下载媒体，这使客户端始终可以以比其播放更快的速度下载。

### 讨论

NGINX Plus 的比特率限制使您的流服务器可以根据所提供的媒体来动态限制带宽，从而使客户端可以根据需要下载尽可能多的内容，以确保无缝的用户体验。9.1节中描述的 MP4 处理程序指定此位置块以流式传输 MP4 媒体格式。限速指令（例如 `mp4_limit_rate_after` ）告诉 NGINX 仅在指定的时间（以秒为单位）后限速流量。MP4 速率限制中涉及的另一个指令是 `mp4_limit_rate`，它指定允许客户端下载的相对于媒体比特率的比特率。`mp4_limit_rate` 指令提供的值为 `1` 表示 NGINX 将带宽（1对1）限制为媒体的比特率。为 `mp4_limit_rate` 指令提供大于 `1` 的值将使用户下载速度比观看速度快，因此他们可以缓冲媒体并在下载时无缝观看。

