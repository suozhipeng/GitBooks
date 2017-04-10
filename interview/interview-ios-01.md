# Interview about iOS
---
[**原文链接**](http://blog.tracyone.com/2015/08/22/%E8%B7%B3%E6%A7%BD%E9%9A%8F%E6%83%B3/#more)
**iOS底层实现**

有一些特别基础的类似消息传递区别，转发机制这种的大多只是带过的。

1. runtime的使用场景？为什么能做到运行时替换方法？如果是在C语言中如何实现？

- block的实现？注意事项？为什么能够获取外部变量？

- runloop是什么？哪些场景会用？有哪些源，通知？

- autoreleasePool的实现原理？如何保证嵌套pool的正确管理？

- 内存管理机制？weak如何实现？

- 多线程中GCD，OperationQueue使用场景？多线程中碰到的挑战？如何解决？

这些问题大多在实际开发中都会碰到，之前也有去看过Objc的源码，所以大多数都回答出来了。

**iOS框架实现**

主要考了缓存库，网络库，动态配置，hybrid以及hotfix的实现。

1. 缓存策略？如何保证多线程下的安全读写？顺便还问了文件目录的区别？然后还问了下Unix下的文件I/O。

- 网络协议？对象Json映射？加密策略，区别？然后有问到Unix下的socket。

- 动态配置主要问的是一种想法，主要就是容器的搭建，组件的可配置化，后台系统的维护。

- hybrid的原理？js调用Objc的策略？区别是什么？路由机制？然后还问了一些js的相关问题。

- hotfix用了哪些技术？wax和jsPatch区别？jsPatch实现原理？如何解决C中的数据结构和js中的对象映射等。

**计算机基础**

这方面一般都是对方的技术总监问的，也是被面的最惨的地方，回答的零零散散，接下来要好好的学习下。

1. 操作系统（进程，异步I/O，线程的区别？线程同步机制？线程局部存储机制？内核态，用户态是什么？）

- 计算机网络（http如何保证长连接？tcp窗口滑动机制？路由算法？https的链接过程）

- 算法与数据结构（主要考了一些ACM的题目，常规算法的设计思路？数据结构和抽象数据类型的关系等）

幸亏曾经参加过ACM比赛，在算法那一块回答的还算可以。

**开发的思路**

这一方面考的很灵活，主要是现场让你设计一个功能。

1. 让你设计如何保证UDP的可靠性？

- 当App达到一定量级后，如何拆分工程来达到多部门协作？

- 如何设计一个测试，来定位到webview的内存泄露点？

**看过的书**
```
基础理论：            深入理解计算机系统（第2版）

Objc:                Objc编程全解+Objc高级编程+Effective Objc2.0

编程语言理论：            程序设计语言——实践之路（第3版）

算法与数据结构：        编程珠玑（第2版）+数据结构与算法分析(c语言)

计算机网络：            TCP/IP卷1 

OS:                    Linux私房菜+Unix高级编程

编程实践：            代码大全（第2版）+编程之美

面向对象程序设计：        设计模式+敏捷开发原则

专业开发：            程序员修炼之道：从小工到专家+程序员职业素养

项目管理：            人月神话
```
**iOS学习之路**


```
iOS：

General & Xcode
Laguage (runtime)
Data Manage (coredata,file)
User Experience (uikit)

Performance & Security (内存，多线程)
Networking & Internet
Audio & Video
Graphics & Animation
Swift

工具：
linux：（正则，shell（awk，管道，重定向），shell script）
js：（node，HTML，CSS）
git：（github，console）
mac：（Charles，dash，sublime，Alfred）
反编译：（classdump，IDA，reveal）

计算机理论：
OS
网络
数据结构&算法
C标准库

架构：
服务端
设计模式，思想（结构化，对象，函数式）
敏捷，重构
代码质量（规范，review）
程序员素养
```


