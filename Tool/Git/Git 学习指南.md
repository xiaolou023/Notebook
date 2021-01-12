# Git 学习指南

[廖雪峰网站](https://www.liaoxuefeng.com/wiki/896043488029600)

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





















