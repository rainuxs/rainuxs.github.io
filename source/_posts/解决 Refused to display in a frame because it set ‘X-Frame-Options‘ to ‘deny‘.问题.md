---
title: 解决 Refused to display in a frame because it set ‘X-Frame-Options‘ to ‘deny‘.问题
type: 'tags'
categories: ['Web']
date: 2022-02-26 19:00:00
---

**Code Is Never Die !**
**问题：** 在做iframe预览PDF文件时，虽然nginx配置了`X-Frame-Options  SAMEORIGIN`,但在iframe中仍然获取不到内容。

**介绍：**`X-Frame-Options` HTTP 响应头是用来给浏览器指示允许一个页面可否在 frame , iframe 或者 object 中展现的标记。网站可以使用此功能，来确保自己网站的内容没有被嵌到别人的网站中去，也从而避免了点击劫持 (clickjacking) 的攻击。

只有当用户使用支持`X-Frame-Options`的浏览器访问文档时，才提供增加的安全性。`Content-Security-Policy` HTTP头中的`frame-ancestors`指令会替代这个非标准的`header.CSP`的`frame-ancestors`会在壁虎4.0中支持,但是并不会被所有浏览器支持。然而`X-Frame-Options`是个已广泛支持的非官方标准,可以和CSP结合使用。

`X-Frame-Options `有三个可能的值：

`deny` 表示该页面不允许在 frame 中展示，即便是在相同域名的页面中嵌套也不允许。

`sameorigin` 表示该页面可以在相同域名页面的 frame 中展示。

`allow-from uri(http://......)` 表示该页面可以在指定来源的 frame 中展示。

## 解决办法：Django中提供了一些简单的方法来在站点的响应中包含这个协议头
**（1）一个简单的中间件，在所有响应中设置协议头。**
如果要为你的站点中所有的响应设置相同的`X-Frame-Options`值，就可以将项目中`settings.py`文件中的添加中间件：‘`django.middleware.clickjacking.XFrameOptionsMiddleware` 设置为`MIDDLEWARE`:

```python
MIDDLEWARE = [
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

在开启该中间件之后，默认会为任何开放的`HttpResponse`设置`X-Frame-Options`协议头为DENY,如果你想要设置为`SAMEOGIGIN`,可以在`settings.py`文件中设置：`X_FRAME_OPTIONS = 'SAMEORIGIN'`.

**但是这样的话会使该站点所有的视图都使用X-Frame-Options协议头，对于某些视图函数，我们可以使用特定的装饰器告诉中间件不要设置协议头.**

**（2）使用修饰器。**
在views.py文件中使用装饰器
**导入模块**
```python
from django.views.decorators.clickjacking import xframe_options_sameorigin, xframe_options_exempt,xframe_options_deny
```

1.引用装饰器xframe_options_sameorigin，允许同源访问的装饰器

```python
from django.views.decorators,clickjacking import xframe_options_sameorigin
 
@xframe_options_sameorigin
def send_file(request,filename):
    fp = open(os.path.join(UEDITOR_UPLOAD_PATH,filename),'rb')
    response = FileResponse(fp)
    response['X-Frame-Options'] = settings.X_FRAME_OPTIONS
    return response
```
2. 引用装饰器`xframe_options_exempt`，告诉中间件访问该视图时不要设置协议头：
```python
from django.http import HttpResponse
from django.views.decorators.clickjacking import xframe_options_exempt
 
@xframe_options_exempt
def xframe_exempt(request):
    return HttpResponse('这个页面是安全的')
```


3.引用装饰器`xframe_options_deny`, 告诉中间件访问该视图时屏蔽在加载iframe时的所有资源：

```python
from django.http import HttpResponse
from django.views.decorators.clickjacking import xframe_options_deny
 
@xframe_options_deny
def deny_xframe(request):
    return HttpResponse('拒绝所有的资源')
```

