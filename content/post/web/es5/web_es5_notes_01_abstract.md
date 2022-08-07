+++
banner = ""
categories = ["前端"]
date = "2021-04-11T09:03:51+02:00"
description = ""
images = []
tags = ["es5规范"]
title = "es5规范以及DOM规范——01入门介绍"

+++
# ES5 以及 DOM 规范--01入门介绍
> 学习参考链接 https://wangdoc.com/javascript/

浏览器的控制台console是可以敲代码运行的，shift + enter 是换行。

JavaScript语言优缺点：[《JavaScript: The Good Parts》](http://javascript.crockford.com/)

#### 语言的产生

1995年5月，Brendan Eich 只用了10天，就设计完成了这种语言的第一版。它是一个大杂烩，语法有多个来源。

- 基本语法：借鉴 C 语言和 Java 语言。
- 数据结构：借鉴 Java 语言，包括将值分成原始值和对象两大类。
- 函数的用法：借鉴 Scheme 语言和 Awk 语言，将函数当作第一等公民，并引入闭包。
- 原型继承模型：借鉴 Self 语言（Smalltalk 的一种变种）。
- 正则表达式：借鉴 Perl 语言。
- 字符串和数组处理：借鉴 Python 语言。

JavaScript 的编程风格是函数式编程和面向对象编程的一种混合体。

#### 个重要时间节点

* 2009年，Node.js 项目诞生，创始人为 Ryan Dahl，它标志着 JavaScript 可以用于服务器端编程，从此网站的前端和后端可以使用同一种语言开发。并且，Node.js 可以承受很大的并发流量，使得开发某些互联网大规模的实时应用变得容易。

* 2010年，三个重要的项目诞生，分别是 NPM、BackboneJS 和 RequireJS，标志着 JavaScript 进入模块化开发的时代。
* 2012年，单页面应用程序框架（single-page app framework）开始崛起，AngularJS 项目，是一款构建[用户界面](https://baike.baidu.com/item/用户界面/6582461)的[前端](https://baike.baidu.com/item/前端/5956545)JS框架，后为[Google](https://baike.baidu.com/item/Google/86964)所收购。同时 Ember 项目也发布了1.0版本。
* 2013年5月，Facebook 发布 UI 框架库 React，引入了新的 JSX 语法，使得 UI 层可以用组件开发，同时引入了网页应用是状态机的概念。
* 2014年，Vue 框架诞生，他的作者为中国人–尤雨溪(江苏无锡人)
