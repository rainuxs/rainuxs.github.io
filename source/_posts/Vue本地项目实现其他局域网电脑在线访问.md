---
title: Vue本地项目实现其他局域网电脑在线访问
type: 'tags'
categories: ['Vue']
date: 2022-04-01 10:00:00

---

**Code Is Never Die ！**

项目在本地`npm run dev`跑起来，默认为`http://localhost:8080`在当前IP下访问没有问题，但是同一局域网下的其他同事却访问不了，显示`ERR_CONTENT_LENGTH_MISMATCH`，没有办法访问
![原本地跑项目](https://img-blog.csdnimg.cn/89fb71ab67bc48c09e28a655465b5d95.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
同时直接通过同事电脑访问我的IP`http://192.168.1.20:8080`，也显示连接失败无法访问也无法访问成功。
看到网上的解决办法如下：
1.`package.json`中`scripts`的`dev`中最后加入`--host 0.0.0.0`   亲测后无效；
2.`config`下的`index.js`中的host属性“`localhost`”改为`0.0.0.0`  亲测后无效；
（备注：可能是上述方法有效，但我的项目未满足条件）
我解决问题的办法：
1.`package.json`中`scripts`的`dev`中最后加入`--host 本机IP`；
2.`config`下的`index.js`中的host属性“`localhost`”改为`本机IP`
这样的话重新启动项目即可在同一局域网下的其他IP下访问本地项目。
![在这里插入图片描述](https://img-blog.csdnimg.cn/12e4f78b053749c9aca43fff0b2a2ce9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
PS：注意要把电脑防火墙给关了，这方面也会影响同一局域网下在线访问本机项目（仅限于工作环境局域网，不然可能会产生危险哦）。
![在这里插入图片描述](https://img-blog.csdnimg.cn/1fc71c9792a345918cb6a8c95ddaebcb.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)

