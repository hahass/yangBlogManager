---
title: JVM学习笔记-运行时数据区域
date: 2019-05-21 15:35:37
categories: 
    - JAVA_JVM
tags: 
    - JVM
---


&#160; &#160; &#160; &#160;​java虚拟机在运行java程序的时候，会将内存划分成不同的数据区域，每个区域负责不同的功能，通常分为：方法区、虚拟机栈、本地方法栈。接下来我们一一介绍这些概念。

![jvm_area.png](./jvm_area.png)


### 1.程序计数器

&#160; &#160; &#160; &#160;​程序计数器是一块非常小的内存，它是当前线程所执行的字节码的行号指示器。在虚拟机的概念里，字节码解释器是通过改变这个计数器的值来选取下一个需要执行的字节码指令， 分支、循环、异常处理、线程恢复都依赖这个程序计数器来完成。
&#160; &#160; &#160; &#160;java多线程执行是通过不停切换处理器来分别执行各个线程实现的，也就是同一时刻只有一个处理器只能执行一条线程，每个线程执行一段时间在执行其他的线程，所以每个线程都需要有自己独立的程序计数器，才能在处理器切回自己线程的时候，继续正确执行，所以**程序计时器是线程私有的**。
&#160; &#160; &#160; &#160;程序计数器是java虚拟机唯一一个没有OutOfMemoryError的区域。

### 2.java虚拟机栈

&#160; &#160; &#160; &#160;java虚拟机栈描述的是java方法执行的内存模型，每个方法执行的时候，会在创建一个栈帧，存储局部变量表、操作数栈、动态链接、方法出口等。同时栈是线程私有的，生命周期与线程相同。
&#160; &#160; &#160; &#160;局部变量表存放了编译器可知的各种基本数据类型（boolean，byte，char,short,int,float,long,double）、对象引用和returnAddress类型。
&#160; &#160; &#160; &#160;64位长度的long和double类型的数据会占用两个局部变量的空间，其余的数据类型都只占用1个空间。局部变量表需要的空间，在编译期间完成分配，当进入一个方法时，这个方法需要的在栈分配的大小是完全确定的在方法运行时，局部变量表的大小不会改变。
&#160; &#160; &#160; &#160;这个区域规定了两种异常状况：如果线程请求的栈深度大于虚拟机所允许的深度，会抛出StackOverFlowError异常。如果虚拟机栈可以动态扩展，如果扩展时无法申请到足够的内存，就会抛出OutOfMemoryError。



### 3.本地方法栈

&#160; &#160; &#160; &#160;本地方法栈与java虚拟机栈非常相似，虚拟机栈为java方法服务，而本地方法栈为Native方法服务。

### 4.java堆

&#160; &#160; &#160; &#160;堆是java虚拟机管理的最大的一块内存。在虚拟机启动的时候创建，并且是线程共享的。java堆主要用于存放对象实例。几乎所有的对象实例都在这里分配内存。
&#160; &#160; &#160; &#160;​java堆也是垃圾收集器主要处理的区域。很多时候也被叫做“GC堆”，从内存回收的角度来看，现在收集器基本都采用分代收集法，所有java堆可以细分为新生代和老年代，在细分一点就是Eden空间、From Survivor空间、To Survivor空间。
&#160; &#160; &#160; &#160;根据Java虚拟机规范的规定，Java堆可以处于物理上不连续的内存空间中，只要逻辑上是连续的即可，就像我们的磁盘空间一样。在实现时，既可以实现成固定大小的，也可以是可扩展的，不过当前主流的虚拟机都是按照可扩展来实现的（通过-Xmx和-Xms控制）。

&#160; &#160; &#160; &#160;如果在堆中没有内存完成实例分配，并且堆也无法再扩展时，将会抛出OutOfMemoryError异常。


### 5.方法区

&#160; &#160; &#160; &#160;方法区是线程共享的一块区域，用于存储已被虚拟机加载的类信息、常量、静态变量、及时编译器编译后的代码等数据。java虚拟机规范吧方法区描述为堆的一个逻辑部分，但是他也有一个别名Non-Heap(非堆)。目的与java堆分区开。
&#160; &#160; &#160; &#160;习惯HotSpot虚拟机的开发者，更愿意把方法区成为“永久代”，本质上两种不等价，仅仅因为HotSpot虚拟机的设计团队选择吧GC分代收集扩展到方法区。或者说永久代来实现方法区而已。这样HotSpot的垃圾收集器可以向管理java堆一样管理这部分内存，能够省去专门为方法区编写内存管理代码的工作。
&#160; &#160; &#160; &#160;java虚拟机堆方法区的限制非常宽松，不需要联系的内存和可以选择固定大小或者可扩展外，还可以选择不实现垃圾收集。相对而言，垃圾收集行为在这个区域比较少出现，但是并非数据进入了方法区就不收集了。这个区域内存回收的主要目标是针对常量池的回收和对类型的卸载。一般这个区域回收条件比较苛刻，但是回收还是有必要的。
&#160; &#160; &#160; &#160;当方法区无法申请到足够的内存的时候，也会抛出OutOfMemoryError异常。

### 6.运行时常量池

&#160; &#160; &#160; &#160; 方法区的一部分。Class文件除了有类的版本、字段、方法、接口等描述信息外，还有一项信息就是常量池，用于存放编译器生成的各种字面量和符号引用。这部分内容将在类加载后进入方法区的运行时常量池中存放。在常量池无法在申请到内存会抛出OutOfMemoryError。
&#160; &#160; &#160; &#160;运行时常量池有一个重要的特征-具备动态性。java语言不要求常量一定只有在编译器才能产生，运行期间也可以能将新的常量放在池中，这种特性被开发人员利用比较多的便是String类的intern()方法。


### 7.加课：OutOfMemoryError异常

- <font color='red'>堆</font>

java堆用于存储对象实例，只要不断创建对象，并且保证 GC Roots 到对象之间有可达路径，对象数量达到最大堆的容量限制就会产生内存溢出异常。

堆抛出 java.lang.OutOfMemoryError会进一步提示 java heap space.

要解决堆异常，一般需要通过内存映像分析工具对Dump处理的堆转储快照进行分析，重点是确定内存中对象是否是必要的，也就是要先分清楚到底是出现了内存泄漏还是内存溢出。

如果内存泄漏，通过工具查看泄漏对象到GC Roots的引用链。就能找到泄漏对象是通过怎样的路劲与GC Roots相关联并导致垃圾收集器无法自动回收他们的，掌握了泄漏对象的类型信息以及GC Roots引用链的信息，就能比较准确定位泄漏代码的位置。

如果不存在泄漏。检查虚拟机的堆参数与机器物料内存对比，是否还可以调大。代码上查看是否存在某些对象生命周期过长、持有状态时间过长的情况，尝试减少程序运行期间的内存消耗。

设置参数
```
-Xms设置堆的最小空间大小。

-Xmx设置堆的最大空间大小。

-XX:+HeapDumpOnOutOfMemoryError:出现内存溢出Dump出当前内存堆转储快照，以便事后分析
```


- <font color='red'>栈</font>

栈的容量通过 -Xss 参数设置，java虚拟机描述了两种异常：

+ 线程请求的栈深度大于虚拟机有允许的最大深度，抛出 StackOverflowError异常。
+ 虚拟机在扩展栈时无法申请到足够的内存空间，则会抛出OutOfMemoryError异常。












```
-Xms设置堆的最小空间大小。

-Xmx设置堆的最大空间大小。

-XX:NewSize设置新生代最小空间大小。

-XX:MaxNewSize设置新生代最大空间大小。

-XX:PermSize设置永久代最小空间大小。

-XX:MaxPermSize设置永久代最大空间大小。

-Xss设置每个线程的堆栈大小。
```
没有直接设置老年代的参数，但是可以设置堆空间大小和新生代空间大小两个参数来间接控制。

```
老年代空间大小=堆空间大小-年轻代大空间大小
```
