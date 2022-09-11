

+++
banner = ""
categories = ["前端"]
date = "2022-08-20T09:03:51+02:00"
description = ""
images = []
tags = ["es5规范"]
title = "es5规范以及DOM规范--05 语法介绍"

+++
# ES5 以及 DOM 规范--05 语法介绍
> 学习参考链接 https://wangdoc.com/javascript/features/conversion.html

## 数据类型的转换

JavaScript 是一种动态类型语言，变量没有类型限制，可以随时赋予任意值。

```
var x = y ? 1 : 'a';
```

### 强制转换方法

强制转换主要指使用

* `Number()`：转换数字

* `String()`：转换字符串

* `Boolean()`：转换布尔值

注意：`Boolean()`函数可以将任意类型的值转为布尔值。

它的转换规则相对简单：除了以下五个值的转换结果为`false`，其他的值全部为`true`。

- `undefined`
- `null`
- `0`（包含`-0`和`+0`）
- `NaN`
- `''`（空字符串）

由于自动转换具有不确定性，而且不易除错，建议在预期为布尔值、数值、字符串的地方，全部使用`Boolean()`、`Number()`和`String()`函数进行显式转换。

## 错误处理机制

常见错误类型

* `SyntaxError`对象是解析代码时发生的语法错误

* `ReferenceError`对象是引用一个不存在的变量时发生的错误。

* `RangeError`对象是一个值超出有效范围时发生的错误。主要有几种情况，一是数组长度为负数，二是`Number`对象的方法参数超出范围，以及函数堆栈超过最大值。

* `TypeError`对象是变量或参数不是预期类型时发生的错误。比如，对字符串、布尔值、数值等原始类型的值使用`new`命令，就会抛出这种错误，因为`new`命令的参数应该是一个构造函数。

* `URIError`对象是 URI 相关函数的参数不正确时抛出的错误，主要涉及`encodeURI()`、`decodeURI()`、`encodeURIComponent()`、`decodeURIComponent()`、`escape()`和`unescape()`这六个函数。

* `eval`函数没有被正确执行时，会抛出`EvalError`错误。该错误类型已经不再使用了，只是为了保证与以前代码兼容，才继续保留。

  * `eval()` 函数计算或执行参数。

    如果参数是表达式，则 `eval()` 计算表达式。如果参数是一个或多个 JavaScript 语句，则 `eval()` 执行这些语句。

    ```
    // 传入字符串形式 JS 语句
    console.log(eval('const a = 0')); // undefined
    
    // 传入字符串形式 JS 表达式
    console.log(eval('1 + 1')); // 2
    console.log(eval('(() => 3)()')); // 3
    
    // 传入非字符串
    console.log(eval({ a: 1 })); // {a: 1}
    ```

错误处理机制

正常使用`try...catch...finally`机制

## console 对象与控制台

1. `console.log`打印调试信息

   * 接受一个或多个参数，将它们连接起来输出

   * 打印信息每次调用后自动换行

   * 支持占位符

     - `%s` 字符串
     - `%d` 整数
     - `%i` 整数
     - `%f` 浮点数
     - `%o` 对象的链接
     - `%c` CSS 格式字符串

     ```
     //  1 + 1 = 2
     console.log(' %s + %s = %s', 1, 1, 2)
     
     // 1 + 1  = 2
     console.log(' %s + %s ', 1, 1, '= 2')
     
     // 使用%c占位符时，对应的参数必须是 CSS 代码，用来对输出内容进行 CSS 渲染。
     console.log(
       '%cThis text is styled!',
       'color: red; background: yellow; font-size: 24px;'
     )
     ```

2. `console.table()`：对于某些复合类型的数据，可以将其转为表格显示。

   示例：

   ```
   var languages = [
     { name: "JavaScript", fileExtension: ".js" },
     { name: "TypeScript", fileExtension: ".ts" },
     { name: "CoffeeScript", fileExtension: ".coffee" }
   ];
   
   console.table(languages);
   ```

3. `console.count()`：用于计数，输出它被调用了多少次。

   示例：可以接受一个字符串作为参数，作为标签，对执行次数进行分类

   ```
   function greet(user) {
     console.count(user);
     return "hi " + user;
   }
   
   greet('bob')
   // bob: 1
   // "hi bob"
   
   greet('alice')
   // alice: 1
   // "hi alice"
   
   greet('bob')
   // bob: 2
   // "hi bob"
   ```

4. `console.time()，console.timeEnd()`：用于计时，可以算出一个操作所花费的准确时间。

   示例：

   ```
   console.time('Array initialize');
   
   var array= new Array(1000000);
   for (var i = array.length - 1; i >= 0; i--) {
     array[i] = new Object();
   };
   
   console.timeEnd('Array initialize');
   // Array initialize: 1914.481ms
   ```

5. `clear()`：清除控制台的历史。可以在打印前进行控制台清空操作。

6. `debugger`：Chrome 浏览器中，当代码运行到`debugger`语句时，就会暂停运行，自动打开脚本源码界面。

