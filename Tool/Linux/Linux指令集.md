# Linux指令集

1. 查询并输出
   | 指令 | 功能 |
   | ------  | ------ |
   | `top` |查看服务器当前使用情况 |
   | `q`   | 退出 |
   | `ctrl` + `c` | 取消 |
   | `cd` | 进入根目录 |
   | `ls`     | 列出当前文件夹下所有文件                |
   | `ls -a`  | 列出当前文件夹中所有文件，包含以"."开头的文件|
   | `ls -al` | 查看当前目录下所有的文件列表的全部信息        |
   | `cd`  | 进入根目录                                   |
   | `cd xx`  | 进入xx目录                                    |
   | `ls xx`  | 查看xx目录下的文件列表                        |
   | `pwd` | 显示当前目录 |

2. 创建目录、创建文件，删除目录、删除文件
   | 指令 | 功能 |
   | ------  | ------ |
   | `mkdir xx` | 新建为xx的文件夹 |
   | `rm xx` | 删除xx文件 |
   
3. 复制 移动
   | 指令 | 功能 |
   | ------  | ------ |
   | `cp xx1 xx2` | 将当前目录下的xx1文件复制并并命名为xx2 |
   | `mv`          | 重命名或移动         |
   | `mv xx1 xx2`  | 将xx1文件重命名为xx2     |
   | `mv xx1 xx2/` | 将xx1文件移动到xx2目录下 |
   
4. `screen`的使用
   | 指令 | 功能 |
   | ------  | ------ |
   | `screen -S yourname` | 新建一个叫yourname的session |
   | `screen -r yourname` | 回到yourname这个session |
   | `screen -d yourname` | 远程detach某个session |
   | `kill xx` | 停止XX线程 |
   | `screen -ls` | 查看所有sessions |
   | `ctrl` + `a` + `d` | "退出"当前线程界面 |

5. 环境变量

   [Linux 更改用户环境变量和所有用户环境变量](https://blog.csdn.net/flw8840488/article/details/90513873)
   
   -  仅对当前用户，永久有效：通过修改`.bashrc`文件
   
   
      第一步：`vim ~/.bashrc`，进入`.bashrc`文件
   
      第二步：在最后一行添上：`export PATH=/usr/local/mongodb/bin:$PATH`
   
      第三步：`source ~/.bashrc`,立即生效
   
   -  仅对当前用户，临时有效
   -  针对所有用户，永久有效
   
6. `vi`,`vim`编辑文件
   
   第一步：`cd`到该文件的目录下
   
   第二步：`vi` 要编辑的文件名，进入普通模式，（可以查看文件内容）
   
   第三步：输入`i`  进入编辑模式，开始编辑文本
   
   第四步：编辑之后，按`ESC`退出到普通模式。
   
   第五步：在普通模式下，输入 `:`进入命令模式
   
   第六步：在命令模式下输入`wq`, 即可保存并退出
   
7. 运行
   `java -jar xx.jar`
   `bash run.sh`
   `bash run.sh > log.txt`
   `bash run.sh >> log.txt`

