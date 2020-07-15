Socket介绍

1. ##### 什么是Socket

   计算机通信领域，socket被翻译成“套接字”，计算机之间进行通信的一种方式。

   简单概况，建立连接、数据传输、关闭连接

2. ##### 网络中进程如何通信

   Tcp/Ip协议族(应用层、传输层、网络层、数据链路层)；(ip地址，协议，端口)三元组

3. ##### Socket怎么通信

   a.面向连接的数据传输方式（http）  确保数据的正确性

   b.无连接的数据传输方式（udp）user datagram protocol  只管传输（例：语音、视频）

4. ##### TCP/IP协议

   TCP(传输控制协议)和IP(网际协议)提供点对点的链接机制

   TCP**建立连接**是要传输三个数据包，俗称三次握手

   TCP断开连接，俗称四次握手

5. OSI模型

   ​				 ![img](https://upload-images.jianshu.io/upload_images/11362584-d6275ac25abac5cc.jpeg?imageMogr2/auto-orient/strip|imageView2/2/format/webp) 

   

    	![img](https://upload-images.jianshu.io/upload_images/11362584-ec76f69e2ea76d41.jpeg?imageMogr2/auto-orient/strip|imageView2/2/format/webp) 