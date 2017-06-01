# laradock-lite
基于Docker的laravel本地开发环境

# 前言
我对一个完美的本地开发环境的要求：

1. 一键启动所有的组件，不需要mock任何service，没有任何dummy client。新人入职后一小时内即可上手开发新功能。
2. 系统资源占用少，即cpu和内存占用少，在MacBook Pro上开发不卡
3. 隔离本机环境，在本机上安装尽可能少的依赖的软件，例如不在本机上安装mysql
4. 和集成开发、集成测试以及生产环境近似，容易排查环境引起的问题。团队使用统一的开发与测试环境配置，能提高协作效率。
5. 方便调试，能和IDE集成就更好了
6. REPL功能（当然受限于语言）
7. 便于执行unit test
8. 便于尝试各种service, server的使用方法，比如快速启动elastic search server后，可基于一本书、一部视频去学习如何使用es

# 由来
最早用Laravel开发web应用的时候，使用的是Homestead作为本地开发环境。Homestead基于Vagrant和VirtualBox，无论是自己把开发环境配置好，还是帮助别人配置都需要一定的时间，每次有新人入职都要折腾一番。后来laravel官方文档中推荐的Valet我并没有去尝试，看文档是基于Homebrew来安装到本机上，我个人不喜欢污染本机环境，所以还是转向了docker的解决方案。

当发现了[laradock](https://github.com/laradock/laradock) 后，眼前一亮，心想这正是我想要的。遂试之，大喜。docker的优势我就不在这里重复了，使用docker来build开发、测试及生产环境是大势所趋。目前在我的项目里仅把docker用于开发环境，用于生产环境需要额外的运维能力，有兴趣的高手可以尝试。

laradock里集成了很多组件，在定制化的过程中，我只把自己需要的组件剥离出来，同时基于alpine的镜像减少docker image的大小。同时安装了xdebug方便调试和学习laravel框架。


# 谁适合
1. laravel开发新手，快速学习laravel
2. 打算以此来作为本地开发环境的开发者
3. debug laravel框架，并深入学习的开发者

# 快速入门
[install docker](https://docs.docker.com/docker-for-mac/install/)
确保docker-compose也安装正确
```
$docker-compose -v
docker-compose version 1.11.2, build dfed245
```
`composer global require "laravel/installer"`

`laravel new blog && cd $_`

修改.env中的DB部分
```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=default
DB_USERNAME=default
DB_PASSWORD=secret
```

`git clone https://github.com/yangliuyu/laradock-lite.git && cd laradock-lite`

`cp env-example .env`

修改.env文件中的DOCKER_HOST_IP=172.16.30.1 改为你本机的ip，这里主要是用于xdebug功能，开箱即用的xdebug功能的文档稍后释出。

`docker-compose up` or `docker-compose up -d`

最后在浏览器中打开 http://localhost

执行php artisan xxx命令:
```
docker-compose exec workspace /bin/ash
php artisan migrate:refresh
```

# 组件
通过查看docker-compose.yml中的各个镜像，可看到所有组件，其中每个组件运行在各自的容器中，即一个组件一个容器
1. nginx 1.12
2. php-fpm 基于php7.1
3. mysql 5.7
4. redis 3.2
5. elastic search 5.3.2 (XPack 默认用户名密码 elastic/changeme)

# 没有涉及的点
对于前端项目，比如React.js + webpack，暂时推荐使用npm或者yarn在本地安装开发依赖，可参考[create-react-app](https://github.com/facebookincubator/create-react-app) 快速上手。

# 写在最后
适合自己的才是最好的，祝大家玩的愉快。