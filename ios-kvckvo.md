## KVC/KVO的底层实现机制

KVC实现机制：[http://www.cnblogs.com/cnSirM/p/5817258.html](http://www.cnblogs.com/cnSirM/p/5817258.html)  
KVO实现机制：[http://www.cnblogs.com/zy1987/p/4616764.html](http://www.cnblogs.com/zy1987/p/4616764.html)

---

KVC和KVO都属于键值编程而且底层实现机制都是**isa-swizzing，**都依赖于Runtime的动态机制

## **KVC原理**

---

KVC是Key Value Coding的简称。它是一种可以通过字符串的名字（key）来访问类属性的机制。而不是通过调用Setter、Getter方法访问。  
关键方法定义在 NSKeyValueCodingProtocol  
KVC支持类对象和内建基本数据类型。

#### KVC键值查找 {#kvc键值查找}

##### KVC概述 {#搜索单值成员}

* KVC是Key Value Coding的简称。它是一种可以通过字符串的名字（key）来访问类属性的机制。而不是通过调用Setter、Getter方法访问。
* 关键方法定义在 NSKeyValueCodingProtocol
* KVC支持类对象和内建基本数据类型。

#### KVC使用 {#kvc使用}

* 获取值  
  valueForKey: 传入NSString属性的名字。  
  valueForKeyPath: 属性的路径，xx.xx  
  valueForUndefinedKey 默认实现是抛出异常，可重写这个函数做错误处理

* 修改值  
  setValue:forKey:  
  setValue:forKeyPath:  
  setValue:forUnderfinedKey:  
  setNilValueForKey: 对非类对象属性设置nil时调用，默认抛出异常。搜索单值成员

* setValue:forKey:搜索方式

  > 1、首先搜索setKey:方法。（key指成员变量名，首字母大写）
  >
  > 2、上面的setter方法没找到，如果类方法accessInstanceVariablesDirectly返回YES。那么按 \_key，\_isKey，key，iskey的顺序搜索成员名。（NSKeyValueCodingCatogery中实现的类方法，默认实现为返回YES）
  >
  > 3、如果没有找到成员变量，调用setValue:forUnderfinedKey:

* valueForKey:的搜索方式

  > 1、首先按getKey，key，isKey的顺序查找getter方法，找到直接调用。如果是BOOL、int等内建值类型，会做NSNumber的转换。
  >
  > 2、上面的getter没找到，查找countOfKey、objectInKeyAtindex、KeyAtindexes格式的方法。如果countOfKey和另外两个方法中的一个找到，那么就会返回一个可以响应NSArray所有方法的代理集合的NSArray消息方法。
  >
  > 3、还没找到，查找countOfKey、enumeratorOfKey、memberOfKey格式的方法。如果这三个方法都找到，那么就返回一个可以响应NSSet所有方法的代理集合。  
  > 4、还是没找到，如果类方法accessInstanceVariablesDirectly返回YES。那么按 \_key，\_isKey，key，iskey的顺序搜索成员名。
  >
  > 5、再没找到，调用valueForUndefinedKey。

#### KVC实现分析 {#kvc实现分析}

KVC运用了isa-swizzing技术。isa-swizzing就是类型混合指针机制。KVC通过isa-swizzing实现其内部查找定位。isa指针（is kind of 的意思）指向维护分发表的对象的类，该分发表实际上包含了指向实现类中的方法的指针和其他数据。

比如说如下的一行KVC代码：

```
[site setValue:@"sitename" forKey:@"name"];

//会被编译器处理成

SEL sel = sel_get_uid(setValue:forKey);
IMP method = objc_msg_loopup(site->isa,sel);
method(site,sel,@"sitename",@"name");
```

> 每个类都有一张方法表，是一个hash表，值是还书指针IMP，SEL的名称就是查表时所用的键。  
> SEL数据类型：查找方法表时所用的键。定义成char\*，实质上可以理解成int值。  
> IMP数据类型：他其实就是一个编译器内部实现时候的函数指针。当Objective-C编译器去处理实现一个方法的时候，就会指向一个IMP对象，这个对象是C语言表述的类型。

**KVC的内部机制：**  
一个对象在调用setValue的时候进行了如下操作：

* （1）根据方法名找到运行方法的时候需要的环境参数
* （2）他会从自己的isa指针结合环境参数，找到具体的方法实现接口。
* （3）再直接查找得来的具体的实现方法 

## **KVO原理**

---

**KVO概述**

键值观察Key-Value-Observer就是观察者模式。

**观察者模式的定义**：一个目标对象管理所有依赖于它的观察者对象，并在它自身的状态改变时主动通知观察者对象。这个主动通知通常是通过调用各观察者对象所提供的接口方法来实现的。观察者模式较完美地将目标对象与观察者对象解耦。  
当需要检测其他类的属性值变化，但又不想被观察的类知道，有点像FBI监视嫌疑人，这个时候就可以使用KVO了。

#### KVO实现步骤 {#kvo实现步骤}

* 注册

```
//keyPath就是要观察的属性值
//options给你观察键值变化的选择
//context方便传输你需要的数据
-(void)addObserver:(NSObject *)anObserver 
        forKeyPath:(NSString *)keyPath 
           options:(NSKeyValueObservingOptions)options 
           context:(void *)context
```

* 实现方法

```
//change里存储了一些变化的数据，比如变化前的数据，变化后的数据；如果注册时context不为空，这里context就能接收到。
-(void)observeValueForKeyPath:(NSString *)keyPath 
                     ofObject:(id)object
                       change:(NSDictionary *)change 
                      context:(void *)context
```

* 移除

```
- (void)removeObserver:(NSObject *)observer forKeyPath:(NSString *)keyPath;
```

#### KVO的实现分析 {#kvo的实现分析}

使用观察者模式需要被观察者的配合，当被观察者的状态发生变化的时候通过事先定义好的接口（协议）通知观察者。在KVO的使用中我们并不需要向被观察者添加额外的代码，就能在被观察的属性变化的时候得到通知，这个功能是如何实现的呢？同KVC一样依赖于强大的Runtime机制。

系统实现KVO有以下几个步骤：

* 当类A的对象第一次被观察的时候，系统会在运行期动态创建类A的派生类。我们称为B。
* 在派生类B中重写类A的setter方法，B类在被重写的setter方法中实现通知机制。
* 类B重写会 class方法，将自己伪装成类A。类B还会重写dealloc方法释放资源。
* 系统将所有指向类A对象的isa指针指向类B的对象。

KVO同KVC一样，通过 isa-swizzling 技术来实现。当观察者被注册为一个对象的属性的观察对象的isa指针被修改，指向一个中间类，而不是在真实的类。其结果是，isa指针的值并不一定反映实例的实际类。

所以不能依靠isa指针来确定对象是否是一个类的成员。应该使用class方法来确定对象实例的类。

