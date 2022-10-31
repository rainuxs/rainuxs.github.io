---
title: Git：放弃本地(或Linux下)修改内容，全部拉取远端git仓库代码
type: 'tags'
categories: ['Git']
date: 2022-07-22 19:00:00

---

**Code Is Never Die**

本地(或者服务器)修改了部分内容，想要放弃本地的更改，拉取使用远程git仓库所有内容，可以进行下面操作：
```javascript
// 一、拉取所有更新，不同步
git fetch --all
// 二、指向master最新版本，覆盖本地内容（包含本地修改）
//    拿到所有远程master内容
git reset --hard origin/master
```

```javascript
 // 单条执行命令--覆盖本地内容（效果同上一&二）
 git fetch --all && git reset --hard origin/master
```
