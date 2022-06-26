# 手写Ajax

获得Ajax请求的几种方式

- Axios
- jQuery
- VueResource
- window.fetch

```javascript
const ajax = (method, url, data, success, fail) => {
  var request = new XMLHttpRequest();
  request.open(method, url);
  request.onreadystatechange = function () {
    // XMLHttpRequest.readyState === 4的时候，代表请求操作已经完成。这意味着数据传输已经彻底完成或失败。
    if (request.readyState === 4) {
      // HTTP状态码200-300之间代表服务器请求成功，404代表请求页面不存在，304代表可以使用缓存的内容
      if (
        (request.status >= 200 && request.status < 300) ||
        request.status === 304
      ) {
        success(request);
      } else {
        fail(request);
      }
    }
  };
  request.send();
};
```

## http响应状态码

#### 304

- 说明无需再次传输请求的内容，也就是说可以使用缓存的内容

- 这是用于缓存的目的。它告诉客户端响应还没有被修改，因此客户端可以继续使用相同的缓存版本的响应。

#### 200-299

- 成功响应

```javascript
const request = new XMLHttpRequest()
request.open('get')

```





