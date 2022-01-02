+++
banner = ""
categories = ["工具软件"]
date = "2022-01-01T12:10:51+02:00"
description = ""
images = []
tags = ["软件安装"]
title = "linux docker 安装"

+++
## Linux 安装 Docker

> 参考资料：https://www.runoob.com/docker/centos-docker-install.html

### CentOS 安装

使用阿里源手动安装：
配置命令：

```bash
sudo yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

安装命令（需要确认两次下载）：

```
sudo yum install docker-ce docker-ce-cli containerd.io
```

启动 Docker

```
sudo systemctl start docker
```

