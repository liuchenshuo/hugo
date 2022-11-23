

+++
banner = ""
categories = ["前端"]
date = "2022-10-01T09:52:51+02:00"
description = ""
images = []
tags = ["es5规范"]
title = "es5规范以及DOM规范--07-2 标准库"

+++
# ES5 以及 DOM 规范--07-2 标准库
> 学习参考链接 https://wangdoc.com/javascript/stdlib/index.html

标准库主要对象

* Object 对象
* 属性描述对象
* Array 对象

* 包装对象
* Boolean 对象
* Number 对象
* String 对象
* Math 对象
* Date 对象
* RegExp 对象
* JSON 对象

## 包装对象

对象是 JavaScript 语言最主要的数据类型，三种原始类型的值——数值、字符串、布尔值——在一定条件下，也会自动转为对象，也就是原始类型的“包装对象”（wrapper）。

所谓“包装对象”，指的是与数值、字符串、布尔值分别相对应的`Number`、`String`、`Boolean`三个原生对象。这三个原生对象可以把原始类型的值变成（包装成）对象。

包装对象的设计目的，首先是使得“对象”这种类型可以覆盖 JavaScript 所有的值，整门语言有一个通用的数据模型，其次是使得原始类型的值也有办法调用自己的方法。

某些场合，原始类型的值会自动当作包装对象调用，即调用包装对象的属性和方法。这时，JavaScript 引擎会自动将原始类型的值转为包装对象实例，并在使用后立刻销毁实例。

```
// valueOf() 方法
new String('abc').valueOf() // "abc"

// toString() 方法
new String('abc').toString() // "abc"

// 自动将原始类型的值转为包装对象实例
'abc'.length // 3
```

### Boolean 对象

注意 是否加 new 的区别

```
if (new Boolean(false)) {
  console.log('true');
} // true

if (new Boolean(false).valueOf()) {
  console.log('true');
} // 无输出
```

上面代码的第一个例子之所以得到`true`，是因为`false`对应的包装对象实例是一个对象，进行逻辑运算时，被自动转化成布尔值`true`（因为所有对象对应的布尔值都是`true`）。而实例的`valueOf`方法，则返回实例对应的原始值，本例为`false`。

### Number 对象

