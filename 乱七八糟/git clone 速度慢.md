---
title: git clone 速度慢
date: 2019-08-16 08:26:00
tags: Git
---

### 思路：

git clone特别慢是因为github.global.ssl.fastly.net域名被限制了。
只要找到这个域名对应的ip地址，然后在hosts文件中加上ip–>域名的映射，刷新DNS缓存便可。

### 实施：

在网站 https://www.ipaddress.com/ 分别搜索：

```
github.global.ssl.fastly.net
github.com
```

得到ip:



1. 打开hosts文件

   - Windows上的hosts文件路径在`C:\Windows\System32\drivers\etc\hosts`
   - Linux的hosts文件路径在：`sudo vim /etc/hosts`

2. 在hosts文件末尾添加两行(对应上面查到的ip)

   ```
   151.101.185.194 github.global-ssl.fastly.net
   192.30.253.112 github.com
   ```

3. 保存更新DNS

   1. Winodws系统的做法：打开CMD，输入`ipconfig /flushdns`
   2. Linux的做法：在终端输入`sudo /etc/init.d/networking restart`



[原文连接](https://blog.csdn.net/shahuhu000/article/details/83965642)