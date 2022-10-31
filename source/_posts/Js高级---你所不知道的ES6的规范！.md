---
title: Js高级---你所不知道的ES6的规范！
type: 'tags'
categories: ['Web']
date: 2021-02-01 10:00:00

---

**Code Is Never Die !**

今天我们一起揭开JS中ES6的神秘面纱！
## 1. ES6相关概念（★★）

### 1.1 什么是ES6

ES 的全称是 ECMAScript , 它是由 ECMA 国际标准化组织,制定的一项脚本语言的标准化规范。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706094200257.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)

ES6 实际上是一个泛指，泛指 ES2015 及后续的版本。 

### 1.2 为什么使用 ES6 ?

每一次标准的诞生都意味着语言的完善，功能的加强。JavaScript语言本身也有一些令人不满意的地方。

- 变量提升特性增加了程序运行时的不可预测性
- 语法过于松散，实现相同的功能，不同的人可能会写出不同的代码

## 2. ES6新增语法

### 2.1 let（★★★）

ES6中新增了用于声明变量的关键字

#### 2.1.1 let声明的变量只在所处于的块级有效

```javascript
 if (true) { // 大括号可以形成块级作用域
     let a = 10;
 }
console.log(a) //报错: a is not defined
```

**注意：** 使用let关键字声明的变量才具有块级作用域，使用var声明的变量不具备块级作用域特性。

**好处** : 可以防止循环变量变成全局变量 : (使用var就不会报错)

```js
for (let i = 0; i < 2; i++) {}
console.log(i);//报错: i is not defined
```

#### 2.1.2 不存在变量提升

```javascript
console.log(a); // a is not defined 
let a = 20;
```

#### 2.1.3 暂时性死区

利用let声明的变量会绑定在这个块级作用域，不会受外界的影响

```javascript
 var tmp = 123;
 if (true) { //因为在此块级作用域中，使用了let声明了tmp变量，那么tmp会与此块级作用域进行绑定，形成死区，不受外界影响（无法访问外部的tmp）
     tmp = 'abc';//这里会报错，变量未声明，不能赋值
     let tmp; 
 } 
```

#### 2.1.4 经典面试题

面试题1：此题没有用到let

```javascript
 var arr = [];
 for (var i = 0; i < 2; i++) {
     arr[i] = function () {
         console.log(i); 
     }
 }
 arr[0]();//2
 arr[1]();//2

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706094303838.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)


**经典面试题图解：** 此题的关键点在于变量i是全局的，函数执行时输出的都是全局作用域下的i值。

面试题2：此题用到let关键字

```javascript
 let arr = [];
 for (let i = 0; i < 2; i++) {
     arr[i] = function () {
         console.log(i); 
     }
 }
 arr[0]();//0
 arr[1]();//1

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706094331252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)


**经典面试题图解：**

- 此题的关键点在于**每次循环都会产生一个块级作用域**，
- 每个块级作用域中的变量都是不同的，
- 函数执行时输出的是自己上一级（循环产生的块级作用域）作用域下的i值.

#### 2.1.5 小结

- **let关键字就是用来声明变量的**
- **使用let关键字声明的变量具有块级作用域**
- 在一个大括号中 使用let关键字声明的变量才具有块级作用域 var关键字是不具备这个特点的
- 防止循环变量变成全局变量
  - 循环中的i，使用var声明的话是全局变量，但是这样不合理，而使用let就是局部变量
- **使用let关键字声明的变量没有变量提升**
- 使用let关键字声明的变量具有暂时性死区特性
  - 死区：不受外界影响

### 2.2 const（★★★）

**声明常量**，常量就是值（内存地址）不能变化的量

**常量：常态的量，值是常态的量，值无法改变**

const：constant常量

#### 2.2.1 具有块级作用域

```javascript
 if (true) { 
     const a = 10;
 }
console.log(a) // a is not defined
```

#### 2.2.2 声明常量时必须赋值

```javascript
const PI; // Missing initializer in const declaration，声明常量时丢失初始化
```

#### 2.2.3 常量赋值后，值不能修改 （栈中存储的内容无法修改）

```javascript
const PI = 3.14;
PI = 100; // Assignment to constant variable. //给常量重新指定值

const ary = [100, 200];
ary[0] = 'a';//复杂数据类型内部的值，是可以改变的
ary[1] = 'b';
console.log(ary); // ['a', 'b']; 
ary = ['a', 'b']; // Assignment to constant variable.//但是复杂数据类型变量本身无法改变
```

#### 2.2.4 小结

- **const声明的变量是一个常量**
- **既然是常量不能重新进行赋值**，如果是基本数据类型，不能更改值，如果是复杂数据类型，不能更改地址值
  - 复杂数据类型变量中存储的是地址值
- 声明 const时候必须要给定初始值（**因为没有办法重新赋值，所以在声明时必须有初始值**）

### 2.3 let、const、var 的区别

- 使用 var 声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象
- 使用 let 声明的变量，其作用域为该语句所在的代码块内，不存在变量提升
- 使用 const 声明的是常量，在后面出现的代码中不能再修改该常量的值

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706094356725.png)

### 2.4 解构赋值（★★★）

- ES6中允许从数组中提取值，按照对应位置，对变量赋值，对象也可以实现解构

- 解构：分解数据结构  (可以理解为拆包，将数组中的元素拆出来)

- 赋值：为变量赋值

- 解构赋值，可以让我们更快捷的从数组或对象中提取值，然后对变量赋值


#### 2.4.1 数组解构

- 数组解构允许我们按照一一对应的关系从数组中提取值 
- 然后将值赋值给变量 

```javascript
 let [a, b, c] = [1, 2, 3];
 console.log(a)//1
 console.log(b)//2
 console.log(c)//3
//如果解构不成功，变量的值为undefined
```

#### 2.4.2 对象解构

- 对象解构允许我们使用变量的名字匹配对象的属性 
- 匹配成功之后将对象属性的值赋值给变量 

```javascript
let { name, age } = { name: 'zhangsan', age: 20 };
console.log(name); // 'zhangsan' 
console.log(age); // 20

//注意这里的name仅仅是用于属性匹配，不在是变量，myName才是变量
let {name: myName, age: myAge} = { name: 'zhangsan', age: 20 };
console.log(myName); // 'zhangsan' 
console.log(name);//无法获取到zhangsan
console.log(myAge); // 20
//如果变量不想与对象的属性名保持一致，那么采用第二种方式解构
```

#### 2.4.3 小结

- 解构赋值就是把数据结构分解，然后给变量进行赋值

- 如果解构不成功，变量跟数值个数不匹配的时候，变量的值为undefined

- 数组解构用中括号包裹，多个变量用逗号隔开，对象解构用花括号包裹，多个变量用逗号隔开

- 利用解构赋值能够让我们方便的去取对象中的属性跟方法

- 补充:

  ```js
  //不管是数组还是对象在去处理结构赋值时,都是通过key匹配变量,然后进行赋值.
   let [a, b, c] = [0:1, 1:2, 2:3];
  let { name, age } = { name: 'zhangsan', age: 20 };
  ```

  

### 2.5 箭头函数（★★★）

#### 2.5.1 箭头函数介绍

ES6中新增的定义函数的方式：箭头函数

语法：

```javascript
() => {} //()：代表是函数； =>：代表指向，指向哪一个代码块；{}：代码块，函数体
const fn = () => {}//代表把一个函数赋值给fn
```

代码：

```js
// 箭头函数是用来简化函数定义语法的
 const fn = () => {
 	console.log(123)
 }
 fn();
var fn = function(){}

```

函数体中只有一句代码，且代码的执行结果就是返回值，可以省略大括号

```javascript
 function sum(num1, num2) { 
     return num1 + num2; 
 }
 //es6写法
 const sum = (num1, num2) => num1 + num2; 

```

如果形参只有一个，可以省略小括号

```javascript
 function fn (v) {
     return v;
 } 
//es6写法
 const fn = v => v;

```

箭头函数不绑定this关键字，箭头函数中的this，指向的是函数定义位置的上下文this

```javascript
const obj = { name: '张三'} 
 function fn () { 
     console.log(this);//this 指向 是obj对象
     return () => { 
         console.log(this);
         //this 指向 的是箭头函数定义区域的this，那么这个箭头函数定义在fn里面，而这个fn指向是的obj对象，所以这个this也指向是obj对象
         //理解为当前箭头函数作用域中没有this，要向上一级作用域查找
     } 
 } 
 const resFn = fn.call(obj); 
 resFn();

```

#### 2.5.2 小结

- 箭头函数中不绑定this，箭头函数中的this指向是它所定义的位置
  - **理解**：箭头函数不绑定this，箭头函数没有自己的this关键字，如果在箭头函数中使用this，this关键字将指向箭头函数定义位置中的this 
  - **再理解**：理解为当前箭头函数作用域中没有this，要向上一级作用域查找
- 箭头函数的优点在于解决了this执行环境所造成的一些问题。
  - 比如：解决了匿名函数this指向的问题（匿名函数的执行环境具有全局性），包括setTimeout和setInterval中使用this所造成的问题

#### 2.5.3 面试题

```javascript
var age = 100;

var obj = {
	age: 20,
	say: () => {
		alert(this.age)
	}
}

obj.say();//100；
//箭头函数this指向的是被声明的作用域里面，而对象没有作用域的(对象没有块级作用域)
//所以箭头函数虽然在对象中被定义，但是this指向的是全局作用域
```

### 2.6 剩余参数（★★）

#### 2.6.1 剩余参数介绍

- 剩余参数语法允许我们将一个不定数量的参数表示为一个数组
- 不定参数定义方式，这种方式很方便的去声明不知道参数情况下的一个函数
- 代码：

```javascript
function sum (first, ...args) {//...args为剩余参数，理解为不定长参数
     console.log(first); // 10
     console.log(args); // [20, 30] 
 }
 sum(10, 20, 30)
```

#### 2.6.2 剩余参数和解构配合使用

- 剩余参数不仅仅可以在函数定义的形参中使用
- 还可以配合解构使用
- 代码：

```javascript
let students = ['wangwu', 'zhangsan', 'lisi'];
let [s1, ...s2] = students; //...s2为剩余参数，理解为不定长变量
console.log(s1);  // 'wangwu' 
console.log(s2);  // ['zhangsan', 'lisi']

```

## 3. ES6 的内置对象扩展

### 3.1 Array 的扩展方法（★★）

#### 3.1.1 扩展运算符...（展开语法）

- 扩展运算符可以**将数组转为用逗号分隔的参数序列**


```javascript
 let ary = [1, 2, 3];
 ...ary  // 1, 2, 3
 console.log(...ary);    // 1 2 3,相当于下面的代码
 console.log(1,2,3);
```

- 扩展运算符可以**应用于合并数组**

```javascript
// 方法一 
let ary1 = [1, 2, 3];
let ary2 = [3, 4, 5];
let ary3 = [...ary1, ...ary2];
// 方法二 
ary1.push(...ary2);
//方式三
console.log(ary1.concat(ary2));

```

- 将**伪数组或可遍历对象转换为真正的数组**

```javascript
let oDivs = document.getElementsByTagName('div'); 
oDivs = [...oDivs];
```

**总结**：

- 扩展运算符...
- 可以理解为拆包，将数组中的元素拆出来

#### 3.1.2 构造函数方法：Array.from()

**将伪数组或可遍历对象转换为真正的数组**

```javascript
//定义一个集合
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
}; 
//转成数组
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
//length不是数组中的元素，而是数组的一个属性，所以打印是看不到的，只能在控制台点击数组变量的小三角才能看见length
```

如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706094431696.jpg)
方法还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组

```javascript
 let arrayLike = { 
     "0": 1,
     "1": 2,
     "length": 2
 }
 let newAry = Array.from(arrayLike, item => item *2)//[2,4]
 //第二个参数是一个箭头函数，因为一个参数，一行代码，所以简写
 //这里的item是一个变量，代表属性值
 //item这个变量名可以随便写，但是一般用item
```

#### 3.1.3 实例方法：find()

用于找出第一个符合条件的数组成员，如果没有找到返回undefined

```javascript
let ary = [{
     id: 1,
     name: '张三'
 }, { 
     id: 2,
     name: '李四'
 }]; 
 let target = ary.find((item, index) => item.id == 2);//找数组里面符合条件的值，当数组中元素id等于2的查找出来，注意，只会匹配第一个
//要查找的条件，写到箭头函数的函数体中
//find接收的箭头函数的参数是固定的，item和index，属性值和索引
//注意这里的属性值item是一个个的对象
//target是id为2的item对象

```

#### 3.1.4 实例方法：findIndex()

用于找出第一个符合条件的数组成员的**位置**，如果没有找到返回-1

```javascript
let ary = [1, 5, 10, 15];
let index = ary.findIndex((value, index) => value > 9); 
console.log(index); // 2
```

#### 3.1.5 实例方法：includes()

- 判断某个数组是否包含给定的值，返回布尔值。
- includes：包括
- 语法：

```javascript
[1, 2, 3].includes(2) // true 
[1, 2, 3].includes(4) // false

```

### 3.2 String 的扩展方法

#### 3.2.1 模板字符串（★★★）

- ES6新增的创建字符串的方式，使用反引号定义
- 反引号在键盘的位置：1的左侧，与~同一个键

```javascript
let name = `zhangsan`;
```

- 模板字符串中可以解析变量

```javascript
let name = '张三'; 
let sayHello = `hello,my name is ${name}`; // hello, my name is zhangsan
//模板字符串中，通过${变量名}的方式来获取变量值
```

- 模板字符串中可以换行

```javascript
 let result = { 
     name: 'zhangsan', 
     age: 20,
     sex: '男' 
 } 
 let html = ` <div>
     <span>${result.name}</span>
     <span>${result.age}</span>
     <span>${result.sex}</span>
 </div> `;

```

- 在模板字符串中可以调用函数
- 同样是通过${}来调用

```javascript
const sayHello = function () { 
    return '哈哈哈哈 追不到我吧 我就是这么强大';
 }; 
 let greet = `${sayHello()} 哈哈哈哈`;
 console.log(greet); // 哈哈哈哈 追不到我吧 我就是这么强大 哈哈哈哈

```

**总结：**

- 模板字符串中可以写代码，html代码（可以识别空格和换行等格式），js代码（写在${}）

#### 3.2.2 实例方法：startsWith() 和 endsWith()

- startsWith()：表示参数字符串是否在原字符串的头部，返回布尔值
- endsWith()：表示参数字符串是否在原字符串的尾部，返回布尔值

```javascript
let str = 'Hello world!';
str.startsWith('Hello') // true 
str.endsWith('!')       // true

```

#### 3.2.3 实例方法：repeat()

repeat方法表示将原字符串重复n次，返回一个新字符串

```javascript
'x'.repeat(3)      // "xxx" 
'hello'.repeat(2)  // "hellohello"
```

### 3.3. Set 数据结构（★★）

#### 3.3.1 介绍

- ES6 提供了新的数据结构  Set。
- 它类似于数组，但是**成员的值都是唯一**的，没有重复的值。
- Set本身是一个构造函数，用来生成  Set  数据结构
- 创建Set类型的变量，语法如下：

```javascript
const s = new Set();
```

Set函数可以接受一个数组作为参数，用来初始化。

```javascript
const set = new Set([1, 2, 3, 4, 4]);//{1, 2, 3, 4}

```

#### 3.3.2 实例方法

- add(value)：添加某个值，返回 Set 结构本身
- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功
- has(value)：返回一个布尔值，表示该值是否为 Set 的成员
- clear()：清除所有成员，没有返回值

```javascript
 const s = new Set();
 s.add(1).add(2).add(3); // 向 set 结构中添加值 
 s.delete(2)             // 删除 set 结构中的2值   
 s.has(1)                // 表示 set 结构中是否有1这个值 返回布尔值 
 s.clear()               // 清除 set 结构中的所有值
 //注意：删除的是元素的值，不是代表的索引
```

#### 3.3.3 遍历

Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。

```javascript
s.forEach(value => console.log(value))
```

**PS:**[ 博主博客主页(Rainux)，精彩继续，欢迎来访！](https://rainux.top)
