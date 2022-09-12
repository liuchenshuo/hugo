

+++
banner = ""
categories = ["前端"]
date = "2022-09-10T09:03:51+02:00"
description = ""
images = []
tags = ["es5规范"]
title = "es5规范以及DOM规范--07 标准库"

+++
# ES5 以及 DOM 规范--07 标准库
> 学习参考链接 https://wangdoc.com/javascript/stdlib/index.html

## Object对象

1. 重要静态方法 `Object.keys`

   `Object.keys`方法和`Object.getOwnPropertyNames`方法都用来遍历对象的属性。

   一般两者相同，只有涉及不可枚举属性时，才会有不一样的结果。`Object.keys`方法只返回可枚举的属性，`Object.getOwnPropertyNames`方法还返回不可枚举的属性名。

   示例：

   ```
   var a = ['Hello', 'World'];
   
   Object.keys(a) // ["0", "1"]
   Object.getOwnPropertyNames(a) // ["0", "1", "length"]
   ```

   一般情况下，几乎总是使用`Object.keys`方法，遍历对象的属性。

   示例：

   ```
   var obj = {
     p1: 123,
     p2: 456
   };
   
   Object.keys(obj) // ["p1", "p2"]
   ```

2. 重要实例方法 `Object.prototype.hasOwnProperty()`

   `Object.prototype.hasOwnProperty`方法接受一个字符串作为参数，返回一个布尔值，表示该实例对象自身是否具有该属性。

   示例：

   ```
   var obj = {
     p: 123
   };
   
   // 对象obj自身具有p属性，所以返回true
   obj.hasOwnProperty('p') // true
   
   // oString属性是继承的，所以返回false
   obj.hasOwnProperty('toString') // false
   ```

## 属性描述对象

