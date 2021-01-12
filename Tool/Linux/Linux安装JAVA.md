# Linux平台上安装Java

[Linux安装JAVA步骤](https://www.cnblogs.com/wjup/p/11041274.html)

**方式一：yum方式下载安装**

**方式二：官网下载jdk后，上传服务器解压安装**

1. 官网下载：`jdk-8u221-linux-x64.tar.gz`

2. 创建目录

   在`/usr/`目录下创建`java`目录

   ```
   mkdir /usr/local/java
   cd /usr/local/java
   ```

   把下载的文件 `jdk-8u151-linux-x64.tar.gz` 放在`/usr/local/java/目录下。

3. 解压JDK文件

   ```
   tar -zxvf jdk-8u151-linux-x64.tar.gz
   ```

4. 设置环境变量

   **区分：[修改系统环境变量和用户环境变量](https://blog.csdn.net/flw8840488/article/details/90513873)**

   ```
   export JAVA_HOME=/usr/local/java/jdk1.7.0_71

   export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

   export PATH=$JAVA_HOME/bin:$PATH
   ```

5. 测试

   ```
   java -version
   javac
   ```
   
   显示Java版本信息，则说明成功。
   
   
   



