---
title: 05_linux环境安装redis
date: 2021-08-04 18:04:49
tags: [黑马程序员, redis]
---

## Redis 安装

### 基于Linux环境安装Redis



#### 基于Center OS7安装Redis

- 下载安装包 

  ​	wget http://download.redis.io/releases/redis-?.?.?.tar.gz

- 解压 

  ​	tar –xvf 文件名.tar.gz

- 编译 

  ​	make

- 安装 (直接进入解压目录下运行 make install就行)

  ​	make install [destdir=/目录]

#### Redis基础环境设置

- 创建软链接 

  ​	ln -s 原始目录名 快速访问目录名

- 创建配置文件管理目录 

  ​	mkdir conf 

  ​	mkdir config

- 创建数据文件管理目录 

  ​	mkdir data

#### Redis服务启动

- 默认配置启动 

  ​	redis-server 

  ​	redis-server –-port 6379 

  ​	redis-server –-port 6380 ……

- 指定配置文件启动 

  ​	redis-server redis.conf 

  ​	redis-server redis-6379.conf 

  ​	redis-server redis-6380.conf …… 

  ​	redis-server conf/redis-6379.conf 

  ​	redis-server config/redis-6380.conf ……

#### Redis客户端连接

- 默认连接 

  ​	redis-cli

- 连接指定服务器 

  ​	redis-cli -h 127.0.0.1

  ​	redis-cli –port 6379 

  ​	redis-cli -p 6379
  
  ​	redis-cli -h 127.0.0.1 –port 6379

#### Redis服务端配置

- 基本配置 
  - `daemonize yes `
  - 以守护进程方式启动，使用本启动方式，redis将以服务的形式存在，日志将不再打印到命令窗口中 
  - `port 6*** `
  - 设定当前服务启动端口号 
  - `dir “/自定义目录/redis/data“ `
  - 设定当前服务文件保存位置，包含日志文件、持久化文件（后面详细讲解）等 
  - `logfile "6***.log“ `
  - 设定日志文件名，便于查阅