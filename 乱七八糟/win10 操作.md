---
title: win10 修改文件权限
date: 2019-08-16 15:49:32
tags: 
---

### win10 修改文件权限

更改自己为所有者

编辑：给自己写入的权限

### Windows10 添加快捷方式到开始菜单

1. 打开C:\Users\Yourname\AppData\Roaming\Microsoft\Windows\Start Menu
2. 将快捷方式拷贝到该文件夹下面。就可以在开始菜单中找到你所拷贝的快捷方式了。
   



## 关闭端口占用进程

```cmd
# 查找端口占用进程
netstat -ano|findstr "8080"

# 2.通过进程ID查找进程名
tasklist |findstr "15036"

# 3.杀死进程（指定进程ID或进程名）
taskkill /f /t /im 15036
```

#### 查看局域网内正在使用的ip

```cmd
for /L %i IN (1,1,254) DO ping -w 2 -n 1 10.6.211.%i
arp -a
```

