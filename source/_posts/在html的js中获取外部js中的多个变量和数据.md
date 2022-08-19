---
title: 在html的js中获取外部js中的多个变量和数据
type: 'tags'
categories: ['Web']
date: 2021-11-15 19:00:00
---

**Code is never die !**

通常如果数据过多，我们会将数据单独拉出来存储到一个单独的 js 文件中，然后通过外部 js 引入进来使用数据。

目前比较简单而且用的比较多的是 ES6 语法规范的`exports&import`方法。
使用方法是：

```javascript
// 外部定义dataList.js
exports.dataList = {
  	uname = 'Rain',
    uage = '18',
    year = '2021-04-22 09:30',
    hometown = 'China',
}
```

```javascript
使用数据的index.html文件
<script>
	import { dataList } from './data.js';
	console.log(dataList);
</script>
```

当然在项目中使用完全没有任何问题，但是当你测试或者单独两个文件这样使用的话就会出现问题，因为这种方法是 ES6 语法规范下的方法，在普通的 JS 中是使用的 JavaScript 语法，所以肯定会出现“不适”的问题出现，就是下面这个啦！
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210422100907549.png)
“无法在模块外部使用 import 语句”，意思就是说导入文件是 ES6 模块化语法，而浏览器并不支持 ES6 语法。就是这个问题导致的错误。

看到网上很多人给出的解决方法是：在 script 标签中加入 type="module"属性
然而，不管是看评论还是自己亲身测试发现，然而并没有什么用处，依然会报错！！！

其实刚刚开头也说了在项目中使用较多，为什么在项目中可以正常使用呢？其实这里所说的意思是，默认你的项目配置了 webpack 包，然后在 webpack 配置文件中初始化配置一下：`module.exports = { mode: 'development' // mode 用来指定构建模式 }` 然后是启动 webpack 项目打包，将原本的 js 文件改为 dist 目录下的 main.js 文件使用，这里就可以正常使用`exports&import`方法！

这是在项目中使用，当然不会有什么问题，但有人说了我自己测试一些数据，或者自己学习练习，小 demo 中使用，难道还得打包......那岂不是大材小用，这里讲一下原生 js、html 的方法：在 html 的 js 中获取外部 js 中的多个变量值。
首先上代码：
HTML 文件部分

```javascript
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Document</title>
	</head>
	<body>
		<!-- 引入定义数据的js文件 -->
		<script src="./data.js"></script>
		<script>
			// 直接使用js文件方法获取数据
			var dataList = dataList();
			console.log(dataList);
		</script>
	</body>
</html>
```

所引用的 data.js 文件

```javascript
function dataList() {
	var uname = 'Rain';
	var uage = '18';
	var year = '2021-04-22 09:30';
	var hometown = 'China';
	// 这里可以return两种类型数据：对象  数组 （按需求）
	return { uname, uage, year, hometown };
	// return [uname, uage, year, hometown];
}
```

展示下控制台分别打印的数据情况以及测试情况（大家见图即理解）
① 返回数组
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210422102329101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
② 返回对象

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210422102350124.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
如上图大家所见，可以对数据进行遍历等等等操作，方便大家测试，当然在正式项目中也可以使用呀，个人感觉不是特别麻烦，主要是不会报错啦！！！

**Ending：** 坚持写下去，前端的魅力无法言说，努力做自己认为对的事！
