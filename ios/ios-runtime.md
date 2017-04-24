_书籍推荐📚：_[Effective Objective-C 2.0](https://book.douban.com/subject/25829244/)

## Objective-C语言的动态性总结\(编译时与运行时\)

[http://blog.csdn.net/cordova/article/details/53876682](http://blog.csdn.net/cordova/article/details/53876682)

---

> OC语言的动态性主要体现在三个方面：
>
> * 动态类型\(Dynamic typing\): 
>   id类型
> * 动态绑定\(Dynamic binding\)
> * 动态加载\(Dynamic loading\)

* 动态类型识别方法\(面向对象语言的内省Introspection特性\)

1.首先是Class类型：

> * **Class class = \[NSObject class\];**
>   // 通过类名得到对应的Class动态类型
> * **Class class = \[obj class\];**
>   // 通过实例对象得到对应的Class动态类型
> * **if\(\[obj1 class\] == \[obj2 class\]\)**
>   // 判断是不是相同类型的实例

2.Class动态类型和类名字符串的相互转换：

> * **NSClassFromString\(@”NSObject”\);**
>   // 由类名字符串得到Class动态类型
> * **NSStringFromClass\(\[NSObject class\]\);**
>   // 由类名的动态类型得到类名字符串
> * **NSStringFromClass\(\[obj class\]\);**
>   // 由对象的动态类型得到类名字符串

3.判断对象是否属于某种动态类型：

> * **-\(BOOL\)isKindOfClass:class**
>   // 判断某个对象是否是动态类型class的实例或其子类的实例
> * **-\(BOOL\)isMemberOfClass:class**
>   // 与isKindOfClass不同的是，这里只判断某个对象是否是class类型的实例，不放宽到其子类

4.判断类中是否有对应的方法：

> * **-\(BOOL\)respondsTosSelector:\(SEL\)selector**
>   // 类中是否有这个类方法
> * **-\(BOOL\)instancesRespondToSelector:\(SEL\)selector**
>   // 类中是否有这个实例方法
>
> _**区别：**_  
> 上面两个方法都可以通过类名调用，前者判断类中是否有对应的类方法\(通过‘+’修饰定义的方法\)，后者判断类中是否有对应的实例方法\(通过‘-’修饰定义的方法\)。此外，前者respondsTosSelector函数还可以被类的实例对象调用，效果等同于直接用类名调用后者instancesRespondToSelector函数。  
> 举个例子：假设有一个类**Test**，有它的一个实例对象**test**，Test类中定义了一个类函数：**+ \(void\)classFun;**和一个实例函数：**- \(void\)objFunc;**，那么各种调用情况的结果如下：

```objectivec
    [1][Test instancesRespondToSelector:@selector(objFunc)];//YES
    [2][Test instancesRespondToSelector:@selector(classFunc)];//NO

    [3][Test respondsToSelector:@selector(objFunc)];//NO
    [4][Test respondsToSelector:@selector(classFunc)];//YES

    [5][test respondsToSelector:@selector(objFunc)];//YES
    [6][test respondsToSelector:@selector(classFunc)];//NO
```

> **结论：**如果想判断一个类中是否有某个类方法，应该使用\[4\]; 如果想判断一个类中是否有某个实例方法，可以使用\[1\]或者\[5\]。

5.方法名字符串和SEL类型的转换

> 在编译器,编译器会根据方法的名字和参数序列生成唯一标识改方法的ID,这个ID为SEL类型。到了运行时编译器通过SEL类型的ID来查找对应的方法，方法的名字和参数序列相同,那么它们的ID就都是相同的。另外，可以通过@select\(\)指示符获得方法的ID。常用的方法如下：

```objectivec
SEL funcID = @select(func)；// 这个注册事件回调时常用，将方法转成SEL类型
SEL funcID = NSSelectorFromString(@"func"); // 根据方法名得到方法标识
NSString *funcName = NSStringFromSelector(funcID); // 根据SEL类型得到方法名字符串
```

** 动态绑定**

> 动态绑定指的是**方法确定的动态性**，具体指的是利用OC的消息传递机制将要执行的方法的确定推迟到运行时，可以动态添加方法。
>
> 动态绑定是基于动态类型的，在运行时对象的类型确定后，那么对象的属性和方法也就确定了\(包括类中原来的属性和方法以及运行时动态新加入的属性和方法\)，这也就是所谓的动态绑定了。动态绑定的核心就该是在运行时动态的为类添加属性和方法，以及方法的最后处理或转发，主要用到C语言语法，因为涉及到运行时，因此要引入运行时头文件：`#include <objc/runtime.h>`。

**消息传递机制**  
**消息转发机制**

动态加载

> 动态加载主要包括两个方面，一个是**动态资源加载**，一个是一**些可执行代码模块的加载**，这些资源在运行时根据需要动态的选择性的加入到程序中，是一种**代码和资源的‘懒加载’模式**，可以降低内存需求，提高整个程序的性能，另外也大大提高了可扩展性。

**官方运行时源码：**[**https://opensource.apple.com/source/objc4/objc4-532/runtime/**](https://opensource.apple.com/source/objc4/objc4-532/runtime/)

**OC运行时编程指南：**[**Objective-C Runtime Programming Guide**](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008048)

[**Cocoa消息**](http://blog.csdn.net/kesalin/article/details/6689226)[**Cocoa类与对象**](http://blog.csdn.net/kesalin/article/details/7211228)

**问题： 我们所说的Objective-C是动态运行时语言是什么意思？**

> 主要指的是OC语言的动态性，包括动态性和多态性两个方面。
>
> 动态性：即OC的动态类型、动态绑定和动态加载特性，将对象类型的确定、方法调用的确定、代码和资源的装载等推迟到运行时进行，更加灵活；  
> 多态：多态是面向对象变成语言的特性，OC作为一门面向对象的语言，自然具备这种多态性，多态性指的是来自不同类的对象可以接受同一消息的能力，或者说不同对象以自己的方式响应相同的消息的能力。

**问题： 动态绑定是在运行时确定要调用的方法？**

> 动态绑定将调用方法的确定推迟到运行时。在编译时，方法的调用并不和代码绑定在一起，只有在消实发送出来之后，才确定被调用的代码。通过动态类型和动态绑定技术，代码每次执行都可以得到不同的结果。运行时负责确定消息的接收者和被调用的方法。运行时的消息分发机制为动态绑定提供支持。当向一个动态类型确定了的对象发送消息时，运行环境会通过接收者的isa指针定位对象的类，并以此确定被调用的方法，方法是动态绑定的。

**问题： 解释OC中的id类型？id、nil代表什么?**

> id表示变量或对象的类型在编写代码时\(编译期\)不确定，视为任意类型，直到程序跑起来推迟到运行时才最终确定其类型。id类似于C/C++中的void _,但id和void_并非完全一样。id是一个指向继承了NSObject的OC对象的指针，注意id是一个指针，虽然省略了_号。id和C语言的void_之间需要通过bridge关键字来显式的桥接转换。具体转换方式示例如下：

```objectivec
id nsobj = [[NSObject alloc] init];
void *p = (__bridge void *)nsobj;
id nsobj = (__bridge id)p;
```

OC中的nil定义在objc/objc.h中，表示的是一个指向空的Objctive-C对象的指针。例如weak修饰的弱引用对象在指向的对象释放时会自动将指针置为nil，即空对象指针，防止‘指针悬挂’。

**问题： instancetype和id的区别？**

> instancetype和id都可以用来代表任意类型，将对象的类型确定往后推迟，用于体现OC语言的动态性，使其声明的对象具有运行时的特性。
>
> 它们的区别是：instancetype只能作为返回值类型，但在编译期instancetype会进行类型检测，因此对于所有返回类的实例的类方法或实例方法，建议返回值类型全部使用instancetype而不是id，具体原因后面举例介绍；id类型既可以作为返回值类型,也可以作为参数类型,也可以作为变量的类型，但id类型在编译期不会进行类型检测。

**问题： 一般的方法method和OC中的选择器selector有何不同？**

> selector是一个方法的名字，基于动态绑定环境下，method是一个组合体，包含了名字和实现。
>
> 可以理解@selector\(\)就是取类方法的编号,他的行为基本可以等同C语言的中函数指针,只不过C语言中，可以把函数名直接赋给一个函数指针，而Objective-C的类不能直接应用函数指针，这样只能做一个@selector语法来取. 它的结果是一个SEL类型。这个类型本质是类方法的编号\(函数地址\)。

**问题：什么是目标-动作\(target-action\)机制?**

> 目标是动作消息的接收者。例如一个控件，或者更为常见的是它的单元，  
> 以插座变量的形式保有其动作消息的目标。 动作是控件发送给目标的消息，或者从目标的角度看，它是目标为了响应动作而实现的方法。程序需要某些机制来进行事件和指令的翻译。这个机制就是目标-动作机制。

**问题：下列代码取决于Objective-C的哪样特性？**

```objectivec
id myobj;
... ...
[myobj draw];
```

> 预处理机制  
> 枚举数据类型  
> 静态类型  
> 动态类型\(right\)  
> 问题： Object-C有私有方法吗? 私有变量呢?

首先要看私有的含义。私有主要指的是通过类的封装性，将不希望让外界看到的方法或属性隐藏在类内部，只有该类可以在内部访问，外部不可见不可访问。

表面上OC中是可以实现私有的变量和方法的，即将它们隐藏不暴露在头文件，不可以显式地直接访问，但是OC中这种私有并不是绝对的私有，例如即使将变量和方法隐藏在.m实现文件中，开发者仍然可以利用runtime运行时机制强行访问没有暴露在头文件的变量和方法。

OC中实现变量和方法‘私有‘的方式：  
一种是在类的头文件中生命私有变量：

```objectivec
#import <Foundation/Foundation.h>

@interface Test : NSObject {
    /* 头文件中定义私有变量，默认为@protected */
    @private
    NSString *major;
}

@end
```

另外一种是在.m实现文件头部的类扩展区域定义私有属性或方法，其中方法可不用声明，直接在实现文件中实现即可，只要不在头文件生命的方法都对外不可见：

```objectivec
#import "Test.h"
@interface Test() {
/* 类扩展区域定义私有变量，默认就是@private */
int age;
}

/* 类扩展区域定义私有属性 */
@property (nonatomic, copy) NSString *name;

/* 类扩展区域定义私有实例方法(可省略声明，类方法的作用主要就是提供对外接口的，所以一般不会定义为私有) */
- (void)test;

@end

@implementation Test

/**
* 私有实例方法
*/
- (void)test {
NSLog(@"这是个私有实例方法！");
}
@end
```

---

## Objective-C语言消息传递机制三道防线：消息转发机制详解

原文链接：[http://blog.csdn.net/cordova/article/details/70181837](http://blog.csdn.net/cordova/article/details/70181837)

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

原文链接:[https://www.zhihu.com/question/30721573/answer/139448488](https://www.zhihu.com/question/30721573/answer/139448488)

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



