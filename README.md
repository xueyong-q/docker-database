## 简介

本项目使用 Docker 搭建开发所需的 MySQL 数据库和 Redis 缓存数据库,并使用 PHPMyAdmin 管理 MySQL 数据库。

以下是各个服务的版本：

| 容器       | 版本              |
| ---------- | ----------------- |
| MySQL      | 5.7               |
| Redis      | 5.x               |
| PHPMyAdmin | 5.x(使用最新版本) |  
>以上容器版本均可在 `.env` 环境变量文件中修改。

## 搭建

首先需要先安装 Docker 如果是 windows 系统的话则是安装 Docker Desktop for Windows，然后将本项目克隆至本地。  
复制项目下 `.env.example` 文件为 `.env` 并配置其内容。  

```
MYSQL_VERSION        # MYSQL 的镜像版本
MYSQL_USER           # 新建 MySQL 用户名称
MYSQL_PASSWORD       # 新建 MySQL 用户密码
MYSQL_ROOT_PASSWORD  # MySQL root 用户密码
MYSQL_CONTAINER_NAME # MySQL 实例名称

REDIS_VERSION        # REDIS 的镜像版本
REDIS_CONTAINER_NAME # REDIS 实例名称

MYADMIN_VERSION      # phpmyadmin 的镜像版本
MYADMIN_UPLOAD_LIMIT # 设置文件上传的大小
```

>注意：MYSQL_CONTAINER_NAME 和 REDIS_CONTAINER_NAME 不能与现有的 Docker 实例名称重复，配置好实例名称后在同一网络的容器之间可以通过实例名称进行相互访问了。

将以上环境变量配置完成后接下来新建一个虚拟网络，如下命令：  
```sh
$ docker network create database_app
```

新建好虚拟网络后直接在本项目下运行 `docker-compose up -d` 命令启动容器。  
启动容器完毕后可以使用 `docker ps` 命令查看容器是否启动成功。    
到此数据库已构建完成。  

## 使用

容器启动成功后，可以在浏览器中使用 `localhost:8888` 访问 phpMyAdmin 来管理 MySQL 数据库了，无需账号密码登录。

以下是容器映射至主机的端口：

| 容器       | 映射端口 |
| ---------- | -------- |
| MySQL      | 3306     |
| Redis      | 6379     |
| PHPMyAdmin | 8888     |  
可通过访问主机的以上端口来访问对应的服务。

由于以上容器设置了 restart 为 always，所以在每次 Docker 启动后这三个容器也会跟着启动，无需我们手动去启动这三个容器了。