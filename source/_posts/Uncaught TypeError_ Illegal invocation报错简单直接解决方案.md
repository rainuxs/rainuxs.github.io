---
title: Uncaught TypeError_ Illegal invocation报错简单直接解决方案
type: 'tags'
categories: ['Web']
date: 2021-09-22 10:00:00
---

**Code Is Never Die !**

**环境：** jQuery、Ajax、formData；

**描述：** 用于上传PDF、doc等文件时，文件POST请求需要通过使用`formData`作为`data`的属性值传入，这样才能正确的得到文件信息，但是今天出现了这个错误。

**解决：**  
修改`ajax`请求的内容部分，增加下面两个属性：
```javascript
// 告诉jQuery不要设置Content-Type请求头，无分界符
// 默认true，有分界符，导致服务器无法正确识别文件起始位置
contentType: false,
// 告诉jQuery不要去处理发送的数据
// 默认为true，会将文件等数据转换为查询字符串
processData: false,
```

