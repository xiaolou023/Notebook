[如何在右键新建项中添加Typora新建Markdown文件快捷选项](https://blog.csdn.net/windowsxp2018/article/details/109140956)


1. 新建一个test.txt 文本文件,写入以下代码内容:

   ```
    Windows Registry Editor Version 5.00
    [HKEY_CLASSES_ROOT\.md]
    @="Typora.md"
    "Content Type"="text/markdown"
    "PerceivedType"="text"
    [HKEY_CLASSES_ROOT\.md\ShellNew]
    "NullFile"=""
   ```

2. 修改.txt后缀为.reg 的注册表文件即可
3. 然后双击运行即可! 现在右键的新建项中就会有markdown的快捷新建方式了!