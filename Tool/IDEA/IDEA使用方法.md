# IDEA使用方法

[TOC]

## 为Java文件设置作者信息

`File -> Setting-> Editor -> File and Code Templates -> Includes -> File Header`

```java
/** 
* @author by Ying 
* @version ${DATE}
*/ 
```

![idea_添加作者信息](../../../Images/idea_添加作者信息.png)

## 添加Jar包

`File -> Project Structure -> Modules -> Dependencies-> '+'`

![idea_添加jar](../../../Images/idea_添加jar.PNG)

## 导出可执行Jar

> https://www.jetbrains.com/help/idea/2019.1/creating-and-running-your-first-java-application.html?utm_campaign=IC&utm_content=2019.1&utm_medium=link&utm_source=product#package

备注：在没有使用CPLEX时，操作简单，仅仅使用CPLEX也还OK，容易出错的是使用CP时。

1. `File -> Project Structure`

2. `Artifacts -> '+' -> Jar -> 'from modules with dependencies'`

3. 配置`Main Class`: `MainTest.class`

4. 配置`Jar files from libraries`: `copy...`

5. 配置`Directory for META-INF/MAINFEST.MF` (default)

6. 回到IDEA的主菜单，选择`Build - Build Artifacts`下的`Build`或者`Rebuild`即可生成最终的可运行的jar。在`D:\XXX\XX\out\artifacts\XX_jar`下面找到生成的目标jar

![idea_导出jar](../../../Images/idea_导出jar_1.PNG)

![idea_导出jar](../../../Images/idea_导出jar_2.PNG)

