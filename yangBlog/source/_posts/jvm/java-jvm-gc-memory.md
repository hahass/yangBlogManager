---
title: java内存分配与回收策略
date: 2019-05-28 15:43:05
categories: 
    - JAVA_JVM
tags: 
    - JVM
---

大多数的情况下，对象在新生代Eden区中分配。当Eden没有足够的空间进行分配时，虚拟机会触发一次Minor GC。

大对象是指需要大量连续内存空间的java对象，最典型的大对象是那种很长的字符串以及数组。

-XX:pretenureSizeThreshold参数，令大于设置值的对象直接分配到老年代中，从而避免对象在Eden区与Survivor区之间发生大量复制。


虚拟机通常采用分代收集的思想来管理内存。虚拟机为每个对象定义了一个对象年龄计数器，如果对象在Eden区经过了一次Minor GC 还存活， 那么该对象会进入Survivor中，并且age设置为1。每经过一次Minor GC age都会加1，直到达到一定程度（默认是15岁），会进入到老年代。年龄阈值通过参数-XX:MaxTenuringThreshold设置。

为了更好的适应不同程序的内存状况，虚拟机并不是永远的要求对象的年龄必须达到了参数才能晋升到老年代，如果在Survivor空间中相同年龄所有对象大小的总和大于Survivor空间的1半，年龄大于或者等于改年龄的对象接可以直接进入老年代，不用等到MaxTenuringThreshold中的年龄要求。

<font color= "red">注：</font>
```
Minor GC(新生代GC)：指发生在新生代的垃圾收集动作，触发频率频繁，回收速度也比较快。

Major GC/Full GC(老年代GC)：指发生在老年代的GC，出现Major GC，经常伴随至少一次的Minor GC。
```