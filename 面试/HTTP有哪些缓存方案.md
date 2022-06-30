# HTTP有哪些缓存方案

![image-20220630204940865](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630204940865.png)



强缓存在本地的上（1年内都用这个，不用再请求了）





返回的是304,就继续用

返回200就删了，用最新的



1.0

再特定的时间后过期

如果过了特定时间，要不要删掉？



![image-20220630210342193](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630210342193.png)

Bug:用户时间错乱

## 什么是缓存

- 缓存是保存资源副本
- 并在下次请求时直接使用该副本的技术。

#### 具体操作

- 当 Web 缓存发现请求的资源已经被存储

- 它会拦截请求，返回该资源的拷贝
- 而不会去源服务器重新下载。

## 为什么我们需要HTTP缓存

> 重复使用以前获取的资源。
>
> Web 缓存减少了等待时间和网络流量，因此减少了显示资源表示形式所需的时间

当我们打开一个新的网页的时候，需要加载html/css/js/img等资源，这个过程是较为缓慢的。

如果我们进入网站时不需要等待下载，直接从内存中获取了这些数据，那么打开网站的速度自然就变快了。

缓存就是把之前请求的资源存储浏览器中



#### 从输入网站地址，到加载出页面，会有哪些操作？

- 其中网络请求的耗时相对较长

![image-20220630214408945](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630214408945.png)



![image-20220630212852524](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630212852524.png)

## `HTTP1.1`

![image-20220630221956270](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630221956270.png)

### 强缓存

![image-20220630222134860](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630222134860.png)

##### 什么是强缓存

- 简单来说就是本地存储，遇到请求直接从本地存储中找

##### 在读取本地缓存的时候，要做什么事情

- 判断缓存是否过期
  - 如果没有过期，直接读取
  - 如果缓存已经过期了，判断内容是否过期
    - 内容没有过期，返回304,
    - 内容过期了，返回200，重新获取内容
- 通过什么来获得缓存中的内容

##### 用什么来设置缓存时间

- `Cache-Control:max-age`

  - 设置缓存存储的最大周期，超过这个时间缓存被认为过期 (单位秒)
  - 在响应头中写，自动缓存一个小时

  ![image-20220630223818755](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630223818755.png)

  - 如果一小时内，如果访问相同的url，就不发请求

  ![image-20220630223949994](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630223949994.png)

##### 用什么来判断缓存是否过期

- 访问一个网站后，会给一个特征值，也就是ETag，在协商的时候使用
- ![image-20220630224321594](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630224321594.png)

- 依据就是这个Etag
- 把文件的特征记录一下

##### 怎么去问是否过期呢？

![image-20220630224634193](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630224634193.png)

- 浏览器向服务器发送一个询问，Etag能不能删
- 服务器会返回304代表不能删，内容还没过期，可以继续用
- 服务器返回200代表可以删，内容过期了，直接获取新的资源吧

##### `Etag`

- 是资源的特定版本的标识符
- 有助于防止资源的同时更新相互覆盖（“空中碰撞”）。

有一个特征值，方便再内容协商时找到它

缓存过期之后用Etag循环（文件的特征值？）

### 协商缓存

![image-20220630222118748](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630222118748.png)

- 浏览器发送了请求，服务器返回资源，然后被存储在本地缓存中

- 然后通过Cache-control（缓存控制）来设置缓存请求
- 通过`max-age=<seconds>`来设置缓存存储的最大周期，超过这个时间缓存被认为过期 (单位秒)
  - 通常是设置1年的秒数



![image-20220630213005973](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213005973.png)



![image-20220630214637689](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630214637689.png)

把重复资源放到本地存储中



![image-20220630214604138](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630214604138.png)





![image-20220630213110882](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213110882.png)



![image-20220630213246624](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213246624.png)

![image-20220630213314545](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213314545.png)

 单位是秒



![image-20220630213403237](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213403237.png)

<img src="C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213415004.png" alt="image-20220630213415004" style="zoom:33%;" />

网页框架如果不经常改变，就可以这样设置



![image-20220630213511511](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213511511.png)

每次都要请求资源



![image-20220630213559502](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213559502.png)

![image-20220630213629525](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213629525.png)

<img src="C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213640588.png" alt="image-20220630213640588" style="zoom:80%;" />

![image-20220630213710644](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213710644.png)

![image-20220630213723514](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630213723514.png)



什么时候



## `http1.0`

#### 用什么来设置缓存时间

![image-20220630224944351](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630224944351.png)

#### 用什么来表示特征值？

- 最后一次更新的时间
- ![image-20220630225017595](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630225017595.png)

#### 谁来问过期的缓存要不要删？

- 通过最后一次修改来设置

#### Expires的问题是什么

- 时间错乱

#### Last-Modified的问题是什么？

- 如果有一个文件在一秒钟之内改了10次呢
- 精度不够



