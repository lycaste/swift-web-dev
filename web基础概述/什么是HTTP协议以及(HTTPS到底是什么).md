# http协议


 [知识共享署名-相同方式共享 3.0 中国大陆许可协议](https://creativecommons.org/licenses/by-sa/3.0/cn/)
#前言
这部分笔记我本来是不敢放出来的，因为网上关于HTTP的资料太多了，HTTP权威指南，图解HTTP，都是非常值得去读的书，而我这种业余程序员写出来东西准确性很难有保证。
#http协议，端口，加密与封帧
一般来说，我们使用的web程序都是运行在TCP/IP  协议之上，通过socket进行通信。而HTTP协议就是描述了程序之间交换数据的一种方法，只要遵循它就能很方便的交流，它的大致流程 ：

客户端(暂且认为都是浏览器)向www.baidu.com发起TCP连接->百度服务器接受连接->客户端发送包含URL的HTTP请求->服务器接受请求，并且返回返回内容->浏览器接受响应，并且开始解析渲染内容->服务器关闭连接

以上大致就是当你在浏览器中输入一个网址发生的后的事情，当然远远不止这些，还有例如**DNS的Lookup**以及**TCP Connection**这些都是及其复杂的过程。值得注意的是浏览器一旦发送了完整的请求，客户端就会进行等待，直到从服务器接受到完整的响应。至少在目前的HTTP/1.1版本的协议中，是不允许客户端在尚未收到上一个请求的响应之前就在**同一个**套接字上开始发送第二个响应。

什么是HTTP协议，其实HTTP协议就是一串固定格式的文本

| 1            | 2    | 3            | 4     | 5      | 6     |
| ------------ | ---- | ------------ | ----- | ------ | ----- |
| http方法       | sp   | URL          | SP    | http版本 | cr-lf |
| header field | ：    | field -value | cr-lf |        |       |
| body         |      |              |       |        |       |


| 1            | 2    | 3            | 4     | 5    | 6     |
| ------------ | ---- | ------------ | ----- | ---- | ----- |
| http版本       | sp   | 状态码          | SP    | 状态   | cr-lf |
| header field | ：    | field -value | cr-lf |      |       |
| header field | ：    | field -value | cr-lf |      |       |
| cr-lf-cr-lf  |      |              |       |      |       |
| body         |      |              |       |      |       |

   

Http 请求
>GET /hello.htm HTTP/1.1                                    
>User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)           
>Host: example.com                               
>Accept-Language: en-us         
>Accept-Encoding: gzip, deflate       

Http 响应
> HTTP/1.1 200 OK                                  
> Date: Mon, 27 Jul 2009 12:28:53 GMT         
> Server: Apache/2.2.14 (Win32)          
> Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT       
> Content-Length: 88      
> Content-Type: text/html
> Connection: Closed

表示请求从get开始。响应以表示版本号的HTTP/1.1开始，在响应头后面跟了一个空行。然后是几行JSON文本。请求和响应的标准名称都是HHTP消息，每个消息都是由以下三个部分组成。
1. 在请求消息中，第一行包含一个方法名和要请求的温度；在响应消息中，第一行包含了返回码和描述信息。无论是在请求还是响应消息中，第一行都是以回车和换行来结尾（ASCII 13 10）。
2. 第二部分包含0个或者多个头信息，每个头信息由一个key，一个冒号，一个value组成（HTTP协议是区分大小写的）。每个头信息也必须由cr-lf格式来结尾，在头信息结束之后必须在跟上一个空行，这个空行由CR—LF—CR-LF组成，这个是必须的，无论有没有头信息。
3. 第三部分是由一些可选的消息体组成。





#request与respone
#路径和主机
#状态码
#缓存
#传输编码
#content
#http认证
#cookies
#连接，Keep-Alive和httplib
#SSL、TLS和密码学
#HTTP和浏览器安全问题
#（实践）如何自己手写一个http代理