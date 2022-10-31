---
title: IP地址进行函数封装处理--常见的前端封装js函数
type: 'tags'
categories: ['Web']
date: 2021-11-20 10:00:00


---

**Code is never die ！**

每日一小更，主要分享一下工作中遇到的一些小问题以及觉得比较 有用可以分享给大家都东西。

想必身为前端的你，也会经常遇到这样的问题吧，接班上一位 “优秀的前端工程师”，继续完成或者维护修改他的 “佳作”，那不堪入目的html、随处可放的css，不知哪里搞来一段js以及前后端交流商量出来的接口...  只有你想不到，没有它不敢出的...

废话不多说，进入正题！今天遇到的情况是对数据IP地址进行二次封装----修改为    **boss** 想要的格式和混淆加密方式
如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210519113911723.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20210519113919374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTkxODY1Nw==,size_16,color_FFFFFF,t_70)
需要对ip进行一定规则的二次处理，这里就以一个规则为例。四组数的范围都为0~255（且不取到0、255），拿到正确的ip，四组数分别进行+5处理，比如：`myip：118.19.11.253`这是后台返回正确数据，处理之后变成了`myip：123.24.16.4`即为展现数据。

大眼一看，不同页面多个地方都有此类数据需要进行处理，果断选择封装一个函数处理（这里说明一下：我封装的不一定是最简单的，但却是真实的第一思路往下走的，重在遇到需求要有思路）
逻辑没有那么复杂，直接上代码，留存备用！

```javascript
packIP(ip) {
      var regexp =
        /^([0-9]|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.([0-9]|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.([0-9]|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.([0-9]|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])$/;
      //说明一下，由于实际业务的需求，可能会出现数据不是IP的情况，选择原封不动
      var res = regexp.test(ip);
      if (res === true) {
        // 这里设置ip规则
        var newip = ip.split('.');//每个网段单独拿出来操作
        var resip = [];
        newip.forEach(function (item) {//遍历+5
          item = Number(item);
          if (item + 5 >= 255) {//保证有效正确性
            item = item - 249;
          } else {
            item = item + 5;
          }
          resip.push(item);
        });
        resip = resip.join('.');//以.分隔符再拼接到一块
        return resip;//成功返回
      } else {
        // 这里直接还原无需操作的数据
        return ip;
      }
	}
```


**PS:**[ 博主博客主页(Rainux)，精彩继续，欢迎来访！](https://rainux.top)
