## 常用排序算法总结(一)
> http://www.cnblogs.com/eniac12/p/5329396.html

## 常用排序算法总结(二)
>http://www.cnblogs.com/eniac12/p/5332117.html

## iOS算法目录合集

> http://www.jianshu.com/p/4f8e4071f85b

## 很全面的算法和数据结构知识（含代码实现）
> https://github.com/kdn251/interviews/blob/master/README-zh-cn.md

### 1.在 N 个数中，找到前 k 个数** 或者 **100亿个数字找出最大的10个

> 链接1：[https://www.zhihu.com/question/28874340/answer/43276792](https://www.zhihu.com/question/28874340/answer/43276792)  
> 链接2：[http://www.cnblogs.com/nzbbody/p/3576894.html](http://www.cnblogs.com/nzbbody/p/3576894.html)

---

## 算法列表

在这个表格中，n是要被[排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)的纪录数量以及k是不同键值的数量。

### 稳定的

[冒泡排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（bubble sort） — O\(n^2）

[鸡尾酒排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)\(Cocktail sort，双向的冒泡排序\) — O\(n^2）

[插入排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（insertion sort）— O\(n^2\)

[桶排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（bucket sort）— O\(n\); 需要 O\(k\) 额外空间

[计数排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)\(counting sort\) — O\(n+k\); 需要 O\(n+k\) 额外空间

[合并排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（merge sort）— O\(nlogn\); 需要 O\(n\) 额外空间

原地合并排序— O\(n^2\)

[二叉排序树](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)排序 （Binary tree sort） — O\(nlogn\)期望时间； O\(n^2\)最坏时间； 需要 O\(n\) 额外空间

[鸽巢排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)\(Pigeonhole sort\) — O\(n+k\); 需要 O\(k\) 额外空间

[基数排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（radix sort）— O\(n·k\); 需要 O\(n\) 额外空间

[Gnome 排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(n^2\)

[图书馆排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(nlogn\) with high probability，需要 （1+ε\)n额外空间

### 不稳定的

[选择排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（selection sort）— O\(n^2\)

[希尔排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（shell sort）— O\(nlogn\) 如果使用最佳的现在版本

[组合排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(nlogn\)

[堆排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（heapsort）— O\(nlogn\)

[平滑排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(nlogn\)

[快速排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（quicksort）— O\(nlogn\) 期望时间，O\(n^2\) 最坏情况； 对于大的、乱数列表一般相信是最快的已知排序

[Introsort](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(nlogn\)

[Patience sorting](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(nlogn+k\) 最坏情况时间，需要 额外的 O\(n+k\) 空间，也需要找到[最长的递增子串行](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（longest increasing subsequence）

### 不实用的

[Bogo排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(n×n!\) 期望时间，无穷的最坏情况。

[Stupid sort](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(n^3\); 递归版本需要 O\(n^2\) 额外[存储器](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)

[珠排序](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)（Bead sort） — O\(n\) or O（√n\)，但需要特别的硬件

[Pancake sorting](http://baike.baidu.com/edit/排序算法/5399605?dl=3#)— O\(n\)，但需要特别的硬件

stooge sort——O（n^2.7）很漂亮但是很耗时

---

[冒泡排序](http://www.jianshu.com/p/a8e4e540aa7f)  
[快排](http://www.jianshu.com/p/e93101534ccb)  
[插入排序](http://www.jianshu.com/p/8f714c7bbf35)

[希尔排序](http://www.jianshu.com/p/9e4359555af0)  
[链表](http://www.jianshu.com/p/cb2d43859eb5)  
[堆排序](http://www.jianshu.com/p/a175d7dafe4c)  
[二叉树](http://www.jianshu.com/p/319dfc9b36c9)  
[汉诺塔](http://www.jianshu.com/p/58b77836ae13)

**冒泡排序**

> [冒泡排序](http://baike.baidu.com/item/冒泡排序) 是这样实现的：  
> 1、从列表的第一个数字到倒数第二个数字，逐个检查：若某一位上的数字大于他的下一位，则将它与它的下一位交换。  
> 2、重复1号步骤，直至再也不能交换。  
> 冒泡排序的平均 [时间复杂度](http://baike.baidu.com/item/时间复杂度)与[插入排序](http://baike.baidu.com/item/插入排序)相同，也是平方级的，但冒泡排序是原地排序的，也就是说它不需要额外的存储空间。

```objectivec
//@2,@8,@7,@1,@10,@87,@3,@9
/* 结果:87,10,9,8,7,3,2,1*/
+ (void)bubbleSortWithArray:(NSMutableArray *)array{
    for (int i = 0; i < array.count; i++) {
        for (int j = 0; j < array.count - i - 1; j++) {
            if (array[j] < array[j+1]) {
                int temp = [array[j] intValue];
                array[j] = array[j + 1];
                array[j + 1] = [NSNumber numberWithInt:temp];
            }
        }
    }
}
// 加注释
+(void)bubbleSortWithArray:(NSMutableArray *)array{
    // NSLog(@"0000==== %@",array);
    for (int i = 0; i < array.count; i++) {
        for (int j = 0; j < array.count - i - 1; j++) {
            // NSLog(@"j = %d,ary[j] =%@,j+1 = %d,ary[j+1] =%@",j,array[j],j+1,array[j+1]);
            if (array[j] < array[j+1]) {
                int temp = [array[j] intValue];
                array[j] = array[j + 1];
                array[j + 1] = [NSNumber numberWithInt:temp];
            }
            // NSLog(@"1111==== %@",array);
        }
        // NSLog(@"2222==== %@",array);
    }
    // NSLog(@"3333==== %@",array);
}
```

**快速排序**  
[http://baike.baidu.com/item/快速排序算法/369842?fromtitle=快速排序&fromid=2084344](http://baike.baidu.com/item/快速排序算法/369842?fromtitle=快速排序&fromid=2084344)

```objectivec
// 2,8,6,5,1,4,7,3
//===> 1,2,3,4,5,6,7,8

/*
 1）设置两个变量i、j，排序开始的时候：i=0，j=N-1；
 2）以第一个数组元素作为关键数据，赋值给key，即key=A[0]；
 3）从j开始向前搜索，即由后开始向前搜索(j--)，找到第一个小于key的值A[j]，将A[j]和A[i]互换；
 4）从i开始向后搜索，即由前开始向后搜索(i++)，找到第一个大于key的A[i]，将A[i]和A[j]互换；
 5）重复第3、4步，直到i=j； (3,4步中，没找到符合条件的值，即3中A[j]不小于key,4中A[i]不大于key的时候改变j、i的值，使得j=j-1，i=i+1，直至找到为止。找到符合条件的值，进行交换的时候i， j指针位置不变。另外，i==j这一过程一定正好是i+或j-完成的时候，此时令循环结束）。
 */
+ (void)quickSortWithArray:(NSMutableArray *)array withLeft:(NSInteger)left andRight:(NSInteger)right{
    if (left >= right) return;
    NSInteger i = left;
    NSInteger j = right;
    NSInteger key = [array[left] integerValue];
    while (i < j) {
        while (i < j && key <= [array[j] integerValue]) {
            j--;
        }
        array[i] = array[j];

        while (i < j && key >= [array[i] integerValue]) {
            i++;
        }
        array[j] = array[i];
    }
    array[i] = [NSNumber numberWithInteger:key];
    [[self class] quickSortWithArray:array withLeft:left andRight:i - 1];
    [[self class] quickSortWithArray:array withLeft:i + 1 andRight:right];
}
```

[**插入排序**](http://www.jianshu.com/p/8f714c7bbf35)

> _每一步都将一个待排数据按其大小插入到已经排序的数据中的适当位置，直到全部插入完毕。_

直接插入排序、折半插入排序  
![](/assets/算法-直接插入排序.gif)

> 假定n是数组的长度，首先假设第一个元素被放置在正确的位置上，这样仅需从1到n-1范围内对剩余元素进行排序。  
> 对于每次遍历，从0到i-1范围内的元素已经被排好序，  
>     **每次遍历的任务是**：通过扫描前面已排序的子列表，将位置i处的元素定位到从0到i的子列表之内的正确的位置上。  
> 1、将arr\[i\]复制为一个名为target的临时元素。  
>         2、向下扫描列表，比较这个目标值target与arr\[i-1\]、arr\[i-2\]的大小，依次类推。  
>         3、这个比较过程在小于或等于目标值的第一个元素\(arr\[j\]\)处停止，或者在列表开始处停止（j=0）。  
>         4、在arr\[i\]小于前面任何已排序元素时，后一个条件（j=0）为真，因此，这个元素会占用新排序子列表的第一个位置。  
>         5、在扫描期间，大于目标值target的每个元素都会向右滑动一个位置（arr\[j\]=arr\[j-1\]）。  
>         6、一旦确定了正确位置j，目标值target（即原始的arr\[i\]）就会被复制到这个位置。  
>  与选择排序不同的是，插入排序将数据向右滑动，并且不会执行交换。

```objectivec
//3,1,8,9,10,2
//===>  1,2,3,8,9,10

/// 直接插入排序
+ (void)insertSort:(NSMutableArray *)list{
    for (int i = 1; i < [list count]; i++) { //第0位独自作为有序数列，从第1位开始向后遍历
        int j = i;
        NSInteger temp = [[list objectAtIndex:i] integerValue]; //保存第i位的值

        while (j >0 && temp < [[list objectAtIndex:j - 1] integerValue]) { // 第i位的值，比第i-1位的值小，那么就替换位置
            [list replaceObjectAtIndex:j withObject:[list objectAtIndex:(j - 1)]];
            j--;
        }
        [list replaceObjectAtIndex:j withObject:[NSNumber numberWithInteger:temp]];
    }
}

/// 折半插入排序
+ (void)binaryInsertSort:(NSMutableArray *)list{
    for (int i = 1; i < [list count]; i++) {
        NSInteger temp = [[list objectAtIndex:i] integerValue];
        int left = 0;
        int right = i - 1;
        while (left <= right) {
            int middle = (left + right) / 2;
            if (temp < [[list objectAtIndex:middle] integerValue]) {
                right = middle - 1;
            }else{
                left = middle + 1;
            }
        }
        for (int j = i; j > left; j--) {
            [list replaceObjectAtIndex:j withObject:[list objectAtIndex:j-1]];
        }
        [list replaceObjectAtIndex:left withObject:[NSNumber numberWithInteger:temp]];
    }
}
```

**希尔排序**  
http://www.jianshu.com/p/9e4359555af0
http://baike.baidu.com/item/希尔排序

> **缩小增量排序**，是**直接插入排序算法**的一种更高效的改进版本.  
> **该方法实质上是一种分组插入方法.**
>
算法先将要排序的一组数按某个[增量](http://baike.baidu.com/item/%E5%A2%9E%E9%87%8F)d分成若干组，每组中记录的下标相差d.对每组中全部元素进行排序，然后再用一个较小的增量对它进行，在每组中再进行排序。当[增量](http://baike.baidu.com/item/%E5%A2%9E%E9%87%8F)减到1时，整个要排序的数被分成一组，排序完成。
>
一般的初次取序列的一半为[增量](http://baike.baidu.com/item/%E5%A2%9E%E9%87%8F)，以后每次减半，直到增量为1。

eg 
> 假设待排序文件有10个记录，其关键字分别是：
49，38，65，97，76，13，27，49，55，04。
[增量](http://baike.baidu.com/item/%E5%A2%9E%E9%87%8F)序列的取值依次为：
5，2，1

![](/assets/算法-希尔排序算法分解.png)

```objectivec
//3,9,10,4,5,11
//===>3,4,5,9,10,11

+ (void)shellSort:(NSMutableArray *)list{
    int gap = [list count]/2.0;
    while (gap >= 1) {
        for (int i = gap ; i < [list count]; i++) {
            NSInteger temp = [[list objectAtIndex:i] integerValue];
            int j = i;
            while (j >= gap && temp < [[list objectAtIndex:(j-gap)] integerValue]) {
                [list replaceObjectAtIndex:j withObject:[list objectAtIndex:j-gap]];
                j-=gap;
            }
            [list replaceObjectAtIndex:j withObject:[NSNumber numberWithInteger:temp]];
        }
        gap = gap/2;
    }
}

```

**二叉树**
http://baike.baidu.com/item/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91
http://www.jianshu.com/p/319dfc9b36c9
>



**堆排序**
http://baike.baidu.com/item/%E5%A0%86%E6%8E%92%E5%BA%8F
http://www.jianshu.com/p/a175d7dafe4c
> 



**链表**
http://www.jianshu.com/p/cb2d43859eb5

**汉诺塔**
http://www.jianshu.com/p/58b77836ae13




