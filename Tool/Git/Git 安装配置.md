# Git安装与配置

[CSND](https://blog.csdn.net/huangqqdy/article/details/83032408)

## Windows安装

1. 下载

2. 安装

3. 生成公钥和私钥

   上传代码到远程仓库的时候需要秘钥进行验证是否本人上传的。打开Git目录下的Git Bash，输入ssh-keygen，回车。

   ```bash
   ssh-keygen
   ```

   此时打开C:\Users\Administrator目录（默认目录），会看到.ssh的文件。这是存放秘钥的文件，打开这个文件会看到有两个文件，分别是id_rsa和id_rsa.pub。id_rsa是私钥文件，id_rsa.pub是公钥文件。
   
4. 配置user.name和user.email

   ```bash
   git config --global user.name "liuying"
   git config --global user.email "claire_0422@163.com"
   ```

   ```bash
   git config --global --list # 查看
   ```





