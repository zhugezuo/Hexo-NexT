---
title: Python Challenge (Level 6-10)
date: 2016-09-04 20:18:24
tags:
- Python Challenge
- python
categories:
- Python Challenge
---
# [第6关](http://www.pythonchallenge.com/pc/def/channel.html)
查看网页源码获得提示“zip”，试着替换网址中的“html”，发现果然可以下载。下载后打开里面的readme.txt，获得两个提示：
 - hint1: start from 90052
 - hint2: answer is inside the zip
<!-- more -->

打开90052.txt获得下个提示“Next nothing is 94191”，和第4关一样的方法继续找下去，得到结果“Collect the comments.”。根据这个提示，依次获得文件的comment()属性并打印:
``` python
import re,zipfile
z = zipfile.ZipFile('channel.zip', 'r')
num = 90052
c = z.getinfo('%s.txt' % num).comment.decode('utf8')
for i in range(1000):
    text = z.read('%s.txt' % num).decode('utf8')
    try:
        num = re.search('Next nothing is ([0-9]*)',text).group(1)
    except:
        break
    c = z.getinfo('%s.txt' % num).comment.decode('utf8')
    print(c, end='')
```
打印结果：
![](http://i2.buimg.com/567571/ce2ab8aee019488b.png)
老方法，网址中的“channel”替换为“hockey”，得到提示“it's in the air. look at the letters.”，注意组成字母“HOCKEY”的小字母分别为O,X,Y,G,E,N，坑爹呢这是！不愧是解谜网站，哈哈。最终，得到下一关地址：http://www.pythonchallenge.com/pc/def/oxygen.html
 <br /> 
# [第7关](http://www.pythonchallenge.com/pc/def/oxygen.html)

# [第8关]()

# [第9关]()

# [第10关]()