## ref 属性

### ref 有什么作用

1. 被用来给元素或子组件注册引用信息（id 的替代者）

2. 放入组件标签中，可以获取组件实例对象

   ![Image](D:\jirengu\learn-notes\assets\Image-1649688510065.png)

3.

4. 放入 html 标签中，可以获取 DOM 节点

5.

6. ![Image](Vue___ref属性.assets/Image.png)

   ![Image](D:\jirengu\learn-notes\assets\Image-1649688555240.png)

### 怎么使用 ref

- 打标识
  - ![打标识](D:\jirengu\learn-notes\assets\image-20220411230656440.png)
- 获取
  - `$refs`在组件实例对象上
  - 使用`this.$refs`得到对象
  - 如果要得到具体的 ref 需要使用`this.$refs.具体的ref`

![Image](D:\jirengu\learn-notes\assets\Image.png)

### 用`id和ref`有什么区别？

- 如果对组件标签使用`id`，然后用 DOM 方法得到它，那么得到的就是`DOM结构`

  - ![得到的是整个DOM](D:\jirengu\learn-notes\assets\Image-1649689296587.png)
  - ![得到的是DOm](D:\jirengu\learn-notes\assets\Image-1649689318836.png)

- 如果用的是`ref`，那么得到的是`VueComponent`（也就是组件实例对象）

  ### 用 ref 得到实例对象有什么作用？

- 可以用于组件通信（待深入）

![Image](Image.png)

![Image](./assets/Image-1649690133007.png)
