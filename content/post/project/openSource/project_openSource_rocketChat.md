+++
banner = ""
categories = ["开源软件"]
date = "2022-01-02T12:10:51+02:00"
description = ""
images = []
tags = ["开源聊天室"]
title = "开源聊天室 RocketChat 安装"

+++
# 开源聊天室 RocketChat 安装
参考资料
> 官方使用Docker 部署说明 https://hub.docker.com/_/rocket-chat

> 官网：https://rocket.chat/

> git 地址：https://github.com/RocketChat/Rocket.Chat#docker

### 安装mongo
默认容器网络启动一个名为**db**的mongo数据库，必须是这个名字，其他的就需要制定mongo链接地址了，详细参考上面 **官方使用Docker 部署说明**

```
docker run --name db -d mongo:4.0 --smallfiles --replSet rs0 --oplogSize 128
```

初始化  replicaSet:

```
docker exec -ti db mongo --eval "printjson(rs.initiate())"
```

### 安装 RocketChat

*  -p 3000:3000 第一个3000为物理机端口，第二个为容器端口
* --link db：db即为上面创建的mongo 容器
* ROOT_URL=http://110.40.173.22：物理机的ip即外部访问ip
```$xslt
docker run --name rocketchat -p 3000:3000 --link db --env ROOT_URL=http://110.40.173.22 --env MONGO_OPLOG_URL=mongodb://db:27017/local -d rocket.chat
```

