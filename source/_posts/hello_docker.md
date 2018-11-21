---
title: Hello Docker 菜鸟笔记
date:  2018-11-5
tags:  [vps,docker]
---

### 可以直接运行官方的安装脚本一键安装

- 执行脚本方法如下：
```
curl -sSL https://get.docker.com/ | sh
# 或者
wget -qO- get.docker.com | bash 
```
- 安装完成后，运行下面的命令，验证是否安装成功。
	docker version 
- 启动 Docker
	systemctl start docker 

- 查看 Docker 启动状态
	systemctl status docker

- 允许 Docker 开机自启
	systemctl enable docker 


# 使用DOCKER安装PORTAINER
https://portainer.io/install.html
Portainer在Docker引擎或Swarm集群上作为轻量级Docker容器（Docker映像权重小于4MB）运行。因此，在使用Docker的任何计算机上运行容器都是一个命令。
### 部署PORTAINER
使用以下Docker命令部署Portainer：
```
$ docker volume create portainer_data
$ docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```


### 另一个别人 app 模版的PORTAINER 镜像使用
```
mkdir -p /opt/portainer/local-certs /opt/portainer/data

cd /opt/portainer/local-certs
openssl genrsa -out portainer.key 2048
openssl ecparam -genkey -name secp384r1 -out portainer.key
openssl req -new -x509 -sha256 -key portainer.key -out portainer.crt -days 3650

docker run -d -p 9000:9000 -v /opt/portainer/data:/data -v /opt/portainer/local-certs:/certs -v /var/run                                                                                      /docker.sock:/var/run/docker.sock --label owner=portainer --name ui --restart=always lihaixin/portainer -l owne                                                                                      r=portainer --ssl --sslcert /certs/portainer.crt --sslkey /certs/portainer.key

```

## 使用 Dockerfile 定制镜像  有空学习

https://yeasy.gitbooks.io/docker_practice/image/build.html