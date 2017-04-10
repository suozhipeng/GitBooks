# 前端工程师应该对 HTTP 了解到什么程度？从哪些途径去熟悉更好？

[MrPeak的回答](https://www.zhihu.com/question/20391668/answer/44411176)

---
## HTTP的常见知识点

1. http 的组成结构要清楚，`request line`,`status line`,`head` 和`body` 是什么样子。
- 常见的 `status code`有哪些， 200，404，1xx，3xx，5xx 各代表什么含义。
- request 的时候一般分 `post`和`get`，两个啥区别要理解，get的时候 `url encode`又是干嘛用的？post 一般body 里有哪几种类型（content-type）？
- head 里面常用的几个字段有哪些要知道，比如说`connection`,`content-type`,`cache-control`...
    - 说到`cache-control`,要知道文件的缓存和过期机制..
    - 说到`connection`,**keep-alive**要知道有什么用
    - 说到 keep-alive，要知道http通道和 socket tcp 通道啥区别？http 又怎么保持长连接？poling 是什么之类的..
    - 说到 tcp， 三次握手和 slow start 要知道是啥，tcp 的header前20个字节各代表啥要明白，option选择了解...
    - tcp header 里面第14个字节所代表的8个flag要明白，你用 tcpdump抓包的时候总要能理清一个http请求从哪里开始，哪里结束..
    - tcpdump怎么用要知道，常用的参数要存到你的大脑中
- 抓包的时候遇到https你就抓瞎了，但是https是啥要知道的。
    - 说到https，PKI是什么就要明白
    - tcpdump 是牛刀，有时候curl就够用了，curl 要知道是什么
    - http 是明文协议，安全性没法保证，怎么让里面的数据更安全，常用的对称加密算法要会用。
    - http 是明文协议，有时候运营商会截获然后给你加点料，你要有提防.

总而言之，你最好对从 
> 用户敲键盘，到数据怎么经过TCP/IP 5层协议，然后怎么到达server，数据最后怎么回来到用户显示器上，整个过程都清楚点

对了，你是前段工程师，JavaScript，CSS，DOM应该是如数家珍吧，body里装的什么东西一眼要能看明白的
    