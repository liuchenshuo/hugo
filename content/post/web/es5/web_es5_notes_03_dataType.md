+++
banner = ""
categories = ["前端"]
date = "2021-07-09T09:03:51+02:00"
description = ""
images = []
tags = ["es5规范"]
title = "es5规范以及DOM规范--03数据类型"

+++
# ES5 以及 DOM 规范--03数据类型
> 学习参考链接 https://wangdoc.com/javascript/types/general.html

### 概述

六种基本类型

* 数值（number）：整数以及小数，例如：`1; 3.14`。
* 字符串（string）：文本，例如 `hello`。
* 布尔值（boolean）：表示真伪，两个取值`true; false`。
* undefined：表示未定义或不存在。
* null：表示空值。
* 对象（object）：各种值的集合。

对象可以细分为三个子类

* 狭义对象（object）
* 数组（array）
* 函数（function）

由于函数可以作为一种类型，为**支持函数式**编程提供了基础。

### typeof 运算符

返回对象类型，特殊的 null 类型是 object，这个是由于历史原因，null是后来作为一种特殊数据类型。
