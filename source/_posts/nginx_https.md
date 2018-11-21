---
title: Nginx网页服务器 https证书部署
date: 2018-9-1
tags:  [nginx]
---

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)

### 腾讯云https证书申请和部署

域名型证书申请流程
https://cloud.tencent.com/document/product/400/6814

证书安装部署指引
https://cloud.tencent.com/document/product/400/4143

### 实例本站证书部署

- 本站Nginx网页服务器使用 apt-get install nginx 进行安装
- nginx.conf 配置文件存放目录是 /etc/nginx/
- 使用 **nginx -t** 命令会很方便找到 nginx.conf 目录
- 站点配置 存放 /etc/nginx/sites-enabled
---
- 实例 把证书文件1 和 私钥文件2 同nginx.conf放一起，本例放 /etc/nginx/
- cd /etc/nginx/sites-enabled  建立 https 配置文件，粘贴以下代码内容
---

~~~c
# https 配置文件，存放 /etc/nginx/sites-enabled

server {
        listen 443;
        server_name www.srgb.xyz; #填写绑定证书的域名
        ssl on;
        
        # 找到存放nginx.conf文件目录  把证书文件1 和 私钥文件2 同nginx.conf放一起，本例放 /etc/nginx
        ssl_certificate 1_www.srgb.xyz_bundle.crt;    
        ssl_certificate_key 2_www.srgb.xyz.key;
        
        ssl_session_timeout 5m;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2; #按照这个协议配置
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;#按照这个套件配置
        ssl_prefer_server_ciphers on;
        location / {
            root   /var/www;    #站点目录
            index  index.html index.htm;
        }
    }
~~~

### 调试测试配置文件
- 配置完成后，先用 **nginx –t** 来测试下配置是否有误，正确无误的话，**service nginx restart** 重启nginx

	nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
	nginx: configuration file /etc/nginx/nginx.conf test is successful
	
- 使用命令 **systemctl status nginx.service** 查看nginx日志信息，看看443端口是否占用

	Sep 01 12:59:40 vultr.guest nginx[10753]: nginx: [emerg] bind() to 0.0.0.0:443 failed (98: Address already in use)
- 本站由于 frps 配置使用了443端口，到时启动失败，把frps.ini里443端口改成4443才正确配置好