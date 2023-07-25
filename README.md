# PHP开发环境（使用alpine）
# 由来

以前本地开发都使用 XAMPP ，经常需要切换工作目录，使用起来不很方便，就用docker 做了一个 PHP 开发环境。

# 特性

* 目前集成 php 、nginx、redis、mysql
* alpine 包较 ubuntu、centos 包体积小
* 配置任意版本，包括 nginx、mysql、redis、php
* 自由切换 htdocs 目录

# 使用帮助

## 安装运行

需要 docker 和 docker-compose，[下载地址](https://docs.docker.com/engine/installation/)

下载文件包：

```
https://github.com/spetacular/php-alpine/archive/master.zip 
```

解压后进入目录执行 build。如果下次启动时没更改 Dockerfile，就不需要再次build。只更改  docker-compose.yml 不需要重新 build。

```
docker-compose build
```

执行如下命令即可启动:

```
docker-compose up
```

## 运行环境
PHPMyAdmin 的首页链接：
http://localhost:8081/index.php
登录页面，server可以不填，Username默认为root，Password默认为123456

PHP环境为
http://localhost:8080/

## docker-compose.yml 字段说明

| 字段                  | 说明                        |
| ------------------- | ------------------------- |
| ports               | 端口映射，本机端口：docker端口。只能改本机。 |
| volumes             | 文件夹映射，本机目录：docker目录。只能改本机 |
| MYSQL_ROOT_PASSWORD | mysql root用户默认密码          |



# 注意事项

1.由于代码跑在docker里，所以 localhost 和 127.0.0.1不再可用。如需要连接 redis 和 mysql，应使用如下地址：

```redis-server
redis-server
mysql-server
```
2.403
这个是权限问题，建议volumes的本机目录设置在家目录
3.Alpine
```bash
#Alpine Linux使用apk作为其包管理工具，同时提供了一些服务管理工具，例如OpenRC和runit。下面是一些常用的Alpine Linux命令：
apk add packagename #安装指定软件包。例如，apk add nginx将安装Nginx Web服务器。
apk upgrade #升级所有已安装的软件包。
apk search keyword #搜索软件包，其中keyword是要搜索的关键字。例如，apk search mysql将搜索包含“mysql”关键字的软件包。
apk info packagename #显示软件包的信息。例如，apk info nginx将显示Nginx软件包的详细信息。
apk del packagename #卸载指定软件包。例如，apk del nginx将卸载Nginx软件包。
rc-service servicename start/stop/restart #启动、停止或重新启动指定服务。例如，rc-service nginx restart将重新启动Nginx Web服务器。
rc-update add servicename #将指定服务添加到系统启动时启动。例如，rc-update add nginx将添加Nginx Web服务器到系统启动时启动。
runitctl start/stop/restart servicename #启动、停止或重新启动指定服务。例如，runitctl restart nginx将重新启动Nginx Web服务器。
```
