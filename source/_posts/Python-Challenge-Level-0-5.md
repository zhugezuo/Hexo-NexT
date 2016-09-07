---
title: Python Challenge (Level 0-5)
date: 2016-09-04 09:19:11
tags:
- Python
- Python Challenge
categories:
- Python
- Python Challenge
---
# 简介
Python Challenge是一个过关式的解谜站点，使用的是经典在线解谜站点Not Pr0n的模式：根据提示找出下一关的网页地址。和Not Pr0n不同的是，在每一关里你都需要编写程序来寻找答案。虽然这个解谜站点的名字叫做Python Challenge，但事实上你可以使用任意一种程序语言（除了少数一两关可能会用到点Python的知识），目前总共有33关。
**挑战地址:** [Python Challenge](http://www.pythonchallenge.com/)
<!-- more -->


# [第0关](http://www.pythonchallenge.com/pc/def/0.html)
图片上面写着2<sup>38</sup>，用python可以轻松求解，结果为：274877906944。替换掉地址栏的0，得到下一关地址:
http://www.pythonchallenge.com/pc/def/274877906944.html


# [第1关](http://www.pythonchallenge.com/pc/def/274877906944.html)
从图中的**K->M**,**O->Q**,**E->G** 容易看出，把字母往后加二得到相应的字母，Y和Z应该是分别对应A和B。接下来对网页下方的字符串进行处理：

``` python
import string
text = "# 省略字符串"
table = text.maketrans(string.ascii_lowercase,string.ascii_lowercase[2:]+string.ascii_lowercase[:2])
print(text.translate(table))
```

在上面的代码中，我们用到了maketrans()方法创建字符映射的转换表，对字符串进行处理，maketrans()方法语法：

``` python
str.maketrans(intab, outtab)
```

**intab** -- 字符串中要替代的字符组成的字符串。
**outtab** -- 相应的映射字符的字符串。
上述代码的打印结果为“i hope you didnt translate it by hand. thats what computers are for. doing it in by hand is inefficient and that's why this text is so long. using string.maketrans() is recommended. now apply on the url.”
再对地址栏中的"map"进行转换，得到下一关地址：http://www.pythonchallenge.com/pc/def/ocr.html


# [第2关](http://www.pythonchallenge.com/pc/def/ocr.html)
题目提示“MAYBE they are in the page source”。那么我们右键查看网页源码，注释中指出“find rare characters in the mess below”，让我们找出出现次数较少的字符，那就直接数出每个字符的出现次数并排序：

``` python
str = """
# 省略字符串
"""
s = set(str)
d = {}
for i in s:
    d[i]=str.count(i)
print(sorted(d.items(), key=lambda x:x[1]))
```

可以看出出现次数最少的字母为q,t,a,y,e,i,u,l，正好可以拼出单词“equality”，得到下一关地址：http://www.pythonchallenge.com/pc/def/equality.html


# [第3关](http://www.pythonchallenge.com/pc/def/equality.html)
题目强调了“EXACTLY”，一个小写字母被**正好**三个大写字母包围，不能多也不能少，依旧是查看网页源码获得字符串，可以用正则表达式进行匹配：

``` python
import re
text = """
# 省略字符串
"""
print("".join(re.findall('[^A-Z][A-Z]{3}([a-z])[A-Z]{3}[^A-Z]', text)))
```

这里用到了正则表达式，可以在[菜鸟教程](http://www.runoob.com/python/python-reg-expressions.html)学习
执行结果为：linkedlist，得到下一关地址：http://www.pythonchallenge.com/pc/def/linkedlist.html



# [第4关](http://www.pythonchallenge.com/pc/def/linkedlist.html)
将网址上的".html"改为".php"，点击图片得到提示“and the next nothing is 44827”，将网址中的"12345"替换为“44827”，很明显，是让你一路替换下去。什么时候停止呢？源码中提示“400 times is more than enough”。

``` python
from urllib import request
import re
num = 12345
for i in range(400):
    u = request.urlopen('http://www.pythonchallenge.com/pc/def/linkedlist.php?nothing=%s'% num)
    text = u.read().decode('utf8')
    try:
        num = re.search('and the next nothing is ([0-9]*)',text).group(1)
    except:
        print(text)
        break
    print(num)
```

执行得到数字“16044”，页面上提示“Yes. Divide by two and keep going”，将上面的"12345"替换为"8022"继续执行，得到下一关地址：http://www.pythonchallenge.com/pc/def/peak.html
**注意：**我使用的是python3，如果是python2，用法略有不同，具体请自行搜索



# [第5关](http://www.pythonchallenge.com/pc/def/peak.html)
提示："pronounce it"，“peak hell”读音像什么呢？像python自带的模块pickle，那么就用pickle处理[banner.p](http://www.pythonchallenge.com/pc/def/banner.p)。

``` python
import pickle
text = """
# 省略字符串
"""
data = pickle.loads(text.encode('utf8'))
for line in data:
    print(''.join(map(lambda x: x[0] * x[1], line)))
```

先用pickle模块获取到列表[[(' ', 95)], [(' ', 14), ('#', 5), ···]，很明显数字表示前面字母的重复次数，按照该列表进行绘图如下：
![](http://i2.buimg.com/567571/c23a3e912ec342fb.png)
拼出了单词“channel”，得到下一关地址：http://www.pythonchallenge.com/pc/def/channel.html