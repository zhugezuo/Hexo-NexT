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



# [第7关](http://www.pythonchallenge.com/pc/def/oxygen.html)
可以看到图片中有一段灰度条，猜测需要用到图片处理模块。取图片的RGBA，发现灰度条（R=G=B）范围为：w:0-607,h:43-51，RGB数值7个一组，猜测为ASCII值，进行转化：

``` python
import urllib.request
import io
from PIL import Image
img = urllib.request.urlopen(
    'http://www.pythonchallenge.com/pc/def/oxygen.png').read()
im = Image.open(io.BytesIO(img))
w, h = 607, 50 		 # 取w:0-607,h=50的线段进行处理
print(''.join([chr(im.getpixel((i, h))[0]) for i in range(0, w, 7)]))
```

获得提示：“smart guy, you made it. the next level is [105, 110, 116, 101, 103, 114, 105, 116, 121]”，再次根据ASCII码转化为字符，得到下一关地址：http://www.pythonchallenge.com/pc/def/integrity.html


# [第8关]()
点击图上的蜜蜂发现要输入用户名和密码，查看网页源码发现下面有提示：

>un: 'BZh91AY...'
>pw: 'BZh91AY...'

看来是需要转换呀，怎么做呢？可以观察到两串字符都是以'BZh...'开头的，应该是bz2压缩后的结果，那么直接进行解压缩看看：

``` python
import bz2
un = b'BZh91AY...'
pw = b'BZh91AY...'
print(bz2.decompress(un),bz2.decompress(pw))
```

点击图中的蜜蜂，输入运行的结果，用户名：**huge**，密码：**file**


# [第9关](http://www.pythonchallenge.com/pc/return/good.html)
图中黑点描出这棵树的轮廓，又看到网页源码中给了两串数字，是什么意思呢？猜测应该是坐标，试着根据这两串坐标绘图：

``` python
from PIL import Image, ImageDraw
first = [146,399,163,...]
second = [156,141,165,...]
newIm = Image.new('L', (800,800))  #新建800*800的背景图
draw = ImageDraw.Draw(newIm)
draw.line(first, fill=255)
draw.line(second, fill=255)
newIm.show()
```

打印图像，是一头公牛（bull）
![](http://i2.buimg.com/567571/0cf2ad06cf30292d.jpg)
得到下一关地址：http://www.pythonchallenge.com/pc/return/bull.html

# [第10关](http://www.pythonchallenge.com/pc/return/bull.html)
图片下方写着“len(a[30]) = ?”，点击图中的公牛，获得提示“a = [1, 11, 21, 1211, 111221, ”看来是一道找规律的题目。仔细看，后一个数字是在描述前一个数字，比如第二项11表示前一项是1个1，第三项21表示前一项是2个1，第四项1211表示前一项是1个2加上1个1，依此类推。

``` python
import re
# 定义一个函数，先用正则表达式分割出相同的数字块，然后组成下一个数字
def describe(a):
    sets = re.findall("(1+|2+|3+|4+|5+|6+|7+|8+|9+|0+)", a)
    return "".join([str(len(x)) + x[0] for x in sets])
a = '1'
for i in range(30):
    a = describe(a)
print(len(a))
```

最后结果是5808，得到下一关地址：http://www.pythonchallenge.com/pc/return/5808.html