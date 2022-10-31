---
title: 超简单使用Vue项目引入Vuex，随时更新新问题
type: 'tags'
categories: ['Vue']
date: 2022-09-12 19:00:00

---

**Code Is Never Die !**

如何更好地在组件外部管理状态，Vuex 可以帮助我们管理共享状态，并附带了更多的概念和框架，将会成为自然而然的选择。

今天就简单记录一下最简单的使用Vuex的方法。

#### 一、安装引入
如果是Vue项目搭建的底层，推荐`npm/yarn`安装

```powershell
#npm
npm install vuex --save
#yarn
yarn add vuex
```
#### 二、结构添加
经过步骤一，成功安装了vuex，下面需要在src目录下新建`store/store.js`,当然了，需要在项目中使用，肯定是要引入到main.js中的。以下以登陆成功保存用户名和用户所在用户组为例：
**1.以下为基本的main.js设置：**
```javascript
import Vue from 'vue'
import App from './App'
import axios from 'axios'
import router from './router'
import store from './store'
Vue.prototype.$http = axios
new Vue({
  el: '#app',
  router,
  store,
  components: { App },
  template: '<App/>'
})
```
**2.使用vuex保存信息的用户(Login.vue):**

```javascript
this.$store.commit('saveUsername',data.username) 
this.$store.commit('saveUsergroup',data.groupname)
```

**3.以下为基本的store.js设置：**

```javascript
//  在store里面的store.js文件写入
import Vue from "vue"
import Vuex from "vuex"
Vue.use(Vuex);

export default new Vuex.Store({
    state:{
    	// 保存信息的变量名
        userName: "",
        userGroup: "",
    },
    mutations:{
        // 保存当前用户的信息
        saveUsername(state,userName){
            state.userName = userName;
        },
        // 保存当前用户组的信息
        saveUsergroup(state,userGroup){
            state.userGroup = userGroup;
        },
    }
  })
```
**4.其他模块使用已存储在vuex中的数据：**

```javascript
<p id="name_part">
<span>欢迎您, </span>
// 这里使用用户名
<span class="titleusername" v-html="this.$store.state.userName"></span>
</p>
<p class="other_part">
<span>角色：</span>
// 这里使用用户组
<span class="other_val" v-html="this.$store.state.userGroup"></span>
</p>
```
这样一个简单的vuex的使用就做好了，在登陆成功时将用户的信息存储在vuex中，在进入其他页面需要用到用户信息的时候可以直接获取。

**`JavaScript代码是运行在内存当中的，代码运行时的变量，函数，也都是保存在内存中的。刷新页面后，之前申请的所有内存会被释放，重新加载JavaScript代码，变量和函数将重新赋值和初始化。因此，刷新页面保留数据就必须使用外部存储——客户端 or 服务器`**

这里其实就是说存储在vuex中，当页面刷新后内存被释放，数据也会丢失，所以需要从客户端存储中获取，即Local Storage & Session Storage。具体使用如下：

```javascript
// 页面重新加载执行
created(){
	if (this.$router.path != 'Login') {
	//在页面加载时读取localStorage里的状态信息
		localStorage.getItem("userThing") && this.$store.replaceState(Object.assign(this.$store.state, JSON.parse(
		localStorage.getItem("userThing"))));
		//在页面刷新时将vuex里的信息保存到localStorage里
		window.addEventListener("beforeunload", () => {
		localStorage.setItem("userThing", JSON.stringify(this.$store.state))
		})
	}
}
```

