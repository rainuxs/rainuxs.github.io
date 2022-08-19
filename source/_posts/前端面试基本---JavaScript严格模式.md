---
title: 前端面试基本---JavaScript严格模式
type: 'tags'
categories: ['Web']
date: 2022-05-08 16:00:00
---

**Code is never die !**

### 1.0 什么是严格模式

- JavaScript 除了提供正常模式外，还提供了**严格模式**（strict mode）。
- ES5 的严格模式是采用具有限制性 JavaScript 变体的一种方式，即在严格的条件下运行 JS 代码。
- 严格模式在 IE10 以上版本的浏览器中才会被支持，旧版本浏览器中会被忽略。

- 严格模式对正常的 JavaScript 语义做了一些更改：
  - 1.消除了 Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为。
  - 2.消除代码运行的一些不安全之处，保证代码运行的安全。
  - 3.提高编译器效率，增加运行速度。
  - 4.禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class,enum,export, extends, import, super 不能做变量名

### 2.0 开启严格模式

严格模式可以应用到整个脚本或个别函数中。

因此在使用时，我们可以将严格模式分为为**脚本开启严格模式**和**为函数开启严格模式**两种情况。

- 情况一 ：为脚本开启严格模式

  - 有的 script 脚本是严格模式，有的 script 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他
    script 脚本文件。

    ```js
    (function (){
      //在当前的这个自调用函数中有开启严格模式，当前函数之外还是普通模式
    　　　　"use strict";//use使用，strict严格。使用严格模式
           var num = 10;
    　　　　function fn() {}
    })();
    //或者
    <script>
      　"use strict"; //当前script标签开启了严格模式
    </script>
    <script>
      			//当前script标签未开启严格模式
    </script>
    ```

- 情况二：为函数开启严格模式

  - 要给某个函数开启严格模式，需要把“use strict”; (或 'use strict'; ) 声明放在函数体所有语句之前。

    ```js
    function fn() {
    	'use strict'; //当前fn函数开启了严格模式
    	return '123';
    }
    ```

### 3.0 严格模式中的变化

严格模式对 Javascript 的语法和行为，都做了一些改变。

1. 变量规定

   ① 在正常模式中，如果一个变量没有声明就赋值，默认是全局变量。严格模式禁止这种用法，变量都必须先用

   var 命令声明，然后再使用。

   ② 严禁删除已经声明变量。例如，delete x; 语法是错误的。

2. 严格模式下 this 指向问题

   ① 以前在全局作用域函数中的 this 指向 window 对象。

   ② **严格模式下全局作用域中函数中的 this 是 undefined。**

   ③ 以前构造函数时不加 new 也可以 调用,当普通函数，this 指向全局对象

   ④ 严格模式下,如果 构造函数不加 new 调用, this 指向的是 undefined 如果给他赋值则 会报错

   ⑤ new 实例化的构造函数指向创建的对象实例。

   ⑥ 定时器 this 还是指向 window 。

   ⑦ 事件、对象还是指向调用者。

代码：

```js
<script>
    'use strict';
    // 1. 我们的变量名必须先声明再使用
    // num = 10;
    // console.log(num);
    var num = 10;
    console.log(num);
    // 2.我们不能随意删除已经声明好的变量
    // delete num;
    // 3. 严格模式下全局作用域中函数中的 this 是 undefined。
    // function fn() {
    //     console.log(this); // undefined。

    // }
    // fn();
    // 4. 严格模式下,如果 构造函数不加new调用, this 指向的是undefined 如果给他赋值则 会报错.
    // function Star() {
    //     this.sex = '男';
    // }
    // // Star();
    // var ldh = new Star();
    // console.log(ldh.sex);
    // 5. 定时器 this 还是指向 window
    // setTimeout(function() {
    //     console.log(this);

    // }, 2000);
    // a = 1;
    // a = 2;
    // 6. 严格模式下函数里面的参数不允许有重名
    // function fn(a, a) {
    //     console.log(a + a);

    // };
    // fn(1, 2);
    function fn() {}
</script>
```

[更多严格模式要求点击参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)

**Ending...**
