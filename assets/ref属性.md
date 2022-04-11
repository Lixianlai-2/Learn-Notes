## ref属性

### ref有什么作用

1. 被用来给元素或子组件注册引用信息（id的替代者）

2. 放入组件标签中，可以获取组件实例对象

   ![Image](D:\jirengu\learn-notes\Image-1649688510065.png)

3. 放入html标签中，可以获取DOM节点

   ![Image](D:\jirengu\learn-notes\Image-1649688555240.png)

### 怎么使用ref

```html
 
<div id="app">
    <h1 v-text="msg" ref="title"></h1>
    <school ref="sch" />
    <button @click="showName" ref="btn">点我展示DOM</button>
  </div>
```





![Image](D:\jirengu\learn-notes\Image.png)

怎么输出DOM?

如果给自闭和组件写了ref，会有什么不利影响吗？

为什么ref有存在的必要呢？它有什么作用？