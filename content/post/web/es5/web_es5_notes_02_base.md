+++
banner = ""
categories = ["前端"]
date = "2021-05-21T09:03:51+02:00"
description = ""
images = []
tags = ["es5规范"]
title = "es5规范以及DOM规范——02基本语法"

+++
# ES5 以及 DOM 规范--02基本语法
> 学习参考链接 https://wangdoc.com/javascript/basic/grammar.html

#### 语句

一般情况下，JavaScript程序的一行就是一个语句。

#### 变量

`var a =1;`

* 变量只有声明 var a; 没有赋值情况下，变量值都是 `undefined` 。

* JavaScript 是动态类型语言，变量类型没有限制，可以随时更改类型。

* 注意变量提升，JavaScript 引擎工作方式，先解析代码，获得所有的声明变量，然后逐行执行，会导致所有变量语句都被提升到代码头部。

  ```
  console.log(a);
  var a = 1;
  不会报错，实际执行为：
  var a;
  console.log(a);
  a = 1;
  ```

#### 标识符

大小写敏感，中文也是合法字符

#### 注释

```
// 1.单行注释
/*
	2.多行
	注释
*/
<!-- 3.也是支持的 -->
```

#### 区块

使用大括号构成区块，不过`var`区块外也生效

```
{ var a= 1}
console.log(a) // 1
```

#### 条件语句

支持 `if else`以及`switch`

switch 中的判断执行的是 `===` 严格相等运算符，而不是`==`所以不会发生类型转化

```
var x= 1;
switch (x) {
  case true:
    console.log('x 发生类型转换');
    break;
  default:
    console.log('x 没有发生类型转换');
}
// x 没有发生类型转换
```

#### 三元运算符

支持 `条件 ? 表达式1 : 表达式2`

#### 循环语句

支持常见三种循环语句

* while 循环
* do ... while 循环
* for 循环

#### 循环中断语句

支持 break 以及 continue语句

#### 标签

JavaScript 允许语句前面带有标签，可以用于程序跳转，标签通常与`break`语句和`continue`语句配合使用

如下示例：跳出双层循环

```
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top;
      console.log('i=' + i + ', j=' + j);
    }
  }
  console.log("next");
```

这里`break`会跳出最外层循环，打印log，如果使用`continue`会继续执行外层循环。
