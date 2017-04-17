# runtime 有哪些应用，感觉实际项目几乎用不上～？
---
[原文链接](https://www.zhihu.com/question/30721573/answer/139448488)
_书籍推荐📚：_[Effective Objective-C 2.0](https://book.douban.com/subject/25829244/)
## 什么是rumtime
> 
Objective-C 语言是一门动态语言，编译器不需要关心接受消息的对象是何种类型，接收消息的对象问题也要在运行时处理。

pragramming 层面的 runtime 主要体现在以下几个方面：
> 
- 关联对象 [Associated Objects](http://nshipster.cn/associated-objects/)
- 消息发送 [Messaging](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Articles/ocrtHowMessagingWorks.html#//apple_ref/doc/uid/TP40008048-CH104-SW1)
- 消息转发 [Message Forwarding](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Articles/ocrtForwarding.html#//apple_ref/doc/uid/TP40008048-CH105-SW1)
- 方法调配 [Method Swizzling](http://nshipster.com/method-swizzling/)
- “类对象” [NSProxy Foundation | Apple Developer Documentation](https://developer.apple.com/reference/foundation/nsproxy)
- KVC、KVO  [About Key-Value Coding](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/KeyValueCoding/)

总是写业务当然用到的比较少，如果要封装一些组件可能就会碰到了，举几个简单的栗子：
> 
1. 方法交换，可以用来捕获系统方法并进行修改，常用来做兼容iOS版本；
2. 拦截系统自带的方法调用（Swizzle 黑魔法），比如拦imageNamed:、viewDidLoad、alloc；
3. 动态添加属性，尤其是在分类中；实现NSCoding协议的自动归档和解档；
4. 实现json到model的转化；


**动态获取 class 和 slector**


```objectivec
NSClassFromString(@"MyClass");
NSSelectorFromString(@"showShareActionSheet");
```


除了这个还有就是，**给分类添加属性**和 **KVC/KVO**了。
大多数情况下，我们是不会直接用 runtime 写业务代码的（至于为什么，可以看看@MrPeak怎么说的），所以，大部分时候，我们只会在一些平时用起来很方便的框架里面，看到有用到 runtime 的黑魔法（当然你也可以自己造轮子）。runtime 用起来的最大感受就是，底层写一堆 runtime，外面用起来超清爽！对于那些“代码艺术家”来说，简直是爽到爆。

大概说说一下自己在开发中用到的一些基于 runtime 的开源框架吧，具体应用自己可以去看看源码：
> 
- Aspects（AOP必备，“取缔” baseVC，无侵入埋点）
- MJExtension（JSON 转 model，一行代码实现 NSCoding 协议的自动归档和解档）
- JSPatch（动态下发 JS 进行热修复）
- NullSafe（防止因发 unrecognised messages 给 NSNull 导致的崩溃）
- UITableView-FDTemplateLayoutCell（自动计算并缓存 table view 的 cell 高度）
- UINavigationController+FDFullscreenPopGesture（全屏滑动返回）

## RunTime学习的 意义
> 
1. 直接用 runtime 写业务的场景比较少，原因在于 runtime 所涉及的逻辑都比较隐蔽。
2. runtime 的学习个人觉得阅读 Aspect 源码就差不多了， AOP 也应该是runtime 的主要用途。
3. 学习 runtime 的最大意义，个人觉得在于了解编程语言的可能性，对于语言特性掌握的越多，**语感** 越好，技术视野的拓展和抽象能力也就越强。



---
