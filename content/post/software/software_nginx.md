+++
banner = ""
categories = ["工具软件"]
date = "2021-02-14T20:06:22+02:00"
description = ""
images = []
tags = ["软件安装"]
title = "Nginx linux 安装"

+++
## Linux 安装 Nginx

### CentOs 安装

```bash
yum install nginx
```

### Linux 安装

```bash
apt install nginx
```

### 配置文件位置

通过系统命令安装的会默认生成到 `/etc/nginx`

其他的配置 目录中的 `nginx.conf` 即可。

### Nginx 基本命令

```bash
nginx -s reload  //修改完成后重加载配置文件
nginx -t  //检查修改后的nginx配置
systemctl start nginx  //启动 nginx 服务
systemctl status nginx  //检查 nginx 服务的运行情况
systemctl restart nginx  //重启 nginx 服务
```



### 其他配置

1. 配置支持https

   ```bash
   在服务器目录 /etc/nginx 中生成私钥: openssl genrsa -out rulenuts.key.
   根据私钥生成证书（公钥）: openssl req -new -x509 -key rulenuts.key -out rulenuts.crt.
   ```

2. 本地支持hugo静态网页配置示例

   按类似如下形式修改服务器 nginx 的配置文件: `vim /etc/nginx/nginx.conf`.

   ```
       server {
           listen  1313;
           server_name  localhost;
           location / {
               root   /home/hugo/public;
               index  index.html index.htm;
           }
           error_page  404  /404.html;
           location = /404.html {
               root  /home/hugo/public;
           }
       }
   ```
   域名重定向
   ```bash
    server {
        listen  80;
        server_name  liuchenshuo.com;
        location / {
            proxy_pass http://localhost:1313;
        }
    }
   ```

