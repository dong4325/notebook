---
title: Linux-命令积累
date: 2019-08-16 15:48:08
tags: Linux
---

#### linux踢出其他正在ssh登陆用户

```shell
who
who am i		#查看当前自己占用终端，别把自己干掉了
pkill -kill -t pts/1	#pkill命令踢出对方
```

