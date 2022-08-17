---
title: TypeError_ util.print is not a function 用node.js安装hotnode后启动报错
type: 'tags'
tags: ['Node', 'Nodejs', 'Web', 'JavaScript']
categories: ['Web']
date: 2021-03-10 10:00:00
---

**Code is never die !**

```javascript
//终端安装插件
npm install -g hotnode
```

直接展示错误地方：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021042019323395.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
点击下划线处部分进入 hotloader.js 中（长按 ctrl+鼠标点击）进入自动定位到下方位置
修改代码`util.print ->console.log`保存，重新跑项目
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210420193304705.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)

最终成功跑项目：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021042019332219.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
**Ending...**
