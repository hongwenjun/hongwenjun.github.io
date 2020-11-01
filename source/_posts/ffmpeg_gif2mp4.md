---
title: 使用FFMPEG把gif转换到MP4格式方便上传
date: 2018-10-10
tags:  [ffmpeg]
---

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)

![](/webp/gif2mp4.webp)


### 使用FFMPEG把gif转换到MP4格式方便上传

https://youtu.be/EN7QLAhJrEo

### gif 视频使用GifCam录制成640x360，转换后为720P (1280x720)
	ffmpeg   -i  a.gif   -s 1280x720  new.mp4

