
# [FFMPEG]安装

## Python

[conda-forge/ffmpeg-feedstock](https://github.com/conda-forge/ffmpeg-feedstock)已编译好`Python`包，可以直接安装

```
$ conda config --add channels conda-forge
$ conda install ffmpeg
# 搜索指定版本
$ conda search ffmpeg --channel conda-forge
```

## Docker

使用[ffmpeg-feedstock/.scripts/run_docker_build.sh](https://github.com/conda-forge/ffmpeg-feedstock/blob/master/.scripts/run_docker_build.sh)安装`FFMPEG Docker`镜像

## 源码编译

使用[ffmpeg-feedstock/recipe/build.sh](https://github.com/conda-forge/ffmpeg-feedstock/blob/master/recipe/build.sh)执行源码编译，可以根据需要增减编译选项

## 查询当前使用

```
$ whereis ffmpeg
ffmpeg: /usr/bin/ffmpeg /usr/share/ffmpeg /home/zj/anaconda3/bin/ffmpeg /usr/share/man/man1/ffmpeg.1.gz
```

## 指定当前使用

设置全局变量

```
export FFMPEG_HOME=/path/to/ffmpeg
export PATH=$FFMPEG_HOME/bin:$PATH
```

**当出现多个`ffmpeg`，一定要查询全局变量，不让你操作调整的可能一直不是实际运行的那个。:cry: :cry: :cry:**