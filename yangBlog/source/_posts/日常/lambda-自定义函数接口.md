---
title: lambda-自定义函数接口
date: 2020-11-12 17:12:49
categories: 
    - 日常
tags: 
    - lambda
---



## 自定义函数式编程

编写一个只有一个抽象方法的接口类，使用 @FunctionalInterface 修饰。@FunctionalInterface是可选的，但加上该标注编译器会帮你检查接口是否符合函数接口规范

``` java
@FunctionalInterface
public interface AddInterface {
    int add(Integer a, Integer b);
}
```

那么我们就可以在代码中直接使用了

```java
    AddInterface addInterface = (a,b) -> a-b;
```



## lambda表达式的使用

### 1.无参

```java
Thread thread = new Thread(() -> System.out.println("执行线程方法"));
```

### 2.有参数

上面自定义的接口就是有两个参数的接口

```java
   AddInterface addInterface = (a,b) -> a-b;
```


### lambda表达式

使用lambda表达式时，java在进行编译的使用，不会像匿名内部类那样生成新的类文件，而是作为主类的私用方法