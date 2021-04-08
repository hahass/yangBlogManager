---
title: java-jvm-命令的使用
date: 2020-11-26 11:23:33
categories: 
    - JAVA_JVM
tags: 
    - JVM
---

# jps

jps是JavaVirtual Machine Process Status Tool的缩写，是java提供的查看进程的命令

```
命令格式：jps [options ] [ hostid ] 

[options]选项 ：
-q：仅输出VM标识符，不包括classname,jar name,arguments in main method 
-m：输出main method的参数 
-l：输出完全的包名，应用主类名，jar的完全路径名 
-v：输出jvm参数 
-V：输出通过flag文件传递到JVM中的参数(.hotspotrc文件或-XX:Flags=所指定的文件 
-Joption：传递参数到vm,例如:-J-Xms512m

[hostid]：
[protocol:][[//]hostname][:port][/servername]
命令的输出格式 ：
lvmid [ [ classname| JARfilename | "Unknown"] [ arg* ] [ jvmarg* ] ]

```

## 1. jps

{% asset_img jps1.png [jps1.png] %}

## 2. jps -q :仅仅显示java进程号

{% asset_img jps2.png [jps2.png] %}

## 3. jps -l :输出主类或者jar的完全路径名

{% asset_img jps3.png [jps3.png] %}


# jstat

jstat -gc PID :查看java进程的内存和GC情况

{% asset_img stat1.png [stat1.png]%}

jstat -gccapacity PID 堆内存分析

jstat -gcnew PID 年轻代GC分析

jstat -gcnewcapacity PID 年轻代内存分析

jstat -gcold PID 老年代GC分析

jstat -gcoldcapacity PID 老年代内存分析

jstat -gcmetacapacity PID 元数据内存分析



