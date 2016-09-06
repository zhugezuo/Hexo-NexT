---
title: 如何实现python2和python3的共存
date: 2016-09-06 14:04:25
tags:
- Python
categories:
- python
---
大家都知道，目前python有2.x版本和3.x版本，python3相比python2有很大的改进，很多人都会选择python3入门，但是由于很多环境自带的都是python2，而且很多库也只支持python2，所以我们经常会在python2和python3上跑不同的程序。下面就来介绍如何在同一台电脑上安装python2和python3，并且相互独立。
<!-- more -->
# Windows环境
## python的共存
1. 首先去[官网](https://www.python.org/downloads/)下载并安装python2和python3。
2. 将两个安装路径以及路径下的Scripts目录都添加进环境变量PATH中：

> ;C:\Python\Python3\Scripts\;C:\Python\Python3\;C:\Python\Python2\Scripts\;C:\Python\Python2\

3. 将Python2目录下的python.exe修改为python2.exe
4. 分别执行python和python2即可启动相应版本的python
![](http://i1.piimg.com/567571/ab25d1f04ce48a1f.png)

## pip的共存
pip是python的包管理工具，两个python版本需要有相应的pip，安装好python之后，由于修改了exe的文件名，执行pip时会报错
> Fatal error in launcher: Unable to create process using '"'

修复方法：
1. 分别执行以下命令
```
python -m pip install pip --upgrade
python2 -m pip install pip --upgrade
```
2. 删除python2\Scripts目录下的pip.exe，保留pip2.exe
3. 分别用pip和pip2命令管理两个版本的包
![](http://i4.buimg.com/567571/edc1ba4b105538a6.png)


# Linux环境

