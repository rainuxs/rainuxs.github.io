---
title: 不得不知道的事儿---前端Gojs之去除水印
type: 'tags'
categories: ['Web']
date: 2021-08-25 12:00:00
---

**Code is never die !**
刚开始是这个样子的，带有水印，显得特别难看，太影响界面了吧 ！![在这里插入图片描述](https://img-blog.csdnimg.cn/20210422215938389.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
打开你项目引入的 go.js 文件，然后甭管其他的，直接**ctrl+f** 然后复制这段文字`5da73c80a36755dc038e4972187c3cae51fd22`，然后就能查找到图中所示位置了
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210422220215420.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
此时就是从 b[c]开始的内容，一直到 if(...)这里，全部注释掉！直接**ctrl+s**保存，本来将信将疑，然而奇迹般地就出现了下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210422220220523.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
附记录：
今天发现这个地方可能长得不太一样，不过影响不大，都差不多，而且效果都能显示出来（以下亲测）
![在这里插入图片描述](https://img-blog.csdnimg.cn/202104241736355.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
**Ending...**
