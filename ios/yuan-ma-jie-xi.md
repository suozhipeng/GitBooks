# iOS源码解析案例

_推荐博客：_ 
1. [分析代码逻辑](http://draveness.me/)

---

## **CocoaPods 源码解析**

[_CocoaPods都做了什么_](https://zhuanlan.zhihu.com/p/22652365)

---

## **iOS App 签名的原理**

[原文链接](https://zhuanlan.zhihu.com/p/25873775) 
公钥基础设施PKI体系

> 1. 非对称加密
> 2. 数字签名
> 3. 简单签名
> 4. 复杂签名
> 5. 当前使用的签名方式

**当前使用的签名方式**
![](/assets/v2-779c5beca262fbd0da75c26ca1f84b55_r.png) 
整个流程：

> 1. 在你的 Mac 开发机器生成一对公私钥，这里称为公钥L，私钥L。L:Local
> 2. 苹果自己有固定的一对公私钥，跟上面 AppStore 例子一样，私钥在苹果后台，公钥在每个 iOS 设备上。这里称为公钥A，私钥A。A:Apple
> 3. 把公钥 L 传到苹果后台，用苹果后台里的私钥 A 去签名公钥 L。得到一份数据包含了公钥 L 以及其签名，把这份数据称为证书。
> 4. 在苹果后台申请 AppID，配置好设备 ID 列表和 APP 可使用的权限，再加上第③步的证书，组成的数据用私钥 A 签名，把数据和签名一起组成一个 Provisioning Profile 文件，下载到本地 Mac 开发机。
> 5. 在开发时，编译完一个 APP 后，用本地的私钥 L 对这个 APP 进行签名，同时把第④步得到的 Provisioning Profile 文件打包进 APP 里，文件名为 embedded.mobileprovision，把 APP 安装到手机上。
> 6. 在安装时，iOS 系统取得证书，通过系统内置的公钥 A，去验证 embedded.mobileprovision 的数字签名是否正确，里面的证书签名也会再验一遍。
> 7. 确保了 embedded.mobileprovision 里的数据都是苹果授权以后，就可以取出里面的数据，做各种验证，包括用公钥 L 验证APP签名，验证设备 ID 是否在 ID 列表上，AppID 是否对应得上，权限开关是否跟 APP 里的 Entitlements 对应等。

---

## **携程是如何做React Native优化的**

[原文链接](https://zhuanlan.zhihu.com/p/23715716)

RN开发中，经常遇到的问题和优化

> 1. 打包出来的JSBundle过大；
> 拆包业务模块
> 2. 首次进入RN页面加载缓慢； 
> 页面加载优化：
>
> 打包工具优化：Unbundle --&gt; CRNUnbunle 
> unbundle只适用 Android 
> prepack适用iOS
>
> 3. 稳定性不够，有大量因为RN导致的crash；
>
> iOS Crash处理： 
> 基本都来自RCTFatalException，都是RCTFatal抛出错误信息所知， 处理也相对简单, 设置自己的Error Handler即可 
> void RCTSetFatalHandler\(RCTFatalHandler fatalHandler\);
>
> Android Crash处理： 
> 1、bundle加载过程中的RuntimeException； 
> 2、JS执行过程中的，处理NativeExceptionsManagerModule； 
> 3、native模块执行出错， 处理NativeModuleCallExceptionHandler 
> 4、so lib加载失败，经典的java.lang.UnsatisfiedLinkError, 这种问题，解决方案很简单，给System.load添加try catch，并且在catch里面做补偿，可以大大降低由此导致的crash；
>
> 4. 大数据量时候listview加载卡顿；
>
> CRNListView

---

## **如何优雅地使用 KVO**

[原文链接](https://zhuanlan.zhihu.com/p/25582696) 
使用Facebook 开源的 [KVOController](https://github.com/facebook/KVOController) 框架

```objective-c
[self.KVOController observe:self.fizz
keyPath:@"number"
options:NSKeyValueObservingOptionNew | NSKeyValueObservingOptionOld
block:^(id _Nullable observer, id _Nonnull object, NSDictionary<NSString *,id> * _Nonnull change) {
NSLog(@"%@", change);
}];
```

> 使用 KVOController 进行键值观测可以说完美地解决了在使用原生 KVO 时遇到的各种问题。 
> 1. 不需要手动移除观察者； 
> 2. 实现 KVO 与事件发生处的代码上下文相同，不需要跨方法传参数； 
> 3. 使用 block 来替代方法能够减少使用的复杂度，提升使用 KVO 的体验； 
> 4. 每一个 keyPath 会对应一个属性，不需要在 block 中使用 if 判断 keyPath；

---