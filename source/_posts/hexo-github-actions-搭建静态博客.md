---
title: 对喜欢的hexo主题进行定制化改造
date: 2024-06-16 16:31:21
tags:
categories:
- code
---

>    *注意本文适合对于hexo以及基本的前端知识有一定了解的同学*



### 背景

看到凡凡的博客写的很好，自己也燃起了写博客的欲望，于是开始思考搭建博客平台的方案。

1.   方案一 前后端分离全都自己写
     优点：做web网站也算是自己老本行，博客的每一行代码都是出自自己手下，是很有成就感的一件事情

     缺点：成本高，需要投入时间，需要云服务器。

2.   方案二 使用hexo 搭建静态网站

     优点：使用现有方案，不自己造轮子，节约人力成本，静态网站可以用Github Pages进行托管，节约资金成本

     缺点：成就感会低一点。

最后考虑到我的目的是写博客而不是写博客网站，因此选择了成本较低的第二种方案。



### 1. 选择喜欢博客主题

原本是想前端界面全部自己设计的，但是结果看到[cactus](https://github.com/probberechts/hexo-theme-cactus) 这个主题后感觉这跟我想要设计的差不多，于是我就选择了[cactus](https://github.com/probberechts/hexo-theme-cactus) 这个主题



### 2. 定制化改造

#### 2.1 效果预览

点击 [cactus界面预览](https://probberechts.github.io/hexo-theme-cactus/cactus-dark/public/), 即可看到原界面，很简洁好看，上边的四个nav分别是 home, about, writing和projects，很符合一个常规的hexo博客的nav。

但是我不太想要这样分，我想要有五个栏目

1.   自我介绍（首页）
2.   技术博客
3.   平时的思考
4.   长短期规划
5.   有趣的事情

这个样子分的话会简单许多，另外我想要每个栏目都用icon表示而不是文字最后效果如下。

<img src="https://raw.githubusercontent.com/akaakking/pic/master/image-20240617130844517.png" alt="image-20240617130844517" style="zoom:50%;" />

可以看到改造下来其实并没有官方的那么好看，不过也可以看的过去。

#### 2.2 主题代码目录层级结构介绍

下边是这个主题的目录层级结构

其中languages中主要放国际化相关代码，就是让网站支持多种国家语言，这个我们不关注。

scripts中主要放一些简单的脚本代码，在构建博客（hexo g）的的时候会加载



![image-20240617141941366](https://raw.githubusercontent.com/akaakking/pic/master/image-20240617141941366.png)

我们主要关注layout目录中的代码，layout目录中的一个个ejs文件可以看作是网页的模板，根据模板会生成一个个网页（不熟悉ejs的可以熟悉一下ejs

最核心的是layout.ejs，这个模板可以看作模板的顶层设计，所有其他类的模板都由他引入，具体的引入逻辑可以看一下代码。



介绍完目录结构后，我们其实就可以上手改造了

#### 2.3 改造

首先明确需求

1.   将 nav 栏文字变为icon
2.   将 nav 栏链接到五个栏目（见上）而不是原有的home,about,writing,projects

改造代码如下

1.   将nav栏文字变为icon

     首先找到nav栏对应的模板代码 header.ejs（左边是改造前的右边是改造后的）

     ![image-20240617221329255](https://raw.githubusercontent.com/akaakking/pic/master/image-20240617221329255.png)

     原本是从theme.nav中拿到配置的文字在显示出来，改造后就是拿到配置的图片的path在这里显示出来，这样就达到了显示icon的目的。

     这是改造前后的theme的配置的对比

     ![image-20240617221817968](https://raw.githubusercontent.com/akaakking/pic/master/image-20240617221817968.png)

     

     2.将 nav 栏链接到五个栏目而不是原有的home,about,writing,project)

     见前述改造模板代码可知我们其实只是改变了a标签的href属性。

这样经过小小的改造就达到了我们的目的。

### 3. 使用github action 将网站部署在github pages上

 见 https://hexo.io/zh-cn/docs/github-pages



### 参考

待补充
