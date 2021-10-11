### 1. `配置Dubbo-Admin打包时npm rum build..`

解决办法：安装nodejs

```shell
yum -y install nodejs
```

> 安装时可参考官方https://github.com/apache/dubbo-admin



并解决`building for production...Killed`该错误

```shell
sudo /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024
sudo /sbin/mkswap /var/swap.1
sudo /sbin/swapon /var/swap.1
```

原理好像是：服务器内存不够用了，这样就给他配置一个单独的内存出来就解决了



### 2.  Compilation failure

[ERROR] No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK?

**原因**：只安装了JRE没有安装JDK。可以尝试输入`java`命令和`javac`命令验证。

#### 解决方法：

进入根目录安装

```shell
cd /
yum install -y java-devel
```

