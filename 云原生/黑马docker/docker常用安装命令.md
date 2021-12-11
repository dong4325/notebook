```shell
# 建立宿主机数据库目录
mkdir /root/mysql/datadir
# 建立宿主机数据库配置文件
mkdir /root/mysql/conf
# 建立宿主机数据库日志目录
mkdir /root/mysql/log


docker run --name mysql -p 3306:3306 -v /root/mysql/datadir:/var/lib/mysql -v /root/mysql/conf:/etc/mysql/conf.d -v /root/mysql/logs:/var/log/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
 
 docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:8.0.12
 
##腾讯云开启3306端口
```

