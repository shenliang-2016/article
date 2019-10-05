## 9.2 使用 HLS 的流

### 问题

你需要为 H.264/AAC-编码内容打包成的 MP4 文件支持 HTTP 实时流 (HLS) 。

### 解决方案

利用 NGINX Plus 的 HLS 模块进行实时分段，分组和多路复用，并控制分段缓冲等功能，例如转发 HLS 参数：

````
location /hls/ {
        hls;  # Use the HLS handler to manage requests
        # Serve content from the following location
        alias /var/www/video;
        # HLS parameters
        hls_fragment
        hls_buffers
        hls_mp4_buffer_size
        hls_mp4_max_buffer_size 5m;
}
````

此位置块指示 NGINX 将从 `/var/www/video` 目录中产生 HLS 媒体流，将媒体分成四秒的片段。HLS 缓冲区的数量设置为10个单位，单位大小为10 MB。初始 MP4 缓冲区大小设置为1 MB，最大5 MB。

### 讨论

NGINX Plus 中提供的 HLS 模块提供了动态传输 MP4 媒体文件的功能。有许多指令可让您控制媒体的分段和缓冲方式。必须将位置块配置为通过 HLS 处理程序将媒体用作 HLS 流。HLS 分段设置为秒数，指示 NGINX 按时间长度分段媒体。使用 `hls_buffers` 指令设置缓冲的数据量，该指令指定缓冲区的数量和大小。在 `hls_mp4_buffer_size` 指定的一定的缓冲量后，允许客户端开始播放媒体。但是，可能需要更大的缓冲区，因为有关视频的元数据可能会超出初始缓冲区的大小。该缓冲区大小以 `hls_mp4_max_buffer_size` 为上限。这些缓冲变量使 NGINX 可以优化最终用户体验。为这些指令选择正确的值需要了解目标受众和您的媒体。例如，如果您的媒体大部分是大型视频文件，并且您的目标受众具有较高的带宽，则可以选择更大的最大缓冲区大小和更长的片段长度。这将允许最初下载有关内容的元数据而不会出现错误，并且您的用户可以接收更大的片段。

