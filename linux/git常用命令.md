# git常用命令

```bash
touch README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/cjinle/crawler.git
git push -u origin master

git remote add origin https://github.com/cjinle/crawler.git
git push -u origin master

git blame file  # 查看文件历史修改记录

git config --global user.name "Jinle Chen"
git config --global user.email "xxxxx@gmail.com"
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=86400'
```

**合并分支：**
```
[root@localhost demo]# git checkout master
[root@localhost demo]# git merge demo2
[root@localhost demo]# git push origin master
```

**忽略文件用法：**
```bash
git rm -r --cached .
git add .
git commit -m 'update .gitignore
```
在项目目录下建立 `.gitignore`
例子：
```bash
# 以'#' 开始的行，被视为注释.
# 忽略掉所有文件名是 foo.txt 的文件.
foo.txt
# 忽略所有生成的 html 文件,
*.html
# foo.html是手工维护的，所以例外.
!foo.html
#  忽略所有.o 和 .a文件.
*.[oa]
# 忽略文件夹
tmp/
```

### 分支管理
```bash
git branch # 查看分支
git branch branch_name # 创建分支
git checkout branch_name # 切换分支
git checkout -b branch_name # 创建+切换分支
git merge branch_name # 合并某分支到当前分支
git branch branchname <sha1-of-commit> # 按某次提交创建分支
git branch branchname HEAD~3  # 前3次的提交创建分支
git branch -d branch_name # 删除分支
git push origin --delete branch_name # 删除远程仓库分支
```

### 代码回滚
```bash
git reset --hard HEAD~1

# git rm a.txt ，误将a.txt删除后找回方法：
git log #找到离没删文件前最近的commit id
# 将操作过的其它文件转移
git reset --hard "commit id"

# 如果一不小reset错了，想反悔，可以进行下面操作
git reflog 
# 88a9cae HEAD@{0}: commit: xxx
git reset --hard 88a9cae
```

### 使用vimdiff来git diff
```bash
git config --global diff.tool vimdiff  
git config --global difftool.prompt false  
git config --global alias.d difftool  
```

### 导出干净代码
```bash
git archive --format zip --output "../master.zip" develop -0
```

### 导出git日志
```bash
git log --date=iso --pretty=format:'"%h","%an","%ad","%s"' >log.csv
```

### 解决冲突
```bash
# 使用他们的
git checkout --theirs .
git add .

# 使用本地的
git checkout --ours .
git add .

# 使用他们的某一个文件
git checkout --theirs path/to/file
```

### 备份与回复
```bash
# 备份
git clone --mirror yourrepo backup.repo
tar cjf backup.repo.tar.bz2 backup.repo
scp backup.tar.bz2 ssh://somewhereelse

# 恢复

tar xjf backup.repo.tar.bz2
git clone backup.repo yourrepo
```

## 标签

```sh
git tag -a v1.0.0 # 然后打开编辑器，输入tag信息
git log --decorate # 查看tag日志信息
git push origin v1.0.0 # 把tag推送到远程仓库
git push origin --tags # 把所有tag推送到远程仓库

git tag -d v1.0.0 # 删除tag

```





### git server

```bash
mkdir ipa-server.git
cd ipa-server.git/
git init --bare

// 客户机
cd ipa-server/
git init .
t commit -m "first"
git remote add origin ssh://git@sz2.lok.me:7011/data/gitrepo/ipa-server.git
git push origin master;
```