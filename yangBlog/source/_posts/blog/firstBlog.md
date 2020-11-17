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

{% asset_img nodejs.png [nodejs.png] %}


安装过程 我就忽略了哈， 这个不会 就真的小白了，哈哈（其实是作者懒的在操作一遍   :laughing: ， 有空补上）

### 2.安装 git

因为需要将我们的静态网站，部署到github上， 所有需要现在本地安装git.

### 3.下载并安装hexo


### 4.创建博客目录

新建一个目录，执行下面命令

```
hexo init blog
```
执行完之后，会自动创建一个hexo目录


从[hexo](https://hexo.io/themes/) 选择自己喜欢的主体，下载到本地。放在\themes目录下。

### 5.修改配置文件根目录下的 _config.yml

1. 使用自己下载的主题

```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: ayer
```

2. 在github或者码云上新建一个仓库，仓库名需要和用户名相同

```
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: https://gitee.com/xxx/xxxx.git
  branch: master
```

### 6.安装插件



在博客根目录下安装部署插件
```
npm install hexo-deployer-git --save
```


### 4.常用操作

- 创建新的文章
```
hexo n "firstBlog"
```
    会在_posts文件加下创建出一个文件夹（存储文章中图片），和一个md文件,使用下面代码可以引入图片
```
 ![newfirstBlog.png](newfirstBlog.png)
```
![newfirstBlog.png](newfirstBlog.png)



部署命令

hexo clean # 清除已生成文件及缓存
hexo generate # 生成静态页面，简写做hexo g
hexo server # 启动本地WEB服务器，简写做hexo s

hexo clean "&&" hexo deploy 

hexo clean "&&" hexo generate "&&" hexo deploy 


## 访问地址

```
https://hhass.gitee.io
```





