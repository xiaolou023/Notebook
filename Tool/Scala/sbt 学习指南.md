# sbt 学习指南

[官网 sbt 用户手册](https://www.scala-sbt.org/1.x/docs/zh-cn/Getting-Started.html)

[下载地址](https://www.scala-sbt.org/download)：下载 msi

### sbt 常用命令

[官方文档](https://www.scala-sbt.org/1.x/docs/zh-cn/Running.html)

```bash
sbt compile  # 编译
sbt run      # 运行
sbt -mem 32000 run # 设置内存上限运行
sbt run -Djava.library.path=/Users/naiquh/Applications/CPLEX_Studio128/cplex/bin/x86-64_osx:/Users/naiquh/Applications/CPLEX_Studio128/cpoptmizer/bin/x86-64_osx:/Users/naiquh/Applications/CPLEX_Studio128/opl/bin/x86-64_osx: #如果用到cplex但无设置环境变量 
sbt test     # 执行测试
sbt doc      # 生成API文档，路径 ./target/scala-2.xx/api/index.html
```











