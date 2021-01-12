# VScode通过Git推动到Github


## Git下载安装

[博客园](https://www.cnblogs.com/zhangyaolan/p/11105330.html)

1. Git下载地址
   
   git下载，国外官网地址一般下载很慢，可以使用国内淘宝镜像地址，版本根据电脑使用系统合理选择。
   
   git官网：https://git-scm.com

   git镜像：https://npm.taobao.org/mirrors/git-for-windows

2. Git安装
   
   按默认选项安装

   点击进入Git Bash，输入`git`，测试是否安装成功。

## Git与Github相连

[博客园](https://www.cnblogs.com/zhangyaolan/p/11106091.html)

1. 在Github创建仓库：`create a new repository`
2. 配置SSH key
   
   - 在电脑空白处点击`Git Bash Here`;
   - 输入`ssh-keygen -t rsa`
   - 陆续回车三次
   - 在`C:\Users\dell\.ssh`，找到公私钥文件(.pub)
   - 在Github网站上, 点击`Setting`-`New SSH keys`, 输入title,输入public key, 点击添加.
   - 回到Git Bash, 输入`ssh -T git@github.com`, 输入`yes`.
   
3. 配置`username`, `email`
   
   ```
   $ git config --global user.name "liuying"
   $ git config --global user.email "claire_0422@163.com"
   ```

   查看配置是否成功，使用`git config`命令

   ```
   $ git config user.name
   $ git config user.email
   ```

## VScode上传到Github

https://www.jianshu.com/p/154322554d9d

1. 确保系统环境变量添加了`Git`路径
2. 在本地和Github上建立同名的仓库
3. 在本地仓库文件夹中, 点击`Git Bash Here`, 并输入
   ```
   git init
   git add README.md
   git commit -m "first commit"
   git remote add origin git@github.com:xiaolou023/Research.git
   git push -u origin master
   ```

   

