
# [FFMPEG]RTSP/RTMP推流

## Python实现

```
import cv2
import subprocess as sp

way = 'rtsp'
push_url = "xxx"
camera_path = "xxx"

cap = cv2.VideoCapture(camera_path)

# Get video information
fps = int(cap.get(cv2.CAP_PROP_FPS))
width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
print(fps, width, height)
# ffmpeg command
if way == "rtmp":
    command = ['ffmpeg',
               '-y',
               '-f', 'rawvideo',
               '-vcodec', 'rawvideo',
               '-pix_fmt', 'bgr24',
               '-s', "{}x{}".format(width, height),
               '-r', str(fps),
               '-i', '-',
               '-c:v', 'libx264',
               '-pix_fmt', 'yuv420p',
               '-preset', 'ultrafast',
               '-f', 'flv',
               push_url]
else:
    command = ['ffmpeg',
               '-loglevel', 'error',
               '-c',
               '-y',
               '-f', 'rawvideo',
               '-vcodec', 'rawvideo',
               '-pix_fmt', 'bgr24',
               '-s', "{}x{}".format(width, height),
               '-r', str(fps),
               '-i', '-',
               '-c:v', 'libx264',
               '-pix_fmt', 'yuv420p',
               '-preset', 'ultrafast',
               '-rtsp_transport', 'tcp',
               '-f', 'rtsp',
               push_url]
# 管道配置
p = sp.Popen(command, stdin=sp.PIPE)
# read webcamera
while (cap.isOpened()):
    ret, frame = cap.read()
    # print("running......")
    if not ret:
        print("Opening camera is failed")
        break
    p.stdin.write(frame.tobytes())

return_value, frame = cap.read()
```

## 相关阅读

* [python 使用ffmpeg推送视频流 ](https://bbs.csdn.net/topics/398223669)