Linux 常用命令
+ 关机
```shell
# 即可关机
pooweroff 
halt
shutdown -h nw
```

+ 防火墙
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

+ 更改文件属性
```shell
# 递归更改文件属组为 root
chgrp -R root 文件名称

# 递归更改文件属主为 root
chown -R root:root 文件名称

# 更改文件读写执行权限
chmod 777 文件名称

# 增加文件执行权限
chmod +x 文件名称
```

+ vim 文件编辑
```shell
# 显示行号
:set nu 

# 跳转到第100行
:100

# 插入模式
i 

# 退出
:q

# 强制推出
:q!

# 保存推出 
:wq

```




























