---
title: Redis安装
date: 2016-12-01 22:04:25
tags:
- Redis

categories:
- Redis

---

# 首先安装gcc和tcl
``` shell
yum install gcc -y
yum install tcl -y
```

# 下载并解压Redis
``` shell
wget http://download.redis.io/releases/redis-3.2.5.tar.gz
tar xzf redis-3.2.5.tar.gz
cd redis-3.2.5
```

# 安装Redis
``` shell
make
make install
```

出现如下信息，表示安装成功
![](http://i1.piimg.com/567571/2d0147a115983a37.png)

# 启动redis-server
``` shell
./src/redis-server
```

![](http://i1.piimg.com/567571/37a63378312f3c01.png)

# 启动客户端
``` shell
./src/redis-cli
```

![](http://p1.bpimg.com/567571/4703b667101312dd.png)

# 如果没安装gcc和tcl，会出现报错
make: cc: Command not found make: *** [adlist.o] Error 127
...
You need tcl 8.5 or newer in order to run the Redis test
