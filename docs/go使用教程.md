GO 入门

### 一、环境准备

go 命令基本用法

```shell
# 查看当前go语言版本
go version

# go build 生成二进制文件
go build hello.go


```

linux 配置环境环境变量
```shell
export GO111MODULE=on
```

goctl 安装  
```shell
go install github.com/zeromicro/go-zero/tools/goctl@latest
```

安装 protoc

```shell
# 安装依赖检测
go env check --install

# 安装 protoc
goctl env check --install --verbose --force 
```

安装 swagger 工具

```shell
go install github.com/go-swagger/go-swagger@latest

goctl api plugin -plugin goctl-swagger="swagger -filename user.json" -api user.api -dir .
```



go zero 创建文件目录

```shell
# 创建 api 服务
goctl api new xxx

# 创建 rpc 服务
goctl rpc new xxx
```



##### go-myql 

```shell
# 根据 sql 文件生成代码
goctl model mysql ddl --src user.sql --dir .
```



### 二、打包

##### window 环境打包运行

```shell
# 查看 GOOS  系统，如果需要在 linux 上运行，需要修改该变量
go env 

# 打包,window 下将生产exe文件
# -gcflags 跳过优化
go build -gcflags="all=-N -l"  user.go

```



##### 运行在Linux二进制包

```shell
# window 下采用 export 设置环境变量
export GOOS=linux
set GOARCH=amd64
go build -o main-linux main.go
```





