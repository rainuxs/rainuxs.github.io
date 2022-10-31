---
title: 关于node的不同取参方式
type: 'tags'
categories: ['Web&Node']
date: 2022-10-20 19:00:00

---

1.req.query（无需载入中间件）

通过req.query可以获取`GET请求`的参数
```javascript
// GET /search?username=tom+braint
req.query.username
// => "tom braint"

// GET /shoes?username=jack&info[age]=20&info[hobby]=dance
req.query.order
// => "jack"
```
### 2.req.params（无需载入中间件）
通过req.param同样是获取`GET请求`参数，用于router.get("/user/:userinfo",....)
```javascript
// router.get("/user/:userinfo",function(req,res,next){
//     console.log(req.params.userinfo)
// })
// 那么“userinfo”属性可作为req.params.userinfo
// 示例：GET /user/jack
req.params.userinfo
// => "jack"
```
### 3.req.body（中间件body-parser）
通过req.body获取`POST请求`参数
注意：不使用body-parser，直接获取`req.body`为`undefined`

```javascript
// POST /login.do  {name:"tom"}
var express = require('express')
var app = express()

app.use(express.json()) // for parsing application/json
app.use(express.urlencoded({ extended: true })) // for parsing application/x-www-form-urlencoded

app.post('/login.do', (req, res) => {
    console.log('********************')
    console.log(req.body) // ★  {name:'tom'}

    res.end();
})

app.listen(3000, () => {
    console.log('http://127.0.0.1:3000')

```

