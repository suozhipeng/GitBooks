# nginx、swoole高并发原理初探
[原文链接](https://segmentfault.com/p/1210000008951495/read)

---
- 同步、异步
- 阻塞、非阻塞
- Nginx 如何处理高并发
- I/O复用
- 一个代理可以同时观察许多I/O流事件
- epoll代理：当连接有I/O流事件产生的时候，epoll就会去告诉进程哪个连接有I/O流事件产生，然后进程就去处理这个进程。
- 基于epoll的Nginx
- Nginx是基于epoll的，异步非阻塞的服务器程序
- Reactor模型

I/O复用异步非阻塞程序使用经典的Reactor模型
> Reactor顾名思义就是反应堆的意思，它本身不处理任何数据收发。只是可以监视一个socket(也可以是管道、eventfd、信号)句柄的事件变化。
- swoole: **多线程Reactor+多进程Worker**
> 因为reactor基于epoll，所以每个reactor可以处理无数个连接请求。 如此，swoole就轻松的处理了高并发。

- swoole如何实现异步I/O
- swoole的worker进程有2种类型：
一种是 普通的worker进程，
一种是 task worker进程。

`worker`进程是用来处理普通的耗时不是太长的请求；
` task worker`进程用来处理**耗时较长的请求**，比如数据库的`I/O`操作。

![异步Mysql举例](/assets/3930775123-58e4a555eb4cb_articlex.jpeg)
**如此，通过worker、task worker结合的方式，我们就实现了异步I/O**
