## iOS视图生命周期简析

原文：[http://www.jianshu.com/p/55d1cc1a73fb](http://www.jianshu.com/p/55d1cc1a73fb)

---

视图控制对象通过alloc和init来创建，但是视图控制对象不会在创建的那一刻就马上创建相应的视图，而是等到需要使用的时候才通过调用loadView来创建，这样的做法能提高内存的使用率。

#### iOS视图控制对象生命周期

-init、viewDidLoad、viewWillAppear、viewDidAppear、viewWillDisappear、viewDidDisappear的区别及用途

**init**－初始化程序  
**viewDidLoad**－加载视图  
**viewWillAppear**－UIViewController对象的视图即将加入窗口时调用；  
**viewDidApper**－UIViewController对象的视图已经加入到窗口时调用；  
**viewWillDisappear**－UIViewController对象的视图即将消失、被覆盖或是隐藏时调用；  
**viewDidDisappear**－UIViewController对象的视图已经消失、被覆盖或是隐藏时调用；  
**viewVillUnload**－当内存过低时，需要释放一些不需要使用的视图时，即将释放时调用；  
**viewDidUnload**－当内存过低，释放一些不需要的视图时调用。

当一个视图控制器被创建，并在屏幕上显示的时候。 代码的执行顺序  
1、 alloc 创建对象，分配空间  
2、init \(initWithNibName\) 初始化对象，初始化数据  
3、loadView 从nib载入视图 ，通常这一步不需要去干涉。除非你没有使用xib文件创建视图  
4、viewDidLoad 载入完成，可以进行自定义数据以及动态创建其他控件  
5、viewWillAppear 视图将出现在屏幕之前，马上这个视图就会被展现在屏幕上了  
6、viewDidAppear 视图已在屏幕上渲染完成

当一个视图被移除屏幕并且销毁的时候的执行顺序，这个顺序差不多和上面的相反  
1、viewWillDisappear 视图将被从屏幕上移除之前执行  
2、viewDidDisappear 视图已经被从屏幕上移除，用户看不到这个视图了  
3、dealloc 视图被销毁，此处需要对你在init和viewDidLoad中创建的对象进行释放

关于viewDidUnload ：在发生内存警告的时候如果本视图不是当前屏幕上正在显示的视图的话， viewDidUnload将会被执行，本视图的所有子视图将被销毁，以释放内存,此时开发者需要手动对viewLoad、viewDidLoad中创建的对象释放内存。 因为当这个视图再次显示在屏幕上的时候，viewLoad、viewDidLoad 再次被调用，以便再次构造视图。在设备上按了Home键之后，系统也不一定会调用这个方法，因为IOS4之后，系统允许将APP在后台挂起，并将其继续滞留在内存中，因此，viewcontroller并不会调用这个方法来清除内存。

  


