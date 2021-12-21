# docker积累

## tomcat

访问404：

默认的包在webapps.dist目录下，需要将webapps删除，将webapps.dist目录更改为默认目录，即可访问默认页面。



普通用户使用docker 添加到docker用户组即可

```bash
usermode -a -G docker dong
```

