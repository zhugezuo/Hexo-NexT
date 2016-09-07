---
title: 如何实现python2和python3的共存
date: 2016-09-06 14:04:25
tags:
- Python
categories:
- Python
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
``` shell
python -m pip install pip --upgrade
python2 -m pip install pip --upgrade
```
2. 删除python2\Scripts目录下的pip.exe，保留pip2.exe
3. 分别用pip和pip2命令管理两个版本的包
![](http://i4.buimg.com/567571/edc1ba4b105538a6.png)


# Linux环境
## python的共存
由于我使用的是CentOS，系统自带了python2，所以只要再安装python3就可以了.

1. 下载最新的python3源码
``` shell
wget https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tgz
```

2. 解压并进入文件夹
``` shell
tar -xzvf Python-3.5.2.tgz
```

3. 编译安装
``` shell
./configure --prefix=/usr/local/python3
make
make install
```
4. 新建连接
``` shell
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
```

5. 分别执行python和python3可以进入启动相应版本的python
![](http://i4.buimg.com/567571/faf440965cea57be.png)

## pip的共存
1. 建立pip3的软连接
```
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
```

2. 分别用pip和pip3命令管理两个版本的包
![](http://i4.buimg.com/567571/9b7a7544c7038b64.png)

