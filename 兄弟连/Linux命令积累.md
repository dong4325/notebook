### 将用户添加进sudoers

```shell
# root权限运行
usermod -aG wheel username
# sudo以root权限执行，但仍是自己的环境变量，root为root的环境变量

# 添加用户到用户组
usermod -a -G groupA user

# 查看用户所属的组使用命令
groups user
cat /etc/group
```



查看ip

```
ip addr
```

#### linux踢出其他正在ssh登陆用户

```shell
who
who am i		#查看当前自己占用终端，别把自己干掉了
pkill -kill -t pts/1	#pkill命令踢出对方
```



python 安装使用镜像

```python
pip3 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```



### 部署jar包

```bash
# 打包
mvn clean install -Dmaven.test.skip

# 后台运行
nohup java -jar test.jar >temp.txt &

# 查看进程
ps -ef|grep xxx.jar

# 干掉进程
kill -9 端口号对应的PID

# 查看端口是否被占用
lsof -i:端口号
netstat -tunlp | grep 端口号
```



### 安装

```bash
# 安装vim
yum -y install vim*

# 容器安装vi
apt-get update
apt-get install vim
```





