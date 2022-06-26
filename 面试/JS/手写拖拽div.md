手写拖拽div

## 要点：

- 监听document，不能只监听div

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <style>
      div {
        border: 1px solid blue;
        position: absolute;
        top: 0;
        left: 0;
        width: 100px;
        height: 100px;
      }

      * {
        margin: 0;
        padding: 0;
      }
    </style>
  </head>
  <body>
    <div id="box"></div>
    <script>
      // 用来判断是否拖拽了
      var dragging = false;
      // 判断位置是否变化？
      var position = null;

      box.addEventListener("mousedown", function (e) {
        dragging = true;
        //得到box区域内的，按下鼠标左键的横纵坐标
        position = [e.clientX, e.clientY];
      });

      // 对整个文档进行监听
      document.addEventListener("mousemove", function (e) {
        // 如果没有点击box时，就不管他
        if (dragging === false) return;
        const x = e.clientX;
        const y = e.clientY;
        // 当前的横坐标减去在box点击时的初始坐标
        const deltaX = x - position[0];
        // 得到纵坐标差值，根据差值去改变竖坐标
        const deltaY = y - position[1];
        // 将字符串转化为number，没有设置radix，默认为10进制
        const left = parseInt(box.style.left || 0);
        //找到box的left坐标
        const top = parseInt(box.style.top || 0);
        box.style.left = left + deltaX + "px";
        box.style.top = top + deltaY + "px";
        position = [x, y];
      });

      document.addEventListener("mouseup", function (e) {
        dragging = false;
      });
    </script>
  </body>
</html>

```



## 知识补充

#### `clientX和clinenY`的作用是什么

- `clientX`它提供事件发生时的应用客户端区域的水平坐标 (与页面坐标不同)
- `clinenY`它提供事件发生时的应用客户端区域的垂直坐标 (与页面坐标不同)

#### `parseInt`的作用

- `parseInt(string, radix)`  解析一个字符串
- 并返回指定基数的十进制整数
- 把第一个参数看成是一个数的n进制，返回的值却是十进制
- radix 是 2-36 之间的整数，表示被解析字符串的基数。
- 简单来说，第二个参数就代表进制
- 如果 radix 没有指定或者为 0，参数会被假定以 10 为基数来解析
- `parseInt`的第一个参数string要小于第二个参数radix,所以`parseInt('3', 2)`等于`NaN`;
- 如果第一个参数string大于等于第二个参数radix，那么直接返回NaN

![image-20220626091012560](D:\learn-notes\assets\image-20220626091012560.png)

#### `Math.pow(base, exponent)` 

5的2次方`Math.pow(5,2) // 25` 

#### `parseInt('123',5)`怎么计算？

![image-20220626090739831](D:\learn-notes\assets\image-20220626090739831.png)

![image-20220626090857806](D:\learn-notes\assets\image-20220626090857806.png)