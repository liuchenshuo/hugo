

+++
banner = ""
categories = ["前端"]
date = "2022-09-11T09:03:51+02:00"
description = ""
images = []
tags = ["js相关语法详解"]
title = "js相关语法详解--01 call()、apply()、bind()语法"

+++
# js相关语法详解--01 call()、apply()、bind()语法
> 学习参考链接：前置学习函数解释 https://www.w3school.com.cn/js/js_function_invocation.asp
>
> 学习参考链接：call() 语法学习 https://www.w3school.com.cn/js/js_function_call.asp
>
> 学习参考链接：Apply() 语法学习 https://www.w3school.com.cn/js/js_function_call.asp
>
> 学习参考链接：比较好的语法解释 https://blog.csdn.net/wkl115211/article/details/80255967
>
> 学习参考链接：比较好的示例 https://www.runoob.com/w3cnote/js-call-apply-bind.html

一般来说，call()、apply()、bind() 三个方法都是一起介绍，因为用法类似，只是有细微差距。

所有函数（这里说的函数是指对象以及对象的方法）都具有call()、apply()、bind() 三个方法。他们可以在执行方法时候用一个值指向this，并改变面向对象的作用域。

## call() 语法

* `call()` 方法是预定义的 JavaScript 方法。

* 它可以用来调用所有者对象作为参数的方法。

* 通过 `call()`，您能够使用属于另一个对象的方法。

* call() 方法可接受参数。

示例：

```
// 定义一个 person 对象
var person = {
    firstName:"Bill",
    lastName: "Gates",
    fullNameWithAge: function (age) {
        return this.firstName + " " + this.lastName+ ", age: " + age;
    }
}
// 执行对象内部函数
person.fullNameWithAge(30)	// 将返回 "Bill Gates, age:30

// 定一个新的 personCall 对象
var personCall = {
    firstName:"Steve",
    lastName: "Jobs",
}
// 使用call方法传入新的对象作为this执行方法
// call() 使用参数 20
person.fullNameWithAge.call(personCall, 20)
```

## apply() 语法

`apply()` 方法与 `call()` 方法非常相似，只是参数不同。

不同之处是：

* `call()` 方法分别接受参数。

* `apply()` 方法接受数组形式的参数。

如果要使用数组而不是参数列表，则 `apply()` 方法非常方便。

示例：

```
// 定义一个 person 对象
var person = {
    firstName:"Bill",
    lastName: "Gates",
    fullNameWithAge: function (age) {
        return this.firstName + " " + this.lastName+ ", age: " + age;
    }
}
// 执行对象内部函数
person.fullNameWithAge(30)	// 将返回 "Bill Gates, age:30

// 定一个新的 personApply 对象
var personApply = {
    firstName:"Steve",
    lastName: "Jobs",
}
// 使用apply方法传入新的对象作为this执行方法，这里注意参数要是数组
// call() 使用参数 20
person.fullNameWithAge.apply(personApply, [20])
```

一个常用的场景：在数组上模拟 max 方法，由于 JavaScript 数组没有 max() 方法，因此您可以使用apply()方法应用 `Math.max()` 方法。

示例：

```
// 正常使用 Math 函数
Math.max(1,2,3);  // 会返回 3
// 借用 apply 使用 Math 函数
Math.max.apply(Math, [1,2,3]); // 也会返回 3
// 使用es6语法也是可以的，将数组转换为正常参数
Math.max(...[1,2,3]);  // 会返回 3
```

## bind() 语法

`apply()` 方法与 `call()` 方法参数方面完全一样，只是返回的是一个函数需要增加括号直行。

示例：

```
// 定义一个 person 对象
var person = {
    firstName:"Bill",
    lastName: "Gates",
    fullNameWithAge: function (age) {
        return this.firstName + " " + this.lastName+ ", age: " + age;
    }
}
// 执行对象内部函数
person.fullNameWithAge(30)	// 将返回 "Bill Gates, age:30

// 定一个新的 personBind 对象
var personBind = {
    firstName:"Steve",
    lastName: "Jobs",
}
// 使用bind方法传入新的对象作为this执行方法，这里注意返回的是函数，需要加括号执行
// bind() 使用参数 20
person.fullNameWithAge.bind(personBind, 20)()
```

## 总结

call 、bind 、 apply 这三个函数的第一个参数都是 this 的指向对象，第二个参数差别就来了：

* call 的参数是直接放进去的，第二第三第 n 个参数全都用逗号分隔，直接放到后面 **person.fullNameWithAge.call(personCall, 20, ..., 'string' )**。

* apply 的所有参数都必须放在一个数组里面传进去 **person.fullNameWithAge.apply(personCall, [20, ..., 'string'] )**。

* bind 除了返回是函数以外，它 的参数和 call 一样**person.fullNameWithAge.bind(personCall, 20, ..., 'string' )()**。

当然，三者的参数不限定是 string 类型，允许是各种类型，包括函数 、 object 等等！
