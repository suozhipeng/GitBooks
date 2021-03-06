# 如何面试 iOS leader 或者移动端 leader？
---
[原文链接](https://www.zhihu.com/question/47218985)

===

**创业型公司的话，招聘leader岗位一定是技术型的**管理技能和技术实力最多二八开，两成的精力用在管理上已经足够。

管理上的要求面试相对简单，谈管理方式的时候，能注重团队沟通即可，搞技术的都闷一些，大部分的管理问题都是由于缺乏沟通导致的。不用口才多好，思路清晰，谈吐得宜，不偏激，不内敛，基本就能说明沟通上不存在问题。

技术方面的要求要放搞一些，leader在知识积累上一定是**广度精于深度**。
iOS方面一下一项都不能缺：

>1. 项目基础架构的理解。对架构的了解不用深于架构师，但常见的架构方式及其基本差别应该如数家珍，架构不分对错，能有自己的一套理解会更好。
- UI方面需要对性能优化有一定的了解。UI问题一般比较好定位，麻烦的都是流畅度优化，一旦出了问题，找不准切入点会非常浪费团队时间。
- 安全方面。非对称加密体系和常用的对称加密算法，以及大大小小都会踩得坑都需要知道。**https的安全握手流程**是个很好的话题切入点。
- 网络方面。 tcp ip 协议要有一定的了解，tcp的三次握手和slow start 特性我都会问到。http协议要有非常全面的了解，包括常见的 header，body格式。
- 数据库方面。索引的功能，事务的盖面，多线程安全，死锁等都需要知道。
- 计算机基础方面。 基本功很重要，计算机基础直接和解决问题的能力相关，很多时候遇到问题都会去查各种资料，基础是否扎实会影响解决问题的思路。我一般会问到：
  - `操作系统的常见线程调度策略`         
  - `常用的缓存淘汰策略`
  - `binary search tree 和 hash table 访问元素的时间复杂度`，还有一些类似的就不一一列出来了
  
  以上6个方面游刃有余的话，就可以了解对方的期望了