你可以用 pm2 运行相应的服务。

也可以使用 docker 

## ubutnu 18.04+ 安装 docker

```
apt install docker.io
```

## docker-composer 安装

```
curl -L https://get.daocloud.io/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

## 启动

根据需要配置 .env 文件（里面有环境变量）

`docker-compose up`  即可启动所有服务（内置了mysql和redis【内置的 redis 容器不支持哨兵模式】）

注意： 这里的 .env 是为了兼容 k8s 的环境变量配置，对线上部署不造成任何影响。

### env

```
######### DEFAULT: PATH ##########################################

本地使用： mysql 存储路径（仅限docker-compose 单机部署）

######### DEFAULT: MYSQL #########################################

本地使用： docker mysql 配置

###### K8S: SERVICE HOST ########################################

各个服务地址

###### K8S: SERVICE CONFIG ######################################

redis 及 mysql 环境变量

########## BUILD: GIT_ADDRESS ###################################

构建使用： git 仓库地址

```
