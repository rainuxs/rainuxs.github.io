---
title: 使用Echarts出现的一些问题......
type: 'tags'
categories: ['Web']
date: 2022-06-26 19:00:00

---

**Code Is Never Die !**

#### 一、Echarts图表显示大小与屏幕之间的问题

终极解决方案： **`window.onresize = myChart.resize`**

**P1.页面中只有一个Echarts图**

```javascript
<div id="echartFirst"></div>
......
var myChart = echarts.init(document.getElementById('echartFirst'));
var options = {//图表配置项....}
myChart.setOption(options)
window.onresize = myChart.resize
```
**P2.页面中存在多个Echarts图**

```javascript
<div id="echartFirst"></div>
<div id="echartSecond"></div>
<div id="echartThird"></div>
......
var myChartFir = echarts.init(document.getElementById('echartFirst'));
var myChartSec = echarts.init(document.getElementById('echartSecond'));
var myChartThi = echarts.init(document.getElementById('echartThird'));
var optionsF = {//图表配置项....}
var optionsS = {//图表配置项....}
var optionsT = {//图表配置项....}
myChartFir.setOption(optionsF)
myChartSec.setOption(optionsS)
myChartThi.setOption(optionsT)
// ★★★ 需用到 addEventListener
// ☆☆☆ 否则页面上只有一个图表会根据浏览器的变化而自适应
window.addEventListener("resize",function (){
    myChartFir.resize();
    myChartSec.resize();
    myChartThi.resize();
});
// ★★★ 或者可以另一种写法
window.onresize = function(){
    myChartFir.resize();
    myChartSec.resize();
    myChartThi.resize();
}
```
