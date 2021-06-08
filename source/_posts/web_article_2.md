---
title: reverse()使用方法及常见问题
type: "tags"
tags: ["JavaScript","Vue","Web"]

---

**Header：** 原创不易，还请大家不吝指导赐教，Code is never die！

ps：本着让更多人不止解决问题，更能够学到一点点方法的目的。

今天给大家分享一下JavaScript中最实用的方法之一——reverse()。
#### 一、简单用法
相信身为前端工程师或者正在成为前端工程师的小伙伴都对它并不陌生，甚至非常熟悉，主要作用就是用于颠倒数组中元素的顺序，这里举个例子：

```javascript
var arrData = ["I","like","your","voice"]
console.log(arrData) // ["I","like","your","voice"]
var arrData2 = ["I","like","your","voice"]
console.log(arrData2.reverse()) // ["voice","your","like","I",]
```
这就是最简单的例子，能够使数组元素顺序发生变化，从而满足前端项目的需要。
#### 二、理解含义
当然本篇小记并不是简单记一下流水账，说一下定义而已。重点在于讲一下颠倒数组元素之后发生的那些事儿。且听后面慢慢分析~~
接着上面的这个例子来说，

```javascript
var arrData = ["I","like","your","voice"]
//第一次 arrData
console.log(arrData) // ["I","like","your","voice"]
//reverse()
console.log(arrData.reverse()) // ["voice","your","like","I"]
//第一次 arrData
console.log(arrData) // ["voice","your","like","I"]
```
如前面所述，定义了两个变量分别单独打印原变量和`reverse()`后的数据都是正常的，但这里，打印同一个数据时就出现了“意外惊喜”，为什么第一次打印的`arrData`和第二次打印的`arrData`不一样呢？原因就在于：reverse()方法改变原数组，而不创建新数组。什么意思呢，我们分析一下整个过程：

①第一次正常打印`arrData`数据，也就是定义的值；

②第二步打印`arrData.reverse()`，同样是正常的颠倒数组元素打印。这里颠倒所发生的行为是颠倒然后打印出来，**但是** 随之改变的是 `arrData = ["voice","your","like","I"]`；

③第二次打印arrData，不言而喻，上一步`arrData.reverse()`已然改变了数据，故第二次打印的是改变后的数据。
#### 三、深入使用
代码的世界如此美妙。接下来再进一步升华用法，不要走开，依然精彩...

```javascript
var arrData = ["I","like","your","voice"]
// 第一种方式
console.log(arrData + arrData.reverse()) // voice,your,like,Ivoice,your,like,I

var arrData2 = ["I","like","your","voice"]
// 第二种方式
console.log(arrData2 + "~" + arrData2.reverse()) // I,like,your,voice~voice,your,like,I
```
我只是简单的在中间多加了一个字符串`~`，出现了两种截然不同的结果是为什么呢？其实还是万变不离其宗，深入理解：**reverse()方法改变原数组，而不创建新数组**  接下来逐个分析

第一种方式：定义arrData，打印时拿到变量arrData，然后再拿到变量arrData.reverse()，此时会修改原定义的arrData，所以打印时的变量arrData就随之改变，此时`+`两边都是数组会被强制转换为字符串，然后拼接，最后一起打印出来，即出现代码中所示结果；

第二种方式：定义arrData，打印括号内拿到变量arrData，然后执行`+"~"`(这里需要知道，代码执行顺序都是从左至右)，这里变量arrData会被强制转化为字符串String类型，然后再拿到变量arrData.reverse()（此时前面已经被强制转化String类型，所以不会再受后面影响），接下来就是字符串`"I,like,your,voice~"+arrData.reverse()`，也会转化为字符串然后拼接，最后打印出来。

**总结：** 字符串不会被“策反”而发生改变，而变量会随变量值是什么，它就跟着是什么。

**Ending...**
好啦，又一次地怀着激动的心啰里啰唆竟然码了2k，主要的是想要给大家分享拿到问题的整个流程和想法，咱们讨论区相互学习，还望各位支持一下~~~
