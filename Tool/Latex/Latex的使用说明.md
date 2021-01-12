# Latex的使用说明
[TOC]

## 注释

在Latex中的注释有三种：
1. 用`%`注释一行文字
2. 用`iffalse...fi`注释一段文字 （非建议）
3. 用`begin{comment}...end{comment}`包含被注释的文字，需要在引言区引入对应宏包，即`usepackage{verbatim}`

## 参考文献

### 插入参考文献的步骤

1. 新建一个`bib`文件，如：`ref.bib`
2. 在`tex`文件中插入
   ```
   （文初）
    \usepackage{cite}

    (document开始后)
    \bibliographystyle{plain}

    （文末）
    \bibliography{ref.bib}
    ```
3. 编译顺序：`PDFLarex`, `BiLatex`, `PDFLatex`, `PDFLatex`

### 保持参考文献中的大小写

在排版时，`BibTex`会根据参考文献的格式将除了title中的第一个字符外的其他字符转换成小写，为了保持大写，可以使用左右大括号将需保留的字段括起来。

```
title = "Pascal, {C}, {Java}: were they all conceived in {ETH}?"
```

## Excel转Latex

工具：excel2latex.xla 
[使用Excel中导出latex代码的表格](https://blog.csdn.net/Jiajikang_jjk/article/details/80788501)

## Latex中文

[Latex中文utf-8编码的三种方式](https://www.cnblogs.com/dezheng/p/3874434.html)

## 跨栏与分栏

### 表格、图片在分栏情况下跨栏

表格横跨两栏
```
\begin{table*}...\end{table*}
```

图片横跨两栏
```
\begin{figure*}...\end{figure*}
```

## 英文字体

### Latex下使用`Times New Romance`字体

[LaTeX下使用Times New Roman字体的正确姿势](https://www.latexstudio.net/archives/9323.html)

使用`fontspec`宏包(推荐)
 ```
 \documentclass{article}
 \usepackage{fontspec}
 \setmainfont{Times New Roman}
 \usepackage{mathspec}
 \setallmathfont{Times New Roman}
 \begin{document}
 This is the typeface Times New Roman. Enjoy!
 \end{document}
 ```  

## Texmaker: 从PDF指定行跳转到源文件对应位置

1. 保证目录是英文目录
2. 在Texmaker中的PDF文件右击“点击跳转到行”或者ctrl+click

## 表格：设置表格宽度与文本宽度相同

```
\begin{table}[!ht]
\caption{Parameter values}\label{tab:parametervalues}
\begin{tabular*}{\hsize}{@{}@{\extracolsep{\fill}}lllllllllllll@{}}
\toprule
$p_{t}$  &21  &22  &20  &15  &10  &8   &5   &10  &18  &10  &14  &18\\
\midrule
$c_{t}$  &5   &13  &10  &10  &10  &10  &10  &10  &10  &10  &10  &10\\
$h_{t}$  &10  &5   &5   &5   &5   &5   &5   &5   &5   &5   &5   &5 \\
$s_{t}$  &100 &100 &100 &100 &100 &100 &100 &100 &100 &100 &100 &100\\
$d_{t}$  &30  &45  &50  &55  &45  &55  &90  &80  &90  &65  &80  &70 \\
\bottomrule
\end{tabular*}
\end{table}
```