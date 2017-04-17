# SDWebImage图片二级缓存异步加载基本原理

[原文链接](http://blog.csdn.net/cordova/article/details/54708029)：http://blog.csdn.net/cordova/article/details/54708029

链接2：http://www.jianshu.com/p/f14b17467dd9#

---

### 关于SDWebImage {#关于sdwebimage}

SDWebImage是一个针对图片加载的插件库，提供了一个支持缓存的用于异步加载图片的下载工具，特别的为常用的UI元素：UIImageView,UIButton和MKAnnotationView提供了Category类别扩展，可以作为一个很方便的工具。其中SDWebImagePrefetcher可以预先下载图片，方便后续使用.

SDWebImage的Github地址为：[https://github.com/rs/SDWebImage](https://github.com/rs/SDWebImage)

![](http://img.blog.csdn.net/20170124150746687?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY29yZG92YQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

> ### SDWebImage的几点特性 {#sdwebimage的几点特性}

* 为UIImageView,UIButton和MKAnnotationView进行了类别扩展，添加了web图片和缓存管理；
* 是一个异步图片下载器；
* 异步的内存+硬盘缓冲以及自动的缓冲过期处理；
* 后台图片解压缩功能；
* 可以保证相同的url（图片的检索key）不会被重复多次下载；
* 可以保证假的无效url不会不断尝试去加载；
* 保证主线程不会被阻塞；
* 性能高；
* 使用GCD和ARC；

> ### 支持的图片格式 {#支持的图片格式}

* UIImage支持的图片格式（JPEG,PNG等等）包括GIF都可以被支持；
* Web图片格式，包括动态的Web图片（使用WebP subspec）

> ### 使用方法示例 {#使用方法示例}

SDWebImage的使用非常简单，开发中需要的主要就是为一个UIImageView添加在线图片，用到的函数主要就是**sd\_setImageWithURL**函数\(新版本函数名都加了sd前缀\)，sd\_setImageWithURL函数提供了几种重载方法，包括只使用图片URL参数的，以及设置占位图片placeholderImage参数的等等，这个函数也是框架封装的最顶层的应用函数，开发中实际主要就用这个函数即可，以这个函数为入口，可以层层打开往底层看，可以对应到SDWebImage的整个加载逻辑和流程。

[Objective-C](http://lib.csdn.net/base/objective-c):

```objectivec
#import <SDWebImage/UIImageView+WebCache.h>
// 使用SDWebImage框架为UIImageView加载在线图片
[imageView sd_setImageWithURL:[NSURL URLWithString:@"http://www.***.com/***/image.jpg"]
             placeholderImage:[UIImage imageNamed:@"placeholder.png"]];
```

[Swift](http://lib.csdn.net/base/swift):

```swift
imageView.sd_setImageWithURL(NSURL(string: "http://www.***.com/***/image.jpg"), placeholderImage:UIImage(imageNamed:"placeholder.png"))
```

> ### SDWebImage 加载图片的流程原理： {#sdwebimage-加载图片的流程原理}

SDWebImage异步加载图片的使用非常简单，一个函数调用即可完成，但实际上这一个函数的调用会使得框架立刻完成一系列的逻辑处理，以最高效的方式加载需要的图片，具体加载流程逻辑如下：

![](http://img.blog.csdn.net/20161110152911554 "这里写图片描述")

根据流程可以知道，图片的加载采用了一种**二级缓存**机制，简单概括意思就是：能从内存缓存直接取就从内存缓存取，内存缓存没有就去硬盘缓存里取，再没有就根据提供的URL到网上下载\(下载自然会慢很多\)，下载的图片还有一个解码的过程，解码后就可以直接用了，另外下载的图片会保存到内存缓存和硬盘缓存，从而下次再取同样的图片就可以直接取了而不用重复下载。

官方的[架构](http://lib.csdn.net/base/architecture)图和时序图展示：  
![](https://github.com/rs/SDWebImage/raw/master/Docs/SDWebImageClassDiagram.png)

![](https://github.com/rs/SDWebImage/raw/master/Docs/SDWebImageSequenceDiagram.png)

上面的整个流程对应到SDWebImage框架内部，依次会挖掘出下面几个关键函数，最外层的也就是我们直接调用的sd\_setImageWithURL函数，以此函数为入口依次可能会调用到后面的函数，来完成上面的整个优化加载流程，这里以其中一个入口函数为例：

1. **sd\_setImageWithURL**： UIImageView\(WebCache\)的sd\_setImageWithURL函数只是个UIView的类扩展接口函数，负责调用并将参数传给UIView\(WebCache\)的sd\_internalSetImageWithURL函数，参数这里有图片的url和placeholder占位图片；

2. **sd\_internalSetImageWithURL**：UIView\(WebCache\)的sd\_internalSetImageWithURL函数首先将placeholder展位图片异步显示，然后给SDWebImageManager单例发送loadImageWithURL消息，传给它url参数让其再给它的SDImageCache对象发送queryCacheOperationForKey消息先从本地搜索缓存图片；

3. **loadImageWithURL**：收到loadImageWithURL消息后，SDWebImageManager单例向SDImageCache对象发送queryCacheOperationForKey消息开始在本地搜索缓存图片，SDImageCache对象先对自己发送imageFromMemoryCacheForKey消息从内存中搜索图片缓存，搜到则取出图片并通过SDCacheQueryCompletedBlock回调返回，否则再对自己发送diskImageForKey消息去硬盘搜索图片，搜到则取出图片通过SDCacheQueryCompletedBlock回调返回，内存和硬盘都搜不到则只好重新下载；

4. **downloadImageWithURL**：如果本地搜索失败，SDWebImageManager会新建一个SDWebImageDownloader下载器，并向下载器发送downloadImageWithURL消息开始下载网络图片；下载成功并解码后一方面将图片缓存到本地，另一方面取出图片进行显示。其中像图片下载以及图片解码等耗时操作都是异步执行，不会拖慢主线程。

> ### 补充说明 {#补充说明}

SDImageCache在初始化的时候会注册一些消息通知，在内存警告或退到后台的时候会清理内存图片缓存，应用结束的时候会清理掉过期的图片。

