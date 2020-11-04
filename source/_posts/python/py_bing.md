---
title: Python下载Bing每日壁纸，代码编辑器使用 CodeBlocks
date:  2020-11-04
tags:  python
---

蘭雅sRGB 龙芯2F服务器和博客 | [https://262235.xyz](https://262235.xyz)
---

###  普通的方法使用浏览器Chrome下载
- 浏览器Chrome下载精美壁纸,打开bing.com；按F12快捷键，然后点击Sources

![](/img/2011/chrome_f12.jpg)


### 使用Python调试脚本,下载bing精美壁纸

- 录制了一个python测试视频，放在了B站和youtube，参考使用下面脚本

- https://www.bilibili.com/video/BV1Ba411c7NX/

- https://youtu.be/xtYuuoDvbYI

###  正则获取图片文件名

```
name = re.search( r'id=(.*\.jpg)&rf', image_url)
```

![](/img/python/reg_search.png)

### bing.py 源码

```
#!/usr/bin/python
import requests
import time
import re

# 时间戳
timestamp = str(int(time.time() * 1000))

# 拼接请求地址
url = 'https://cn.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1&nc=' + timestamp + '&pid=hp'

# 请求头，模拟浏览器UA
headers = {
    'User-Agent': ' '.join(['Mozilla/5.0 (Windows NT 10.0; Win64; x64; ServiceUI 14)',
                            'AppleWebKit/537.36 (KHTML, like Gecko)', 'Chrome/70.0.3538.102', 'Safari/537.36',
                            'Edge/18.18363'])
}

# 发送请求
r = requests.get(url=url, headers=headers)

# 将响应的字符串转化为json数据，即dict类型
result = r.json()

# 获取第一个图片的链接
image_url = result['images'][0]['url']

# 图片文件名  name[1]
name = re.search( r'id=(.*\.jpg)&rf', image_url)

# 拼接上bing的域名
image_url = 'https://cn.bing.com' + image_url

# 定义图片保存地址
save_image_file = '/home/samba/bing/' + name[1]

# 下载图片
r = requests.get(url=image_url, headers=headers)

# 注意要以二进制只写打开文件
with open(save_image_file, 'wb') as f:
    # 图片的二进制数据
    f.write(r.content)

```

###  编辑定时任务执行  ** crontab -e **
```
# m   h  dom mon dow   command  # 分 时 日 月 周

  1 */12  *  *   *    cd /home/samba/bing  &&   python3 bing.py

```

### 之前制作没有语音的视频，有时间制作重制版
[![](/img/2011/vod_list.jpg)](https://www.youtube.com/sRGB18)