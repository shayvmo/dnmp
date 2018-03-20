## Docker DNMP 2.2

Docker DNMP 可以构建出基于 Docker 的 PHP 多版本开发环境，其优势有在短时间内随意构建不同版本的相关服务、环境统一分布在不同服务器等，使开发者能够更专注于开发业务本身。

##### 产品特色

* 灵活切换适合国内的源（APT-GET、PHP Composer）
* 组件精简易懂，学习、测试环境、生产环境均适合

##### 版本及组件

* 当前版本：2.0
* 自带组件：PHP/FPM 5.6、Nginx 1.12.2、Mysql 5.7、Redis 4.0.8

##### 目录结构

    docker_lnmp
    |----/build                  镜像构建目录
    |----/databases              数据持久化目录
    |----/conf                   配置持久化目录
    |----/logs                   日志持久化目录
    |----/www                    站点程序持久化目录
    |----/docker-compose.yml     docker compose 配置文件

#### 开始安装

    git clone 克隆项目

    cd dnmp

    # 构建镜像并启动容器，如果某些容器起不来注意检查持久化目录下面的组件目录是否有可写权限
    sudo docker-compose up --build -d

#### 可能遇到的问题

##### 常用操作命令

    # 查看当前启动的容器
    sudo docker ps
    
    # 启动部分服务在后边加服务名，不加表示启动所有，-d 表示在后台运行
    sudo docker-compose up [nginx|php56|mysql57|redis] -d
    
    # 停止和启动类似
    sudo docker-compose stop [nginx|php56|mysql57|redis]

    # 删除所有未运行的容器
    sudo docker rm $(docker ps -a -q)

    # 删除所有镜像，-f 可以强制删除
    sudo docker rmi $(docker images -q)

##### 修改镜像文件怎么处理？
    
    # 比如在 php 里新增一个扩展
    # 1、更改对应的 dnmp/build/php56/dockerfile
    # 2、重新构建镜像
    sudo docker-compose build [php56|...]

## License

Apache License