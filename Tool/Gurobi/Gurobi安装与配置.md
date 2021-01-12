# Gurobi 安装与配置

## Gurobi + Windows

#### 安装遇到的问题

##### Gurobi 安装遇到"Installation directory must be on a local hard drive"。

解决方案：

windows权限的原因 

以下文件复制到 txt 中，将后缀名修改为bat以管理员执行即可。

```
cls
icacls %temp% /reset /T /Q /C
pause
```





