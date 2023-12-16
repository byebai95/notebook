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

### 操作容器
```shell
# 暂停容器
docker stop <container-id>

# 删除容器
docker rm -f <container-id>

# 查询全部容器
docker ps -a 
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
