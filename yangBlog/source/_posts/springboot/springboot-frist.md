---
title: 再学SpringBoot-搭建第一个springboot项目
date: 2019-05-29 16:59:41
categories: 
    - SpringBoot
tags: 
    - SpringBoot
---
springboot 已经使用了两年，但是对springboot没有系统的学习过，所以打算系统的学习一下Springboot。以较为学，应该是最有效的学习方法，所以通过边学边写教程的方式，来学习。


## 环境

- jdk:1.8
- springboot:2.0.1
- 开发工具：idea
- 构建工具：maven

## 项目搭建

springboot为开发者提供了模板，所以开发者可以通过网站直接创建一个springboot项目。这里我通过idea直接创建第一个springboot项目

### 1 步骤

点击File -> new - project，选择Spring Initializr。
![springboot1.png](./springboot1.png)
输入信息
![springboot2.png](./springboot2.png)
在这里我们可以选择需要的jar包，创建时会自动为我们引入，不在需要自己手动去添加。同时可以选择springboot的版本。
![springboot3.png](./springboot3.png)
选择路径，创建完成。
![springboot3.png](./springboot3.png)


### 2.目录结构

```
- src
    -main
        -java
            -package
                #主函数，启动类，运行它如果运行了 Tomcat、Jetty、Undertow 等容器
                -SpringbootApplication	
        -resouces
            #存放静态资源 js/css/images 等
            - statics
            #存放 html 模板文件
            - templates
            #主要的配置文件，SpringBoot启动时候会自动加载application.yml/application.properties		
            - application.yml
    #测试文件存放目录		
    -test
 # pom.xml 文件是Maven构建的基础，里面包含了我们所依赖JAR和Plugin的信息
- pom
```