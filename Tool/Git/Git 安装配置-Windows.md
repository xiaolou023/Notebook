# Git在windows上安装与配置

[博客园](https://www.cnblogs.com/leeego-123/p/10756603.html)

1. 下载

2. 安装

3. 生成公钥和私钥

   上传代码到远程仓库的时候需要秘钥进行验证是否本人上传的。打开Git目录下的Git Bash，输入**ssh-keygen**，回车。

   ```bash
   ssh-keygen
   ```

   此时打开C:\Users\Administrator目录（默认目录），会看到.ssh的文件。这是存放秘钥的文件，打开这个文件会看到有两个文件，分别是id_rsa和id_rsa.pub。id_rsa是私钥文件，id_rsa.pub是公钥文件。