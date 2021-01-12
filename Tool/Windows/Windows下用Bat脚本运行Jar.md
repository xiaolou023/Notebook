# Windows下用Bat脚本运行Jar

> [windows下从bat脚本运行jar包](https://blog.csdn.net/hz_1943/article/details/51784740)

1. 从ECLIPSE导出`Runable jar`
   
    1)、选择需要打包的项目，右键 `Export`
   
    2)、选择`Runnable JAR file`,然后点击 `Next`
   
    3)、选择`jar`包运行的`main`类、以及定义`jar`包的名字、保存的地方

    举例：你可能会得到一个`tsp.jar`和`tsp_lib`的文件夹。其中`lib`文件夹中包含了你需要的外部`jar`包，如`cplex.jar`。

2. 新建一个文件夹，把`tsp.jar`, `tsp_lib`, `data`, `run.bat`放入其中。其中`run.bat`的形式如下:
   
    ```
    java [可能有你对java vm的设置] -jar rspspl2.jar [可能有你自己的输入参数]
    ```

3. 你可以选择直接双击`run.bat`文件执行，也可以选择把`run.bat`文件拖入`cmd`执行。
   
4. 如果你需要把输出内容放在一个文本中，可以在`run.bat`中添加`>> E:\RunTest\log.txt`,即：
   
   ```
   java -jar rspspl2.jar >> E:\RunTest\log.txt
   ```


