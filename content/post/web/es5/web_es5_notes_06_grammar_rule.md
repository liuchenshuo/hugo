

+++
banner = ""
categories = ["前端"]
date = "2022-09-10T09:03:51+02:00"
description = ""
images = []
tags = ["es5规范"]
title = "es5规范以及DOM规范--06 编程风格（个人）"

+++
# ES5 以及 DOM 规范--06 编程风格（个人）
> 学习参考链接 https://wangdoc.com/javascript/features/style.html

## 编程风格（根据个人喜好总结）

1. 缩进：使用tab缩进。

2. 区块：使用大括号划分可能引起歧义的区块。同时为了防止自动添加句末分号引起的问题，推荐区块起首的大括号位置跟在关键字的后面。

   ```
   block {
     // ...
   }
   ```

3. 圆括号：在 JavaScript 中有两种作用，一种表示函数的调用，另一种表示表达式的组合（grouping）。

   为了方便区分，最好遵循如下约束

   * 表示函数调用时，函数名与左括号之间没有空格。
   * 表示函数定义时，函数名与左括号之间没有空格。
   * 其他情况时，前面位置的语法元素与左括号之间，都有一个空格。

   ```
   foo(bar) // 函数定义
   return (a+b); // 返回值
   if (a === 0) {...} // 判断条件
   function foo(b) {...} // 函数调用
   ```

4. 行尾的分号：一般不要省略，除非语法规定本来就不需要在结尾添加分号。例如判断、循环、函数定义等。

5. 全局变量：使用全大写加下划线定义方式 `UPPER_CASE`

6. with语句：尽量不使用，由于大量使用with语句会导致性能的下降，同时也会给代码的调试造成困难，因此在开发大型应用程序的时候，不建议使用with语句。

   语法：with (expression) statement

   示例：

   定义with语句的目的主要是为了简化多次编写同一个对象的工作，如下面的例子

   ```
   var qs = location.search.substring(1);
   var hostName=location.hostname;
   var url =location.href;
   ```

   以上编辑行代码都包含location对象，如果使用with语句，可以把上边的代码改写成如下所示：

   ```
   with(location){
   	var qs = search.subtring(1);
   	var hostName = hostname;
   	var url = href;
   }
   ```

   在这个重写的例子中。使用with语句关联了location对象。这意味着在with语句的代码块的内部，每个变量首先被认为是一个局部的变量，而如果在局部环境中找不到该变量的定义，就会查询location对象中是否有同名的属性。如果发现了同名的属性，则以location对象属性的值作为变量的值。

7. 使用严格相等`===`：防止自动转换类型导致的异常。

8. 减少影响代码理解的**语句合并**：建议不要将不同目的的语句，合并成一行。

   例如下面的例子，虽然效果相同，但是后者容易引起歧义。

   ```
   // 推荐写法
   a = b;
   if (a) {
     // ...
   }
   
   // 语句合并
   if (a = b) {
     // ...
   }
   
   // 容易误理解为
   if （a === b）{
     // ...
   }
   ```

9. 为了代码易于理解，建议自增（`++`）和自减（`--`）运算符尽量使用`+=`和`-=`代替。

   放在变量的前面或后面，返回的值不一样，为了便于理解所以推荐直接加一。

   ```
   ++x
   // 等同于
   x += 1;
   ```

10. `switch...case`结构建议用对象结构代替，减少因为忘记break、没有大括号导致的流程混乱。

    示例，将`switch...case`改写成 对象结构

    ```
    // switch...case 结构
    function doAction(action) {
      switch (action) {
        case 'hack':
          return 'hack';
        case 'slash':
          return 'slash';
        case 'run':
          return 'run';
        default:
          throw new Error('Invalid action.');
      }
    }
    
    // 对象结构
    function doAction(action) {
      var actions = {
        'hack': function () {
          return 'hack';
        },
        'slash': function () {
          return 'slash';
        },
        'run': function () {
          return 'run';
        }
      };
    
      if (typeof actions[action] !== 'function') {
        throw new Error('Invalid action.');
      }
    
      return actions[action]();
    }
    ```
