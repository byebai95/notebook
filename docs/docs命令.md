## windows系统快捷操作

+ 端口被占用
```shell
# 查询占用端口的进程
netstat -ano|findstr 8080

# 强制关闭进程
taskkill  -F -PID 6832
```