## 简介

本项目使用 Docker 搭建开发所需的 MySQL 数据库和 Redis 缓存数据库,并使用 PHPMyAdmin 管理 MySQL 数据库。

## 搭建

首先需要先安装 Docker 如果是 windows 系统的话则是安装 docker for windows，然后将本项目克隆至本地。  
复制项目下 .env.example 文件为 .env 并配置其内容。  

MYSQL_USER #新建MySQL用户名称  
MYSQL_PASSWORD #新建MySQL用户密码  
MYSQL_ROOT_PASSWORD #MySQL root 用户密码  
MYSQL_CONTAINER_NAME #MySQL实例名称  
REDIS_CONTAINER_NAME #REDIS实例名称  

>注意：MYSQL_CONTAINER_NAME 和 REDIS_CONTAINER_NAME 不能与现有的 Docker 实例名称重复，配置好实例名称后容器之间可以通过实例名称进行访问了，当然还需要在同一网络中。

将以上环境变量配置完成后接下来新建一个虚拟网络，如下命令：  
```sh
$ docker network create database_app
```

新建好虚拟网络后直接在本项目下运行 `docker-compose up` 命令启动容器。  
启动容器完毕后可以使用 `docker ps` 命令查看容器是否启动成功。    
到此数据库已构建完成，接下来就是配置 Nginx + PHP 环境了。

## 使用

容器启动成功后，可以在浏览器中使用 `localhost:8080` 访问 phpMyAdmin 来管理MySQL数据库了。
在 phpMyAdmin 登录页面的服务器配置项使用环境变量 MYSQL_CONTAINER_NAME 的值，mysql 账号密码使用环境变量中配置的账号密码。