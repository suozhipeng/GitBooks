# 程序猿代码规范

原文链接：[http://www.jianshu.com/p/8579ec4cb4f8](http://www.jianshu.com/p/8579ec4cb4f8)

---

从代码的整洁度上就可以看出一个程序员的实力，规范其实就是让你养成一种良好习惯的标杆，在此面前我们应该顺从（本篇以OC为例）。

1. 单页代码最好控制在800行以内，每个方法最好不要超过100行，过多建议对代码进行重构

2. 相同的逻辑方法定义避免在多个地方出现，尽量将公用的类、方法抽取出来

3. 删除未被使用的代码，不要大片注释未被使用的代码，确定代码不会使用，请及时删除

4. 对其他项目中copy过来的代码，根据具体需要更新代码风格，及时删除未被使用的代码

5. 项目中所有Group或者文件名称（图片名字等），不要使用汉字命名，尽量使用英文命名，国内特有名词可以使用拼音。

6. 项目中所有Group都需要在项目目录中存在一个真实的目录，Group中的文件与真实目录中文件一一对应。

7. 请在项目中写必要代码的注释

8. 请多使用 \#pragma mark - Mark Name 对方法进行分组 。如:

   ```
   #pragma mark - **********View lifeCycle******
   ```

9. 所有类名称以项目工程开头命名，如：“JS”（简书）。针对不同视图控制器，在末尾添加后缀，如： UIButton 后缀添加“Button"或大家皆知的简写，NSArray的变量命名为xxxArray等。

10. 类、方法、属性等命名，做到见名知意，采用驼峰式命名规则。

11. 根据资源类型或者所属业务逻辑对项目资源进行分组，使得整个项目结构清晰明了；整个项目保持一种代码书写风格。

12. 避免在程序中直接出现常数，使用超过一次的应以宏定义的形式来替代。常数的宏定义应与它实际使用时的类型相一致。如以3.0来定义浮点类型，用3表示整型。 常量的命名应当能够表达出它的用途，并且用大写字母表示。例如：

    ```
    #define PI 3.1415926
    ```

13. 当使用条件语句编码时，不要嵌套if语句，多个返回语句也是OK。

    ```objectivec
    - (void)testMethod {
       if (![testSome boolValue]) {// 不合适就返回，下面做处理
       return;
      }
     //Do something important
    }
    ```

14. 当方法通过引用来返回一个错误参数，判断返回值而不是错误变量。在成功的情况下，有些Apple的APIs记录垃圾值\(garbage values\)到错误参数\(如果non-NULL\)，那么判断错误值会导致false负值和crash。

    ```objectivec
    NSError *error;
    if (![self trySomethingWithError:&error]) {
    // Handle Error
    }
    ```

15. 当参数过长时，每个参数占用一行，以冒号对齐。如：

    ```
    - (void)aboutFisrtNumber:(NSString *)oneStr
              withNextNumber:(NSString *)twoStr
              withLastNumber:(NSString *)threeStr{
        // do something
    }
    ```

16. 一行很长的代码应该分成两行代码，下一行用两个空格隔开

    ```
    self.productsRequest = [[JSProductsRequest alloc] 
      initWithProductIdentifiers:productIdentifiers];
    ```

17. 删除多余的空行，所有方法与方法之间空1行，所有代码块之间空1行。变量声明后需要空1行，如果需要分类区别，各类别之间空1行。条件、循环，选择语句，整个语句结束，需要空1行。最后一个括弧之前不空行。注释与代码之间不空行。

    ```
     #pragma 与方法之间空1行

    ```

18. 每行代码最多不得超过100个字

19. 如果类声明中包含多个protocol，每个protocol占用一行，缩进2个字符如:

    ```
      @interface BootViewController : UITableViewController<</p>
      UITableViewDelegate,
      UITableViewDataSource,
      UITextFieldDelegate,
      UITextViewDelegate
      >{
      // code
      }
    ```

20. 图片命名：采用单词全拼，或者大家公认无岐义的缩写\(比如：nav，bg，btn等\)；采用“模块+功能”命名法，模块分为公共模块、私有模块。公共模块主要包括统一的背景，导航条，标签，公共的按钮背景，公共的默认图等等；私有模块主要根据app的业务；功能模块划分，比如用户中心，消息中心等。建议背景图采用以bg作前缀，按钮背景采用btn作前缀。

![](http://upload-images.jianshu.io/upload_images/1170656-798d683d4df650ce.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

