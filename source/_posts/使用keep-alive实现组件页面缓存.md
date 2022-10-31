---
title: 使用keep-alive实现组件页面缓存
type: 'tags'
categories: ['Vue']
date: 2022-10-11 20:00:00


---

**Code Is Never Die ！**

### keep-alive  [参考文档](https://cn.vuejs.org/guide/built-ins/keep-alive.html#keepalive)

- **Props**：

  - `include` - 字符串或正则表达式。只有名称匹配的组件会被缓存。
  - `exclude` - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。
  - `max` - 数字。最多可以缓存多少组件实例。

- **用法**：

  `<keep-alive>` 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。

  `<keep-alive>` 是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在组件的父组件链中。

  当组件在 `<keep-alive>` 内被切换，它的 `activated` 和 `deactivated` 这两个生命周期钩子函数将会被对应执行。
  
  > 在 2.2.0 及其更高版本中，`activated` 和 `deactivated` 将会在 `<keep-alive>` 树内的所有嵌套组件中触发。

### 实现步骤

1. 给`app.vue`中的<router-view />添加keep-alive组件，并通过include来决定缓存哪些页面

   ```vue
   <template>
     <div id="app">
       <!-- 路由的出口 -->
       <keep-alive include="LayoutIndex">
         <router-view />
       </keep-alive>
     </div>
   </template>
   ```

   

2. 在文章列表页加载的时候监听元素滚动事件，记录当前浏览的滚动条的高度

   ```js
   <template>
     <div class="article-list" ref="article-list">
     	...
     </div>
   </template>
   
   
   data () {
   	+ scrollTop: 0 // 列表滚动的高度
   }
   
   mounted () {
       // 当页面加载的时候监听列表元素的滚动事件，把列表的滚动高度记录下来
       const articleList = this.$refs['article-list']
       articleList.onscroll = () => {
         this.scrollTop = articleList.scrollTop
       }
     }
   ```

   

3. 然后在切换到缓存的组件时，在`activated`钩子函数中把高度设置为保存的高度

   ```js
   activated () {
       // activated生命周期函数 被 keep-alive 缓存的组件激活时调用。
       // 该钩子在服务器端渲染期间不被调用。
       // 把记录的到顶部的距离重新设置回去
       this.$refs['article-list'].scrollTop = this.scrollTop
     }
   ```

4. 此时发现连个人中心也被缓存了，需要把个人中心排除掉，通过路由的meta属性来定义需要加keep-alive组件的路由

   ```js
   {
       path: '', // 默认子路由，只能有1个
       name: 'home',
       component: () => import('@/views/home'),
       meta: {
       	keepAlive: true
       }
   },
   ```

   然后在app.vue根组件判断一下需要缓存的组件

   ```vue
   <template>
     <div id="app">
       <!-- 路由的出口 -->
       <keep-alive include="LayoutIndex">
         <router-view v-if="$route.meta.keepAlive" />
       </keep-alive>
       <router-view v-if="!$route.meta.keepAlive" />
     </div>
   </template>
   ```

5. 既然通过不同的路由地址来实现缓存，那么此时`include="LayoutIndex"`就没有意义了，而且去掉之后像问答，视频的模块也不会被缓存了。

   ```vue
   <template>
     <div id="app">
       <!-- 路由的出口 -->
       <keep-alive>
         <router-view v-if="$route.meta.keepAlive" />
       </keep-alive>
       <router-view v-if="!$route.meta.keepAlive" />
     </div>
   </template>
   ```


6. 继续优化，给第2步监听滚动条位置事件，增加防抖

   ```js
   import { debounce } from 'lodash'
   
   mounted () {
       // 当页面加载的时候监听列表元素的滚动事件，把列表的滚动高度记录下来
       const articleList = this.$refs['article-list']
       articleList.onscroll = debounce(() => {
         console.log(articleList.scrollTop)
         this.scrollTop = articleList.scrollTop
       }, 100)
     }
   ```

7. 切换用户之后发现频道数据也被缓存了，可以通过router-view 标签的key属性解决复用问题。让不同的用户使用不同的key，用用户的token作为唯一的key

   ```html
   <template>
     <div id="app">
       <!-- 路由的出口 -->
       <keep-alive>
         <router-view
           v-if="$route.meta.keepAlive"
           :key="$store.state.user ? $store.state.user.token : null"
         />
       </keep-alive>
       <router-view v-if="!$route.meta.keepAlive" />
     </div>
   </template>
   ```

   

   

### 最终的代码：

   app.vue

   ```html
<template>
  <div id="app">
    <!-- 路由的出口 -->
    <keep-alive>
      <router-view
        v-if="$route.meta.keepAlive"
        :key="$store.state.user ? $store.state.user.token : null"
      />
    </keep-alive>
    <router-view v-if="!$route.meta.keepAlive" />
  </div>
</template>
   ```

   router/index.js

   ```js
   {
           path: '', // 默认子路由，只能有1个
           name: 'home',
           component: () => import('@/views/home'),
           meta: {
             keepAlive: true
           }
         }
   ```

   views/home/components/article-list.vue

   ```js
   import { debounce } from 'lodash'
   
   data () {
       return {
   	...
         scrollTop: 0 // 记录滚动条的高度
       }
     }
   // 当缓存组件被激活的时候触发
   activated () {
       this.$refs['article-list'].scrollTop = this.scrollTop
     },
         
     mounted () {
        // 获取文章列表容器的引用对象
       const articleList = this.$refs['article-list']
       articleList.onscroll = debounce(() => {
         // console.log(articleList.scrollTop)
         this.scrollTop = articleList.scrollTop
       }, 100)
     },
   ```

  **PS:**[ 博主博客主页(Rainux)，精彩继续，欢迎来访！](https://rainux.top)
