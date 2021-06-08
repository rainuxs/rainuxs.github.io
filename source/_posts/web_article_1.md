---
title: 使用innerHTML向DOM元素中追加问题
type: "tags"
tags: ["JavaScript","Vue","Web"]
---

**Header：** 首创不易，还请大家不吝指导赐教，Code is never die！

ps:本着让更多人不止解决问题，更能够学到一点点方法的目的，内容有点赘述，还请耐心。

今天在修改项目时，偶然碰到了innerHTML部分知识的使用。
**直击问题：** 
根据后台返回数据的个数循环动态添加dom元素，并且对dom元素进行相应的操作（例如：添加、编辑dom元素等）

```javascript
for (let i = 0; i < This.dataList.length; i++) {
    // 此处为每个div添加一个id（为简洁直接以i作为id）
	dom.innerHTML += `<div id=${i} style="width:200px;height:200px;"></div>`;
	let domItem = document.getElementById(i);
	// 此处以添加一个echarts图表为例；
	domItem.myChart = echarts.init(domItem);
	......
}
```
**问题阐述：** 
这是一段很常规的代码，但是当真正渲染时会发现，当有两个（及以上）的数量时，最终只会展现最后一个可视化部分，而前面的部分dom元素也存在，但就是无法显示出来。

**初步想法：** 
① 一开始更多的想的是可视化的数据出现了问题，用过echarts的朋友都知道，数据不准确会导致这种情况。在反复各种打印控制台log各种数据后发现，各类数据都一一打印出来。所以，数据部分导致的设想Pass掉了。
② 考虑的是初始化echarts时，也就是上面代码中的`domItem`，因为每次循环使用同一个变量，后面的可能会把前面的覆盖，导致前面可视化图形展示不出来。后面通过对象赋予不同变量`domItem[i]` 然而发现，并没有什么作用，原因猜测是当前面的可视化初始化-->完成，已经完成了本轮图形化的构建，当第二次循环使用的话相当于用了一个“新”的变量，所以这个不是主要原因。所以，也Pass掉了。

**最终原因：** 
后面瞪着代码看，然后瞪着代码看，然后再瞪着代码看，最终跟着循环走了第一圈，发现当第一次可视化完成之后，来到第二次可视化，关键来了！`dom.innerHTML +=...... `其实也就是`dom.innerHTML = dom.innerHTML +......` 这个过程，相当于前面我第一次完成的echarts构建，在这里就是`dom.innerHTML +` +号前面的部分，又重新绘制了一遍，那么问题就浮出了水面，会导致已经可视化完成的第一个图表，再进行第二轮可视化时发生了 **重绘** 整个dom元素，所以前面已然完成的可视化，又将被“打回原形”，变成了一个空壳子，而第二次的可视化正常，以此类推...所以最终只会显示最后一个可视化（真实创建并渲染完成显示）

**解决办法：** 
① 针对上述这种需要进行操作的类型，既然会发生重绘，那我何不将计就计，等你各种重绘完成之后，我再去给你每个盒子进行操作呢。这就好比于下课的时候大家都在吵闹，你去制止A同学，A不说话了，当你再去制止B，会发现A继续和大家吵闹，而B不说了，往复循环，最后发现让他们吵闹去吧，一上课大家就立马安静了。这里的上课就类比于重绘完成，一切就绪，就可以一个一个的去批评啦，哈哈哈.....例子稍微一点点牵强，不过意思到了。
代码也非常简单

```javascript
//孩子创建过程，随便重绘
for (let i = 0; i < This.dataList.length; i++) {
	dom.innerHTML += `<div id=${i} style="width:200px;height:200px;"></div>`;
}
// 创建完成了，不会再重绘了..后续操作
for (let i = 0; i < This.dataList.length; i++) {
	let domItem = document.getElementById(i);
	// 此处以添加一个echarts图表为例；
	domItem.myChart = echarts.init(domItem);
	......
}
```
②当你需要循环添加的dom元素内容单一、固定格式的元素时，也可以选择appendChild来解决重绘问题。具体见代码

```javascript
// 给body添加dom元素
var dom=document.createElement('h1');
dom.className='test';
dom.innerHTML='Hello,Rain';
document.body.appendChild(dom);
```
这样也避免了重绘问题。

**Ending...**
好啦，首创怀着激动的心啰里啰唆竟然码了2k，问题不是特别难理解，主要的是想要给大家分享拿到问题的整个流程和想法，如有个别地方表述不当或您有疑问，咱们讨论区相互学习哦，还望各位支持一下哦~
