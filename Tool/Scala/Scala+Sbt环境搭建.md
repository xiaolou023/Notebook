## IDEA+sbt+Scala环境搭建

[CSDN步骤简述](https://blog.csdn.net/l912943297/article/details/80755192)

1. 下载JDK，sbt，Scala，IDEA

2. 安装JDK，sbt，Scala，IDEA

   > 安装路径不要有空格、中文和特殊字符
   >
   > JDK最好安装同时有jdk jre的版本，如jdk8-u221

3. 配置JDK，sbt，Scala的环境变量

   - 配置jdk环境变量

     JAVA_HOME
     
     ```
     C:\Program Files\Java\jdk1.8.0_221 // 无分号
     ```
     
     CLASSPATH
     
     ```
    .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar; //分号 + 点号
     ```
     
     path
     
     ```
     %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
     ```
   
   - 测试jdk是否安装成功
   
     ```bash
     java
     javac
     java -version
     ```
   
     > [java可用， java -version 可用，javac不可用的原因](https://blog.csdn.net/kobedir/article/details/79709287)
   
   - 配置scala环境变量
   
     path
   
     ```
     D:\ProgramData\scala\bin // 会自动添加
     ```
   
   - 测试scala是否安装成功
   
     ```bash
     scala -version
     ```
   
     > [此时不应有 \scala\bin\..\lib\jline-2.14.6.jar](https://blog.csdn.net/qq_34609633/article/details/90718232)：安装路径无空格
     >
     > Unable to create a system terminal, creating a dumb terminal -- 警告，可以运行 // 台式机出现，笔记本没出现
   
   - 配置sbt环境变量
   
     path
   
     ```
     D:\ProgramData\sbt\bin // 会自动添加
     ```
   
4. sbt进一步配置 

   [博客园](https://www.cnblogs.com/zeling/p/8494828.html)

   [CSDN](https://blog.csdn.net/leo3070/article/details/80040400)

   进入安装目录sbt/conf

   - 修改sbtconfig.txt，将以下添加至末尾 // 指定下载依赖包的位置

     ```
    -Dsbt.boot.directory=D:/ProgramData/sbt/data/.sbt/boot
     -Dsbt.global.base=D:/ProgramData/sbt/data/.sbt
     -Dsbt.ivy.home=D:/ProgramData/sbt/data/.ivy2
     -Dsbt.repository.config=D:/ProgramData/sbt/conf/repositories
     ```
   
   - 新建repo.properties文件 // 配置国内镜像

     ```
    [repositories]
       local
       aliyun: http://maven.aliyun.com/nexus/content/groups/public/
       typesafe: http://repo.typesafe.com/typesafe/ivy-releases/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
       sonatype-oss-releases
       maven-central
       sonatype-oss-snapshots
     ```
   
   - 打开cmd，输入sbt，下载依赖包

     > 这会需要一些时间

---