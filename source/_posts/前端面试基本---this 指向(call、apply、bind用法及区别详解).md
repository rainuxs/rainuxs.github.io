---
title: 前端面试基本---this 指向(call、apply、bind用法及区别详解)
type: 'tags'
categories: ['Web']
date: 2022-03-22 12:00:00
---

**Code is never die !**

### 1.0 函数内部的 this 指向

- 这些 this 的指向，是当我们调用函数的时候确定的
- 调用方式的不同决定了 this 的指向不同
- 一般指向我们的调用者
- 总结如下：

| 调用方式     | this 指向                                 |
| ------------ | ----------------------------------------- |
| 普通函数调用 | window                                    |
| 构造函数调用 | 实例对象,原型对象里面的方法也指向实例对象 |
| 对象方法调用 | 该方法所属对象                            |
| 事件绑定方法 | 绑定事件对象                              |
| 定时器函数   | window                                    |
| 立即执行函数 | window                                    |

代码：

```js
   <button>点击</button>
    <script>
        // 函数的不同调用方式决定了this 的指向不同
        // 1. 普通函数 this 指向window
        function fn() {
            console.log('普通函数的this' + this);
        }
        window.fn();
        // 2. 对象的方法 this指向的是对象 o
        var o = {
            sayHi: function() {
                console.log('对象方法的this:' + this);
            }
        }
        o.sayHi();
        // 3. 构造函数 this 指向 ldh 这个实例对象 原型对象里面的this 指向的也是 ldh这个实例对象
        function Star() {};
        Star.prototype.sing = function() {

        }
        var ldh = new Star();
        // 4. 绑定事件函数 this 指向的是函数的调用者 btn这个按钮对象
        var btn = document.querySelector('button');
        btn.onclick = function() {
            console.log('绑定时间函数的this:' + this);
        };
        // 5. 定时器函数 this 指向的也是window
        window.setTimeout(function() {
            console.log('定时器的this:' + this);

        }, 1000);
        // 6. 立即执行函数 this还是指向window
        (function() {
            console.log('立即执行函数的this' + this);
        })();
    </script>
```

### 2.0 改变函数内部 this 指向

改变函数内 this 指向 js 提供了三种方法 call() apply() bind()

#### 2.1 call 方法

- call()方法调用一个对象
- 简单理解为调用函数的方式，但是它可以改变函数的 this 指向
- 应用场景: 经常做继承
- call：打电话，在程序中有调用的意思
- 代码：

```js
var o = {
	name: 'andy',
};
function fn(a, b) {
	console.log(this);
	console.log(a + b);
}
fn(); // 此时的this指向的是window
fn.call(o, 1, 2); //此时的this指向的是对象o,参数使用逗号隔开

// call 第一个可以调用函数 第二个可以改变函数内的this 指向
// call 的主要作用可以实现继承
function Father(uname, age, sex) {
	this.uname = uname;
	this.age = age;
	this.sex = sex;
}

function Son(uname, age, sex) {
	Father.call(this, uname, age, sex);
}
var son = new Son('刘德华', 18, '男');
console.log(son);
```

#### 2.2 apply 方法

- apply() 方法调用一个函数
- 简单理解为调用函数的方式，但是它可以改变函数的 this 指向
- 应用场景: 经常跟数组有关系
- apply：应用，运用
- 代码：

```js
var o = {
	name: 'andy',
};
function fn(a, b) {
	console.log(this);
	console.log(a + b);
}
fn(); // 此时的this指向的是window
fn.apply(o, [1, 2]); //此时的this指向的是对象o,参数使用数组传递
// 1. 也是调用函数 第二个可以改变函数内部的this指向
// 2. 但是他的参数必须是数组(伪数组)
// 3. apply 的主要应用 比如说我们可以利用 apply 借助于数学内置对象求数组最大值
// ***4. apply将第二个参数的数组,进行了拆包,将拆出来的每个元素,作为实参传递进去
// Math.max();
var arr = [1, 66, 3, 99, 4];
var arr1 = ['red', 'pink'];
// var max = Math.max.apply(null, arr);//不需要改变this指向，写null
var max = Math.max.apply(Math, arr); //但是写null不太合适，写max的调用者Math最好
// 以上代码相当于:Math.max(1, 66, 3, 99, 4);
var min = Math.min.apply(Math, arr);
console.log(max, min);
//补充:
Math.max(1, 2); // max计算一组数中的最大值
Math.max(1, 2, 3);
```

#### 2.3 bind 方法

- bind() 方法不会调用函数，但是能改变函数内部 this 指向，返回的是原函数改变 this 之后产生的新函数

- 如果只是想改变 this 指向，并且不想调用这个函数的时候，可以使用 bind

- 应用场景：不调用函数，但是还想改变 this 指向
- bind：绑定
- 代码：

```js
var o = {
	name: 'andy',
};

function fn(a, b) {
	console.log(this);
	console.log(a + b);
}
//this指向的是对象o 参数使用逗号隔开
var f = fn.bind(o, 1, 2); //此处的f是bind返回的新函数
f(); //调用新函数
// 1. 不会调用原来的函数   可以改变原来函数内部的this 指向
// 2. 返回的是原函数改变this之后产生的新函数
// 3. 如果有的函数我们不需要立即调用,但是又想改变这个函数内部的this指向此时用bind
// 4. 我们有一个按钮,当我们点击了之后,就禁用这个按钮,3秒钟之后开启这个按钮
// var btn1 = document.querySelector('button');
// btn1.onclick = function() {
//     this.disabled = true; // 这个this 指向的是 btn 这个按钮
//     // var that = this;
//     setTimeout(function() {
//         // that.disabled = false; // 定时器函数里面的this 指向的是window
//         this.disabled = false; // 此时定时器函数里面的this 指向的是btn
//     }.bind(this), 3000); // 这个this 指向的是btn 这个对象
// }
var btns = document.querySelectorAll('button');
for (var i = 0; i < btns.length; i++) {
	btns[i].onclick = function () {
		this.disabled = true;
		setTimeout(
			function () {
				this.disabled = false;
			}.bind(this),
			2000
		);
	};
}
```

#### 2.4 call、apply、bind 三者的异同

- **共同点:** 都可以改变 this 指向
- **不同点:**

  - call 和 apply 会调用函数, 并且改变函数内部 this 指向.
  - call 和 apply 传递的参数不一样,call 传递参数使用逗号隔开,apply 使用数组传递
  - bind 不会调用函数, 可以改变函数内部 this 指向.

- **应用场景**
  1. call 经常做继承
  2. apply 经常跟数组有关系. 比如借助于数学对象实现数组最大值最小值
  3. bind 不调用函数,但是还想改变 this 指向. 比如改变定时器内部的 this 指向

**Ending...**
