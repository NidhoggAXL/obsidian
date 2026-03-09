# 一、host配置

host设置主机地址：

 - 默认值是localhost；
 - 如果希望其他地方也可以访问，可以设置为 0.0.0.0；

localhost 和 0.0.0.0 的区别：

 - localhost：本质上是一个域名，通常情况下会被解析成127.0.0.1;
 - 127.0.0.1：回环地址(Loop Back Address)，表达的意思其实是我们主机自己发出去的包，直接被自己接收;
	 - 正常的数据库包经常 应用层 - 传输层 - 网络层 - 数据链路层 - 物理层 ;
	 - 而回环地址，是在网络层直接就被获取到了，是不会经常数据链路层和物理层的; 
	 - 比如我们监听 127.0.0.1时，在同一个网段下的主机中，通过ip地址是不能访问的;
 - 0.0.0.0：监听IPV4上所有的地址，再根据端口找到不同的应用程序;
	 - 比如我们监听 0.0.0.0时，在同一个网段下的主机中，通过ip地址是可以访问的;


# 二、port、open、compress

port设置监听的端口，默认情况下是8080

open是否打开浏览器：

 - 默认值是false，设置为true会打开浏览器；
 - 也可以设置为类似于 Google Chrome等值；

compress是否为静态文件开启gzip compression：

 - 默认值是false，可以设置为true；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1773044164000rzkmzh.png)

