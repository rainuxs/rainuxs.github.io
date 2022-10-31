---
title: 记录_设置jtopo节点不可拖拽
type: 'tags'
categories: ['Web']
date: 2022-09-11 20:00:00

---

**Code Is Never Die !**

```javascript
this.scene.mousedrag(function(e)){
	e.target.dragable = false;//将拖拽设置为false
}
```

