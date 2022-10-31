---
title: Electron“安装已中止，安装程序未成功地运行完成”
type: 'tags'
categories: ['Electron']
date: 2022-06-15 19:00:00

---

**Code Is Never Die !**

最近在使用Electron桌面化程序时（官方定义：[使用 JavaScript，HTML 和 CSS 构建跨平台的桌面应用程序](http://www.electronjs.org/)），打包成exe文件时出了点问题，特此记录一下，同时分享给大家。

本人打包安装的是使用比较多的`electron-builder`进行项目的打包，`yarn build`后会在build文件夹下生成 **`.exe`** 程序安装包，点击安装时出现了如图问题：
![安装已中止](https://img-blog.csdnimg.cn/c809a2024c284ba4b6e7fa26b38dc6f1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
检查了一下`package.json`的配置情况，发现一切配置也都正常，并未发现错误，安装路径也没错误。

PS：这里补充一下`electron`安装时的两种情况：
（1）点击直接安装，无需选择路径，默认放到C盘默认目录下
![在这里插入图片描述](https://img-blog.csdnimg.cn/cf5697c06f434b3bbec860d86726f1f3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/d2a823f7935242019d3f32494428adff.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
（2）自定义安装路径，如下所示
![自定义路径](https://img-blog.csdnimg.cn/d6c7d8d397614436b89c900852b76aa4.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
![自定义](https://img-blog.csdnimg.cn/a59f2bb8091d449db0b887be74c42ec5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
好的，回到整体上，检查完之后，发现并没有配置方面的问题，在中止页面看起来好像是能正常安装，好像是和哪产生冲突了，因为提示的是**中止**而不是**出错/失败**。
考虑是不是自己电脑前面已安装过此程序，未删除干净造成的，所以一方面在其他电脑测试了，另一方面找到自己电脑程序与功能面板，查看是否有残余。
综上发现：
（1）在另台电脑上可以正常安装；
（2）在原电脑上找到了未卸载彻底的程序，卸载了，然后就能正常安装
![程序与功能](https://img-blog.csdnimg.cn/3b68e10011d649818048e2288c73b33f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
![正常安装](https://img-blog.csdnimg.cn/95f611329a17473daf613fa0b1d5fdb9.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_20,color_FFFFFF,t_70,g_se,x_16)
最终得知原因：**因为在上一次安装了此程序后，测试完成就删除了，直接删除了如图所示的文件，并未正常进行程序卸载操作，导致再次安装时在程序中找到了相同的`appid`，所以会提示安装被中止问题**
![删除内容](https://img-blog.csdnimg.cn/c7af3999c2394e0f998e287957e071d9.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAcmFpbnV4Lg==,size_11,color_FFFFFF,t_70,g_se,x_16)

**Code Is Never Die ！**
