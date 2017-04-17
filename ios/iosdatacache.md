# iOS五种本地缓存数据方式

原文链接：[http://www.2cto.com/kf/201605/510725.html](http://www.2cto.com/kf/201605/510725.html)

---

前言

iOS本地缓存数据方式有五种：

**1.直接写文件方式**：可以存储的对象有NSString、NSArray、NSDictionary、NSData、NSNumber，数据全部存放在一个属性列表文件（\*.plist文件）中。

**2.NSUserDefaults（偏好设置）**，用来存储应用设置信息，文件放在perference目录下。

**3.归档操作（NSkeyedArchiver）**，不同于前面两种，它可以把自定义对象存放在文件中。

**4.coreData**:coreData是苹果官方iOS5之后推出的综合型[数据库](http://www.2cto.com/database/)，其使用了ORM\(Object Relational Mapping\)对象关系映射技术，将对象转换成数据，存储在本地数据库中。coreData为了提高效率，甚至将数据存储在不同的数据库中，且在使用的时候将本地数据放到内存中使得访问速度更快。我们可以选择coreData的数据存储方式，包括sqlite、xml等格式。但也正是coreData 是完全面向对象的，其在执行效率上比不上原生的数据库。除此之外，coreData拥有数据验证、undo等其他功能，在功能上是几种持久化方案最多的。

**5.FMDB**：FMDB是iOS平台的SQLite数据库框架，FMDB以OC的方式封装了SQLite的C语言API，使用起来更加面向对象，省去了很多麻烦、冗余的C语言代码，对比苹果自带的Core Data框架，更加轻量级和灵活，提供了多线程安全的数据库操作方法，有效地防止数据混乱。

# 方式一：直接写文件

```objectivec

//获取沙盒中缓存文件夹路径

//方法一

//沙盒主目录

NSString *homePath = NSHomeDirectory();

//拼接路径

NSString *path = [homePath stringByAppendingPathComponent:@"Library/Caches"];

//方法二

//第一个参数目标文件夹目录（NSCachesDirectory查找缓存文件夹），第二个参数为查找目录的域（NSUserDomainMask为在用户目录下查找），第三个参数为结果中主目录是否展开，不展开则显示为~

NSArray *arr = NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES);

//虽然该方法返回的是一个数组，但是由于一个目标文件夹只有一个目录，所以数组中只有一个元素。

NSString *cachePath = [arr lastObject];

//或者

// NSString *cachePath = [arr objectAtIndex:0];

/**
 //获取沙盒中Document文件夹或者tmp文件夹路径都可使用上面两种方法
 //tmp文件夹路径可直接这样获取
 NSString *tmpPath = NSTemporaryDirectory();
 NSLog(@"%@",tmpPath);
 **/

//拼接路径（目标路径），这个时候如果目录下不存在这个lotheve.plist文件，这个目录实际上是不存在的。

NSString *filePath = [cachePath stringByAppendingPathComponent:@"tese.plist"];

NSLog(@"%@",filePath);

//创建数据

NSDictionary *content = @{@"字典数据测试1":@"1",@"字典数据测试2":@"2",@"字典数据测试":@"3"};

//将数据存到目标路径的文件中(这个时候如果该路径下文件不存在将会自动创建)

//用writeToFile方法写文件会覆盖掉原来的内容

[content writeToFile:filePath atomically:YES];

//读取数据(通过字典的方式读出文件中的内容)

NSDictionary *dic = [NSDictionary dictionaryWithContentsOfFile:filePath];

NSLog(@"%@",dic);
```

沙盒中Library/Caches目录下多了lotheve.plist文件：

![](http://www.2cto.com/uploadfile/2016/0520/20160520025819779.jpg "\")

文件内容：

![](http://www.2cto.com/uploadfile/2016/0520/20160520025830998.jpg "\")

如何获取模拟器沙盒路径：

打印日志，复制路径打开mac finder，点击左上角菜单前往，前往文件夹，把路径粘贴上去。

```objectivec


NSString *path = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory,NSUserDomainMask,YES) objectAtIndex:0];
NSLog(@"%@",path);
```

## 方式二：NSUserDefaults（偏好设置）

每个应用都有一个NSUesrDefaults实例，通过它可以存储应用配置信息以及用户信息，比如保存用户名、密码、字体大小、是否自动登录等等。数据自动保存在沙盒的Libarary/Preferences目录下。同样，该方法只能存取NSString、NSArray、NSDictionary、NSData、NSNumber类型的数据。

属性列表是一种明文的轻量级存储方式，其存储格式有多种，最常规格式为XML格式。在我们创建一个新的项目的时候，Xcode会自动生成一个info.plist文件用来存储项目的部分[系统](http://www.2cto.com/os/)设置。plist只能用数组\(NSArray\)或者字典\(NSDictionary\)进行读取，由于属性列表本身不[加密](http://www.2cto.com/article/jiami/)，所以安全性几乎可以说为零。因为，属性列表正常用于存储少量的并且不重要的数据。

在程序启动后，系统会自动创建一个NSUserDefaults的单例对象，我们可以获取这个单例来存储少量的数据，它会将输出存储在.plist格式的文件中。其优点是像字典一样的赋值方式方便简单，但缺点是无法存储自定义的数据。

代码示例：

```objectivec


//点击button保存数据
(IBAction)saveData:(id)sender {
//获取NSUserDefaults对象
NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];
//存数据，不需要设置路劲，NSUserDefaults将数据保存在preferences目录下
[userDefaults setObject:@"Lotheve" forKey:@"name"];
[userDefaults setObject:@"NSUserDefaults" forKey:@"demo"];
//立刻保存（同步）数据（如果不写这句话，会在将来某个时间点自动将数据保存在preferences目录下）
[userDefaults synchronize];
NSLog(@"数据已保存");
}
//点击button读取数据
(IBAction)getData:(id)sender
{
//获取NSUserDefaults对象
NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];
//读取数据
NSString *name = [userDefaults objectForKey:@"name"];
NSString *demo = [userDefaults objectForKey:@"demo"];
//打印数据
NSLog(@"name = %@ demo =%@",name,demo);
}
```

点击“保存数据”后，查看沙盒中的Libarary/ Preferences目录：

![](http://www.2cto.com/uploadfile/2016/0520/20160520025846174.jpg "\")

数据以plist的格式写入磁盘中了。点开查看数据：

### ![](http://www.2cto.com/uploadfile/2016/0520/20160520025856358.jpg "\")

方式三：NSKeyedArchiver（归档操作）

与属性列表相反，同样作为轻量级存储的持久化方案，数据归档是进行加密处理的，数据在经过归档处理会转换成二进制数据，所以安全性要远远高于属性列表。另外使用归档方式，我们可以将复杂的对象写入文件中，并且不管添加多少对象，将对象写入磁盘的方式都是一样的。

使用NSKeyedArchiver对自定义的数据进行序列化，并且保存在沙盒目录下。使用这种归档的前提是让存储的数据模型遵守NSCoding协议并且实现其两个协议方法。（当然，如果为了更加安全的存储，也可以遵守NSSecureCoding协议，这是iOS6之后新增的特性）

使用归档操作存储数据的主要好处是，不同于前面两种方法只能存储几个常用的数据类型的数据，NSKeyedArchiver可以存储自定义的对象。

代码示例：

```objectivec


先创建一个继承NSObject的类，该类遵守NSCoding协议
TestPerson.h
@interface TestPerson : NSObject
@property (nonatomic, copy) NSString *name;
@property (nonatomic, assign) NSInteger age;
@property (nonatomic, copy) NSString *sex;
@property (nonatomic, strong) NSArray *familyMumbers;
@end
TestPerson.m
#import "TestPerson.h"
@interface TestPerson ()
@end
@implementationTestPerson
(void)viewDidLoad
{
    [super viewDidLoad];
}
#pragma mark - NSCoding协议方法 (一定要实现)
//当进行归档操作的时候就会调用该方法
//在该方法中要写清楚要存储对象的哪些属性
(void)encodeWithCoder:(NSCoder *)aCoder
{
    NSLog(@"调用了encodeWithCoder方法");
    [aCoder encodeObject:_name forKey:@"name"];
    [aCoder encodeInteger:_age forKey:@"age"];
    [aCoder encodeObject:_sex forKey:@"sex"];
    [aCoder encodeObject:_familyMumbers forKey:@"familyMumbers"];
}
//当进行解档操作的时候就会调用该方法
//在该方法中要写清楚要提取对象的哪些属性
(id)initWithCoder:(NSCoder *)aDecoder
{
    NSLog(@"调用了initWithCoder方法");
    if (self = [super init]) {
        self.name = [aDecoder decodeObjectForKey:@"name"];
        self.age = [aDecoder decodeIntegerForKey:@"age"];
        self.sex = [aDecoder decodeObjectForKey:@"sex"];
        _familyMumbers = [aDecoder decodeObjectForKey:@"familyMumbers"];
    }
    return self;
}
@end
```

这里还要讲一下一个小技巧：使用static修饰来替代宏定义。上面的序列化中，我们可以看到NSCoding的协议方法中对数据进行序列化并且使用一个key来保存它。正常情况下我们可以使用宏来定义key，但是过多的宏定义在编译时也会造成大量的损耗。这时候可以使用static定义静态变量来取代宏定义。

```objectivec


static NSString * const kUserNameKey = @"userName";
让自定义的数据遵循NSCoding协议后，我们就能使用NSKeyedArchiver和NSKeyedUnarchiver来对持久化的数据进行存取操作了:
-(IBAction)saveData:(id)sender
{
    //创建一个自定义类的实例
    _p = [[TestPerson alloc]init];
    _p.name = @"Lotheve";
    _p.age = 20;
    _p.sex = @"m";
    _p.familyMumbers = @[@"Father",@"Mather",@"Me"];
    //获取文件路径
    NSString *docPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
    //文件类型可以随便取，不一定要正确的格式
    NSString *targetPath = [docPath stringByAppendingPathComponent:@"lotheve.plist"];
    //将自定义对象保存在指定路径下
    [NSKeyedArchiver archiveRootObject:_p toFile:targetPath];
    NSLog(@"文件已储存");
}
-(IBAction)getData:(id)sender
{
    //获取文件路径
    NSString *docPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
    NSString *targetPath = [docPath stringByAppendingPathComponent:@"lotheve.plist"];
    TestPerson *person = [NSKeyedUnarchiver unarchiveObjectWithFile:targetPath];
    NSLog(@"name = %@ , age =%ld , sex = %@ , familyMubers = %@",person.name,person.age,person.sex,person.familyMumbers);
    NSLog(@"文件已提取");
}
```

点击“保存数据”后，查看沙盒中Documents目录：

![](http://www.2cto.com/uploadfile/2016/0520/20160520025909919.jpg "\")

点击查看文件内容：

![](http://www.2cto.com/uploadfile/2016/0520/20160520025921563.jpg "\")

点击“提取数据”后打印结果：

#### ![](http://www.2cto.com/uploadfile/2016/0520/20160520025931319.jpg "\")

方式四：coreData

coreData是iOS5之后苹果推出的数据持久化框架，其提供了ORM的功能，将对象和数据相互转换。其中，它提供了包括sqlite、xml、plist等本地存储文件，默认使用sqlite进行存储。coreData具有两个模型：关系模型和对象模型，关系模型即是数据库，对象模型为OC对象。其关系图如下：

![](http://www.2cto.com/uploadfile/2016/0520/20160520030002982.jpg "\")

由于我们不需要关心数据的存储，coreData使用起来算是最简单的持久化方案。要使用coreData有两个方式，一个是在创建项目的时候勾选use core data，另一个则是手动创建。在这里我们要讲解的是前者创建的方式：

1、创建新项目勾选使用coreData

![](http://www.2cto.com/uploadfile/2016/0520/20160520030014906.jpg "\")

2、创建关系模型，在这里我创建的模型名字是LXDCoreDataDemo（注意名字一定要和项目名称保持一致）

![](http://www.2cto.com/uploadfile/2016/0520/20160520030024531.jpg "\")

3、在创建的关系模型中添加实体，命名为Person，并且添加三个字段：name、age、score

![](http://www.2cto.com/uploadfile/2016/0520/20160520030034315.jpg "\")

到了这里我们的实体模型就创建好了，接下来就是通过NSManagedObject来将实体模型转换成对象。通过从coreData取出的对象，全部都是继承自NSManagedObject的子类。那么我们需要根据当前的关系模型来创建Person类

![](http://www.2cto.com/uploadfile/2016/0520/20160520030043993.jpg "\")

选择LXDCoreDataDemo -&gt; Next -&gt; Person -&gt; Create，我们就创建好了Person，这时候三个成员属性都会自动添加完成

![](http://www.2cto.com/uploadfile/2016/0520/20160520030052360.jpg "\")

在执行操作的类实现文件中，我们要加入AppDelegate和Person的头文件，因为在创建项目的时候如果我们勾选了use core data的选项，appDelegate文件中会帮我们生成用于管理、存储这些模型的对象，我们可以通过添加头文件来使用。插入数据的代码如下：

```objectivec


//先取出coredata上下文管理者
AppDelegate *appDelegate = [[UIApplication sharedApplication] delegate];
NSManagedObjectContext *context = appDelegate.managedObjectContext;
//保存新数据
Person *person = [NSEntityDescription insertNewObjectForEntityForName: @"Person" inManagedObjectContext: context];
person.name = @"czk"
person.score = [NSNumber numberWithInt:100]；
person.age = [NSNumber numberWithInt:25];
[appDelegate saveContext];
//查询所有数据
NSError *error;
NSFetchRequest *request = [NSFetchRequest new];
NSEntityDescription *entity = [NSEntityDescription entityForName: @"Person" inManagedObjectContext: context];
[request setEntity: entity];
NSArray *results = [[context executeFetchRequest: request error: &error] copy];
for (Person *p in results) {
    NSLog(@"%@, %@, %@", p.name, p.age, p.score);
}
```

_**注意：如果出现崩溃异常，请卸载App后重新安装。**_

_**方式五：FMDB**_

_**优点:**_

对多线程的并发操作进行处理，所以是线程安全的；

以OC的方式封装了SQLite的C语言API，使用起来更加的方便；

FMDB是轻量级的框架，使用灵活。

缺点:

因为它是OC的语言封装的，只能在ios开发的时候使用，所以在实现跨平台操作的时候存在局限性。

_**FMDB有三个主要的类**_

（1）FMDatabase

一个FMDatabase对象就代表一个单独的SQLite数据库

用来执行SQL语句

（2）FMResultSet

使用FMDatabase执行查询后的结果集

（3）FMDatabaseQueue

用于在多线程中执行多个查询或更新，它是线程安全的

这里建议使用CocoaPods导入FMDB，关于CocoaPods的使用这里就不啰嗦了。

创建数据库：

db=\[FMDatabasedatabaseWithPath:database\_path\];

1、当数据库文件不存在时，fmdb会自己创建一个。

2、 如果你传入的参数是空串：@"" ，则fmdb会在临时文件目录下创建这个数据库，数据库断开连接时，数据库文件被删除。

3、如果你传入的参数是 NULL，则它会建立一个在内存中的数据库，数据库断开连接时，数据库文件被删除。

打开数据库：

\[dbopen\]；

返回BOOL型。

[关闭数据库：](http://www.jianshu.com/p/72c12b0e55f3)

\[dbclose\]；

数据库增删改等操作：

除了查询操作，FMDB数据库操作都执行executeUpdate方法，这个方法返回BOOL型。

![](http://www.2cto.com/uploadfile/2016/0520/20160520030143441.jpg "\")

看一下例子：

[创建表：](http://www.jianshu.com/p/72c12b0e55f3)

```objectivec


if([dbopen]){
    NSString*sqlCreateTable=[NSStringstringWithFormat:@"CREATETABLEIFNOTEXISTS'%@'('%@'INTEGERPRIMARYKEYAUTOINCREMENT,'%@'TEXT,'%@'INTEGER,'%@'TEXT)",TABLENAME,ID,NAME,AGE,ADDRESS];
    BOOLres=[dbexecuteUpdate:sqlCreateTable];
    if(!res){
        NSLog(@"errorwhencreatingdbtable");
    }else{
        NSLog(@"successtocreatingdbtable");
    }
    [dbclose];
}

```

添加数据：

```objectivec


if([dbopen]){
    NSString*insertSql1=[NSStringstringWithFormat:
                         @"INSERTINTO'%@'('%@','%@','%@')VALUES('%@','%@','%@')",
                         TABLENAME,NAME,AGE,ADDRESS,@"张三",@"13",@"济南"];
    BOOLres=[dbexecuteUpdate:insertSql1];
    NSString*insertSql2=[NSStringstringWithFormat:
                         @"INSERTINTO'%@'('%@','%@','%@')VALUES('%@','%@','%@')",
                         TABLENAME,NAME,AGE,ADDRESS,@"李四",@"12",@"济南"];
    BOOLres2=[dbexecuteUpdate:insertSql2];
    if(!res){
        NSLog(@"errorwheninsertdbtable");
    }else{
        NSLog(@"successtoinsertdbtable");
    }
    [dbclose];
}
```

修改数据：

```objectivec


if([dbopen]){
    NSString*updateSql=[NSStringstringWithFormat:
                        @"UPDATE'%@'SET'%@'='%@'WHERE'%@'='%@'",
                        TABLENAME,AGE,@"15",AGE,@"13"];
    BOOLres=[dbexecuteUpdate:updateSql];
    if(!res){
        NSLog(@"errorwhenupdatedbtable");
    }else{
        NSLog(@"successtoupdatedbtable");
    }
    [dbclose];
}
```

删除数据：

```objectivec


if([dbopen]){
    NSString*deleteSql=[NSStringstringWithFormat:
                        @"deletefrom%@where%@='%@'",
                        TABLENAME,NAME,@"张三"];
    BOOLres=[dbexecuteUpdate:deleteSql];
    if(!res){
        NSLog(@"errorwhendeletedbtable");
    }else{
        NSLog(@"successtodeletedbtable");
    }
    [dbclose];
}

```

数据库查询操作：

```objectivec


//查询操作使用了executeQuery，并涉及到FMResultSet。
if([dbopen]){
    NSString*sql=[NSStringstringWithFormat:
                  @"SELECT*FROM%@",TABLENAME];
    FMResultSet*rs=[dbexecuteQuery:sql];
    while([rsnext]){
        intId=[rsintForColumn:ID];
        NSString*name=[rsstringForColumn:NAME];
        NSString*age=[rsstringForColumn:AGE];
        NSString*address=[rsstringForColumn:ADDRESS];
        NSLog(@"id=%d,name=%@,age=%@address=%@",Id,name,age,address);
    }
    [dbclose];
}
```

FMDB的FMResultSet提供了多个方法来获取不同类型的数据：

![](http://www.2cto.com/uploadfile/2016/0520/20160520030157721.jpg "\")

数据库多线程操作：

如果应用中使用了多线程操作数据库，那么就需要使用FMDatabaseQueue来保证线程安全了。 应用中不可在多个线程中共同使用一个FMDatabase对象操作数据库，这样会引起数据库数据混乱。 为了多线程操作数据库安全，FMDB使用了FMDatabaseQueue，使用FMDatabaseQueue很简单，首先用一个数据库文件地址来初使化FMDatabaseQueue，然后就可以将一个闭包\(block\)传入inDatabase方法中。 在闭包中操作数据库，而不直接参与FMDatabase的管理。

```objectivec


FMDatabaseQueue * queue = [FMDatabaseQueue databaseQueueWithPath:database_path];

dispatch_queue_tq1=dispatch_queue_create("queue1",NULL);

dispatch_queue_tq2=dispatch_queue_create("queue2",NULL);

dispatch_async(q1,^{
    
    for(inti=0;i<50;++i){
        
        [queueinDatabase:^(FMDatabase*db2){
            
            NSString*insertSql1=[NSStringstringWithFormat:
                                 
                                 @"INSERTINTO'%@'('%@','%@','%@')VALUES(?,?,?)",
                                 
                                 TABLENAME,NAME,AGE,ADDRESS];
            
            NSString*name=[NSStringstringWithFormat:@"jack%d",i];
            
            NSString*age=[NSStringstringWithFormat:@"%d",10+i];
            
            BOOLres=[db2executeUpdate:insertSql1,name,age,@"济南"];
            
            if(!res){
                
                NSLog(@"errortoinsterdata:%@",name);
                
            }else{
                
                NSLog(@"succtoinsterdata:%@",name);
                
            }
            
        }];
        
    }
    
});

dispatch_async(q2,^{
    
    for(inti=0;i<50;++i){
        
        [queueinDatabase:^(FMDatabase*db2){
            
            NSString*insertSql2=[NSStringstringWithFormat:
                                 
                                 @"INSERTINTO'%@'('%@','%@','%@')VALUES(?,?,?)",
                                 
                                 TABLENAME,NAME,AGE,ADDRESS];
            
            NSString*name=[NSStringstringWithFormat:@"lilei%d",i];
            
            NSString*age=[NSStringstringWithFormat:@"%d",10+i];
            
            BOOLres=[db2executeUpdate:insertSql2,name,age,@"北京"];
            
            if(!res){
                
                NSLog(@"errortoinsterdata:%@",name);
                
            }else{
                
                NSLog(@"succtoinsterdata:%@",name);
                
            }
            
        }];
        
    }
    
});
```

**总结：**

上面已经分别介绍了五种方案的优缺点，在开发中，并没有说哪种持久化方案是最好的，只能说在不同开发场景下，最适合使用的持久化方案

