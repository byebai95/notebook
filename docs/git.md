## Git 常用命令

+ 查看本地分支列表
```shell
git branch -l
```

+ 拉去远程分支到本地  
```shell
git checkout -b branch_name origin/branch_name
```

+ 删除本地分支  
```shell
git branch -D branch_name
```

+ 删除远程分支  
```shell
git push origin --delete branch_name
```

+ 删除git已提交文件
```shell
# 删除 .idea
git rm --cached -r .idea

# 删除 .iml
git rm --cached -r *.iml
```