---
title: java 性能监控与故障处理工具
date: 2019-05-28 17:44:35
categories: 
    - JAVA_JVM
tags: 
    - JVM
---

## 1.JDK命令工具

名称|主要作用
:-|:-
jps|JVM Process Status Tool,显示指定系统内所有的HotSpot虚拟机进程
jstat|JVM Statistics Monitoring Tool,用于收集HotSpot虚拟机各方面的运行数据
jinfo|Configuration Info For Java ,显示虚拟机配置信息
jmap|Memory Map For Java,生成虚拟机的内存转储快照
jhat|JVM Heap Dump Browser,用于分析heapdump文件，它会建立一个Http/HTML服务器，让用户可以在浏览器上查看分析结果
jstack|Stack Trace For Java 显示虚拟机的线程快照

### 1.1 jps:虚拟机进程状态工具
jps列出正在运行的虚拟机进行，并显示虚拟机执行主类名称以及这些进程的本地虚拟机唯一ID。

jps命令:
```
jps [option] [hostid]
```

jps执行样例:
![jps.png](./jps.png)

选项|作用
:-|:-
-q|只输出LVMID，省略主类的名称
-m|输出虚拟机进程启动是传递给主类main()函数的参数
-l|输出主类的全名，如果进程执行的是jar包，输出jar路径
-v|输出虚拟机进程启动时JVM参数

### 1.2 jstat:虚拟机统计信息监视工具

jstat监视虚拟机各种运行状态信息的命令行工具。可以显示本地或者远程虚拟机进程中的类装载、内存、垃圾收集、JIT编译等运行数据。

jstat命令格式
```
jstat [option vmid [interval[s|ms][count]]]
```
vmid:
本地：与本地VMID一致。
远程：格式如下
[protocol:][//]lvmid[@hostname[:port]/servername]

interval:查询间隔。
count：次数。

如果省略两个参数，说明只查询一次。

```
每250秒查询一次进行2777垃圾收集状况，一次查询20次
jstat -gc 2777 250 20
```

option:查询虚拟机信息，分为3类：类装载、垃圾收集、运行编译状况

选项|作用
-|-
-class|监视类装载。卸载数量、总空间以及类装载所消耗的时间
-gc|监视java堆状况，包括Eden区、两个Survivor区、老年代、永久代等容量、已用空间、GC时间合计等信息
-gccapacity|监视内容与-gc基本相同，但是输出主要关注java堆各个区域使用的最大、最小空间
-gcutil|监视内容与-gc基本相同，但是输出主要关注已使用的空间占总空间的百分比
-gccause|与-gcutil功能一样，但是会额外输出导致上一次GC产生的原因
-gcnew|监视新生代GC状况
-gcnewcapacity|监视内容与-gcnew基本相同，输出主要关注使用到的最大、最小空间
-gcold|监视老年代GC状况
-gcoldcapacity|监视内容与-gcold相同，输出主要关注使用到的最大、最小空间
-gcpermcapacity|输出永久代使用到的最大、最小空间
-compiler|输出JIT编译器编译过的方法和耗时等信息
-printcompilation|输出已近被JIT编译方法


### 1.3 jinfo:java配置信息工具

jinfo的作用是实时的查看和调整虚拟机各项参数

jinfo命令
```
jinfo [option] pid
```

### 1.4 jmap:java内存印象工具

jmap用于生成堆转储快照（heapdump/dump文件）。还可以查询finalize执行队列、java堆和永久代的详细信息，如空间使用率、当前用的哪种收集器等。

jmap命令
```
jmap [option] vmid
```
选项|作用
-|-
-dump|生成java堆转储快照，格式为-dump:[live,]format=b,file=<filename\>,其中live子参数说明是否只dump出存活的对象
-finalizerinfo|显示在F-Queue中等待Finalizer线程执行finalize方法的对象。只在Linux/Solaris平台下有效
-heap|显示java堆详细信息，如使用哪种回收器、参数配置、分代状况等。只在Linux/Solaris平台下有效
-histo|显示堆中对象统计信息，包括类、实例数量、合计容量
-permstat|以ClassLoader为统计口径显示永久代内存状态。只在Linux/Solaris平台下有效
-F|当虚拟机进程堆-dump选项没有响应时，可以使用这个选项强制生成dump快照。只在Linux/Solaris
平台下有效

### 1.5 jhat:虚拟机堆转储快照分析工具

jhat用于生成虚拟机当前时刻快照。线程快照是当前虚拟机内每一条线程正在执行的方法堆栈的集合，生成线程快照的主要目的是定位线程出现长时间停顿的原因，如线程间死锁、死循环、请求外部资源导致的长时间等。

jstack命令
```
jstack [option] vmid
```

选项|作用
-|-
-F|当正常输出的请求不被响应时，强制输出线程堆栈
-l|除堆栈外，显示关于锁的附加信息
-m|如果调用本地方法的话，可以显示c/c++的堆栈