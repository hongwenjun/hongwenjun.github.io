---
title: Nginx 全站加密，http自动跳转https
date: 2018-9-2
tags:  [nginx]
---

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)

### Nginx支持rewrite, http跳转https

- **vim /etc/nginx/sites-enabled/http**     建立 **http** 配置文件，粘贴以下代码内容

---

~~~c
# 使用全站加密，http自动跳转https

server {
    listen 80;
    server_name www.srgb.xyz;

# Nginx是支持rewrite的（只要在编译的时候没有去掉pcre）
# 在http的server里增加
    rewrite ^(.*) https://$host$1 permanent;

}

~~~

---
### 也可以把http和https写在同一个文件里
~~~c
# https 配置文件，存放 /etc/nginx/sites-enabled

server {
    listen 443;
    server_name www.srgb.xyz; #填写绑定证书的域名
    ssl on;

# 找到存放nginx.conf文件  把证书文件1 和 私钥文件2 同nginx.conf放一起，本例放 /etc/nginx
    ssl_certificate 1_www.srgb.xyz_bundle.crt;
    ssl_certificate_key 2_www.srgb.xyz.key;

    ssl_session_timeout 5m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2; #按照这个协议配置
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE; #按照这个套件配置
        ssl_prefer_server_ciphers on;
    location / {
        root   /var/www;    #站点目录
            index  index.html index.htm;
    }
}



# 使用全站加密，http自动跳转https

server {
    listen 80;
    server_name www.srgb.xyz;

# Nginx是支持rewrite的（只要在编译的时候没有去掉pcre）
# 在http的server里增加
    rewrite ^(.*) https://$host$1 permanent;

}
~~~
---
### frps 配置文件也可以独立起来存放
~~~c
# frps 配置文件，存放 /etc/nginx/sites-enabled

map $http_x_forwarded_for $clientRealip {
   "" $remote_addr;
   ~^(?P<firstAddr>[0-9\.]+),?.*$  $firstAddr;
}

server {
       listen 80;
       server_name frp.srgb.xyz;  #为frp的控制台绑定一个域名，这样你就可以用http://frp.srgb.xyz访问你的控制台了
       location / {
           proxy_pass http://127.0.0.1:7500;  #此处的7500就是你安装frp时设置的dashboard_port端口
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $clientRealip;  # $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       }
}

server {
       listen 80;
       server_name s.srgb.xyz;   #也可以将所有的srgb.xyz子域名都绑定，
       location / {
           proxy_pass http://127.0.0.1:8080; #此处的8080就是你安装frp时设置的vhost_http_port端口
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $clientRealip;  # $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       }
}
~~~

---

### 调试测试配置文件
- 配置完成后，先用 **nginx –t** 来测试下配置是否有误，正确无误的话，**service nginx restart** 重启nginx
~~~
root@vultr:~# nginx -t
nginx: [warn] conflicting server name "frp.srgb.xyz" on 0.0.0.0:80, ignored
nginx: [warn] conflicting server name "s.srgb.xyz" on 0.0.0.0:80, ignored
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
~~~
	
- 使用命令 **systemctl status nginx.service** 查看nginx日志信息
~~~
root@vultr:~# systemctl status nginx.service
   nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2018-09-02 03:22:31 UTC; 1min 14s ago
     Docs: man:nginx(8)
  Process: 2748 ExecStop=/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid (code=exited, statu
  Process: 2754 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
  Process: 2751 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
 Main PID: 2756 (nginx)
    Tasks: 2 (limit: 4915)
   CGroup: /system.slice/nginx.service
           ├─2756 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           └─2757 nginx: worker process

Sep 02 03:22:31 vultr.guest systemd[1]: Starting A high performance web server and a reverse proxy server...
Sep 02 03:22:31 vultr.guest nginx[2751]: nginx: [warn] conflicting server name "frp.srgb.xyz" on 0.0.0.0:80, ignored
Sep 02 03:22:31 vultr.guest nginx[2751]: nginx: [warn] conflicting server name "s.srgb.xyz" on 0.0.0.0:80, ignored
Sep 02 03:22:31 vultr.guest nginx[2754]: nginx: [warn] conflicting server name "frp.srgb.xyz" on 0.0.0.0:80, ignored
Sep 02 03:22:31 vultr.guest nginx[2754]: nginx: [warn] conflicting server name "s.srgb.xyz" on 0.0.0.0:80, ignored
Sep 02 03:22:31 vultr.guest systemd[1]: nginx.service: Failed to read PID from file /run/nginx.pid: Invalid argument
Sep 02 03:22:31 vultr.guest systemd[1]: Started A high performance web server and a reverse proxy server.
~~~