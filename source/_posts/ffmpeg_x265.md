---
title: FFMPEG 裁剪拼接mp4和转换X.265格式
date: 2020-06-28
tags:  [ffmpeg]
---

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)

### FFMPEG 裁剪mp4

```
-i : source  来源,输入文件
-ss:start time  开始时间
-t :duration    持续时间
-c :video,audio codec   视频，音频编解码器，copy是重新编码
```

### 行车记录仪3分钟视频，从第60秒开始剪裁120秒，剪裁2分钟保存到新文件
	$ ffmpeg.exe -i 2020-06-21-08-53-20.MP4 -ss 60 -t 120 -c copy new.mp4

### 视频个格式转 X.265  也可以使用GPU硬件加速
	ffmpeg -i 01.mp4 -c:v libx265 -crf 30 -map 0:v -map 0:a:0 output.mp4 

- libx265  使用软件CPU驱动
- 老黄显卡硬件加速  hevc_nvenc
- AMD加硬件加速     hevc_amf

  ffmpeg -i 01.mp4 -c:v hevc_amf -crf 30 -map 0:v -map 0:a:0 output.mp4 

### 合并多个文件 参考: https://trac.ffmpeg.org/wiki/Concatenate

	ffmpeg -f concat -safe 0 -i mylist.txt -c copy output.wav

	ffmpeg -i "concat:input1.ts|input2.ts|input3.ts" -c copy output.ts

	ffmpeg -i "concat:intermediate1.ts|intermediate2.ts" -c copy -bsf:a aac_adtstoasc output.mp4


# mp4box 合并 mp4
	mp4box -cat 1.mp4  -cat 2.mp4 new.mp4

### gif 视频使用GifCam录制成640x360，转换后为720P (1280x720)
	ffmpeg   -i  a.gif   -s 1280x720  new.mp4

### ffmpeg 调整视频帧率 -r 参数
	ffmpeg -i a.mp4  -r 5  new.mp4

### 其他命令 
```
# 几条 ffmpeg 的命令
	
1，获取视频的信息
   ffmpeg -i video.avi

2，将图片序列合成视频
   ffmpeg -f image2 -i image%d.jpg video.mpg
   上面的命令会把当前目录下的图片（名字如：image1.jpg, image2.jpg, 等...）合并成video.mpg

3，将视频分解成图片序列
   ffmpeg -i video.mpg image%d.jpg
   上面的命令会生成image1.jpg, image2.jpg, ...
   支持的图片格式有：PGM, PPM, PAM, PGMYUV, JPEG, GIF, PNG, TIFF, SGI

4，为视频重新编码以适合在iPod/iPhone上播放
   ffmpeg -i source_video.avi input -acodec aac -ab 128kb -vcodec mpeg4 -b 1200kb -mbd 2 -flags +4mv+trell -aic 2 -cmp 2 -subcmp 2 -s 320x180 -title X final_video.mp4
   说明：
       * 源视频：source_video.avi
       * 音频编码：aac
       * 音频位率：128kb/s
       * 视频编码：mpeg4
       * 视频位率：1200kb/s
       * 视频尺寸：320 X 180
       * 生成的视频：final_video.mp4

5，为视频重新编码以适合在PSP上播放
   ffmpeg -i source_video.avi -b 300 -s 320x240 -vcodec xvid -ab 32 -ar 24000 -acodec aac final_video.mp4
   说明：
       * 源视频：source_video.avi
       * 音频编码：aac
       * 音频位率：32kb/s
       * 视频编码：xvid
       * 视频位率：1200kb/s
       * 视频尺寸：320 X 180
       * 生成的视频：final_video.mp4

6，从视频抽出声音，并存为Mp3
   ffmpeg -i source_video.avi -vn -ar 44100 -ac 2 -ab 192 -f mp3 sound.mp3
   说明：
       * 源视频：source_video.avi
       * 音频位率：192kb/s
       * 输出格式：mp3
       * 生成的声音：sound.mp3

7，将wav文件转成Mp3
   ffmpeg -i son_origine.avi -vn -ar 44100 -ac 2 -ab 192 -f mp3 son_final.mp3

8，将.avi视频转成.mpg
   ffmpeg -i video_origine.avi video_finale.mpg

9，将.mpg转成.avi
   ffmpeg -i video_origine.mpg video_finale.avi

10，将.avi转成gif动画（未压缩）
   ffmpeg -i video_origine.avi gif_anime.gif

11，合成视频和音频
   ffmpeg -i son.wav -i video_origine.avi video_finale.mpg

12，将.avi转成.flv
   ffmpeg -i video_origine.avi -ab 56 -ar 44100 -b 200 -r 15 -s 320x240 -f flv video_finale.flv

13，将.avi转成dv
   ffmpeg -i video_origine.avi -s pal -r pal -aspect 4:3 -ar 48000 -ac 2 video_finale.dv
   或者：
   ffmpeg -i video_origine.avi -target pal-dv video_finale.dv

14，将.avi压缩成divx
   ffmpeg -i video_origine.avi -s 320x240 -vcodec msmpeg4v2 video_finale.avi

15，将Ogg Theora压缩成Mpeg dvd
   ffmpeg -i film_sortie_cinelerra.ogm -s 720x576 -vcodec mpeg2video -acodec mp3 film_terminate.mpg

16，将.avi压缩成SVCD mpeg2
   NTSC格式：
      ffmpeg -i video_origine.avi -target ntsc-svcd video_finale.mpg
   PAL格式：
      ffmpeg -i video_origine.avi -target pal-svcd video_finale.mpg

17，将.avi压缩成VCD mpeg2
   NTSC格式：
      ffmpeg -i video_origine.avi -target ntsc-vcd video_finale.mpg
   PAL格式：
      ffmpeg -i video_origine.avi -target pal-vcd video_finale.mpg

18，多通道编码
   ffmpeg -i fichierentree -pass 2 -passlogfile ffmpeg2pass fichiersortie-2

19，从flv提取mp3
   ffmpeg -i source.flv -ab 128k dest.mp3
```
