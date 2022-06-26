# 请简述DOM事件模型

要背的要点

![image-20220624194642096](D:\learn-notes\assets\image-20220624194642096.png)



怎么去选择驳货还是冒泡

传false或者不传，就是冒泡阶段

```javascript
elem.addEventListener('click',function(){console.log('点击了')}, {capture: true})
elem.addEventListener('click',function(){console.log('点击了')},true)

// 传false或者不传，就是冒泡阶段
elem.addEventListener('click',function(){console.log('点击了')},false)
elem.addEventListener('click',function(){console.log('点击了')})
```



# DOM事件委托

用大白话说一个event.target和event.curentTarget

![image-20220624203414829](D:\learn-notes\assets\image-20220624203414829.png)

Vue跟React都是绑定到根元素上面



## 实现一个最简单的事件委托

```javascript
ul.addEventListener('click',function(e) {
    if(e.target.tagName.toLowerCase() === 'li') {
        fn() // 执行某个函数
    }
})

// bug 在于，如果用户点击的是 li 里面的 span，就没法触发 fn，这显然不对。
```





metches的作用是什么

- 写个简单例子



怎么查看事件监听

![image-20220624204055276](D:\learn-notes\assets\image-20220624204055276.png)

































