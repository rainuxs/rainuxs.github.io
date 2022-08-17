---
title: 原生JavaScript封装颠倒数组元素
type: 'tags'
tags: ['JavaScript', 'Vue', 'Web']
categories: ['Web']
date: 2021-12-20 09:00:00
---

**Header：** 原创不易，还请大家不吝指导赐教，Code is never die！

ps：本着让更多人不止解决问题，更能够学到一点点方法的目的。

今天给大家分享一下 JavaScript 原生代码封装 reverse()方法。
直接上代码：

```javascript
// 利用封装函数翻转任意数组
function changeArr(arr) {
	var newArr = [];
	for (var i = arr.length - 1; i >= 0; i--) {
		newArr[newArr.length] = arr[i];
	}
	return newArr;
}
var arr1 = changeArr([1, 3, 4, 6, 9]);
console.log(arr1); // [9, 6, 4, 3, 1]
var arr2 = changeArr(['red', 'green', 'purple', 'blue']);
console.log(arr2); // ["blue", "purple", "green", "red"]
```

**Ending...**
好啦，简单明了，自己封装有时候也并不麻烦，相反还可以根据一些实际的特殊需求自己设计，刺激而满满的成就感。还望各位支持一下~~~
