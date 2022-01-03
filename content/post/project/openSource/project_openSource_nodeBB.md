+++
banner = ""
categories = ["开源软件"]
date = "2022-01-01T12:10:51+02:00"
description = ""
images = []
tags = ["开源论坛"]
title = "开源论坛 NodeBB 安装(使用内网数据库)"

+++
# 安装NodeBB论坛（数据库内网配置，无权限）

> 参考：https://www.jianshu.com/p/ab72fe404c8d
>
> 其他论坛：Dizuss （PHP）https://www.discuz.net/

## 0. 前置准备

* 安装docker：参考 http://liuchenshuo.com/2022/01/01/linux-docker-安装

## 1. 安装 mongoBD

> 备份数据库操作：https://www.cnblogs.com/woshimrf/p/docker-install-mongodb-and-backup.html

**先创建所需的 docker 网络**
 `docker network create mongo-net`
创建了一个名字为`mongo-net`的默认网络

可以通过命令：`docker network list` 查看是否创建成功，创建成果结果如下：

```
NETWORK ID     NAME        DRIVER    SCOPE
78a4240d5b93   bridge      bridge    local
b93f96ae1e20   host        host      local
fd99a9463343   mongo-net   bridge    local
ee1974ed8911   none        null      local
```

**安装 mongodb**

**不使用权限，内部网络数据库，现阶段使用**

```
 docker run  \
--name mongo \
--restart always \
--network mongo-net \
-p 27017:27017  \
-v /data/opt/mongodb/data/configdb:/data/configdb/ \
-v /data/opt/mongodb/data/db/:/data/db/ \
-d mongo:4.0 --wiredTigerCacheSizeGB 0.25
```

**数据库备份设置**

全量备份/data/opt/mongodb/data

创建备份目录/data/opt/mongodb/backup/data

```
mkdir -p /data/opt/mongodb/backup/data
```

备份日志目录： /data/opt/mongodb/backup

创建备份脚本： /data/opt/mongodb/backup-mongodb.sh

```
vim /data/opt/mongodb/backup-mongodb.sh
```

拷贝如下内容：

````
#!/bin/bash
LOG_DIR=/data/opt/mongodb/backup
SOURCE_DIR=/data/opt/mongodb/data
BACKUP_DIR=/data/opt/mongodb/backup/data


function log()
{
  echo "[ `date '+%Y-%m-%d %H:%M:%S'` ] $1"
}


# 备份
function main(){
    d=`date "+%Y%m%d%H%M%S"`
    fname=${BACKUP_DIR}/backup_${d}.tgz
    log "开始备份 ${fname}"
    tar -zcf ${fname} ${SOURCE_DIR}


    log "开始删除7天前的备份"
    find ${BACKUP_DIR} -type f  -atime +7 |xargs -t -i rm {}
    log "删除完毕"
}


main >> ${LOG_DIR}/backup.log  2>&1
````

测试备份

```
bash /data/opt/mongodb/backup-mongodb.sh
```

查看备份结果

```
cd /data/opt/mongodb/backup/data
ll
// 可以看到备份结果
... backup_xxx.tgz
```

创建定时任务，每天2点全量备份

> https://blog.csdn.net/renhuan28/article/details/79820281

```
crontab -e
写入
0 2 * * * bash /data/opt/mongodb/backup/backup-mongodb.sh
保存即可
wq
```

**数据库恢复**

启动容器前：拷贝备份文件data目录到

```
// 进入备份目录,注意备份路径解压后是全路径：
cd /data/opt/mongodb/backup/data/data/opt/mongodb
// 解压文件
tar -zxf backup_xxx.tgz
// 拷贝到mongo 数据目录
mv data/ /data/opt/mongodb/
```

然后正常安装即可

* 一定要重新安装mongo 以及nodeBB，并且需要初始化论坛

* 初始化时候需要跟以前数据库配置相同，当前全部使用默认值

## 2. 安装NodeBB

**容器启动NodeBB**

* 对外端口配置：-p 4567:4567
  * 前面4567为物理机端口
  * 后面4567容器内端口

`docker run --restart always --name nodebb --network mongo-net -p 4567:4567 -d nodebb/docker`

**初始化配置**（当前MongDB没有配置权限）

访问 NodeBB

ip:port 这里是 ip:4567

初始化界面如图：

![NodeBB_setup](.\images\NodeBB_setup.png)

1. 创建管理员账户密码

2. 配置数据库
   * **Database Type**：MongoDB
   * **Host IP or address of your MongoDB instance**：mongo（数据库容器名称）
   * **Host port of your MongoDB instance**：27107
   * **MongoDB username**：未使用权限无需填写
   * **Password of your MongoDB database**：未使用权限无需填写
   * **MongoDB database name**：nodebb（使用默认即可）
   
3. 配置论坛

   登录管理员账号，配置即可。
