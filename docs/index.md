
# 引言

本仓库记录了视频流媒体服务器的搭建以及推流/拉流操作的实现

## 内容列表

1. [点播 vs. 直播](./点播-直播.md)
1. [RTSP/RTMP/HLS](./rtmp-vs-rtsp-vs-hls.md)
3. 流媒体服务器搭建
      1. 自建：[nginx-rtmp-module](./nginx-rtmp-module.md)
      2. `Docker`：[rtmp-hls-server](./rtmp-vs-rtsp-vs-hls.md)
4. 推流实现
      1. obj studio
      2. ffmpeg
5. 拉流实现
      1. [浏览器支持编解码器类型](./浏览器支持编解码器类型.md)
      2. vlc
      3. html
6. 错误
      1. [OBS启动串流失败 - 注意：如果你使用的是NVENC或AMD编码器,请确保您的视频驱动程序是最新的.](./error.md)