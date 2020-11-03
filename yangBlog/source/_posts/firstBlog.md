---
title: 搭建个人博客
date: 2019-05-17 13:54:09
categories: 
    - 记录
tags: 
    - 博客
---

第一次搭建自己的博客，所以想要记录下，搭建的完整过程，方便想要搭建的小白少走弯路。


## 所需材料

- 博客的框架使用的是 hexo
- hexo 需要依托在 node.js ，所以需要先安装nodejs
- GitHubPage: 网站在gitHub上托管
- git 



## 步骤

### 1.安装node.js

打开官网：https://nodejs.org/en/ , 下载稳定版本的进行安装。

![nodejs.png](./nodejs.png)

安装过程 我就忽略了哈， 这个不会 就真的小白了，哈哈（其实是作者懒的在操作一遍   :laughing: ， 有空补上）

### 2.安装 git

因为需要将我们的静态网站，部署到github上， 所有需要现在本地安装git.

### 3.下载hexo

现在本地建立一个文件夹，进入文件夹，右键选择 Git bash here



### 4.常用操作

- 创建新的文章
```
hexo n "firstBlog"
```
    会在_posts文件加下创建出一个文件夹（存储文章中图片），和一个md文件,使用下面代码可以引入图片
```
 ![newfirstBlog.png](./newfirstBlog.png)
```
![newfirstBlog.png](./newfirstBlog.png)


