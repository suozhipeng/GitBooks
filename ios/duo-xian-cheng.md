# GCD 深入理解

1. ### GCD 深入理解：第一部分
https://github.com/nixzhu/dev-blog/blob/master/2014-04-19-grand-central-dispatch-in-depth-part-1.md
- ### GCD 深入理解：第二部分
https://github.com/nixzhu/dev-blog/blob/master/2014-05-14-grand-central-dispatch-in-depth-part-2.md
2. ### 【iOS沉思录】NSThread、GCD、NSOperation多线程编程总结

   [http://blog.csdn.net/cordova/article/details/69060085](http://blog.csdn.net/cordova/article/details/69060085)

3. ### 多线程导图

   ![](/assets/多线程.png)

- ### 线程之间的通信

> UI更新，必须要在主线程进行，否则会有未知的操作，无法在界面上及时正常显示。
>
**解决方法**:
> 将UI更新的代码写在主线程上即可，代码同步到主线程上主要有三种方法：NSThread、NSOperationQueue和GCD，三个层次的多线程都可以获取主线程并同步。

```objectivec
简单说将代码同步到主线程执行的三种方法如下：

// 1.NSThread
[self performSelectorOnMainThread:@selector(updateUI) withObject:nil waitUntilDone:NO];

- (void)updateUI {
    // UI更新代码
    self.alert.text = @"Thanks!";
}

// 2.NSOperationQueue
[[NSOperationQueue mainQueue] addOperationWithBlock:^{
    // UI更新代码
    self.alert.text = @"Thanks!";
    }];

// 3.GCD
dispatch_async(dispatch_get_main_queue(), ^{
   // UI更新代码
   self.alert.text = @"Thanks!";
});

```





