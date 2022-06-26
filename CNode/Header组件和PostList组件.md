# Header组件

## reset.css使用

- 直接在app.vue中引入，全局自动实现默认设置`@import "./assets/reset.css";`

```css
* {
  padding: none;
  margin: none;
  box-sizing: border-box;
}

ul,
ol,
li {
  list-style: none;
}

a {
  text-decoration: none;
}

a:hover {
  /* font-size: larger; */
}

.clearfix:after {
  content: "";
  display: block;
  clear: both;
}

```

## display:flex实现左右分布

- container使用`display:flex`
- 然后`justify-content:between`就可以

```html
<template>
  <div class="header">
    <img src="../assets/cnodejs_light.svg" alt="cnode标志" />
    <ul>
      <li><a href="#">首页</a></li>
      <li><a href="#">新手入门</a></li>
      <li><a href="#">API</a></li>
      <li><a href="#">关于</a></li>
      <li><a href="#">注册</a></li>
      <li><a href="#">登录</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Header"
};
</script>

<style scoped>
.header {
  display: flex;
  background: #5a5555;
  justify-content: space-between;
}

img {
  width: 100px;
  padding: 10px;
}

ul {
  padding-left: 100px;
}

li {
  display: inline-block;
  padding-right: 20px;
}

a {
  color: #cccccc;
}
</style>

```



# PostList组件

![image-20220609211331264](C:\Users\16435\AppData\Roaming\Typora\typora-user-images\image-20220609211331264.png)



加载成功跟加载较慢时，用两个不同的div

注意接口

![image-20220609211741739](C:\Users\16435\AppData\Roaming\Typora\typora-user-images\image-20220609211741739.png)

参数分析

![image-20220609213700633](C:\Users\16435\AppData\Roaming\Typora\typora-user-images\image-20220609213700633.png)







问题：无法得到json数据

- 目前只能用官方的api，并且后面必须加上要获取的问题
  - https://cnodejs.org/api/v1/topics

- 这个mock的数据暂时用不上
  - http://mock.hunger-valley.com/cnode/api/v1/topics
  - json分析工具HiJson





怎么去拿到想要的数据

需要用到axios插件 `npm install axios`



使用vue时，在哪里引入axios？

- 在main.js中引入
- 然后要使用插件use
- 然后将其绑定到Vue的原型上
  - 这跟use有区别吗



PostList中创造一个函数来获得获得网址中的api中的JSON数据，然后需要在页面加载完之前来执行这个函数，获得数据，该怎样写呢

- 加载成功，去除动画
- 注意要往页面中渲染





![image-20220609223133055](C:\Users\16435\AppData\Roaming\Typora\typora-user-images\image-20220609223133055.png)

































