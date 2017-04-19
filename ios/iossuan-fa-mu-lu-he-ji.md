## iOS算法目录合集

原文链接：[http://www.jianshu.com/p/4f8e4071f85b](http://www.jianshu.com/p/4f8e4071f85b)


---

## 很全面的算法和数据结构知识（含代码实现）

【2017/04/17】  
链接：[https://github.com/kdn251/interviews/blob/master/README-zh-cn.md](https://github.com/kdn251/interviews/blob/master/README-zh-cn.md)

### 1.在 N 个数中，找到前 k 个数** 或者 **100亿个数字找出最大的10个

> 链接1：[https://www.zhihu.com/question/28874340/answer/43276792](https://www.zhihu.com/question/28874340/answer/43276792)  
> 链接2：[http://www.cnblogs.com/nzbbody/p/3576894.html](http://www.cnblogs.com/nzbbody/p/3576894.html)

---

## 算法列表

在这个表格中，n是要被[排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)的纪录数量以及k是不同键值的数量。

### 稳定的

[冒泡排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（bubble sort） — O\(n^2）

[鸡尾酒排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)\(Cocktail sort，双向的冒泡排序\) — O\(n^2）

[插入排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（insertion sort）— O\(n^2\)

[桶排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（bucket sort）— O\(n\); 需要 O\(k\) 额外空间

[计数排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)\(counting sort\) — O\(n+k\); 需要 O\(n+k\) 额外空间

[合并排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（merge sort）— O\(nlogn\); 需要 O\(n\) 额外空间

原地合并排序— O\(n^2\)

[二叉排序树](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)排序 （Binary tree sort） — O\(nlogn\)期望时间； O\(n^2\)最坏时间； 需要 O\(n\) 额外空间

[鸽巢排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)\(Pigeonhole sort\) — O\(n+k\); 需要 O\(k\) 额外空间

[基数排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（radix sort）— O\(n·k\); 需要 O\(n\) 额外空间

[Gnome 排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(n^2\)

[图书馆排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(nlogn\) with high probability，需要 （1+ε\)n额外空间

### 不稳定的

[选择排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（selection sort）— O\(n^2\)

[希尔排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（shell sort）— O\(nlogn\) 如果使用最佳的现在版本

[组合排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(nlogn\)

[堆排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（heapsort）— O\(nlogn\)

[平滑排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(nlogn\)

[快速排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（quicksort）— O\(nlogn\) 期望时间，O\(n^2\) 最坏情况； 对于大的、乱数列表一般相信是最快的已知排序

[Introsort](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(nlogn\)

[Patience sorting](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(nlogn+k\) 最坏情况时间，需要 额外的 O\(n+k\) 空间，也需要找到[最长的递增子串行](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（longest increasing subsequence）

### 不实用的

[Bogo排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(n×n!\) 期望时间，无穷的最坏情况。

[Stupid sort](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(n^3\); 递归版本需要 O\(n^2\) 额外[存储器](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)

[珠排序](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)（Bead sort） — O\(n\) or O（√n\)，但需要特别的硬件

[Pancake sorting](http://baike.baidu.com/edit/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95/5399605?dl=3#)— O\(n\)，但需要特别的硬件

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
快速排序


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

