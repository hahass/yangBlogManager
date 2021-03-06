---
title: 垃圾收集算法
date: 2019-05-27 13:40:32
categories: 
    - JAVA_JVM
tags: 
    - JVM
---

### 1.标记-清除算法

标记-清除算法是最基础的收集算法。主要分为两步：标记，清除。首先标记处需要回收的对象，标记完成后统一回收被标记的对象。

<font color='red'>缺点</font>
- 效率问题：标记和清除效率都不高
- 空间问题：标记清除后会产生大量不连续的内存碎片。如果程序在运行时需要分配较大的对象，无法找到足够大的内存就不能不提前触发另一次垃圾收集动作。

![biaojiqingchu1.png](biaojiqingchu1.png)

![biaojiqingchu2.png](biaojiqingchu2.png)

### 2.复制算法

复制算法可以更好的解决效率的问题。它将内存分为两块同等大小的区域。每次只回收其中一块区域。当垃圾回收器开始回收时，会将使用的一块内存中还存活的对象复制到另一块内存，然后一次清空这块使用的内存，每次都是对整个半区进行内存回收，内存分配不用考虑内存碎片的问题，只要一动堆顶的指针，按顺序分配内存即可，简单，高效。

现在商业虚拟机都采用这种收集算法来回收新生代。通常将内存分为一块较大的Eden空间和两块比较小的Survivor空间，每次使用Eden和其中的一块Survivor，回收时，将Eden和Survivor中还存活的对象一次性复制到另一块Survivor空间上，最后清理掉Eden和刚才用到的Survivor空间。HotSpot默认Eden和Survivor比例是8:1，也就是每次新生代中可用空间为整个新生代容量的90%，只有10%的内存会被浪费。当Survivor空间不足时，需要依赖其他内存（老年代）进行分担担保。

![fuzhi1.png](fuzhi1.png)

![fuzhi2.png](fuzhi2.png)


### 3.标记-整理算法

标记-整理算法，标记的过程和标记-清除算法一下，后续步骤不是直接回收对象，而是让所有存活的对象都向一端一动，然后直接清除掉端边界以外的内存。

![biaojizhengli.png](biaojizhengli.png)

![biaojizhengli1.png](biaojizhengli1.png)

### 4.分代收集算法

当前商业虚拟机的垃圾收集都采用分代收集算法，根据对象存活周期的不同将内存分为几块，java堆分为新生代和老年代，这样根据各个年代的特点采用适当的收集算法。新生代中每次都会有大量的对象死去，是有少量的存活，就选用复制算法。老年代中因为对象存活率高，没有额外的空间进行分配担保，就需要使用标记-清理或者标记整理算法进行回收。
