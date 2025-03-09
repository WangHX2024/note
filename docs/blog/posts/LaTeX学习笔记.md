---
date: 
    created: 2024-07-31
authors: [wanghx]
draft: false   # 文章是否为草稿
counter: false # 页面上方是否显示字数统计和阅读时间估计（bolg文章不要开启，会导致排版混乱）
comments: true # 页面下方是否显示评论区
---

# LaTeX 学习笔记

利用 TeX 的强大功能，即使没有排版和程序设计知识的人也能生成高质量的文档，尤其适用于生成复杂表格和数学公式，非常适合科技和数学类文档的排版‌。
<!-- more -->

## 1.基本结构

```tex
% 基本示例
\documentclass[UTF8]{ctexart}

\title{文档标题}
\author{王浩雄}
\date{\today}

\begin{document}

\maketitle
\tableofcontents	%打印目录

\section{第一章标题}
第一章正文

\section{第二章标题}
第二章正文

\end{document}
```

## 2.基本格式

### 2.1 摘要

```tex
\begin{abstract}
摘要内容
\end{abstract}
```

### 2.2 引用

```tex
\begin{quote}
引用内容
\end{quote}
```

### 2.3 定理

```tex
\newtheorem{thm}{定理}	% 添加定理前需先在导言区进行定义，其中的“thm”“def”等名称是任取的
\newtheorem{def}[section]{定义}	% [section]为按节计数,它可以使每节的定理从头标号，例如：定理 2.1

\begin{thm}[勾股定理]	% 方括号表示可选参数
直角三角形的斜边等于两直角边的平方和。
\end{thm}
```

### 2.4 脚注和边注

```tex
这里需要加边注\marginpar{这是边注的内容。}
这里需要加脚注\footnote{这是脚注的内容。}
```

### 2.5 公式

```tex
\begin{equation} %公式单独成行
公式内容
\end{equation}

这是勾股定理的公式：$c^2=a^2+b^2$	% 公式和文字在同一行

公式参考：https://blog.csdn.net/ViatorSun/article/details/82826664/
公式编号规则参考：https://blog.csdn.net/AbaloneVH/article/details/125599538
```

### 2.6 换行与分页

```tex
多个空格视为同一个空格。

空格\quad，两个空格\qquad

按两次回车，或用命令\par，进行分段。

用\\，或用命令\newline，强制换行但不分段。

用\newpage分页
```

### 2.7 对齐方式

```tex
% 左对齐、右对齐、居中
\begin{flushleft}
\end{flushleft}

\begin{flushright}
\end{flushright}

\begin{center}
\end{center}
```

## 3.文字

### 3.1 字体族

| 字体族 | 带参数命令        | 声明命令      |
| ------ | ----------------- | ------------- |
| 罗马   | `\textrm{文字}` | `\rmfamily` |
| 无衬线 | `\textsf{文字}` | `\sffamily` |
| 打字机 | `\texttt{文字}` | `\ttfamily` |

### 3.2 字体形状

| 字体形状 | 带参数命令        | 声明命令      |
| -------- | ----------------- | ------------- |
| 加粗     | `\textbf{文字}` | `\bfseries` |
| 倾斜     | `\textsl{文字}` | `\slshape`  |

### 3.3 中文字体声明

| 字体族 | 声明命令      |
| ------ | ------------- |
| 宋体   | `\songti`   |
| 仿宋   | `\fangsong` |
| 楷书   | `\kaishu`   |
| 黑体   | `\heiti`    |

### 3.4 强调文字与下划线

- 强调：`\emph{文字}`，用于将直立体转为意大利体、将意大利体转为斜体。
- 下划线：`\underline{文字}`

### 3.5 字号

- 调整字号的声明命令（由小到大）

  |                   |            |
  | ----------------- | ---------- |
  | `\tiny`         | `\large` |
  | `\scriptsize`   | `\Large` |
  | `\footnotesize` | `\LARGE` |
  | `\small`        | `\huge`  |
  | `\normalsize`   | `\Huge`  |
- 中文字号带参数的声明命令：`\zihao{字号}`

  字号可填：0（初号）、-0（小初）、1、-1/2、-2……

### 3.6 彩色

```tex
\usepackage{color}	% 导入宏包

\color{red}	% 设置全局字体颜色为红色
\textcolor{blue}{某些文字}	% 设置某些文字的颜色为蓝色
\colorbox{blue}{某些文字}		% 设置某些文字的底色为蓝色
\fcolorbox{black}{green}{某些文字}	% 为某些文字的颜色设置为绿色，并在外围加黑色边框

\pagecolor{yellow}	% 设置页面颜色为黄色
```

## 4.列表

### 4.1 有数字自动编号的列表

```tex
\begin{enumerate}
	\item 条目1
	\item 条目2
	\item 条目3
\end{enumerate}
```

### 4.2 无数字自动编号的列表

```tex
\begin{itemize}
	\item 条目1
	\item 条目2
	\item 条目3
\end{itemize}
```

### 4.3 条目及描述

```tex
\begin{description}
	\item[条目名1]条目1
	\item[条目名2]条目2
	\item[条目名3]条目3
\end{description}
```

## 5.抄录与代码

### 5.1 抄录

抄录模式可以使在TeX代码中有意义的符号以原样显示

```tex
% 单行内的抄录
\verb!内容!	%在感叹号之间的内容为抄录的内容
\verb*!内容!	%在感叹号之间的内容为抄录的内容，且其中的空格将会显式打印出

% 成段抄录
\begin{verbatim}
内容
\end{verbatim}
```

### 5.2 代码

```tex
% 要使用listings宏包
\usepackage{listings}

% 设置
\lstset{
	basicstyle=\sffamily,
	keywordstyle=\bfseries,
	commentstyle=\rmfamily\itshape,
	stringstyle=\ttfamily,
	columns=flexible,	% 默认：fixd（等宽）
	numbers=left,	%行号
	numberstyle=\footnotesize,
	escapechar='	% 为在代码中插入中文注释，设置单引号'为逃逸字符，夹在两个单引号之间中文内容将得到支持
}

% 展现代码块
\begin{lstlisting}[language=C]
#include<stdio.h>
int main()
{
	return 0;	//'中文注释'
}
\end{lstlisting}

% 在行文段落中嵌入代码
\lstinline!要嵌入的代码!
```

## 6.标题与章节

### 6.1 标题和标题页

- 声明标题、作者、日期

  ```tex
  % 可分行
  % 花括号内可设置字体、字号
  \title{主标题\\副标题}
  \date{\today}
  \author{作者1\\作者单位1 \and 作者2\\作者单位2}
  
  \maketitle
  ```


- 单独成页的标题

  ```tex
  \begin{titlepage}
  % 手动排版
  \end{titlepage}
  % 页码将从titlepage的下一页开始统计
  ```

### 6.2 划分章节

| 层次 | 名称          | 说明                                    | 命令               |
| ---- | ------------- | --------------------------------------- | ------------------ |
| -1   | part          | 可选的最高层                            | `\part`          |
| 0    | chapter       | report、book、ctexrep、ctexbook的最高层 | `\chapter`       |
| 1    | section       | article、ctexart的最高层                | `\section`       |
| 2    | subsection    |                                         | `\subsection`    |
| 3    | subsubsection |                                         | `\subsubsection` |
| 4    | paragraph     |                                         | `\paragraph`     |
| 5    | subparagraph  |                                         | `\subparagraph`  |

- 不编号，且不加入目录的章节，需加星号（以chapter为例：`\chapter*{章节名}`)
- 编章节的文档必须出现最高层的章节，只有上一层章节存在时才能使用下一层章节
- 使用 `\appendix`表示附录的开始，章节的编号将变为字母（例：附录 A、附录 B）

示例：

```tex
\begin{document}

\maketitle
\tableofcontents

\section[在目录和页眉中显示的短标题]{在文档中显示的完整标题}
第一章正文

\section{第二章标题}
第二章正文

\end{document}
```

### 6.3 定制章节显示格式

ctex宏包的三个文档类：ctexbook、ctexrep、ctexart提供了 `\CTEXsetup`命令来设置章节的显示格式（只适用于 中文文档）

```tex
%格式：
\CTEXsetup[选项1 = 值1 , 选项2 = 值2]{对象}
%（这里的对象指的是：part、chapter等章节名）

%选项：name、number
\CTEXsetup[name={第,章}]{section}
\CTEXsetup[name={第,节}]{subsection}
\CTEXsetup[number={\chinese{section}}]{section}		%以上命令效果：第一节

%选项：format
\CTEXsetup[format={\raggedright\bfseries}]{section}	%设置节标题格式为左对齐、粗体，类似的选项还有nameformat、numberformat、titleformat

%选项：aftername 控制章节名和编号与后面标题之间的内容，通常为一定间距的空格或换行
\CTEXsetup[aftername={\\\vspace{2ex}}]{part}

%选项：beforskip、afterskip 控制章节标题前、后的垂直距离

%选项：indent 控制章节标题的缩进长度
```

### 6.4 多文件编译

```tex
% 一个例子
% chapter1.tex、chapter2.tex是和主文件位于同一文件夹的文件
\begin{document}
\include{chapter1}	% 这里是将chapter1.tex中的所有内容直接贴到此处，若有换页需求，可搭配使用\newpage
\include{chapter2}
\end{document}
```

## 7.页眉、页脚、页码

### 7.1 页码

重新从1开始计数：`\pagenumbering{roman}`

其中，roman为罗马数字，arabic为阿拉伯数字，alph为小写字母

### 7.2 页面格式

整体设置：`\pagestyle{格式}`

单独页面设置：`\thispagestyle{格式}`

| 格式       |                                      |
| ---------- | ------------------------------------ |
| empty      | 没有页眉页脚                         |
| plain      | 没有页眉，页脚是居中的页码           |
| headings   | 没有页脚，页眉是章节名称和页码       |
| myheadings | 没有页脚，页眉是页码和用户自定义内容 |

### 7.3 页眉、页脚的高级自定义

- 导入 `fancyhdr`宏包

```tex
\usepackage{fancyhdr}
\pagestyle{fancy}	% 导入宏包，并设置页面格式为fancy
\fancyhf{}	% 	清除所有页眉页脚
```

- 位置代码（三位字母）
  - 第一位：H（页眉）、F（页脚）
  - 第二位：E（偶数页）、O（奇数页）（对于单面文档，所有页面都看做奇数页进行处理）
  - 第三位：L（左）、C（中）、右（R）
- 代用命令
  - `\rightmark`：节标题
  - `\leftmark`：章标题
  - `\thepage`：当页页码
- 设置命令

```tex
\fancyhf[位置代码]{填充内容}

% 例子：设置奇数页页脚居中显示页码
\fancyhf[FOC]{\thepage}
```

- 页眉与页脚线

`fancy`页面风格自动添加页眉与页脚线，默认线宽为0.4pt。线宽修改方式如下（线宽为0，则为不显示线条）：

```tex
\renewcommand\headrulewidth{0.4pt}
\renewcommand\footrulewidth{0.4pt}
```

## 8.文档类、页面尺寸、分栏

### 8.1 文档类

- 基本文档类：article、report、book

  ctex文档类（专为中文设计）：ctexart、ctexrep、ctexbook

- 声明文档类：`\documentclass[选项1,选项2...]{ctexart}`

- 基本文档类的选项：

  | 类型         | 选项                                                                        |
  | ------------ | --------------------------------------------------------------------------- |
  | 纸张大小     | a4paper、a5paper、b5paper、letterpaper（默认）、leagalpaper、executivepaper |
  | 纸张方向     | landscape（横向）、不填（纵向，默认）                                       |
  | 单双面       | oneside、twoside                                                            |
  | 正文字号大小 | 10pt（默认）、11pt、12pt                                                    |
  | 分栏         | onecolumn、twocolumn                                                        |
  | 标题格式     | titlepage（标题独自成页）、notitlepage（标题不独自成页）                    |

- ctex文档类除上述选项外，还支持的选项：

  | 类型                     | 选项                                   |
  | ------------------------ | -------------------------------------- |
  | 正文字号大小             | c5size（五号字）、c4size（四号字）     |
  | 中文编码                 | GBK、UTF8                              |
  | 标题、编号、日期语言选择 | cap（中文，默认）、nocap（英文）       |
  |                          | punct（启用，默认）、nopunct（关闭）   |
  |                          | indent（启用，默认）、noindent（关闭） |
  | 启用hyperref包           | hyperref（启用）、不填（默认）         |

### 8.2 页面尺寸

- 使用宏包geometry进行设置

  ```tex
  \usepackage{geometry}
  \geometry{a4paper,left=3cm,right=3cm,top=3cm,bottom=3cm}	% 设置纸张大小为a4，上下左右边距均为3cm
  
  \geometry{paperheight=10cm,paperwidth=5cm}	% 设置纸张大小长10cm、宽5cm
  ```

### 8.3 分栏

- 导入 `multicol`宏包

```tex
\usepackage{multicol}

% 正文
\begin{multicols}{2}	% 2为栏数
...
\end{multicols}

% 强制分栏
\columnbreak
```

## 9.目录与引用

### 9.1 目录

- 打印目录

  ```tex
  \tableofcontents
  ```
- 改变编号深度和目录显示的深度

  ```tex
  \setcounter{secnumdepth}{4}		% 增加编号深度至4
  \setcounter{tocdepth}{4}		% 增加目录深度至4
  ```

- 使用命令在正文中直接写入一条目录项

  ```tex
  \addcontentsline{toc}{section}{title}
  
  % 新增了一条名为title的section级别目录项
  ```

- 不编号，且不加入目录的章节，需加星号（以chapter为例：`\chapter*{章节名}`)

### 9.2 交叉引用

标签与引用

```tex
\label{labelname} 	% 在需要被引用处添加标签

\ref{labelname}		% 产生被引用对象的编号，例如：3.1
\pageref{labelname}	% 产生被引用对象的页码，例如：166

% LastPage是一个特殊的标签，可用以下命令产生总页码
\pageref{LastPage}
```

### 9.3 超链接

- 以下功能机基于 `hyperref`宏包

  ```tex
  \usepackage{hyperref}	% 导入宏包
  
  % 若使用ctex文档类，则需在声明文档类时加hyperref选项
  \documentclass[hyperref,UTF8]{ctexart}
  ```

- `hyperref`宏包的选项

  | 选项              | 类型与默认值    | 说明                              |
  | ----------------- | --------------- | --------------------------------- |
  | colorlinks        | bool，默认false | 超链接用彩色显示                  |
  | bookmarks         | bool，默认true  | 为目录添加超链接，生成PDF目录书签 |
  | bookmarksnumbered | bool，默认false | PDF目录标签带编号                 |
  | pdftitle          | 文本            | 文档标题，在PDF属性中显示         |
  | pdfauthor         | 文本            | 文档作者，在PDF属性中显示         |
  | pdfsubject        | 文本            | 文档主题，在PDF属性中显示         |
  | pdfkeyword        | 文本            | 文档关键字，在PDF属性中显示       |

    选项设置示例

```tex
\hyperstart{
	colorlinks=true,
	bookmarks=true,
	pdftitle={文档标题}
}
```

- URL地址超链接

  ```tex
  \url{http://wanghx.work}	% 带超链接的URL
  \nolinkurl{http://wanghx.work}	% 不带超链接的URL
  \href{http://wanghx.work}{点击进入我的个人主页}	%使文字超链接指向URL
  ```

- 文件地址超链接

  ```tex
  \path{文件路径}
  ```

- 标签超链接

  ```tex
  \hypertarget{labelname}{链接文字} 	% 在需要被引用处添加标签
  
  \hyperref{labelname}{链接文字}		% 产生链接到添加标签处的超链接
  ```

## 10.插图

- 插入单张图片

  ```tex
  \usepackage{graphics}	% 导入宏包graphics，用于插图
  \usepackage{caption}	% 导入宏包caption，用于显示标题
  
  \begin{figure}
  \centering
  
  \includegraphics[width=2cm,height=1cm]{文件名}	% 插入图片(指定宽高)
  \includegraphics[scale=0.5]{文件名}	% 插入图片(指定缩放比例)
  
  \caption{图片标题}
  
  \end{figure}
  ```

## 11.幻灯片

- 幻灯片的文档类：beamer

  ```tex
  \documentclass{beamer}
  \usepackage[UTF8,noindent]{ctexcap}	% 若在beamer中使用中文，则需导入此宏包（其中，ctexcap会翻译图表等环境名称，若更改为ctex则只引用必要的中文）
  
  \begin{document}
  ...
  \end{document}
  ```

- 帧：每页幻灯片称为一帧

  ```tex
  % 法一
  \begin{frame}
  	\frametitle{标题}
  	\framesubtitle{小标题}	% 这里的标题与小标题不是下面提到的“分节与目录”中的标题
  \end{frame}
  
  % 法二
  \begin{frame}{标题}{小标题}
  \end{frame}
  ```

- 标题与文档信息

  ```tex
  % 导言区设置标题与文档信息
  \title{标题}
  \subtitle{副标题}
  \institute{单位}
  \author{作者}
  \date{\today}
  \logo{\includegraphics{照片名称}}
  
  % 输出标题页（需要在帧中操作）
  \begin{frame}
  \titlepage
  \end{frame}
  ```

- 分节与目录

  - 在分节时设置的标题会显示在目录中，但是否显示在幻灯片上取决于主题样式
  - 使用 `\tableofcontents`产生目录，需要在帧中操作
  - 使用 `\section、\subsection、\subsubsection、\part`等命令对文档分节，最高层级为section，需要在帧外操作
  - 使用 `\tableofcontents[currentsection]、\tableofcontents[currentsubsection]`产生当前章节的目录，需要在帧中操作
  - 使用 `\titlepage、\sectionpage、\subsectionpage、\partpage`等命令产生当前章节的标题页，需要在帧中操作
  - 示例：

    ```tex
    \begin{frame}{目录}
    \tableofcontents
    \end{frame}
    
    \section{勾股定理在古代}
    \begin{frame}
    \sectionpage
    \end{frame}
    ```

- 停顿

  - 在帧中使用命令 `\pause`，可使同一帧的内容显示在多页PDF文档中

- 区块

  - beamer定义了三种区块环境：block、alertblock、exampleblock，它们的配色不同，但用法和样式大致相同

  - 示例：在一帧上添加两个区块

    ```tex
    \begin{frame}
    
    \begin{block}{块标题}
    这是区块
    \end{block}
    
    \pause	% 在这里引入停顿
    
    \begin{block}{}	% 没有标题的区块
    这是另一个区块
    \end{block}
    
    \end{frame}
    ```
  - 定理、证明等环境也将以区块的形式展现

- 主题风格

  - 主题由内部主题、外部主题、色彩主题、字体主题组合而成

  - 使用已搭配好的主题，在导言区使用命令 `\usetheme{主题名称}`设定
  
  - 自行搭配主题，在导言区使用命令如下：

    ```tex
    \useinnertheme{主题名称}
    % 可选：default、circles、rectangles、rounded、inmargin
    
    \useoutertheme{主题名称}
    % 可选：default、infolines、miniframes、smoothbars、sidebar、split、shadow、tree、smoothtree
    
    \usecolortheme{主题名称}
    % 可选：default、albatross、beaver、beetle、crane、dolphin、dove、fly、lily、orchid、rose、seagull、seahorse、sidebartab、structure、whale、wolverine
    
    \usefonttheme{主题名称}
    % 可选：default、serif
    ```

## 12.参考文献

bib文件的属性用法和特点：https://blog.csdn.net/AbaloneVH/article/details/131604893

在文中引用参考文献时，使用 `\cite{引用关键词}`
