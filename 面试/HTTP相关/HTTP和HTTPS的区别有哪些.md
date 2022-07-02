## 

不写https浏览器会暴露不安全

![image-20220701203800274](HTTP%E5%92%8CHTTPS%E7%9A%84%E5%8C%BA%E5%88%AB%E6%9C%89%E5%93%AA%E4%BA%9B.assets/image-20220701203800274.png)



HTTP是超文本传输协议

SSL协议的作用是什么

![image-20220701203920147](HTTP%E5%92%8CHTTPS%E7%9A%84%E5%8C%BA%E5%88%AB%E6%9C%89%E5%93%AA%E4%BA%9B.assets/image-20220701203920147.png)

负责网络连接的加密





- JSONP
- CORS
- Nginx代理或者Node.js代理





![image-20220701210810397](HTTP%E5%92%8CHTTPS%E7%9A%84%E5%8C%BA%E5%88%AB%E6%9C%89%E5%93%AA%E4%BA%9B.assets/image-20220701210810397.png)

- 不算同源，音乐域名不一样，没有www
- 但是不比较路径![image-20220701210846910](HTTP%E5%92%8CHTTPS%E7%9A%84%E5%8C%BA%E5%88%AB%E6%9C%89%E5%93%AA%E4%BA%9B.assets/image-20220701210846910.png)





![image-20220701211002665](HTTP%E5%92%8CHTTPS%E7%9A%84%E5%8C%BA%E5%88%AB%E6%9C%89%E5%93%AA%E4%BA%9B.assets/image-20220701211002665.png)

- 相同，默认80
- 如果是https，那么就不相同，因为https是443端口



POSTMAN工具，模拟请求

- 这个工具没有跨域限制，因为它不是浏览器



![image-20220701211309373](HTTP%E5%92%8CHTTPS%E7%9A%84%E5%8C%BA%E5%88%AB%E6%9C%89%E5%93%AA%E4%BA%9B.assets/image-20220701211309373.png)

请求跨域发出去，但是回不来，被浏览器拦截了



JSONP的优点跟缺点是什么

- 缺点是用户认证缺失
- 不支持POST





在使用CORS跨域时，对于复杂请求，如 PATCH，响应 OPTIONS 请求时，要在响应中添加怎样的响应头



- 响应 OPTIONS 请求
- 响应 POST 请求，在响应中添加 Access-Control-Allow-Origin 头



为什么在很早的时候



LocalStorage在HTML5之后才出现



![image-20220701215520351](HTTP%E5%92%8CHTTPS%E7%9A%84%E5%8C%BA%E5%88%AB%E6%9C%89%E5%93%AA%E4%BA%9B.assets/image-20220701215520351.png)



前端不懂cookie

















