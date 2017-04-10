# 完整的面试题(整理了02-03)

1. 在oc中如何实现深度拷贝
2. 请描述什么是delegate、block、NSNotification，他们有什么作用
3. 请写出一个线程安全的单例模式
4. 解释属性中strong、weak、assign、copy的区别
5. `#import`和`#include`的区别
6. 描述tableView的重用机制
7. Object-C有多继承吗？没有的话用什么代替？
8. category与继承之间的区别
9. `#define`和`const`定义的变量，有什么区别10. TCP和UDP的区别是什么？ 
11. MD5和Base64的区别是什么，各自场景是什么？
12. 二叉搜索树的概念，时间复杂度多少？
13. 如何添加一个自定义字体到工程中
14. 如何制作一个静态库/动态库，他们的区别是什么？
15. Configuration中，debug和release的区别是什么？
16. push view controller 和 present view controller的区别
17. 描述下tableview cell的重用机制
18. UIView的frame和bounds的区别是什么
19. new与alloc init的区别
20. NSArray实例化时，array与init的区别
---
**中级题目**

1. 什么是arc？（arc是为了解决什么问题诞生的？）
2. 请解释以下keywords的区别： assign vs weak, __block vs __weak
3. __block在arc和非arc下含义一样吗？
4. 使用atomic一定是线程安全的吗？
5. 描述一个你遇到过的retain cycle例子。(别撒谎，你肯定遇到过)
6. +(void)load; +(void)initialize；有什么用处？
7. 为什么其他语言里叫函数调用， objective c里则是给对象发消息（或者谈下对runtime的理解）
8. 什么是method swizzling?
9. UIView和CALayer是啥关系？
10. 如何高性能的给UIImageView加个圆角？（不准说layer.cornerRadius!）
11. 使用drawRect有什么影响？（这个可深可浅，你至少得用过。。）
12. ASIHttpRequest或者SDWebImage里面给UIImageView加载图片的逻辑是什么样的？（把UIImageView放到UITableViewCell里面问更赞）
13. 麻烦你设计个简单的图片内存缓存器（移除策略是一定要说的）
14. 讲讲你用Instrument优化动画性能的经历吧（别问我什么是Instrument）
15. loadView是干嘛用的？
16. viewWillLayoutSubView你总是知道的。。
17. GCD里面有哪几种Queue？你自己建立过串行queue吗？背后的线程模型是什么样的？
18. 用过coredata或者sqlite吗？读写是分线程的吗？遇到过死锁没？咋解决的？
19. http的post和get啥区别？（区别挺多的，麻烦多说点）
20. 我知道你大学毕业过后就没接触过算法数据结构了，但是请你一定告诉我什么是Binary search tree? search的时间复杂度是多少？我很想知道！
21. 哪些类不适合使用单例模式？即使他们在周期中只会出现一次。
22. Notification的使用场景是什么？同步还是异步？
23. 简单介绍一下KVC和KVO，他们都可以应用在哪些场景？
24. UIButton的父类是什么？UILabel呢？
25. 发送10个网络请求，然后再接收到所有回应之后执行后续操作，如何实现？
26. 实现一个第三方控件，可以在任何时候出现在APP界面最上层
27. 不同版本的APP，数据库结构变化了，如何处理?
28. 内存中的栈和堆的区别是什么？那些数据在栈上，哪些在堆上？
29. block中的weak self，是任何时候都需要加的么？
30. GCD的queue，main queue中执行的代码，一定是在main thread么？
31. NSOperationQueue有哪些使用方式
32. NSThread中的Runloop的作用，如何使用？
33. .h文件中的变量，外部可以直接访问么？（注意是变量，不是property）
34. 讲述一下runtime的概念，message send如果寻找不到相应的对象，会如何进行后续处理 ？
35. 利用runtime实现一个对象的拷贝

---
作者：丁洋洋
链接：https://www.zhihu.com/question/19604641/answer/59324405
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

