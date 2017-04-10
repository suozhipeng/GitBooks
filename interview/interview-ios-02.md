# iOS中级面试题
[原文链接：来自MrPeak](https://www.zhihu.com/question/19604641)

---
2016-01-07 中级面试题
---
1. 什么是arc？（arc是为了解决什么问题诞生的？）
- 请解释以下keywords的区别：`assign` vs `weak`,`__block`vs`__weak`。
- `__block`在 arc和非arc下含义一样吗？
- 使用 atomic 一定是线程安全的吗？
- 描述一个你遇到过的 retain cycle 例子。（别撒谎，你肯定遇到过）
- `+(void)load;` `+(void)initialize;`有什么用处？
- 为什么其他于语言里叫_函数调用_，Objective-C 里则是给对象发消息(或者谈下对 runtime 的理解)
- 什么是 method swizzling？
- UIView 和 CALayer 是啥关系？
- 如何高性能的给 UIImageView加个圆角？（不准说layer.cornerRadius!）
- 使用 drawRect 有什么影响？（这个可深可浅，你至少得用过...）
- ASIHttpRequest 或者 SDWebImage 里面给 UIImageView 加载图片的逻辑是什么样的？（把UIImageView放到UITableViewCell 里面问更赞）
- 麻烦你设计一个简单的图片内存缓存器(移除策略是一定要说的)
- 讲讲你用 Instrument 优化动画性能的经历吧（别问我什么是 Instrument）
- loadView 是干嘛用的？
- `viewWillLayoutSubView`你总是知道的...
- CGD 里面有哪几种`Queue`?你自己建立过穿行queue吗？背后的线程模型是什么样的？
- 用过coredata或者sqlite吗？读写是分线程的吗？遇到过死锁没，咋解决的？
- http 的 post 和 get有啥区别（区别挺多的，麻烦多说点）
- 我知道你大学毕业后就没有接触过算法数据结构了，但是请你一定告诉我什么是Binary search tree? search 的时间复杂度是多少？我很想知道！


---




