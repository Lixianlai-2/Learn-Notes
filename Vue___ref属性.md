## ref属性

### ref有什么作用

1. 被用来给元素或子组件注册引用信息（id的替代者）

2. 放入组件标签中，可以获取组件实例对象

   ![Image](D:\jirengu\learn-notes\assets\Image-1649688510065.png)

3. 放入html标签中，可以获取DOM节点

   ![Image](D:\jirengu\learn-notes\assets\Image-1649688555240.png)

### 怎么使用ref

- 打标识
  - ![打标识](D:\jirengu\learn-notes\assets\image-20220411230656440.png)
- 获取
  - `$refs`在组件实例对象上
  - 使用`this.$refs`得到对象
  - 如果要得到具体的ref需要使用`this.$refs.具体的ref`

![Image](D:\jirengu\learn-notes\assets\Image.png)

### 用`id和ref`有什么区别？

- 如果对组件标签使用`id`，然后用DOM方法得到它，那么得到的就是`DOM结构`

  - ![得到的是整个DOM](D:\jirengu\learn-notes\assets\Image-1649689296587.png)
  - ![得到的是DOm](D:\jirengu\learn-notes\assets\Image-1649689318836.png)

- 如果用的是`ref`，那么得到的是`VueComponent`（也就是组件实例对象）

  ### 用ref得到实例对象有什么作用？

- 可以用于组件通信（待深入）

