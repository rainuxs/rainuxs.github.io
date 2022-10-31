---
title: npm err ! Error_ connect ECONNREFUSED 127.0.0.1_8087
type: 'tags'
categories: ['Web']
date: 2022-04-27 20:00:00


---

**Code Is Never Die**

npm安装了express

```javascript
npm install express
```

然后出现了错误

```javascript
npm err !  Error: connect ECONNREFUSED 127.0.0.1:8087
```
解决办法

```javascript
npm config set proxy null
```
然后就OK啦！

