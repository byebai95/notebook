# docker 教程

### 下载 docker

```shell
#  更新yum包
sudo yum install -y yum-utils  

# 设置镜像仓库，ali比国外更快
sudo yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo


# 启动 docker
sudo systemctl start docker

# 关闭 docker
systemctl stop docker
```

### 操作容器
```shell
# 暂停容器
docker stop <container-id>

# 删除容器
docker rm -f <container-id>

# 查询全部容器
docker ps -a 

# 进入容器内部，mysql为例
docker exec -it mysql8 bash


```

### 镜像操作
```shell
# 搜索镜像
docker search <name>

# 查询镜像
docker images

# 删除镜像
docker rmi <name>

# 拉取镜像
docker pull <name>:<version>
```


### 运行 elasticsearch
```shell
# 下载镜像
docker pull elasticsearch:7.5.1

# 启动服务
docker run -d -p 9200:9200 -p 9300:9300 --name es -e "discovery.type=single-node" elasticsearch:7.5.1

# 查看日志
docker logs -f es
```

### 运行 kibana
```shell
# 下载镜像
docker pull kibana:7.5.1

# 启动服务
docker run -d --name kibana --link es:elasticsearch -p 5601:5601 kibana:7.5.1

# 查看日志
docker logs -f kibana
```

### 运行 mysql
```shell
# 下载容器
docker pull mysql:8.0.20

# 启动容器
docker run -p 3307:3306 --name mysql8 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.0.20

# 设置挂在目录，删除原有mysql
mkdir -p /docker/mysql8.0.20/#
docker cp  mysql8:/etc/mysql /docker/mysql8.0.20/
docker stop mysql8
docker rm -f mysql8

# 修改mysql配置
cd /docker/mysql8.0.20/mysql/conf.d

vim my.cnf
[mysqld]
user=mysql
character-set-server=utf8
default_authentication_plugin=mysql_native_password
secure_file_priv=/var/lib/mysql
expire_logs_days=7
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
max_connections=1000
 
[client]
default-character-set=utf8
 
[mysql]

# 增加一个启动脚本
vim docker_insert_mysql8.0.20.sh
#!/bin/sh
docker run \
-p 3307:3306 \
--name mysql8 \
--privileged=true \
--restart unless-stopped \
-v /docker/mysql8.0.20/mysql:/etc/mysql \
-v /docker/mysql8.0.20/logs:/logs \
-v /docker/mysql8.0.20/data:/var/lib/mysql \
-v /etc/localtime:/etc/localtime \
-e MYSQL_ROOT_PASSWORD=123456 \
-d mysql:8.0.20

# 启动mysql
sh docker_insert_mysql8.0.20.sh

# 配置链接信息
docker exec -it mysql8 bash
mysql -u root -p123456

# 设置mysql可远程访问
grant all PRIVILEGES on *.* to root@'%' WITH GRANT OPTION;
use mysql
update user set host='%' where user='root';

# 更新密码算法，方便navicat链接
grant all PRIVILEGES on *.* to root@'%' WITH GRANT OPTION;
ALTER user 'root'@'%' IDENTIFIED BY '123456' PASSWORD EXPIRE NEVER;
ALTER user 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
FLUSH PRIVILEGES;
```