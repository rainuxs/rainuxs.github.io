---
title: vue-element el-table点击行展开，并且收起其他行
type: 'tags'
categories: ['Vue']
date: 2021-03-23 10:00:00


---

**Code Is Never Die !**

代码行中已标注实现点击行展开，并且自动收起其他行的相关设置和代码。

el-table表格是绑定在**vue实例**上的，**相关配置、绑定数据、事件** 将这三部分可以直接**Copy**到自己的项目相关位置，无需修改可以直接使用 !


**1. el-table 相关配置**
```javascript
:row-key="getRowKeys" // 每一行的唯一key值

:expand-row-keys="expands" // 设置目前的展开行(须同时设置row-key)

@expand-change="expandSelect" // 对某行展开/关闭触发

@row-click="clickTable" // 点击单行事件
```

**2.  绑定数据**

```javascript
	// 展开行,数组形式
	expands: [],
	// 每行的唯一key值 用其id表示
	getRowKeys(row) {
	   return row.id;
	},
```
**3.  点击行与展开事件**

```javascript
	// 点击行展开事件
    clickTable(row, index, e) {
      this.$refs.refTable.toggleRowExpansion(row);
    },
    // 折叠面板每次只能展开一行
    expandSelect(row, expandedRows) {
      // console.log('expandedRows', expandedRows)
      // console.log('row', row)
      var that = this;
      if (expandedRows.length) {
        that.expands = [];
        if (row) {
          that.expands.push(row.id); // 每次push进去的是每行的ID
        }
      } else {
        that.expands = []; // 默认不展开
      }
    },
```

**完整代码提供参考**

```html
<el-table
	:row-key="getRowKeys"
	:expand-row-keys="expands"
	@expand-change="expandSelect"
	@row-click="clickTable"
	element-loading-text="拼命加载中"
	element-loading-spinner="el-icon-loading"
	element-loading-background="rgba(0, 0, 0, 0.8)"
	:data="typeList"
	ref="refTable"
>
	<el-table-column type="expand" width="30">
		<template slot-scope="outer">
			<div>
				<template>
					<el-table
						:data="handleData(holeData,outer.row)"
						style="
							width: 100%;
							margin: 0 auto;
							border: 1px solid;
							border-color: #00a1d6;
							border-top-left-radius: 5px;
							border-top-right-radius: 5px;
							border-bottom-color: transparent;
						"
					>
						<el-table-column label="IP">
							<template slot-scope="props">
								<span>{{props.row.ip}}</span>
							</template>
						</el-table-column>
						<el-table-column label="端口">
							<template slot-scope="props">
								<span>{{props.row.duankou}}</span>
							</template>
						</el-table-column>
						<el-table-column label="操作">
							<template slot-scope="props">
								<el-button
									v-on:click="selectconnect(props.row,outer.row)"
									size="small"
									icon="el-icon-s-data"
									>弱口令破解</el-button
								>
							</template>
						</el-table-column>
					</el-table>
				</template>
			</div>
		</template>
	</el-table-column>
	<el-table-column label="类型">
		<template slot-scope="props">
			<span>{{props.row.netType}}</span>
		</template>
	</el-table-column>
</el-table>
```

```javascript
var testarea = new Vue({
  el: '#workspace',
  data: {
    expands: [],
    getRowKeys(row) {
      return row.id;
    },
    ......
  },
  methods: {
  	// 点击行展开事件
    clickTable(row, index, e) {
      this.$refs.refTable.toggleRowExpansion(row);
    },
    // 折叠面板每次只能展开一行
    expandSelect(row, expandedRows) {
      // console.log('expandedRows', expandedRows)
      // console.log('row', row)
      var that = this;
      if (expandedRows.length) {
        that.expands = [];
        if (row) {
          that.expands.push(row.id); // 每次push进去的是每行的ID
        }
      } else {
        that.expands = []; // 默认不展开
      }
    },
    ......
  }
})
```

**PS:**[ 博主博客主页(Rainux)，精彩继续，欢迎来访！](https://rainux.top)
