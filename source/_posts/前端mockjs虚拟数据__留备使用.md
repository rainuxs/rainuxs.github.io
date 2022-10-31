---
title: 前端mockjs虚拟数据__留备使用
type: 'tags'
categories: ['Web']
date: 2022-05-14 20:00:00


---

**Code Is Never Die ！**

#### 1.0 Vue环境下
#### 2.0 引入mock.js文件
在`main.js`中引入`mock.js`

#### 3.0 mock.js文件拦截ajax请求，返回mock数据
```javascript
const Mock = require('mockjs')

// 返回字符串
Mock.mock('/api/data', (req, res) => {
    return Mock.mock({
        'string|3': '*'
    })
})

// 返回指定范围的整数
Mock.mock('/api/getInteger', (req, res) => {
    return Mock.mock({
        'a|1-100': 100
    })
})

// 返回随机个数的对象
Mock.mock('/api/getObject', (req, res) => {
    return Mock.mock({
        'brand|1-3': {
            a: '京东',
            b: '国美',
            c: '苏宁',
            d: '当当',
            e: '天猫',
            f: '淘宝'
        }
    })
})

// 返回随机数组
Mock.mock('/api/getArr', (req, res) => {
    return Mock.mock({
        'data|1-10': [
          {
            'name': '张三'
          }
        ]
      })
})

// 返回随机字符
Mock.mock('/api/getRandom1', (req, res) => {
    return Mock.mock({
        'random1': /[a-z]{2}[A-Z]{2}[0-9]/
    })
})

// 返回随机字符
Mock.mock('/api/getRandom2', (req, res) => {
    return Mock.mock({random2: '@string("lower", 5)'})
})

// 返回UUID
Mock.mock('/api/getUUID', (req, res) => {
    return {'uuid': Mock.Random.id()}
})
```
#### 4.0 单组件中使用axios发起请求

```javascript
import axios from 'axios'
export default {
    components: {
    },
    data () {
        return {

        }
    },
    computed: {
    },
    mounted () {
        this.init()
    },
    methods: {
        init () {
            axios.get('/api/data').then(res => {
                console.log(res.data,'字符串')
            })

            axios.get('/api/getInteger').then(res => {
                console.log(res.data, '数字')
            })

            axios.get('/api/getObject').then(res => {
                console.log(res.data, '对象')
            })

            axios.get('/api/getArr').then(res => {
                console.log(res.data, '数组')
            })

            axios.get('/api/getRandom1').then(res => {
                console.log(res.data, '5个随机字符-方式一')
            })

            axios.get('/api/getRandom2').then(res => {
                console.log(res.data, '5个随机字符-方式二')
            })

            axios.get('/api/getUUID').then(res => {
                console.log(res.data, 'uuid')
            })
        }
    }
}
```

