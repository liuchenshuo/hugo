

+++
banner = ""
categories = ["前端"]
date = "2022-09-10T09:03:51+02:00"
description = ""
images = []
tags = ["es5规范"]
title = "es5规范以及DOM规范--07-1 标准库"

+++
# ES5 以及 DOM 规范--07-1 标准库
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

## Object对象

1. 重要静态方法 `Object.keys`

   `Object.keys`方法和`Object.getOwnPropertyNames`方法都用来遍历对象的属性。

   一般两者相同，只有涉及不可枚举属性时，才会有不一样的结果。`Object.keys`方法只返回可枚举的属性，`Object.getOwnPropertyNames`方法返回不可枚举的属性名。

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
   
   // toString属性是继承的，所以返回false
   obj.hasOwnProperty('toString') // false
   ```

## 属性描述对象

javaScript 提供了一个内部数据结构，用来描述对象的属性，控制它的行为，比如该属性是否可写、可遍历等等。这个内部数据结构称为“属性描述对象”（attributes object）。每个属性都有自己对应的属性描述对象，保存该属性的一些元信息。

`Object.getOwnPropertyDescriptor()`方法可以获取属性描述对象。它的第一个参数是目标对象，第二个参数是一个字符串，对应目标对象的某个属性名。

```
var obj = { p: 'a' };
// 获取描述属性
Object.getOwnPropertyDescriptor(obj, 'p')
返回结果
// Object { value: "a",
//   writable: true,
//   enumerable: true,
//   configurable: true
// }
```

## Array 对象

`Array()`作为构造函数，行为很不一致。因此，不建议使用它生成新数组，直接使用数组字面量是更好的做法。

```
// bad
var arr = new Array(1, 2);

// good
var arr = [1, 2];
```

### pop() 方法

`pop`方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组。

`push`和`pop`结合使用，就构成了“后进先出”的栈结构（stack）。

```
var arr = [];
arr.push(1, 2);
arr.push(3);
arr.pop();
arr // [1, 2]
```

上面代码中，`3`是最后进入数组的，但是最早离开数组。

### shift() 方法

`shift()`方法用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组。

`push()`和`shift()`结合使用，就构成了“先进先出”的队列结构（queue）。

`push`和`pop`结合使用，就构成了“后进先出”的栈结构（stack）。

```
var arr = [];
arr.push(1, 2);
arr.push(3);
arr.shift();
arr // [2, 3]
```

上面代码中，`3`是最后进入数组的，但是最早离开数组。

### unshift() 方法

`unshift()`方法可以接受多个参数，这些参数都会添加到目标数组头部。注意，该方法会改变原数组。

```
var arr = [ 'c', 'd' ];
arr.unshift('a', 'b') // 4
arr // [ 'a', 'b', 'c', 'd' ]
```

### join() 方法

`join()`方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。

```
var a = [1, 2, 3, 4];

a.join(' ') // '1 2 3 4'
a.join(' | ') // "1 | 2 | 3 | 4"
a.join() // "1,2,3,4"
```

### concat() 方法

`concat`方法用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。

```
['hello'].concat(['world'], ['!'])
// ["hello", "world", "!"]

[].concat({a: 1}, {b: 2})
// [{ a: 1 }, { b: 2 }]

[1, 2, 3].concat(4, 5, 6)
// [1, 2, 3, 4, 5, 6]
```

### reverse() 方法

`reverse`方法用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组。

```
var a = ['a', 'b', 'c'];

a.reverse() // ["c", "b", "a"]
a // ["c", "b", "a"]
```

### slice() 方法

`slice()`方法用于提取目标数组的一部分，返回一个新数组，原数组不变。如果`slice()`方法的参数是负数，则表示倒数计算的位置。

```
arr.slice(start, end);

var a = ['a', 'b', 'c'];

a.slice(0) // ["a", "b", "c"]
a.slice(1) // ["b", "c"]
a.slice(1, 2) // ["b"]
a.slice(2, 6) // ["c"]
a.slice() // ["a", "b", "c"]

a.slice(-2) // ["b", "c"]
a.slice(-2, -1) // ["b"]
```

它的第一个参数为起始位置（从0开始，会包括在返回的新数组之中），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员。

### splice() 方法

`splice()`方法用于删除原数组的一部分成员，并可以在删除的位置添加新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组。起始位置如果是负数，就表示从倒数位置开始删除。

```
arr.splice(start, count, addElement1, addElement2, ...);

var a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.splice(4, 2, 1, 2) // ["e", "f"]
a // ["a", "b", "c", "d", 1, 2]

var b = ['a', 'b', 'c', 'd', 'e', 'f'];
b.splice(-4, 2) // ["c", "d"]
```

`splice`的第一个参数是删除的起始位置（从0开始），第二个参数是被删除的元素个数。如果后面还有更多的参数，则表示这些就是要被插入数组的新元素。

### sort() 方法

`sort`方法对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。

`sort`的参数函数本身接受两个参数，表示进行比较的两个数组成员。如果该函数的返回值大于`0`，表示第一个成员排在第二个成员后面；其他情况下，都是第一个元素排在第二个元素前面。

```
['d', 'c', 'b', 'a'].sort()
// ['a', 'b', 'c', 'd']

[10111, 1101, 111].sort(function (a, b) {
  return a - b;
})
// [111, 1101, 10111]
```

### map() 方法

`map()`方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。

```
var numbers = [1, 2, 3];

numbers.map(function (n) {
  return n + 1;
});
// [2, 3, 4]

numbers
// [1, 2, 3]
```

### forEach() 方法

`forEach()`方法与`map()`方法很相似，也是对数组的所有成员依次执行参数函数。但是，`forEach()`方法不返回值，只用来操作数据。这就是说，如果数组遍历的目的是为了得到返回值，那么使用`map()`方法，否则使用`forEach()`方法。

### filter() 方法

`filter()`方法用于过滤数组成员，满足条件的成员组成一个新数组返回。

它的参数是一个函数，所有数组成员依次执行该函数，返回结果为`true`的成员组成一个新数组返回。该方法不会改变原数组。

```
[1, 2, 3, 4, 5].filter(function (elem) {
  return (elem > 3);
})
// [4, 5]
```

### some() , every() 方法

这两个方法类似“断言”（assert），返回一个布尔值，表示判断数组成员是否符合某种条件。

它们接受一个函数作为参数，所有数组成员依次执行该函数。该函数接受三个参数：当前成员、当前位置和整个数组，然后返回一个布尔值。

`some`方法是只要一个成员的返回值是`true`，则整个`some`方法的返回值就是`true`，否则返回`false`。

```
var arr = [1, 2, 3, 4, 5];
arr.some(function (elem, index, arr) {
  return elem >= 3;
});
// true

arr.every(function (elem, index, arr) {
  return elem >= 3;
});
// false
```

### reduce(), reduceRight() 方法

 `reduce()`方法和`reduceRight()`方法依次处理数组的每个成员，最终累计为一个值。它们的差别是，`reduce()`是从左到右处理（从第一个成员到最后一个成员），`reduceRight()`则是从右到左（从最后一个成员到第一个成员），其他完全一样。

如果要对累积变量指定初值，可以把它放在`reduce()`方法和`reduceRight()`方法的第二个参数。建议总是加上第二个参数，这样比较符合直觉，每个数组成员都会依次执行`reduce()`方法的参数函数。另外，第二个参数可以防止空数组报错。

```
// 函数说明
[1, 2, 3, 4, 5].reduce(function (
  a,   // 累积变量，必须
  b,   // 当前变量，必须
  i,   // 当前位置，可选
  arr  // 原数组，可选
) {
  // ... ...
  
// 示例
[1, 2, 3, 4, 5].reduce(function (a, b) {
  console.log(a, b);
  return a + b;
}, 0)
// 0 1
// 1 2
// 3 3
// 6 4
// 10 5
//最后结果：15
```

### indexOf(), lastIndexOf() 方法

`indexOf`方法返回给定元素在数组中第一次出现的位置，如果没有出现则返回`-1`。

`indexOf`方法还可以接受第二个参数，表示搜索的开始位置。

`lastIndexOf`方法返回给定元素在数组中最后一次出现的位置，如果没有出现则返回`-1`。

```
var a = ['a', 'b', 'c', 'a'];

a.indexOf('b') // 1
a.indexOf('y') // -1
a.indexOf('a', 1) // -1

a.lastIndexOf('a') // 3
a.lastIndexOf('y') // -1
```



