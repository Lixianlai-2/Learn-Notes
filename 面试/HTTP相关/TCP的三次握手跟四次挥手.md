![image-20220702110416760](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702110416760.png)



![image-20220702110430978](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702110430978.png)







![image-20220702110459126](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702110459126.png)



三次挥手是为了解决什么问题

![image-20220702110758128](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702110758128.png)



![image-20220702110927848](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702110927848.png)



![image-20220702111028367](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702111028367.png)





面试官你好，这个问题我是知道的。TCP/IP协议是传输层的一个面向连接的安全可靠的传输协议。

三次握手的机制是为了保证能建立一个安全可靠的连接；第一次握手是由客户端发起，客户端会向服务端发送一个报文，报文里面SYN标志位是置1的，当服务端收到这个报文的时候就知道客户端要和我发起一个新的连接，于是服务端就向客户端发送一个确认消息包ACK位置1，以上两次握手之后，对于客户端而言，其实是已经知道了所有信息，就是我既能给服务端发送消息，我还能收到服务端的消息；对于服务端而言，两次握手是不够的，因为到目前为止，服务端只知道一件事情，客户端给我发送的消息我收的到，但是我发给客户端的消息，客户端能不能收到我还不知道。

所以还要进行第三次握手。第三次握手就是当客户端收到服务端发过来的确认消息的报文之后，还要继续给服务端进行一个回应，也是一个ACK位置1的一个确认消息。

通过以上三次连接，不管是服务端还是客户端都彼此知道了，我既能给对方发送消息也能收到对方的消息，那么这个连接就能被安全的建立了。

四次握手机制，也是由客户端首先发起的，客户端会发起一个报文，在报文里面FIN标志位置1；当服务端收到这报文之后，我就知道了客户端想要和我断开连接，但是此时服务端不一定能做好准备，因为当客户端发起断开连接的时候，对于服务端而言它极有可能有未发送完的的消息，它还要继续发送；所以此时对于服务端而言他只能进行一个消息确认，我先告诉服务端，我知道你要和我断开连接了，但是我这还可能没有做好准备，你还需要等我一下，等会我会告诉你；于是，发完这个消息确认包后，可能稍作片刻，它可能会继续发送一个断开连接的报文，一个FIN位置1的报文，是由服务端发给客户端的，这个报文表示了服务端已经做好了断开连接的准备，那么当这个报文发给客户端的时候，客户端同样要给服务端继续发送一个消息确认的报文。一共有四次，通过这四次的相互沟通和连接，我就知道了，不管是服务端还是客户端都已经做好了断开连接的准备，于是连接就可以被断开了。

这是我对三次握手和四次挥手的理解。



能传输任何内容

#### 三次握手机制的目的是什么

为了保证能建立一个安全可靠的连接

#### 什么是TCP

传输控制协议（TCP，Transmission Control Protocol）是一种面向连接的、可靠的、基于字节流的传输层通信协议



![image-20220702112123508](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702112123508.png)

#### 什么是SYN

SYN：同步序列编号（ Synchronize Sequence Numbers ）。 是TCP/IP建立连接时使用的握手信号。 

在客户机和 服务器 之间建立正常的TCP网络连接时

- 客户机首先发出一个SYN消息

- 服务器使用SYN+ACK应答表示接收到了这个消息
- 最后客户机再以 ACK 消息响应。



#### 什么是ACK

ACK (Acknowledge character）即是确认字符。表示发来的数据已确认接收无误。



SYN就是同步，x是序号 ，第x次想跟你同步

acknowledge就是ack的缩写，也就是同意的意思



#### 在脑中想一下三次握手的图片

![image-20220702112935997](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702112935997.png)



![image-20220702113057485](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702113057485.png)



#### 在脑中想一下四次挥手的图片

![image-20220702113134570](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702113134570.png)

#### 什么是FIN

就是FINISH

#### seq是什么的缩写

是Sequence（序列号的缩写）

关闭的一方开始



#### 为什么关闭TCP连接时，第2步和第3步不合并起来呢

2、3 中间服务器很可能还有数据要发送，不能提前发送 FIN

ISN是什么



什么是SYN



#### HTTP/1.1 和 HTTP/2 的区别有哪些？

![image-20220702114928977](C:/Users/Li/AppData/Roaming/Typora/typora-user-images/image-20220702114928977.png)



什么是非对称加密



公钥存在那里

- 























