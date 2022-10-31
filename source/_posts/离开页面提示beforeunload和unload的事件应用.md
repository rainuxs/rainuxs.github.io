---
title: 离开页面提示beforeunload和unload的事件应用
type: 'tags'
categories: ['Web']
date: 2022-05-27 20:00:00


---

**Code Is Never Die ！**

**需求：** 在用户离开页面之前给一个提示，选择是否确认离开，并且用户确认离开的话，需要发出一个请求。

![示意图](https://img-blog.csdnimg.cn/054c2a22fdb642048385898c226d727f.png#pic_center)
**代码：** 

```javascript
<!DOCTYPE HTML>
<html>

<body>
    <script>
        // 只有屏幕和用户互动过后，用户离开页面（关闭、刷新、跳转其他页面）才会触发
        window.onbeforeunload = event => {
            console.log('onbeforeload！！！！！')
            if (event) {
                event.returnValue = '关闭提示';
            }
        }
        // 不管有没有和用户互动过，只要用户离开页面（关闭、刷新、跳转其他页面）就会触发
        window.onunload = () => {
            console.log('onunload！！！！！')
            let xhr = new XMLHttpRequest();
            xhr.open('get', '/test', true)
            xhr.send()
            // 加一段同步代码阻塞一下，不然刷新会发不出去异步请求
            let now = new Date()
            while (new Date() - now < 100) { }
        }
    </script>
</body>

</html>
```
**说明：**
1.离开之前的提示无法自定义，只能是浏览器提供的文案（如上图）；
2.unload事件如果要发异步请求的话，需要后面给补一段同步代码阻塞一下，否则请求会发不出去的。
