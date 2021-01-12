# Git 学习指南

[廖雪峰网站](https://www.liaoxuefeng.com/wiki/896043488029600)

## Git 常用命令

[博客园](https://www.cnblogs.com/junecode/p/11550875.html)

```bash
git init
```

```bash
git add
git add . # 本地把所有新文件加入git
git commit -m "xxxx" # 本地comment所有修改
```

```bash
git status # 查询git状态，显示修改了的文件
git diff
```

```bash
git reset --hard commit_id
git log
git reflog
```

```bash
git reset head
git checkout -- file
```

```bash
git rm
```

```bash
git remote and origin git@server-name:path/repo-name.git
git push -u origin master
git push origin master
```

```bash
git clone
```

```bash
git branch
git checkout
git checkout -b xxxx # 创建名为xxxx的分支，并切换到xxxx分支
git switch
git switch -c
git merge branch-name # 合并分支
git branch -d
```

```bash
git log --graph
```

```bash
--no--f
faster forward
```

```bash
git stash pop
```

```bash
git remote -v # 查看远程库信息
git checkout -b branch-name # 创建分支并切换到该分支
git push --set-upstream origin/branch-name # 初始化推送命令，推送当前分支并建立与远程dev的追踪
git push origin branch-name
git pull # 从服务器代码仓库拉取最新版本
git checkout master # 切换回master分支
```

```bash
rebase
```

```bash
git tag
git tag -a -m "sssss"
```

```bash
git push origin
git push origin --tags
git tag -d
git push origin :refs/tags/
```

```bash
.gitignore
```

### 创建仓库

第一步，先创建并进入一个名为learn的空目录

```bash
mkdir learn
cd learn
pwd # 显示当前目录
```

第二步，仓库初始化

```bash
git init # 仓库初始化，将该目录变为仓库
# .git目录用于git跟踪管理版本库，勿修改。
```

### 把文件添加到仓库

写了一个readme.txt文件

```bash
git add readme.txt # 把文件添加到仓库
git commit -m "write a readme.txt file" # 记录修改 
```

### 版本控制

修改了readme.txt文件

```bash
git status # 查询仓库的状态，显示修改的文件
git diff readme.txt # 显示具体的修改内容
git log # 查看修改日志
git log --pretty=oneline # 简洁版，查看修改日志
```

### 版本回退

回到历史

```bash
git reset --hard Head^ # 回退到上一版本
cat readme.txt # 查看readme.txt文件的内容
```

**回到未来（从历史回来）**

```bash
git reset --hard commit-id # 只要有commit-id，就可以穿梭
cat readme.txt
git reflog # 记录每次修改的commit-id
```

### 管理修改

工作区（本地）、暂存区和仓库（远程）

把文件往Git仓库里添加的时候，是分两步执行的：

- 第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区（Stage)

- 第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支（如master）

```bash
git diff HEAD -- readme.txt # 查看本地和仓库最新版本的区别
```

### 撤销修改

如果修改还没有git add

```bash
git checkout -- readme.txt # 放弃工作区的修改
```

如果修改已经git add，但还没有git commit

```bash
git reset HEAD readme.txt # unstage 将暂存区的修改回退到工作区
git checkout -- readme.txt # 放弃工作区的修改
```

如果已经git commit，但还没有push

```bash
git reset --hard Head^ # 回退到上一版本
```

如果已经push，那你完了😂

### 删除文件

⚡删除也是一种修改

删除了test.txt文件 

```bash
git rm test.txt # 也可以 git add test.txt, git 管理的是修改，而不是文件
git commit -m "delete test.txt"
```

### 远程仓库

添加远程仓库

⚡情景一：先有本地仓库，后有远程仓库，关联远程仓库

关联本地仓库和远程仓库

```bash
git remote add origin git@github.com:xiaolou023/Notebook.git # origin 是远程仓库默认的名字
```

把本地仓库的内容推送到远程仓库

```bash
git push -u origin master # 第一次
git push orgin master # 之后
```

⚡情景二：先构建远程仓库，然后从远程仓库克隆

复制远程仓库

```bash
git clone git@github.com:xiaolou023/Notebook.git
```

### 创建分支

一个分支对应一个指针。

```bash
git branch dev # 创建分支
git checkout dev # 切换分支
git checkout master # dev工作完成后切换到master
git merge dev # 合并到当前分支
git branch -d dev # 删除分支
```

创建并切换到dev分支

```bash
git checkout -b dev # 创建并切换分支
git checkout dev # 切换分支
```

``` bash
git switch -c dev # 创建并切换分支
git switch dev # 切换分支
```

合并分支

```bash
git merge dev # 合并分支，删除dev分支
git merge --no-ff -m "merge with no-ff" dev # 禁用fast-forward模式，保留dev分支的信息
```

查看所有分支

```bash
git branch
```

### 解决分支冲突

```bash
git log --graph # 查看分支合并图
git log --graph --pretty=oneline --abbrev-commit
```





















