---
title: 服务器开发的网站http登录失败，必须https登录
type: 'tags'
categories: ['Web']
date: 2022-06-14 20:00:00


---

**Code Is Never Die ！**

公司系统使用默认（也就是http方式登录）都会出现问题
![在这里插入图片描述](https://img-blog.csdnimg.cn/12cefc7e7ffe4c7e8e18227110c88685.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
应该是之前做了https的安全验证，但是有的时候默认输入地址是http的，所以往往会造成一定的不方便。
考虑最简单的就是让系统自动使用https下访问
在头部增加如下一行代码：

```html
<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests" />
```
这样访问不管是`http/https`都会自动跳到`https`下，可以避免登录迷之操作发生

