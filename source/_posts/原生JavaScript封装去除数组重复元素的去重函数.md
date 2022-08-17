---
title: 原生JavaScript封装去除数组重复元素的去重函数
type: 'tags'
tags: ['JavaScript', 'Vue', 'Web']
categories: ['Web']
date: 2021-12-20 09:00:00
---

**Header：** 原创不易，还请大家不吝指导赐教，Code is never die！

ps：本着让更多人不止解决问题，更能够学到一点点方法的目的。

今天给大家分享一下 JavaScript 封装一个数组去重函数方法。

**题目：** 要求去除数组中重复的元素

**① 思路：** 把旧数组里面不重复的元素选取出来放到新数组中，重复的元素只保留一个，放到新数组中去重；

**② 核心算法：** 我们遍历旧数组，然后拿着旧数组元素去查询新数组，如果该元素在新数组里面没有出现过，我们就添加，否则不添加；

**③ 常见疑问：** 我们怎么知道该元素没有存在？利用新数组.indexOf(数组元素) ，如果返回时 - 1 就说明新数组里面没有改元素。

直接上代码：

```javascript
// 封装函数：去除数组重复元素
function uniqueArr(arr) {
	var newArr = [];
	for (var i = 0; i < arr.length; i++) {
		if (newArr.indexOf(arr[i]) === -1) {
			newArr.push(arr[i]);
		}
	}
	return newArr;
}
var demo1 = uniqueArr(['c', 'a', 'z', 'a', 'x', 'a', 'x', 'c', 'b']);
var demo2 = uniqueArr(['blue', 'red', 'green', 'yellow', 'green', 'blue']);
console.log(demo1); // ["c", "a", "z", "x", "b"]
console.log(demo2); // ["blue", "red", "green", "yellow"]
```

**Ending...**
好啦，简单明了，自己封装有时候也并不麻烦，相反还可以根据一些实际的特殊需求自己设计，刺激而满满的成就感。还望各位支持一下~~~
