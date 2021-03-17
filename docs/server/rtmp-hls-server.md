
# [Docker]rtmp-hls-server

## 安装

```
$ docker run -d -p 1935:1935 -p 8080:8080 alqutami/rtmp-hls
```

## 推流

使用`FFMPEG/OBS`推流视频流到如下地址

```
rtmp://<server ip>:1935/live/<stream_key>
```

示例如下：

```
$ ffmpeg -re -i xxx.mp4 -c copy -f flv  rtmp://localhost:1935/live/rtmplive
```

## 查询

打开网页`http://<server ip>:<server port>/stats`，可以查询当前流服务器状态

## 拉流

进入`VLC`打开流地址

```
rtmp://<server ip>:1935/live/<stream-key>
```

## 相关阅读

* [ phanumax/rtmp-hls-server](https://github.com/phanumax/rtmp-hls-server/tree/b07568c2f92c0a95372048abdfd91b80fe19e379)
* [音视频系列3：使用ffmpeg + nginx搭建本地转发服务器](https://zhuanlan.zhihu.com/p/113776414)