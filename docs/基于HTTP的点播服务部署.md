
# 基于HTTP的点播服务器

nginx 1.1.3之后已经默认支持mp4，flv模块，无须第三方模块支持

## 下载

* [nginx: download](http://nginx.org/en/download.html)

当前使用`nginx-1.18.0`

## 依赖

参考：[rtmp-hls-server/Dockerfile](https://github.com/TareqAlqutami/rtmp-hls-server/blob/master/Dockerfile)

```
apt-get install -y \
        gcc make cmake \
		wget build-essential ca-certificates \
		openssl libssl-dev yasm \
		libpcre3-dev librtmp-dev libtheora-dev \
		libvorbis-dev libvpx-dev libfreetype6-dev \
		libmp3lame-dev libx264-dev libx265-dev
```

## 编译

参考：[nignx搭建流媒体播放器](https://blog.csdn.net/fengchao2016/article/details/104024500)

```
# 解压
$ tar zxvf nginx-1.18.0.tar.gz
# 进入文件夹，配置mp4/flv模块
$ cd nginx-1.18.0
$ ./configure --prefix=/usr/local/nginx  --with-http_mp4_module --with-http_flv_module --with-pcre
# 编译
$ make
# 安装
$ sudo make install
```

安装完成后在`/usr/loca/nginx`路径下有如下内容：

```
# ls
conf  html  logs  sbin
```

进入`sbin`查看`nginx`配置模块

```
# ./nginx -V
nginx version: nginx/1.18.0
built by gcc 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04) 
configure arguments: --prefix=/usr/local/nginx --with-http_mp4_module --with-http_flv_module --with-pcre
```

## 使用

进入目录`/usr/local/nginx/conf`，编译配置文件`nginx.conf`。参考：

* [Module ngx_http_mp4_module](http://nginx.org/en/docs/http/ngx_http_mp4_module.html)
* [Module ngx_http_flv_module](http://nginx.org/en/docs/http/ngx_http_flv_module.html)

```
location /video/ {
    root html/video;
    mp4;
    mp4_buffer_size       1m;
    mp4_max_buffer_size   5m;
}
```

使用`root`指令配置文件路径，如果设置为相对路径，那么其完整路径为`/usr/local/nginx/html/video`

进入`/usr/local/nginx/sbin`，先检查配置文件语法是否正确

```
# ./nginx -t
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful
```

再启动nginx

```
root@bbadc487a664:/usr/local/nginx/sbin# ./nginx 
```

登录网页`http://localhost:80`即可判断`nginx`是否启动成功

```
Welcome to nginx!
If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

For online documentation and support please refer to nginx.org.
Commercial support is available at nginx.com.

Thank you for using nginx.
```

将视频文件该路径下，即可通过`http`链接进行访问

```
http://localhost:80/video/output.mp4
```