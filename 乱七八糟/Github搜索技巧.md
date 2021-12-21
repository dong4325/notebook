---
title: Github搜索技巧
date: 2019-08-16 15:47:30
tags: Git
---

## Git 积累

github搜索技巧

```
//匹配开发语言为Objective-C，star数大于0的
language:Objective-C stars:>0

//匹配用户填写的地址在china的开发者
location:china

//匹配拥有超过一千名关注者的开发者
followers:>=1000

//匹配用户实名为jack的开发者
in:fullname
```

### Trending

瞎逛逛，开开眼界

[官方文档](https://help.github.com/en/articles/about-searching-on-github)



### git 速度慢

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