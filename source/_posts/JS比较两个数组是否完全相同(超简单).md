---
title: JS比较两个数组是否完全相同(超简单)
type: 'tags'
categories: ['Web']
date: 2022-07-11 20:00:00


---

**Code Is Never Die !**


```javascript
// 假设两个数组arr1、arr2
var arr1=["11","22","33"];
var arr2=["11","33","44"];
// 定义变量用于标志
var arr_status;
// 判断两个数组长度是否相同
if(arr1.length == arr2.length){
	// 循环arr1
	for (var x = 0; x < arr1.length; x++) {
		// 默认arr_status 为1
        arr_status = 1;
        // if (arry2.indexOf(arr1[x]) == -1) {
        if (arr2[x] != arr1[x]) {
        // 只要有arr2中查不到arr1的元素，代表不相等
            arr_status = 0;
            break;
        }
    }
}else{
	// 两个数组长度不同不可能相等
	arr_status = 0
}
// arr_status == 1 代表两个数组相等
if (arr_status == 1) {
	console.log("相等");
}else{
	console.log("不相等");
}
```
  **PS:**[ 博主博客主页(Rainux)，精彩继续，欢迎来访！](https://rainux.top)
