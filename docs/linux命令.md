Linux 常用命令
+ 关机
```shell
# 即可关机
pooweroff 
halt
shutdown -h nw
```

+ centos 防火墙
```shell
# 查询防护墙状态
firewall-cmd --state

# 关闭防护墙
systemctl stop firewalld

# 禁用防火墙
systemctl disable  firewalld

# 开启防火墙
systemctl start firewalld

# 启用防火强
systemctl enable  firewalld
```