## KVC/KVO的底层实现机制

原文链接：[http://www.jianshu.com/p/8ce4821ae97b](http://www.jianshu.com/p/8ce4821ae97b)

---
简述：
> 
KVO 内部实现原理
    1. KVO 是基于runtime机制实现的.
    2. 当某个类的对象第一次被观察时,系统就会在运行期动态的创建该类的一个派生类,在这个派生类中重写基类中任何被观察属性的setter方法; 
　　    派生类在被重写的setter方法中实现真正的通知机制 。
KVC：不通过点语法访问对象属性。

---

KVO是基于观察者设计模式来实现的。  
**观察者模式：**一个目标对象管理所有依赖于它的观察者对象，并在它自身的状态改变时主动通知观察者对象。这个主动通知通常是通过调用各观察者对象所提供的接口方法来实现的。观察者模式较完美地将目标对象与观察者对象解耦。

###### 实现原理

KVO的实现是基于runtime运行时的，下面就来详细介绍一下原理：还是这张图：  

![](/assets/ios-KVO原理.png)

* 当某个类的对象第一次被观察时，系统就会在运行期动态地创建该类的一个派生类，在这个派生类中重写基类中任何被观察属性的 setter 方法。
* 派生类在被重写的 setter 方法中实现真正的通知机制，就如前面手动实现键值观察那样。这么做是基于设置属性会调用 setter 方法，而通过重写就获得了 KVO 需要的通知机制。当然前提是要通过遵循 KVO 的属性设置方式来变更属性值，如果仅是直接修改属性对应的成员变量，是无法实现 KVO 的。
* 同时派生类还重写了 class 方法以“欺骗”外部调用者它就是起初的那个类。然后系统将这个对象的 isa 指针指向这个新诞生的派生类，因此这个对象就成为该派生类的对象了，因而在该对象上对 setter 的调用就会调用重写的 setter，从而激活键值通知机制。此外，派生类还重写了 dealloc 方法来释放资源。





###### 手动实现键值观察\(代码示例\)

被观察的对象Target（重写setter/getter方法）  
Target.h

```objectivec 

@interface Target : NSObject
{
   int age;
}
// for manual KVO 
- age- (int) age;
- (void) setAge:(int)theAge;
@end

```

Target.m

```objectivec
@implementation Target
- (id) init{ 
    self = [super init]; 
    if (nil != self) { 
          age = 10; 
     } 
    return self;
}
// for manual KVO - age
- (int) age{
    return age;
}
- (void) setAge:(int)theAge{ 
    [self willChangeValueForKey:@"age"];
    age = theAge; 
    [self didChangeValueForKey:@"age"];
}
+ (BOOL) automaticallyNotifiesObserversForKey:(NSString *)key { 
    if ([key isEqualToString:@"age"]) {
     return NO;
 } 
return [super automaticallyNotifiesObserversForKey:key]**;
}
@end

```

首先，需要手动实现属性的 setter 方法，并在设置操作的前后分别调用**willChangeValueForKey:**和**didChangeValueForKey**方法，这两个方法用于通知系统该 key 的属性值即将和已经变更了；  
其次，要实现类方法**automaticallyNotifiesObserversForKey**，并在其中设置对该 key 不自动发送通知（返回 NO 即可）。这里要注意，对其它非手动实现的 key，要转交给 super 来处理。




