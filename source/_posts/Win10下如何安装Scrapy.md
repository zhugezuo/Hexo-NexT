---
title: Win10下如何安装Scrapy
date: 2016-09-07 22:04:25
tags:
- Python
- Scrapy
categories:
- Python
- Scrapy
---
# 安装介绍
Windows下部署Scrapy比较麻烦，需要装很多依赖包，Scrapy目前只支持到Python27，我的操作系统是Windows10，64位，下面就来详细介绍一下如何在WIN10下安装Scrapy
# 安装依赖包
Windows下，安装Scrapy前需要先安装以下依赖包：
- *lxml:* [下载地址](https://pypi.python.org/pypi/lxml/3.6.0)
根据操作系统选择[lxml-3.6.0.win-amd64-py2.7.exe](https://pypi.python.org/packages/be/80/1d8839496d83ef5e90d63af215730785b8b8ce00d43c64960662adb92ecc/lxml-3.6.0.win-amd64-py2.7.exe#md5=ff6fc39c647241afe7f31490c5b7a61c)
- *pywin32:* [下载地址](https://sourceforge.net/projects/pywin32/files/pywin32/Build%20220)
根据操作系统选择[pywin32-220.win-amd64-py2.7.exe](http://downloads.sourceforge.net/project/pywin32/pywin32/Build%20220/pywin32-220.win-amd64-py2.7.exe?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fpywin32%2Ffiles%2Fpywin32%2FBuild%2520220%2F&ts=1473259515&use_mirror=nchc)
- *Twisted:* [下载地址](https://twistedmatrix.com/Releases/Twisted/15.4/)
根据操作系统选择[Twisted-15.4.0.win-amd64-py2.7.exe](https://twistedmatrix.com/Releases/Twisted/15.4/Twisted-15.4.0.win-amd64-py2.7.exe)

下面的*pyOpenSSL*和*zope.interface*是*Twisted*的依赖包，可以自动安装，如果失败，再手动下载安装
- *pyOpenSSL:* [下载地址](https://pypi.python.org/pypi/pyOpenSSL/0.13.1)
根据操作系统选择[pyOpenSSL-0.13.1.win-amd64-py2.7.exe](https://pypi.python.org/packages/a9/3f/65276ba1b19cbd678a3f3876cd7fa739fd9fd23e2f87f08668e701b9cb60/pyOpenSSL-0.13.1.win-amd64-py2.7.exe#md5=223cc4ab7439818ccaf1bf7f51736dc8)
- *zope.interface:* [下载地址](https://pypi.python.org/pypi/zope.interface/4.3.2)
根据操作系统选择[zope.interface-4.3.2.win-amd64-py2.7.exe](https://pypi.python.org/packages/d7/54/3e2c6ed5eee78d0929edb8982188632d75e1b09d3cc19395f04d26ef5da6/zope.interface-4.3.2.win-amd64-py2.7.exe#md5=9c4c19d72a3f8857c223e60dbc32c301)

# 安装Scrapy
执行命令
``` shell
pip install Scrapy
```

# 查看
执行命令
``` shell
scrapy version
```
能够看到Scrapy版本就表示安装完成了
![](http://i2.buimg.com/567571/d1b2d00b3d6fdf46.png)