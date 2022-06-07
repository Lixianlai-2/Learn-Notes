# Canvas和SVG的区别是什么

### 分别的作用

- Canvas是用**笔刷**进行2D绘图的
- SVG是用**标签**绘制矢量图的
- 它们都用于绘制2D图像

### 区别

- 但是Canvas是用来绘制**位图**的，而SVG是绘制**矢量图**的
- SVG节点较多，渲染较慢。Canvas渲染快，但是写起来稍显复杂（因为没有节点）
- SVG支持分层和事件，Canvas不支持，但是可以用库实现

### 位图跟矢量图的区别

#### 位图

位图图像也称为点阵图像，位图使用我们称为**像素**的一格一格的小点来描述图像

#### 矢量图

矢量图是根据**几何特性来绘制图形**，是用**线段和曲线描述图像**，矢量可以是**一个点或一条线**，矢量图只能靠**软件**生成，矢量图文件占用内在**空间较小**，因为这种类型的图像文件包含独立的分离图像，可以自由无限制的重新组合

#### 区别

- **矢量图形与分辨率无关**，可以将它缩放到任意大小和以任意分辨率在输出设备上打印出来，都不会影响清晰度

- 而位图是由一个一个像素点产生，当放大图像时，像素点也放大了，但每个像素点表示的颜色是单一的，所以在位图放大后就会出现咱们平时所见到的马赛克状。

# BFC是什么

BFC就是块级格式化上下文

### 常见的触发它的方式

- 浮动元素
- 弹性元素（flex布局的直接子元素）
- 绝对定位元素（position为absolute或者fixed)
- 行内块级元素`inline-block`
- overflow值为auto/hidden/scrool，不包括visible的元素

### 解决的问题

- 可以用来清除浮动
- 避免垂直方向上的margin合并

# 如何实现垂直居中

### 如果父元素没有设置height

- 那么只需要设置将parent部分设置padding

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>JS Bin</title>
    <style>
      .parent {
        padding: 30px;
        border: 1px solid green;
      }
      .child {
        background: red;
        border: 1px solid blue;
        width: 100px;
        height: 100px;
        padding: 20px;
        margin: auto;
      }
    </style>
  </head>
  <body>
    <div class="parent">
      <div class="child"></div>
    </div>
  </body>
</html>

```

### 如果把父元素的height写死了

#### 用div模拟table

##### 父级元素

- 用`display:table-cell`
- 用`vertical-align:middle`
- 用`text-align:center`让子级的行内元素居中

##### 子级元素

- `display:inline-block`

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Div模拟table</title>
    <style>
      .father {
        display: table-cell;
        width: 200px;
        height: 200px;
        background: skyblue;
        vertical-align: middle;
        text-align: center;
      }
      .son {
        border: 1px solid red;
        display: inline-block;
        width: 100px;
        height: 100px;
        background: red;
      }
    </style>
  </head>
  <body>
    <div class="father">
      <div class="son"></div>
    </div>
  </body>
</html>

```

#### margin:auto和设置偏移

- 父级设置`position:relative`
- 子级设置`positon:absolute`
  - `top/right/left/bottom`全部设置为0，如果子级没有设计宽高，子级会占满整个父级。因为这四个位置，是相对于父级而设置的
    - ![image-20220607153720349](C:\Users\16435\AppData\Roaming\Typora\typora-user-images\image-20220607153720349.png)
    - ![image-20220607154745117](C:\Users\16435\AppData\Roaming\Typora\typora-user-images\image-20220607154745117.png)
  - 然后设置宽高，子级会按照我们的设置来显示。但子级的虚拟占位，依然是撑满了了整个父级
    - ![image-20220607154256150](C:\Users\16435\AppData\Roaming\Typora\typora-user-images\image-20220607154256150.png)
  - 然后`margin:auto`，它就会上下左右都居中了
    - ![image-20220607154338769](C:\Users\16435\AppData\Roaming\Typora\typora-user-images\image-20220607154338769.png)

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>用margin-top</title>
    <style>
      .father {
        position: relative;
        width: 200px;
        height: 200px;
        background: skyblue;
        margin: auto;
      }
      .son {
        position: absolute;
        border: 1px solid green;
        width: 100px;
        height: 100px;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        margin: auto;
      }
    </style>
  </head>
  <body>
    <div class="father">
      <div class="son"></div>
    </div>
  </body>
</html>

```

#### 根据父级元素设置负margin

- 父级元素相对定位
- 子级元素绝对定位
- 设置`top/left`
- 然后设置`marin-left和margin-top`
  - 负的具体px
  - 负的比例

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>JS Bin</title>
  </head>
  <style>
    .parent {
      height: 600px;
      border: 1px solid red;
      position: relative;
    }
    .child {
      border: 1px solid green;
      width: 300px;
      position: absolute;
      top: 50%;
      left: 50%;
      margin-left: -150px; // 这里可改为-50%
      height: 100px;
      margin-top: -50px;// 这里根据height上调
    }
  </style>
  <body>
    <div class="parent">
      <div class="child">
        一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字
      </div>
    </div>
  </body>
</html>

```

#### 使用`transform:translate`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>JS Bin</title>
    <style>
      .parent {
        height: 600px;
        border: 1px solid red;
        position: relative;
      }
      .child {
        border: 1px solid green;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }
    </style>
  </head>
  <body>
    <div class="parent">
      <div class="child">
        一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字
      </div>
    </div>
  </body>
</html>

```

#### 使用flex布局

- 父级元素
  - `display:flex`
  - `justify-content:center`
  - `align-items:center`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>JS Bin</title>
    <style>
      .parent {
        height: 600px;
        border: 1px solid red;
        /* position: relative; */
        display:flex;
        align-items:center;
        justify-content:center;
      }
      .child {
        border: 1px solid green;
        position: absolute;
        width:100px;
      }
    </style>
  </head>
  <body>
    <div class="parent">
      <div class="child">
        一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字
      </div>
    </div>
  </body>
</html>

```

#### 使用grid

- 父级用`display:grid`
- 子级
  - `align-self:center`
  - `justify-self:center`

```html
<html>
  <head>
    <meta charset="utf-8" />
    <title>JS Bin</title>
    <style>
      .parent {
        height: 600px;
        border: 1px solid red;
        display: grid;
       
      }
      .child {
        border: 1px solid green;
        width:100px;
        align-self:center;
        justify-self:center;
      }
    </style>
  </head>
  <body>
    <div class="parent">
      <div class="child">
        一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字一串文字
      </div>
    </div>
  </body>
</html>
```

# CSS选择器的优先级

- 选择器越具体，其优先级越高
  
- 比如id整个页面只有一个，而class却可以有很多个，那么id的优先级就比class高
  
- 相同层级的选择器，后面的覆盖前面的

- 属性后面加上!important，优先级最高，但是要少用

  - ```css
    .foo[style*="color: red"] {
      color: firebrick !important;
    }
    ```

# 如何清除浮动

在要清除浮动的那个元素的父级元素上添加.clearfix

而clearfix中的内容是

```css
.clearFix:after{
    display:block;
    content:'';
    clear:both;
}
```

















