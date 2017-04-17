# 目录

原文链接：[http://www.jianshu.com/p/437428330df3](http://www.jianshu.com/p/437428330df3)

---

## [前言：程序的演化，从二进制到整个世界](http://www.jianshu.com/p/7593bf463ab6)

1. Hello World在更早之前
2. 图灵和冯·诺伊曼
3. 您好，世界
4. 来到现在
5. 关于此书

### [第一章 重新认识Objective-C](http://www.jianshu.com/p/74eb039b28e3)

1. OC的起源
2. OC的特性
3. 面向对象三原则（封装，继承，多态）

   3.1 封装

   3.2 继承

   3.3 多态
   > 允许不同类的对象对同一消息作出响应。 
   子类对象调用父类方法

   1. OC的动态性 
   > **Runtime：运行时，重要的消息机制、发送消息**

   4.1 动态类型、动态绑定和动态加载
   > 必须到运行时(runtime)才会做一些事情。
   **动态类型，就是id类型。**
   **动态绑定(dynamic binding)需要用到@selector/SEL。**
   **动态加载就是根据需求动态地加载资源，在运行时加载新类。**

   4.2 Method Swizzling

   1. RunLoop
   > **让线程能随时处理事件但不退出的机制**
   **线程和 RunLoop 之间是一一对应的**
   _ runloop作用
    1.使程序一直运行接受用户输入;
   2.决定程序在何时应该处理哪些Event;
   3.调用解耦;
   4.节省CPU时间。_
   >- 主线程的runloop默认是启动的。
  > - Cocoa中的NSRunLoop类并不是线程安全的,
  > - 获取对应的CFRunLoopRef类，来达到线程安全的目的。 
  `- (CFRunLoopRef)getCFRunLoop;`
  
   5.1 系统默认注册的5个Mode

   5.2 轮播图中的NSTimer问题

   5.3 main函数的运行  **Runloop**
   1. 事件响应链
   2. 引用计数器（ARC 和 MRC）
   3. 深浅复制和属性为copy，strong时值的变化
   4. 生命周期
   5. 与其他动态语言比较

## [第二章 细节还是细节](http://www.jianshu.com/p/0396633936ef)

1. Block和Delegate的使用

   1.1 Delegate

   1.2 Block
   > 
   循环引用的问题： __weak typeof(self) weakSelf = self;

   1.3 Block和Delegate的区别
   > 
   - 公共接口和方法较多用delegate进行解耦:tableViewDelegate，textViewDelegate等
   - 异步和简单的回调用block更好，如常用的网络库AFNetwork等。
2. OC中的Class

   2.1 类对象（class object）

   2.2 元类对象\(metaclass object\)

   2.3 实例对象和类的分析

3. Category

   3.1 runtime对category的加载过程

   3.2 Extension

4. iOS视图生命周期
5. NSNotification效率问题
> 
**重定向的实现思路**

6. KVO，NSNotification，delegate及block区别
> 
**NSNotification是通知，也是一对多的使用场景。**
**block是delegate的另一种形式，是函数式编程的一种形式。**
**delegate是一对一关系。**
**KVO可以监测一个值的变化，比如View的高,
   KVO是一对多的关系，一个值的变化会通知所有的观察者。**
7. \_\_weak
8. nil、Nil、NULL、NSNull
> 
1.NULL就知道这是个C指针，
2.nil就知道这是个Objective-C对象，
3.Nil就知道这是个Class类型的数据。
4.NSNull是一个Objective-C类,它表示的是空值，即什么都不存。
另外，NULL是C指针指向的值为空；nil是OC对象指针自己本身为空，不是值为空。
>
> > 空字符串或数组中一个为空，会打印:<null> ，代表着这是一个空字符串，赋值为空，指针是存在的，只是内容为空。在iOS上，字典/数组 内容为空不能简单的判断str==null（null 在ios上得用[NSNull null]）。
> ``` objectivec
if(![location isEqual:[NSNull null]]){
 NSLog(@"YES");
}
```

9. 图像处理中的UI、CG和CI

   9.1 UIImage、CGImage和CGImageRef

   9.2 UIColor、CGColor和CIColor区别和联系

   9.3 创建一个CGColor

   9.4 判断两个颜色是否相等

10. 时间复杂度和空间复杂度

    10.1 **求时间复杂度**

    10.2** 空间复杂度**

第三章 iOS视图成像理论及优化

1. CRT屏幕成像
2. 液晶显示器工作原理
3. 计算机处理成像
4. 屏幕成像问题
5. 离屏渲染

   5.1 离屏渲染的触发

   5.2 特殊的“离屏渲染”方式：CPU渲染

   5.3 当前屏幕渲染、离屏渲染、CPU渲染的选择

6. 补充：图层与UIView

   6.1 CALayer的基本属性

   6.2 CALayer and Mask

   6.3 绘制图形

7. CPU处理优化

8. GPU处理优化
9. GPU 编程的高度优化框架 Metal
10. 总结，优化显示的多种手段

第四章 iOS内存、缓存及存储优化

1. iOS内存优化

   1.1 懒加载

   1.2 复用

   1.3 XIB和Storyboards

   1.4 选择正确的数据结构

   1.5 后台处理

   1.6 处理内存警告

2. iOS缓存优化

   2.1 NSURLConnection

   2.2 NSURLCache

   2.3 NSCache

   2.4 两种图片加载方式

   2.5 补充：CPU缓存简析

3. iOS存储优化

   3.1 Core Data

   3.1.1 CoreData优劣分析

   3.1.2 CoreData多线程安全

   3.2 FMDB

   3.2.1 示例

   3.2.2 多线程操作

   3.3 Yapdatabase

4. 网络请求优化

第五章 iOS项目分析及优化

1. 从代码看一个程序员的笔力
2. 着手一个新项目条理
3. iOS开发的细节及全局观
4. 敏捷开发

   4.1 敏捷开发的起源

   4.2 敏捷开发的方式

   4.2.1 Scrum方式

   4.2.1.1 Scrum开发流程中的三大角色

   4.2.1.2 进行Scrum开发的流程

   4.2.2 XP方式

   4.2.3优秀团队的选择

5. iOS项目分析及重构

第六章 Hybrid App 从细节到源码分析

第七章 从OC到React Native

第八章 您好，Swift

第九章 开发中所应关注的其它方面

第十章 设计模式及算法

后记：程序中的24个比利

附录：iOS自学网站

附录：iOS优秀的第三方库

