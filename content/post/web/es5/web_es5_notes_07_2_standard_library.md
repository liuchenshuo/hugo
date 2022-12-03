

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

## Boolean 对象

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

## Number 对象

几个重要静态属性

- `Number.POSITIVE_INFINITY`：正的无限，指向`Infinity`。
- `Number.NEGATIVE_INFINITY`：负的无限，指向`-Infinity`。
- `Number.NaN`：表示非数值，指向`NaN`。
- `Number.MIN_VALUE`：表示最小的正数（即最接近0的正数，在64位浮点数体系中为`5e-324`），相应的，最接近0的负数为`-Number.MIN_VALUE`。
- `Number.MAX_SAFE_INTEGER`：表示能够精确表示的最大整数，即`9007199254740991`。
- `Number.MIN_SAFE_INTEGER`：表示能够精确表示的最小整数，即`-9007199254740991`。

### Number.prototype.toString() 转换进制应用

toString 方法可以接受一个参数，表示输出的进制。如果省略这个参数，默认将数值先转为十进制，再输出字符串；否则，就根据参数指定的进制，将一个数字转化成某个进制的字符串。方法只能将十进制的数，转为其他进制的字符串。如果要将其他进制的数，转回十进制，需要使用`parseInt`方法。

```
(10).toString(2) // "1010"
(10).toString(8) // "12"
(10).toString(16) // "a"

# 一定要增加括号
10.toString(2)
// SyntaxError: Unexpected token ILLEGAL
```

上面代码中，`10`一定要放在括号里，这样表明后面的点表示调用对象属性。如果不加括号，这个点会被 JavaScript 引擎解释成小数点，从而报错。

### Number.prototype.toFixed() 转为指定位数的小数

`js`的`Number.toFixed()`实际的精度确认规则是四舍六入五成双，逢四下舍，逢六入一，逢五时，根据浏览器内核计算结果也不尽相同。

```
(10.055).toFixed(2) // 10.05
(10.005).toFixed(2) // 10.01
```

`toFixed()`方法的参数为小数位数，有效范围为0到100，超出这个范围将抛出 RangeError 错误。

由于浮点数的原因，小数`5`的四舍五入是不确定的，使用的时候必须小心。

### Number.prototype.toPrecision() 转为指定位数的有效数字

跟 fixed() 方法有一样的问题，四舍五入不可靠，同样范围是1到100，超出这个范围会抛出 RangeError 错误。

```
(12.35).toPrecision(3) // "12.3"
(12.25).toPrecision(3) // "12.3"
(12.15).toPrecision(3) // "12.2"
(12.45).toPrecision(3) // "12.4"
```

## String 对象

### String.prototype.concat() 字符串连接方法

`concat`方法用于连接两个字符串，返回一个新字符串，不改变原字符串。该方法可以接受多个参数。如果参数不是字符串，`concat`方法会将其先转为字符串，然后再连接。

```
var one = 1;
var two = 2;
var three = '3';

''.concat(one, two, three) // "123"
# 跟普通相加区别
one + two + three // "33"
```

### String.prototype.localeCompare() 

比较两个字符串。它返回一个整数，如果小于0，表示第一个字符串小于第二个字符串；如果等于0，表示两者相等；如果大于0，表示第一个字符串大于第二个字符串。该方法的最大特点，就是会考虑自然语言的顺序。举例来说，正常情况下，大写的英文字母小于小写字母。

```
'apple'.localeCompare('banana') // -1
'apple'.localeCompare('apple') // 0
```