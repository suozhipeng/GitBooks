# 吴白的简书
简书链接：http://www.jianshu.com/u/211925b3ca7c
目录链接：[http://www.jianshu.com/p/437428330df3](http://www.jianshu.com/p/437428330df3)

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

   1. OC的动态性 isa指针
   > **Runtime：运行时，重要的消息机制、发送消息**

   4.1 动态类型、动态绑定和动态加载
   > 必须到运行时(runtime)才会做一些事情。
   **动态类型，就是id类型。 编译时、运行时、`objc_msgSend`** 
   **动态绑定(dynamic binding)需要用到@selector/SEL。**
      >  > 动态加载就是根据需求动态地加载资源，在运行时加载新类。在运行时创建一个新类,只需要3步:
1、为 class pair分配存储空间 ,使用 objc_allocateClassPair 函数
2、增加需要的方法使用 class_addMethod 函数,增加实例变量用class_addIvar
3、用objc_registerClassPair函数注册这个类,以便它能被别人使用。
其实就是这么简单。

   >   **动态加载就是根据需求动态地加载资源，在运行时加载新类。**
   > > 在运行时偷换selector对应的方法实现，达到给方法挂钩的目的。每个类都有一个方法列表，存放着selector的名字和方法实现的映射关系。IMP类似函数指针，指向具体的Method实现。
   * 用 method_exchangeImplementations 来交换2个方法中的IMP，
   * 用 class_replaceMethod 来修改类，
   * 用 method_setImplementation 来直接设置某个方法的IMP，归根结底，都是偷换了selector的IMP。

   4.2 Method Swizzling

   1. RunLoop
   > **让线程能随时处理事件但不退出的机制**
   **线程和 RunLoop 之间是一一对应的**
    runloop作用
    `[NSRunLoop currentRunLoop]`
    1.使程序一直运行接受用户输入;
   2.决定程序在何时应该处理哪些Event;
   3.调用解耦;
   4.节省CPU时间。
      5. Runloop同时也负责autorelease pool的创建和释放
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
   > 程序里的所有实例对象(instace object)都是在运行时由Objective-C的运行时库生成的，
   而这个类对象(class object)就是运行时库用来创建实例对象(instance object)的依据。
   实例对象(instance object)的isa指针指向的类对象(class object)里面还有一个isa，类对象(class objec)的isa指向的依然是一个objc-class，它就是元类对象(metaclass object)。

3. Category

   3.1 runtime对category的加载过程
   > 
   ```objectivec
   struct _category_t {
const char *name; // 类的名字
struct _class_t *cls; // 要扩展的类对象，编译期间这个值是不会有的，在app被runtime加载时才会根据name对应到类对象
const struct _method_list_t *instance_methods; // 实例方法
const struct _method_list_t *class_methods; // 类方法
const struct _protocol_list_t *protocols; // 这个category实现的protocol，比较不常用在category里面实现协议，但是确实支持的
const struct _prop_list_t *properties; // 这个category所有的property，这也是category里面可以定义属性的原因，不过这个property不会@synthesize实例变量，一般有需求添加实例变量属性时会采用objc_setAssociatedObject和objc_getAssociatedObject方法绑定方法绑定，不过这种方法生成的与一个普通的实例变量完全是两码事。
};
```

   3.2 Extension

4. iOS视图生命周期
5. NSNotification效率问题
> 
NSNotificationCenter在转发NSNotification消息的时候，在哪个线程中post，就在哪个线程中转发。换句话说，不管你的observer是在哪个线程，observer的回调方法执行线程都和post的线程保持一致，同时**NSNotification是线程阻塞的**，即走完通知后才继续往下执行。如果想让post的线程和转发的线程不同，可以通过NSNotification重定向技术实现
**重定向的实现思路**
> 自定义一个通知队列，让这个队列去维护那些我们需要重定向的Notification。当Notification来了时，根据需要将这个Notification存储到我们的队列中，并发送一个信号(signal)来告诉这个线程需要处理一个Notification。指定的线程在收到信号后，将Notification从队列中移除，并进行处理。
如此，在全局dispatch队列中抛出的Notification就在主线程中接收到了。

```objectivec
@interface ViewController ()
@property (nonatomic) NSMutableArray    * notifications;         // 通知队列

@property (nonatomic) NSThread          * notificationThread;    // 期望线程

@property (nonatomic) NSLock            * notificationLock;      // 用于对通知队列加锁的锁对象，避免线程冲突

@property (nonatomic) NSMachPort        * notificationPort;      // 用于向期望线程发送信号的通信端口
@end

@implementation ViewController
- (void)viewDidLoad {
[super viewDidLoad];

NSLog(@"current thread = %@", [NSThread currentThread]);

// 初始化
self.notifications = [[NSMutableArray alloc] init];
self.notificationLock = [[NSLock alloc] init];
self.notificationThread = [NSThread currentThread];
self.notificationPort = [[NSMachPort alloc] init];
self.notificationPort.delegate = self;
// 往当前线程的run loop添加端口源。当Mach消息到达而接收线程的run loop没有运行时，则内核会保存这条消息，直到下一次进入run loop
[[NSRunLoop currentRunLoop] addPort:self.notificationPort forMode:(__bridge NSString *)kCFRunLoopCommonModes];
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(processNotification:) name:@"TestNotification" object:nil];
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
[[NSNotificationCenter defaultCenter] postNotificationName:@"TestNotification" object:@"" userInfo:nil];
});
}
- (void)handleMachMessage:(void *)msg {
[self.notificationLock lock];
while ([self.notifications count]) {
    NSNotification *notification = [self.notifications objectAtIndex:0];
    [self.notifications removeObjectAtIndex:0];
    [self.notificationLock unlock];
    [self processNotification:notification];
    [self.notificationLock lock];
};
[self.notificationLock unlock];
}
- (void)processNotification:(NSNotification *)notification {
if ([NSThread currentThread] != _notificationThread) {
    // Forward the notification to the correct thread.
    [self.notificationLock lock];
    [self.notifications addObject:notification];
    [self.notificationLock unlock];
    [self.notificationPort sendBeforeDate:[NSDate date]
                               components:nil
                                     from:nil
                                 reserved:0];
}else {
    // Process the notification here;
    NSLog(@"current thread = %@", [NSThread currentThread]);
    NSLog(@"process notification");
}
}
``` 
6.KVO，NSNotification，delegate及block区别
> 
**NSNotification是通知，也是一对多的使用场景。**
**block是delegate的另一种形式，是函数式编程的一种形式。**
**delegate是一对一关系。**
**KVO可以监测一个值的变化，比如View的高,
   KVO是一对多的关系，一个值的变化会通知所有的观察者。**

7.\_\_weak
> 
当一个 `__weak` 类型的指针指向的对象被释放时，该指针会自动被置成nil，因此`__weak`关键字修饰的指针又被称为智能指针。
objc_storeWeak函数会把第二个参数的对象的地址作为key，并将第一个参数（`__weak`关键字修饰的指针的地址）作为值，注册到weak表中。如果第二个参数为0（说明对应的对象被释放了），则将weak表中将整个key-value键值对删除，这就是**`__weak`关键字的核心思想！**

weak表和引用计数表类似，都是通过hash表实现的。如果使用weak表，将被释放的对象地址作为key去检索，就能很高效的获取对应的指向该对象的类型为`__weak`的指针变量的地址。一个对象可能有多个`__weak`指针指向，因此一个对象地址key可能对应多个值。

在调用对象的release方法时，会在其中一步调用objc_clear_deallocating函数，该函数会执行以下操作：以当前对象的地址作为key，从weak表中获取对应的值，即指向该对象的`__weak`类型的指针变量；将取到的所有指针变量的值赋值为nil；从weak表中删除该key对应的整条记录。如果大量使用附有`__weak`修饰符的变量会消耗响应的CPU资源，因此应该尽量少使用`__weak`修饰符。

8.nil、Nil、NULL、NSNull
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

9.图像处理中的UI、CG和CI

   9.1 UIImage、CGImage和CGImageRef

   9.2 UIColor、CGColor和CIColor区别和联系

   9.3 创建一个CGColor

   9.4 判断两个颜色是否相等

10.时间复杂度和空间复杂度
> 
    10.1 **求时间复杂度**
    10.2** 空间复杂度**

## [第三章 iOS视图成像理论及优化](http://www.jianshu.com/p/d3685b4977aa)

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

## [第四章 iOS内存、缓存及存储优化](http://www.jianshu.com/p/a4684a5d2d7f)

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

## [第五章 iOS项目分析及优化](http://www.jianshu.com/p/834f5a824aee)

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

## [第六章 Hybrid App 从细节到源码分析](http://www.jianshu.com/p/e83aa2d1ade3)
>Hybrid App（混合模式移动应用), 跨平台，ReactNative 

## [第七章 从OC到React Native](http://www.jianshu.com/p/318342e139c7)

第八章 您好，Swift

## [第九章 开发中所应关注的其它方面](http://www.jianshu.com/p/7acba16fd929)
## [第十章 设计模式及算法](http://www.jianshu.com/p/4f8e4071f85b)

后记：程序中的24个比利

**[附录：iOS自学网站](http://www.jianshu.com/p/473206f54f9b)**

附录：iOS优秀的第三方库

