---
title: 其他解决方法：Forbidden(403) CSRF verification failed.Request aborted.
type: 'tags'
categories: ['Web']
date: 2022-10-03 20:00:00


---

**Code Is Never Die ！**

今天在完成部分页面发起POST请求时，出现了如下所示的403报错情况
![问题信息](https://img-blog.csdnimg.cn/f13d2a942a5540d0b083efb3c60e1889.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
度娘搜索了一下，解决方法包含了前端修改和后端修改的解决办法，前端来修改操作的90%都集中于在form标签里面添加`{% csrf_token %}`即可，也是最为简单的，然而，很不幸我加了之后依然报错。
后来发现页面登陆进来会有一个接口获取csrfToken，用来防御CSRF攻击，在接口请求时为避免安全性的问题产生漏洞，会在headers中携带此csrfToken，故在请求时加上`headers: { 'X-CSRFToken': token }`，其中token为获取得到的csrfToken，这样就能够正常调用接口，从而访问/存储信息。

**结尾：** 发现只有POST请求接口必须要携带token，而GET请求不携带也可访问，暂时未知原因。猜测为：GET请求数据不会造成安全攻击，只是拿到数据，并不能对数据进行操作。希望有大神可以指导，共同进步！
