## How to start dev
根目录执行命令
```bash
hugo server --theme=hugo-icarus --buildDrafts
```
访问地址：`http://localhost:1313`

## How to deploy
使用nginx直接访问，根目录执行命令
```bash
hugo --theme=hugo-icarus --baseUrl="http://39.99.40.78:1313/"
```
将生成的文件夹 `public` 拷贝到服务即可
* 服务器：39.99.40.78
* 地址：`/home/hugo`

**nginx 配置**
```
    # 博客访问配置
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

    # 域名配置
    server {
        listen  80;
        server_name  liuchenshuo.com;
        location / {
            proxy_pass http://localhost:1313;
        }
    }
```
