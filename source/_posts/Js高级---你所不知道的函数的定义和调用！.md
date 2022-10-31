---
title: Js高级---你所不知道的函数的定义和调用！
type: 'tags'
categories: ['Web']
date: 2021-05-17 10:00:00
---

**Code is never die !**

### 1.0 函数的定义方式

- 方式1： 函数声明方式 function 关键字 (命名函数)

  ```js
  function fn(){}
  ```

- 方式2： 函数表达式(匿名函数)

  ```js
  var fn = function(){}
  ```

- 方式3： new Function()  （函数也是对象，所以可以new）（了解）

  ```js
  var f = new Function('a', 'b', 'console.log(a + b)');
  f(1, 2);
  
  var fn = new Function('参数1','参数2'..., '函数体')
  ```

  注意：

  - Function 里面参数都必须是字符串格式
  - 第三种方式执行效率低，也不方便书写，因此较少使用
  - 所有函数都是 Function 的实例(对象)  
  - 函数也属于对象

### 2.0 函数的调用

```js
/* 1. 普通函数 */
function fn() {
	console.log('人生的巅峰');
}
 fn(); 
/* 2. 对象的方法 */
var o = {
  sayHi: function() {
  	console.log('人生的巅峰');
  }
}
o.sayHi();
/* 3. 构造函数*/
function Star() {};
new Star();
/* 4. 绑定事件函数*/
 btn.onclick = function() {};   // 点击了按钮就可以调用这个函数
/* 5. 定时器函数*/
setInterval(function() {}, 1000);  这个函数是定时器自动1秒钟调用一次
/* 6. 立即执行函数(自调用函数)*/
(function() {
	console.log('人生的巅峰');
})();
```

**Ending...**
