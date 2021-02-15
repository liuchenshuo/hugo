+++
banner = ""
categories = ["个人网站"]
date = "2021-02-12T12:10:51+02:00"
description = ""
images = []
tags = ["软件安装"]
title = "使用Hugo搭建个人博客"

+++
## 使用Hugo搭建个人博客
**写在前面**

个人博客项目有很多

* wordpress（php编写）

* gitBook（git hub支持）

* hugo（go编写）

* .......

其实博客项目一般不需要自己修改源码，自己需要深度定制除外。这里因为仅仅需要存放一些个人md文档，所以在gitBook以及hugo之间进行选择，gitBook界面比较近简单，这里就选取了hugo。

## Hugo介绍

> 英文官方文档：https://gohugo.io/overview/introduction/
>
> 中文官方文档：https://www.gohugo.org/
>
> 皮肤列表：https://github.com/spf13/hugoThemes

Hugo是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。

最喜欢的一点是：博客文章可以以文本文件的方式（MarkDown）在本地维护管理，不需要像之前那样在网页的编辑器里提交到网站数据库。你可以方便的使用github管理你的博客文章，不会丢失，又能追溯到每一次的内容变更。

## 搭建过程 （Windows）

### 下载安装包并安装

> git上的最新地址：https://github.com/gohugoio/hugo/releases
>
> 0.80版本Windows百度云：

下载正常版本即可，对应的extended版本还没搞懂有什么特别的。

下载的是对应的压缩包，解压后进入，**不知道是不是我点击exe没有安装，还是就不会安装，我这里将hugo.exe添加到了系统环境变量path中（重启计算机生效）这样hugo命令在cmd中才会生效，当然进入到hugo.exe的文件夹，输入`cmd`打开命令行也可以，不过后面操作有的就需要输入绝对路径了**

### 生成站点

使用Hugo快速生成站点，比如希望生成到`G:\workspace\hugo` 路径：

```cmd
hugo new site G:\workspace\hugo
```

成功后会有提示：Congratulations! Your new Hugo site is created in G:\workspace\hugo.

这样就在 ` G:\workspace\hugo.` 目录里生成了初始站点，进去目录：

```bash
cd  G:\workspace\hugo
```

站点目录结构：

```
  ▸ archetypes/
  ▸ content/
  ▸ static/
  ▸ layouts/
  ▸ static/
  ▸ themes/
    config.toml
```

### 创建文章

创建一个 `about` 页面（要进入到站点目录，我这里是` G:\workspace\hugo`）：

```bash
hugo new about.md
```

`about.md` 自动生成到了 `content/about.md` ，打开 `about.md` 看下：

```
---
date = "2015-10-25T08:36:54-07:00"
draft = true
title = "about"

---

正文内容
```

内容是 `Markdown` 格式的，`+++` 之间的内容是 [TOML](https://github.com/toml-lang/toml) 格式的，根据你的喜好，你可以换成 [YAML](http://www.yaml.org/) 格式（使用 `---` 标记）或者 [JSON](http://www.json.org/) 格式。

创建第一篇文章，放到 `post` 目录，方便之后生成聚合页面。

```bash
hugo new post/first.md
```

打开编辑 `post/first.md` ：

```
---
date: "2015-10-25T08:36:54-07:00"
title: "first"
 
---

### Hello Hugo

 1. aaa
 1. bbb
 1. ccc
```

### 安装皮肤

到 [皮肤列表](https://www.gohugo.org/theme/) 挑选一个心仪的皮肤，比如你觉得 哪款相关的 `GitHub` 地址，创建目录 `themes`，在 `themes` 目录里把皮肤 `git clone` 下来：

我这里使用的是：hugo-icarus-theme

> git地址：https://gitlab.com/toryanderson/hugo-icarus

```bash
# 创建 themes 目录
cd themes
git clone https://gitlab.com/toryanderson/hugo-icarus
```

#### 皮肤配置

这个皮肤需要进行一些配置

1. 进入皮肤的示例目录：`themes/hugo-type-theme/exampleSite/`

2. 将示例目录`exampleSite/`下面的内容全部拷贝到站点根目录中

3. 修改站点根目录中的配置文件：**`config.toml`**

   将里面的 `themesDir = "../.."` 注释掉，这个是为了启动demo使用的

### 运行Hugo

在你的站点根目录执行 `Hugo` 命令进行调试：

```bash
hugo server --theme=hugo-icarus --buildDrafts
```

（注明：v0.15 版本之后，不再需要使用 `--watch` 参数了）

浏览器里打开： `http://localhost:1313`

### 根据自己需要进行配置

参考对应的主题配置文档即可，这里hugo-icarus-theme文档

https://gitlab.com/toryanderson/hugo-icarus

中文翻译参考：

### 部署

一般推荐GitHub Pages我这里是自己服务器部署，直接使用Nginx作为服务部署

> 参考：https://blog.csdn.net/homography/article/details/106168190

如何安装Nginx以及配置参考：http://liuchenshuo.com/2021/02/14/nginx-linux-%E5%AE%89%E8%A3%85/

**生成静态网站**

执行命令

```bash
hugo --theme=hugo-icarus --baseUrl="http://39.99.40.78:1313/"
```

说明：

* --theme：制定主题
* --baseUrl：制定访问url，这个很重要，制定是如何访问的，比如我是使用云服务器nginx代理1313端口反问，如果不写baseUrl界面渲染就会有问题，什么原理暂时没有搞懂，后面看看源码吧。
