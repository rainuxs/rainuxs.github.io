---
title: 前端面试基本---forEach、filter、some大合集
type: 'tags'
categories: ['Web']
date: 2022-07-07 11:00:00
---

**Code is never die !**

### 1.0 数组方法 forEach 遍历数组 \*\*\*

- 语法：

```js
var arr = [1,2,3];
arr.forEach(function(value， index， array) {
       //参数一是:数组元素
       //参数二是:数组元素的索引
       //参数三是:当前的数组
 })
  //相当于数组遍历的 for循环 没有返回值
function forEach（fn）{
    for(var i=0;i<this.length;i++){
        fn(this[i],i,this);
    }
}
```

- 代码：

```js
    <script>
        // forEach 迭代(遍历) 数组
        var arr = [1, 2, 3];
        var sum = 0;
        arr.forEach(function(value, index, array) {
            console.log('每个数组元素' + value);
            console.log('每个数组元素的索引号' + index);
            console.log('数组本身' + array);
            sum += value;
        })
        console.log(sum);
    </script>
```

### 2.0 数组方法 filter 过滤数组 \*\*\*

- 语法：

```js
  var arr = [12， 66， 4， 88， 3， 7];
  var newArr = arr.filter(function(value， index，array) {
  	 //参数一是:数组元素
     //参数二是:数组元素的索引
     //参数三是:当前的数组
     return value >= 20;
  });
  console.log(newArr);//[66，88] //返回值是一个新数组
function myFilter(fnCallback){
    // 根据fnCallback的返回值来进行过滤
    // 返回值就是过滤条件
    var tj = fnCallback(12,0,arr);
    if(tj){
        newArr.push(12);
    }
}
```

- 代码：

```js
    <script>
        // filter 筛选数组
        var arr = [12, 66, 4, 88, 3, 7];
        var newArr = arr.filter(function(value, index) {
            // return value >= 20;
            return value % 2 === 0;
        });
        console.log(newArr);
    </script>
```

### 3.0 数组方法 some \*\*\*

- 语法：

```js
some 查找数组中是否有满足条件的元素
 var arr = [10， 30， 4];
 var flag = arr.some(function(value，index，array) {
     //参数一是:数组元素
     //参数二是:数组元素的索引
     //参数三是:当前的数组
     return value < 15;
  });
console.log(flag);//返回值是布尔值，只要查找到满足条件的一个元素就立马终止循环

// some的源码
function some(fn) {
    for (var i = 0; i < this.length; i++) {
        var result = fn(this[i], i, this);
        if(result == true){
            return true;
        }
    }
}
```

- 代码：

```js
    <script>
        // some 查找数组中是否有满足条件的元素
        // var arr = [10, 30, 4];
        // var flag = arr.some(function(value) {
        //     // return value >= 20;
        //     return value < 3;
        // });
        // console.log(flag);
        var arr1 = ['red', 'pink', 'blue'];
        var flag1 = arr1.some(function(value) {
            return value == 'pink';
        });
        console.log(flag1);
        // 1. filter 也是查找满足条件的元素 返回的是一个数组 而且是把所有满足条件的元素返回回来
        // 2. some 也是查找满足条件的元素是否存在  返回的是一个布尔值 如果查找到第一个满足条件的元素就终止循环
    </script>
```

**总结**
| 名称 | 作用 |参数 | 返回值| 备注|
|--|--|--|--|--|
| forEach| 遍历数组,取出数组中的每一项| function(value,index,array){}|没有返回值|不会使用回调函数的返回值|
| filter| 遍历数组,筛选出满足条件的项,将满足条件的项放到新数组中,并且返回| function(value,index,array){}|返回存放了满足条件的项的新数组|如果发现回调函数,返回了 true,就会将当前的 value,放到新数组中|
| some| 遍历数组,判断是否有满足条件的元素,如果有返回 true,如果没有返回 false| function(value,index,array){}|返回 true/false|如果发现回调函数,返回了 true,就会停止遍历|

**Ending...**
