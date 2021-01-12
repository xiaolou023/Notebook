# Jar包在LINUX服务器上跑程序

### 从Eclipse到Linux远程服务器

> [博客园：eclipse 打包 jar 到 Linux上运行](https://www.cnblogs.com/ysocean/p/7250121.html)

1、选择需要打包的项目，右键`Export`

2、选择``Runnable JAR file`,然后点击 `Next`

3、选择jar包运行的main类，以及定义jar包的名字，保存的地方

4、将导出来的 jar 包通过远程工具，比如 WinSCP 上传到 Linux 服务器中

5、输入` java -jar MysqlJdbc.jar` 然后就可以执行该 jar 包了

### 从IDEA到Linux远程服务器

备注：在没有使用CPLEX时，操作简单，仅仅使用CPLEX也还OK，容易出错的是使用CP时。

1. `File -> Project Structure`
2. `Artifacts -> '+' -> Jar -> 'from modules with dependencies'`
3. 配置`Main Class`: `MainTest.class`
4. 配置`Jar files from libraries`: `copy...`
5. 配置`Directory for META-INF/MAINFEST.MF` (default)
6. 回到IDEA的主菜单，选择`Build - Build Artifacts`下的`Build`或者`Rebuild`即可生成最终的可运行的jar。在`D:\XXX\XX\out\artifacts\XX_jar`下面找到生成的目标jar
7. 把`D:\XXX\XX\out\artifacts\XX_jar`中生成的jar和复制得到的jar通通复制到远程服务器。

### 运行程序

```bash
java -Xmx1024m -jar rcpsp.jar model 
```



