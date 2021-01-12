# Linux安装CPLEX

[Linux安装Cplex](https://www.cnblogs.com/qujingtongxiao/p/9813285.html)

1. 官网下载：`cplex_studio128.linux-x86-64.bin`

2. 创建目录

   在当前用户目录下创建目录`cplex`

   ```shell
   mkdir cplex
   chmod u=rwx,g=rwx,o=rx cplex_studio128.linux-x86-64.bin
   ```

   把下载的`cplex_studio128.linux-x86-64.bin`放在`cplex`目录下，并修改权限。

3. 安装

   ```shell
   cd cplex
   ./cplex_studio128.linux-x86-64.bin 
   ```

   选择语言为2English后，按ENTER继续，再选择1接受条款，要么按ENTER选择默认安装路径，要么自己输入要安装的绝对路径，我选择的是`/home/username/cplex`，之后一直按ENTER即可。

4. 配置环境变量

   (仅对当前用户)

   打开`.bashrc`文件

   ```vim ~/.bashrc```

   按`i`进行编辑模式

   在最后一行添上：

   ```export PATH=$PATH:~/cplex/cplex/bin/x86-64_linux/:~/cplex/cpoptimizer/bin/x86-64_linux/```

   ps: 还添一句：

   ```bash
   export DYLD_LIBRARY_PATH=/home/ying/cplex/cplex/bin/x86-64_linux:/home/ying/cplex/cpoptimizer/bin/x86-64_linux:
   export LD_LIBRARY_PATH=/home/ying/cplex/cplex/bin/x86-64_linux:/home/ying/cplex/cpoptimizer/bin/x86-64_linux:
   ```

   按`esc`退出编辑模式，接着`:`，然后`wq`保存。

   保存后执行`source ~/.bashrc`生效

5. 测试

   ```bash
   cplex -c read ~/cplex/cplex/examples/data/afiro.mps
   ```

