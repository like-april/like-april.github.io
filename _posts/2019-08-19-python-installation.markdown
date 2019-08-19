---
layout:     post
title:      "Python 安装"
subtitle:   " \" python installation\""
date:       2019-08-19 18:01:00
author:     "张凡"
header-img: "https://aerozf.oss-cn-beijing.aliyuncs.com/images/anaconda_page.jpg"
catalog: true
tags:
    - python
    - 教程
---

# Python 安装

### 1、python是什么&为什么选择python？

- python是什么？

  ​	Python 是一种[面向对象](https://www.baidu.com/s?wd=面向对象&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)的解释型计算机程序设计语言，由荷兰人Guido van Rossum 于 1989 年发明，第一个公开发行版发行于 1991 年。Python 在设计上坚持了清晰划一的风格，这使得 Python 成为一门易读、易维护，并且被大量用户所欢迎的、用途广泛的语言。Python 具有丰富和强大的库。它常被昵称为胶水语言，能够把用其他语言制作的各种模块(尤其是 [C/C++](https://www.baidu.com/s?wd=C%2FC%2B%2B&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao))很轻松地联结在一起。

  

- 为什么选择python?

  ​	在学习编程语言之前我们或许听说过Python、C语言、C++、Java、Matlab、Go、Javascript、ruby、Lua等等很多种编程语言。那么我们（非程序员）为什么要选择Python呢？以我个人学习Python、C语言、Javascript和Matlab的经历来看，学习Python主要有以下优势：

  - Python简单易学。python的语言很简单、而且代码写出来很优美，逻辑层次分明。有C语言基础的话，每天学习两小时，一两周左右就可以学完基础内容。

  - 开发效率高。Python有大量的第三方库和模块，可以使用这些库和模块快速的完成开发。和Matlab做一个横向的比较，Matlab在系统建模与仿真、自动生成代码、数值计算方面Python不可匹敌，但是除了这些之外。Python的优势就十分明显了，Python就像一个巨大的宝库一样，可以做你能想到的任何事（例如桌面应用开发、游戏开发、人工智能、数值处理、图像识别、文件操作、网络开发、云计算等等），做一个形象的比喻：Matlab就像是一个专才，在建模与仿真、数值计算方面做的非常突出；Python就像是一个全才，什么都可以做，也都做的很好。

  - 免费、占用空间小。这是相对于Matlab而言的，Python由于是开源的，所以你可以免费的下载和使用，也可以查看和自主更改相关模块的代码（在Matlab那里想都别想）。在一个是占用空间很小，官方python只有不到100兆的空间占用。

  - 跨平台。你在任何一个系统上都可以安装和运行Python（Linux系统默认自带Python），这就会方便很多，在任何终端都可以写Python。而且通过jupyter notebook可以在浏览器上编写和运行Python代码。

  - 高级语言。当你用Python语言编写程序的时候，你无需考虑诸如如何管理你的程序使用的内存一类的底层细节，只需要把精力放在解决具体的问题上。举个例子，你在Python里面可以计算2的1000次方，但在其他语言里，你得考虑内存占用和是否溢出等烦人的细节。

    ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/python_power.png)

  - 胶水语言。python代码可以插在别的程序语言中运行，也可以在Python中运行别的程序语言

  - 学习资源多。当学习Python遇到什么问题时，在网上一搜就可以搜到很多优质的教程和学习资源。而Matlab遇到问题时，网上经常找不到教程或者合适的学习资源。

### 2、安装Python

​	Python的官网网址是<www.python.org>，进入官网就可以下载适合你电脑操作系统的官方Python软件。但是并不推荐这么做，前面我们说过Python的一大优势就是拥有大量的第三方库，但是官方的Python软件并不自带这些第三方库（仅有少量的官方库），所以实际使用中需要亲自一个一个的去下载第三方库，比较繁琐，而且对于一些库（例如matplotlib——库图库）安装会出现一堆问题，新手可能会不知所措（因为要补很多知识）。

​	推荐安装[Anaconda](https://www.anaconda.com/)，这是一个开源的Python版本，它自带了科学计算、数据处理等常用的第三方库，下载下来就能直接用。

##### 2.1 Python的版本

​	Python有两个大类的发型版本，Python2.x系列和Python3.x系列。Python2.x系列是Python的早期版本，现在仍然大量使用，但其渐渐被Python3.x系列代替。在这里我们选用Python3.x系列的Python3.6版本。

##### 2.2 Anaconda 下载

​	Anaconda的官网为<https://www.anaconda.com/>，但是由于其服务器在境外，下载速度很慢，所以我们选择Anaconda的清华镜像网站进行下载。python的版本我已经选择好了，直接点击[这里](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-4.3.1-Windows-x86_64.exe)下载就可以了（或者在浏览器输入网址<https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-4.3.1-Windows-x86_64.exe>）。

##### 2.3 Anaconda 安装

​	Anaconda 安装包下载好之后，双击就进入安装界面了。需要注意的地方有以下几个，其他的就一路点击下一步和确认就行了。

- 第一个需要注意的问题

  Anaconda的安装位置注意不要选择默认位置（也就是在C盘），请改到D盘或者E盘（如下图中所示）

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/anaconda1.png)

- 第二个需要注意的问题

  下图中两个红框内的小框请全部勾选

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/anaconda2.png)

最后点击上图中的Install 就可以了，等个大概十几分钟就安装好了。

##### 2.4  打开和使用 Anaconda中的Python

​	anaconda安装之后在桌面没有快捷方式，点击win10下面的搜索，输入**spyder**，点击打开，这个就是以后经常要用到的Python代码编辑界面。为了方便以后打开，可以选择固定到任务栏。

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/anaconda3.png)



或者在开始那里的应用列表里直接找，位置：**Anaconda > spyder**

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/anaconda4.png)



下图所示是anaconda的python编辑器spyder打开之后的界面，和Matlab的界面还是有几分相似的。

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/anaconda5.png)



以后写Python代码记得只打开**spyder**就行了（建议固定到任务栏，如下图所示）

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/anaconda6.png)



***至此，本教程完***
