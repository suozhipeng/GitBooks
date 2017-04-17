# 这里主要记录 iOS  开发过程中的零碎知识点\(Objective-C\)

1. iOS-searchbar背景去色，修改输入文字的终于搞定了  
   ![iOS-searchbar背景去色，修改输入文字的终于搞定了](/assets/iOS-searchbar背景去色，修改输入文字的终于搞定了.jpg)

2. nil、Nill、NULL、NSNull的区别  
   ![](/assets/面试：nil、Nill、NULL、NSNull的区别.jpg)

3. OC 中的保留字  
   Objective-c语言的保留字或关键词应全部使用小写字母，除下表中保留字外，private、protected、public、在类型说明中也作为保留字使用。还有nonatomanic,retain,readwrite,  
   readonly等也有特殊的使用场合。这些在我们公司全部不用
   ![ios保留字](/assets/ios保留字.png)
   
- 代码的修改规范
> 修改规范 
> 1、新增代码行新增代码行的前后应有注释行说明。
      //修改人，修改时间，修改说明新增代码行//修改结束2、删除代码行删除代码向的前后用注释行说明//修改人，修改时间，修改说明要删除的代码行(将要删除的语句进行注释)//修改结束3、修改代码行修改代码行以注释旧代码行后再新增代码行的方式进行。//修改人，修改时间，修改说明//修改前代码行开始//修改前代码行//修改前代码行结束//修改后代码行开始修改后代码行//修改结束

- 沙盒路径：
1、Documents目录：您应该将所有的应用程序数据文件写入到这个目录下。这个目录用于存储用户数据或其它应该定期备份的信息。
2、AppName.app目录：这是应用程序的程序包目录，包含应用程序的本身。由于应用程序必须经过签名，所以您在运行时不能对这个目录中的内容进行修改，否则可能会使应用程序无法启动。
3、Library 目录：这个目录下有两个子目录：Caches 和 Preferences
Preferences 目录：包含应用程序的偏好设置文件。您不应该直接创建偏好设置文件，而是应该使用NSUserDefaults类来取得和设置应用程序的偏好.
Caches 目录：用于存放应用程序专用的支持文件，保存应用程序再次启动过程中需要的信息。
4、tmp目录：这个目录用于存放临时文件，保存应用程序再次启动过程中不需要的信息。

获取这些目录路径的方法：
> 1，获取家目录路径的函数：
NSString *homeDir = NSHomeDirectory();
>
2，获取Documents目录路径的方法：
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *docDir = [paths objectAtIndex:0];
>
3，获取Caches目录路径的方法：
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES);
NSString *cachesDir = [paths objectAtIndex:0];
>
4，获取tmp目录路径的方法：
NSString *tmpDir = NSTemporaryDirectory();
>
5，获取应用程序程序包中资源文件路径的方法：
例如获取程序包中一个图片资源（apple.png）路径的方法：
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@”apple” ofType:@”png”];
UIImage *appleImage = [[UIImage alloc] initWithContentsOfFile:imagePath];

