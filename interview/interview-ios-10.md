
【2017-04】
原文链接：http://www.cocoachina.com/bbs/read.php?tid-1718238-page-1.html

---
1，下面代码在按钮点击后，在ARC下会发生什么，MRC下呢？为什么？

```objectivec

@property(nonatomic, assign) void(^block)();

- (void)viewDidLoad {
    [superviewDidLoad];
    int value = 10;
    void(^blockC)() = ^{
        NSLog(@"just a block === %d", value);
    };

    NSLog(@"%@", blockC);
    _block = blockC;

}

- (IBAction)action:(id)sender {
    NSLog(@"%@", _block);
}
```


2，在ARC环境下这段代码为什么不会崩溃？



```objectivec
@property(nonatomic, weak) void(^block)();

- (void)viewDidLoad {
    [super viewDidLoad];

    void(^ __weak blockA)() = ^{
        NSLog(@"just a block");
    };

    _block = blockA;

}

- (IBAction)action:(id)sender {
    _block();
}


```



3，下面是一个员工表，manager_id表示对应的boss的ID。通过一个SQL找出下表中比boss工资还高的人。。。。
> 
id    name    salary    manager_id
1    Noah    70000    NULL
2    西兰花    80000    1
3    椰菜花    80000    NULL
4    没钱花    80000    3

输出格式为：

name
西兰花

4，写一个函数，输入一个数如38，拆分 3 + 8 = 11，1 + 1 = 2，最后2无法拆分就返回（伪代码也行）

5，通过runtime添加的“关联对象”和类的实例变量有什么区别？使用时要注意什么？

6，用一个生活中的例子来说说同步和异步。

7，线程间通信在OC中有几种方式？分别是？常用那种？

8，使用快速枚举迭代一个可变数组时需要注意什么问题？怎么避免？

9，什么是面向对象的多态性？

10，UIViewController的presentViewController和UINavigationController的pushViewController方法分别多用于什么交互场景？

11，NSOperation和GCD的区别是什么？前者多用于什么场景？

12，面向接口编程指的是什么？为什么说面向实现编程是一种错误的编程方式？

13，在iOS开发中遇到那些类族(Class Cluster) ？如NSNumber这种。为什么需要这种设计方式？

14，javascript的原型链和OC的继承有什么区别？

15，Hybrid开发的优势在哪里？目前有那些框架可以实现Hybrid开发？

16，使用了ARC是不是就等于没有内存泄漏了？如果不是的话请举例。

17，下面代码中为什么可以直接用self？
```objectivec
- [UIView animateWithDuration:1 animations:^{
    self.view.backgroundColor = [UIColor yellowColor];
}];
```
下面这段代码可以用self吗？为什么？
```objectivec
- (void)doSomething {
    [BlockClass doSomethingUseBlock:^{
        NSLog(@"%@", self);
    }];
}
```
18，进程的内存布局是怎样的？

19，在GCD中，那几种场景会出现死锁的现象？怎么避免？

20，怎么用NSOperation封装一个异步请求？这个Operation需要放到NSOperationQueue里调度的。

21，CoreFoundation和Foundation有什么区别？

22，怎么判断两个链表是双交的？

23，怎么判断一个链表存在环?

24，当一个View的bounds原点不为0的时候会出现什么情况？

25，OC的数组是怎么实现的？和C的数组区别在？简单说一下即可。

26，weak和assign有什么区别？

27，setNeedLayout的作用是什么？

28，什么时候用NS_OPTIONS，NS_ENUM?



