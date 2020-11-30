
# [FFMPEG]转换MPEG4格式文件到H264

参考：[Videojs does not play converted mp4 file](https://stackoverflow.com/questions/41949324/videojs-does-not-play-converted-mp4-file)

* 转换单个文件

```
ffmpeg -i input.mp4 -c:v libx264 -c:a copy -movflags +faststart output.mp4
```

* 批量转换文件

```
import os
import subprocess as sp

# MPEG-4视频目录
src_dir = '/home/zj/share/src'
# H264视频目录
dst_dir = '/home/zj/share/dst'

if not os.path.exists(dst_dir):
    os.makedirs(dst_dir)


def batch():
    for root, dirs, files in os.walk(src_dir, topdown=False):
        dst_root = os.path.join(dst_dir, root.split(src_dir)[1])
        if not os.path.exists(dst_root):
            os.makedirs(dst_root)
        for name in files:
            if not '.mp4' in name:
                continue
            src_video_path = os.path.join(root, name)
            dst_video_path = os.path.join(dst_root, name)

            cmd = f'ffmpeg -i {src_video_path} -c:v libx264 -c:a copy -movflags +faststart {dst_video_path}'
            print(f'cmd: {cmd}')
            p = sp.Popen(cmd, shell=True)
            p.wait()


if __name__ == '__main__':
    batch()
```