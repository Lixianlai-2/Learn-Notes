# HTTP有哪些缓存方案

![image-20220701105844108](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701105844108.png)

### 打开网页时发生了什么

- CPU计算，页面渲染，网络请求等
- 其中网络请求耗时较长，需要加载`html/css/js/img`等资源

- 如果我们进入网站时不需要等待下载，直接从内存中获取了这些数据，那么打开网站的速度自然就变快了（减少网络请求的体积和数量）。

### 什么是缓存

- 缓存是保存资源副本
- 并在下次请求时直接使用该副本的技术。

##### 具体操作

- 当 Web 缓存发现请求的资源已经被存储

- 它会拦截请求，返回该资源的拷贝
- 而不会去源服务器重新下载。

##### 缓存的好处是什么

- 重复使用以前获取的资源。

- Web 缓存减少了等待时间和网络流量
- 因此减少了显示资源表示形式所需的时间

## `HTTP1.1`

![image-20220630221956270](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630221956270.png)

#### 强缓存

![image-20220701162303056](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701162303056.png)

- 第一次发送请求
- 服务器返回资源和资源标识
- 将资源存储在本地存储中

![image-20220701162049596](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701162049596.png)

- 第二次发送请求和资源标识
- 服务器通过资源标识判断是否为最新的资源（或者资源是否更新）
  - 如果是最新的资源，服务器返回304状态码，直接从缓存中拿资源



那么资源标识是什么呢？

- Last-Modified:资源上一次修改的时间
- Etag：资源对应的唯一字符串







![image-20220630222134860](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630222134860.png)

##### 什么是强缓存

- 简单来说，遇到请求，直接从本地存储中找

#### `Cache-Control:max-age`

- 设置缓存存储的最大周期，超过这个时间缓存被认为过期 (单位秒)
- 在响应头中写，自动缓存一个小时

![image-20220630223818755](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630223818755.png)

- 如果一小时内，如果访问相同的`url`，就不发请求

![image-20220630223949994](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220630223949994.png)

### Etag

![image-20220701162837660](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701162837660.png)

- 浏览器第一次发送请求
- 服务器返回资源跟资源标识

![image-20220701162846709](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701162846709.png)

- 浏览器第二次发送请求，同时附带上资源标识If-None-Match
  - 这里If-None-Match的值，就是之前服务器返回的Etag

![image-20220701163007623](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701163007623.png)

- JS文件一般都是以毫秒为单位的

![image-20220701163355886](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701163355886.png)

这两个东西都是浏览器网服务器中发送的





#### Etag是怎么产生的？

> Etag是属于HTTP **1.1**属性，它是由**服务器生成**返回给前端
>
> 当你**第一次**发起HTTP请求时，**服务器**会返回一个**Etag**
>
> 并在你第二次发起同一个请求时，客户端会同时发送一个If-None-Match，而它的值就是Etag的值（此处由发起请求的客户端来设置）。
>
> 服务器会比对这个客服端发送过来的Etag是否与服务器的相同
>
> 如果相同，就将If-None-Match的值设为false，返回状态为304，客户端继续使用本地缓存，不解析服务器返回的数据（这种场景服务器也不返回数据，因为服务器的数据没有变化嘛）

- 发送请求后，服务器返回资源跟一堆header，其中包括了Etag

  > 服务器会为每份资源分配对应的ETag值。 
  >
  > 当资源更新时，Etag的值也需要更新。
  >
  > 生成Etag值时没有统一的算法规则，而仅仅是有服务器来分配。
  >
  > 且Etag的优先级高于Last-Modified。

### If-None-Match（如果不匹配）

如果不相同，就将If-None-Match的值设为true，返回状态为200，客户端重新解析服务器返回的数据

#### 是什么

- If-None-Match 是一个条件式请求首部
- 当且仅当服务器上没有任何资源的 ETag 属性值与这个首部中列出的相匹配的时候，服务器端才会返回所请求的资源，响应码为 200 
  - ![image-20220701151023991](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701151023991.png)
- 采用 GET 或 HEAD  方法，来更新拥有特定的ETag 属性值的缓存。





浏览器发送请求

- 判断有没有本地缓存（强缓存）
  - 没有，直接去服务器请求资源
  - 有本地缓存
    - 判断本地缓存是否过期
      - 没有过期

## `http1.0`

> HTTP 1.0协议中的。简而言之，就是告诉浏览器在约定的这个时间前，可以直接从缓存中获取资源（representations），而无需跑到服务器去获取。
>
> **另：**Expires因为是对时间设定的，且时间是Greenwich Mean Time （GMT），而不是本地时间，所以对时间要求较高。

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

![image-20220701162658619](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701162658619.png)

- Last-Modified是放在响应头里面的
- If-Modefied-Since是放在请求头里面的 

- 一些文件也许会周期性的更改，但是他的内容并不改变(仅仅改变的修改时间)，这个时候并不希望客户端认为这个文件被修改了重新GET;
- 某些文件修改非常频繁，1秒内修改了N次，If-Modified-Since能检查到的粒度是秒级的，这种修改无法判断
- 某些服务器不能精确的得到文件的最后修改时间；



#### 什么是TCP？

TCP 协议的全称是 `Transmission Control Protocol` 的缩写，意思是`传输控制协议`，HTTP 使用 TCP 作为通信协议，这是因为 TCP 是一种可靠的协议，而`可靠`能保证数据不丢失。







## 放anki中

- http缓存机制主要在http响应头中设定
- 响应头中相关字段为Expires、Cache-Control、Last-Modified、If-Modified-Since、Etag。
- 同时设置了Cache-Control和Expires,Cache-Control的优先级也高于Expires。
- Etag是由谁生成的？Etag是属于HTTP 1.1属性，它是由服务器生成返回给前端，
- 当你第一次发起HTTP请求时，服务器会返回一个Etag
- 并在你第二次发起同一个请求时，客户端会同时发送一个If-None-Match，而它的值就是Etag的值（此处由发起请求的客户端来设置）。
- ![image-20220701152850628](HTTP%E6%9C%89%E5%93%AA%E4%BA%9B%E7%BC%93%E5%AD%98%E6%96%B9%E6%A1%88.assets/image-20220701152850628.png)
- 服务器会比对这个客服端发送过来的Etag是否与服务器的相同
  - 如果相同，就将If-None-Match的值设为false，返回状态为304，客户端继续使用本地缓存，不解析服务器返回的数据（这种场景服务器也不返回数据，因为服务器的数据没有变化嘛）
  - 如果不相同，就将If-None-Match的值设为true，返回状态为200，客户端重新解析服务器返回的数据



[Etag & If-None-Match 专题 - 沧海一滴 - 博客园 (cnblogs.com)](https://www.cnblogs.com/softidea/p/5986339.html)
