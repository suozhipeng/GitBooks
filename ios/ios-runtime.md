_书籍推荐📚：_[Effective Objective-C 2.0](https://book.douban.com/subject/25829244/)

## Objective-C语言消息传递机制三道防线：消息转发机制详解
原文链接：http://blog.csdn.net/cordova/article/details/70181837

---

消息传递机制：

> 在OC中,方法的调用不再理解为对象调用其方法，而是要理解成对象接收消息，消息的发送采用‘动态绑定’机制，具体会调用哪个方法直到运行时才能确定，确定后才会去执行绑定的代码。方法的调用实际就是告诉对象要干什么，给对象\(的指针\)传送一个消息，对象为接收者（receiver），调用的方法及其参数即消息（message），给一个对象传消息表达为：`[receiver message]`; 接受者的类型可以通过动态类型识别于运行时确定。
>
> 在消息传递机制中，当开发者编写`[receiver message]`;语句发送消息后，编译器都会将其转换成对应的一条**objc\_msgSend** C语言消息发送原语，具体格式为：
>
> ```objectivec
> void objc_msgSend (id self, SEL cmd, ...)
> ```
>
> 这个原语函数参数可变，第一个参数填入**消息的接受者**，第二个参数是**消息‘选择子’**，后面跟着可选的消息的参数。有了这些参数，objc\_msgSend就可以通过**接受者的的isa指针**，到其类对象中的方法列表中以选择子的名称为‘键’寻找对应的方法，找到则转到其实现代码执行，找不到则继续根据继承关系从父类中寻找，如果到了根类还是无法找到对应的方法，说明该接受者对象无法响应该消息，则会触发‘消息转发机制’，给开发者最后一次挽救程序崩溃的机会。

**消息转发机制：**

> 如果消息传递过程中，接受者无法响应收到的消息，则会触发进入‘消息转发’机制。

消息转发依次提供了三道防线，任何一个起作用都可以挽救此次消息转发。按照先后顺序三道防线依次为：

* **动态补加方法的实现**

```objectivec

+ (BOOL)resolveInstanceMethod:(SEL)sel
+ (BOOL)resolveClassMethod:(SEL)sel
```

* **直接返回消息转发到的对象（将消息发送给另一个对象去处理）**

```objectivec

- (id)forwardingTargetForSelector:(SEL)aSelector
```

* **手动生成方法签名并转发给另一个对象**

```objectivec

- (NSMethodSignature *)methodSignatureForSelector:(SEL)aSelector;
- (void)forwardInvocation:(NSInvocation *)anInvocation;
```
eg:
> main.m

```objectivec
#import <Foundation/Foundation.h>
#import "Test.h"

int main(int argc, const char * argv[]) {
    Test *test = [[Test alloc] init];
    [test instanceMethod];
    return 0;
}

```
> **Test**

```objectivec
#import <Foundation/Foundation.h>

@interface Test : NSObject

- (void)instanceMethod;

@end


#import "Test.h"
#import "Test2.h"
#import <objc/runtime.h>

@implementation Test
/*
 * 被动态添加的实例方法实现
 */
void instanceMethod(id self, SEL _cmd) {
    NSLog(@"收到消息会执行此处的函数实现...");
}

/*
 * 1.第一道防线：动态补加方法实现
 */
+ (BOOL)resolveInstanceMethod:(SEL)sel {
    // return NO;
    if (sel == @selector(instanceMethod)) {
        class_addMethod(self, sel, (IMP)instanceMethod, "v@:");
        return YES;
    }
    return [super resolveInstanceMethod:sel];
}

/*
 * 2.第二道防线
 */
- (id)forwardingTargetForSelector:(SEL)aSelector {
    // return nil;
    /* 返回转发的对象实例 */
    if (aSelector == @selector(instanceMethod)) {
        return [[Test2 alloc] init];
    }
    return nil;
}

/*
 * 3.第三道防线
 */
- (NSMethodSignature *)methodSignatureForSelector:(SEL)aSelector {
    /* 为指定的方法手动生成签名 */
    NSString *selName = NSStringFromSelector(aSelector);
    if ([selName isEqualToString:@"instanceMethod"]) {
        return [NSMethodSignature signatureWithObjCTypes:"v@:"];
    }
    return [super methodSignatureForSelector:aSelector];
}
- (void)forwardInvocation:(NSInvocation *)anInvocation {
    /* 如果另一个对象可以相应该消息，则将消息转发给他 */
    SEL sel = [anInvocation selector];
    Test2 *test2 = [[Test2 alloc] init];
    if ([test2 respondsToSelector:sel]) {
        [anInvocation invokeWithTarget:test2];
    }
}

@end

```
> **Test2**

```objectivec
#import <Foundation/Foundation.h>

@interface Test2 : NSObject

- (void)instanceMethod;

@end


#import "Test2.h"

@implementation Test2

- (void)instanceMethod {
    NSLog(@"消息转发到这...");
}

@end

```


---

## runtime 有哪些应用，感觉实际项目几乎用不上～？

---

原文链接:https://www.zhihu.com/question/30721573/answer/139448488

## 什么是rumtime

> Objective-C 语言是一门动态语言，编译器不需要关心接受消息的对象是何种类型，接收消息的对象问题也要在运行时处理。

pragramming 层面的 runtime 主要体现在以下几个方面：

> * 关联对象 [Associated Objects](http://nshipster.cn/associated-objects/)
> * 消息发送 [Messaging](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Articles/ocrtHowMessagingWorks.html#//apple_ref/doc/uid/TP40008048-CH104-SW1)
> * 消息转发 [Message Forwarding](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Articles/ocrtForwarding.html#//apple_ref/doc/uid/TP40008048-CH105-SW1)
> * 方法调配 [Method Swizzling](http://nshipster.com/method-swizzling/)
> * “类对象” [NSProxy Foundation \| Apple Developer Documentation](https://developer.apple.com/reference/foundation/nsproxy)
> * KVC、KVO  [About Key-Value Coding](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/KeyValueCoding/)

总是写业务当然用到的比较少，如果要封装一些组件可能就会碰到了，举几个简单的栗子：

> 1. 方法交换，可以用来捕获系统方法并进行修改，常用来做兼容iOS版本；
> 2. 拦截系统自带的方法调用（Swizzle 黑魔法），比如拦imageNamed:、viewDidLoad、alloc；
> 3. 动态添加属性，尤其是在分类中；实现NSCoding协议的自动归档和解档；
> 4. 实现json到model的转化；

**动态获取 class 和 slector**

```objectivec
NSClassFromString(@"MyClass");
NSSelectorFromString(@"showShareActionSheet");
```

除了这个还有就是，**给分类添加属性**和 **KVC/KVO**了。  
大多数情况下，我们是不会直接用 runtime 写业务代码的（至于为什么，可以看看@MrPeak怎么说的），所以，大部分时候，我们只会在一些平时用起来很方便的框架里面，看到有用到 runtime 的黑魔法（当然你也可以自己造轮子）。runtime 用起来的最大感受就是，底层写一堆 runtime，外面用起来超清爽！对于那些“代码艺术家”来说，简直是爽到爆。

大概说说一下自己在开发中用到的一些基于 runtime 的开源框架吧，具体应用自己可以去看看源码：

> * Aspects（AOP必备，“取缔” baseVC，无侵入埋点）
> * MJExtension（JSON 转 model，一行代码实现 NSCoding 协议的自动归档和解档）
> * JSPatch（动态下发 JS 进行热修复）
> * NullSafe（防止因发 unrecognised messages 给 NSNull 导致的崩溃）
> * UITableView-FDTemplateLayoutCell（自动计算并缓存 table view 的 cell 高度）
> * UINavigationController+FDFullscreenPopGesture（全屏滑动返回）

## RunTime学习的 意义

> 1. 直接用 runtime 写业务的场景比较少，原因在于 runtime 所涉及的逻辑都比较隐蔽。
> 2. runtime 的学习个人觉得阅读 Aspect 源码就差不多了， AOP 也应该是runtime 的主要用途。
> 3. 学习 runtime 的最大意义，个人觉得在于了解编程语言的可能性，对于语言特性掌握的越多，**语感** 越好，技术视野的拓展和抽象能力也就越强。

---



