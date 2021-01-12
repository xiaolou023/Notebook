# IDEA配置CPLEX, CP

## CPLEX的配置

> http://oropt.top/cplex/note_java.html

第一步：添加`cplex.jar`

- `File -> Project  structure -> Modules (name: project name) -> add (+) cplex.jar`
- `Cplex.jar`的安装目录：`D:\Program  Files\IBM\ILOG\CPLEX_Studio128\cplex\lib`

第二步：配置 `-Djava.library.path`

- `Run -> Configurations -> VM options` 添加 `-Djava.library.path="D:\Program Files\IBM\ILOG\CPLEX_Studio128\cplex\bin\x64_win64"`
- 注意引号

## CP的配置

第一步：添加`ILOG_CP.jar`

- `File  -> Project structure -> Modules (name: project name) -> add (+) ILOG.CP.jar`
- `ILOG_CP.jar`的安装目录：`D:\Program Files\IBM\ILOG\CPLEX_Studio128\cpoptimizer\lib`

第二步：配置 `-Djava.library.path`

- `Run -> Configurations -> VM options` 添加` -Djava.library.path="D:\Program Files\IBM\ILOG\CPLEX_Studio128\cplex\bin\x64_win64;D:\Program  Files\IBM\ILOG\CPLEX_Studio128\cpoptimizer\bin\x64_win64"`
- 注意引号