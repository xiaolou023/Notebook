# CPU使用率管理


## Linux 查看CPU使用率

[Top命令详解](https://www.cnblogs.com/niuben/p/12017242.html)

``` bash
top
```

退出`top`：`Ctrl` + `c`

``` bash
top -bn 1 -i -c
```

## 限制CPU使用率

[CSDN](https://blog.csdn.net/cyan20115/article/details/106554884)

安装CPULimit

``` bash
sudo apt-get install cpulimit
```

例如，我们有一个用python编写的cron作业（名称= mycronjob.py，pid = 1234）

通过可执行文件名将进程“ mycronjob.py”限制为50％CPU使用率

``` bash
cpulimit -e mycronjob.py -l 50
```

通过PID（1234）将进程限制为50％CPU：

``` bash
cpulimit -p 1234 -l 50
```


