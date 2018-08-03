---
title: "Markdown学习笔记"
date: 2018-07-26T00:00:01+08:00
draft: true
---

# 一、快速入门：

## 1.Headers 标题：
# H1
## H2
### H3
...
###### H6

一级标题
===

二级标题
---

## 2.Emphasis 文本强调

*斜体* or _强调_

**加粗** or __加粗__

***粗斜体*** or ___粗斜体___

## 3.list列表

Unordered 无序列表

* 无序列表
* 子项
* 子项

+ 无序列表
+ 子项
+ 子项

- 无序列表
- 子项
- 子项

Ordered 有序列表

第一种写法：
1. 第1行
2. 第2行
3. 第3行

第二种写法：
1. 第1行
- 第2行
- 第3行

组合使用这些列表

* 产品介绍（子项无项目符号）
    此时子项，要以一个制表符或者4个空格缩进
 
* 产品特点
    1. 特点1
    - 特点2
    - 特点3
* 产品功能
    1. 功能1
    - 功能2
    - 功能3

## 4.Links连接
Inline-style 内嵌方式:
[W3Cschool](http://www.w3cschool.cn/ "W3Cschool")

Reference-style 引用方式:
[链接文字][id]
[id]: http://www.w3cschool.cn/ "标题文字"

Relative reference to a repository file 引用存储文件：
[链接文字](../path/file/readme.text "标题文字")

[链接文字][]
[链接文字]: http://www.w3cschool.cn/

Email 邮件：
<example@w3cschool.cn>

## 5.Images 图片

Inline-style 内嵌方式：
![替代文字](http://statics.w3cschool.cn/images/w3c/index-logo.png "标题文字")

Reference-style 引用方式：
![替代文字][logo]
[logo]: http://statics.w3cschool.cn/images/w3c/index-logo.png "标题文字"

## 6.Code and Syntax Highlighting 代码和语法高亮：
标记一小段行内代码：
```
包裹起来
```

语法高亮：
```html
    <div>Syntax Highlighting</div>
```
(html/css/javascript/php/python)

## 7.Block Code 代码分组(代码区块)：
Blockquotes 引用：
> Email-style angle brackets
> are used for blockquotes.
> > And, they can be nested.
> #### Headers in blockquotes
> * You can quote a list.
> * Etc.

## 8.Hard Line Breaks 换行：
在一行的结尾处加上2个或2个以上的空格，也可以使用</br>标签
第一行文字，  
第二行文字

## 9.Horizontal Rules 水平分割线：
***
* * *
- - -

## 10.Escape character 转义符(反斜杠)：
Markdown 可以利用反斜杠来插入一些在语法中有其它意义的符号，例如：如果你想要用星号加在文字旁边的方式来做出强调效果，你可以在星号的前面加上反斜杠：
\*literal asterisks\*

Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

\反斜杠  `反引号  *星号  _下划线  {}花括号  []方括号  ()括弧  #井字号  +加号  -减号  .英文句 !感叹号

## 11.Additional 补充:
Markdown也支持传统的HTML标签。

比如一个链接，你不太喜欢Markdown的写法，也可以直接写成

<a href="https://www.w3cschool.cn/">W3Cschool</a>

# 二、Markdown 概述

## 1.Markdown 兼容HTML

HTML是一种发布格式，MarkDown是一种书写格式；

## 2.Markdown 特殊字符自动转换

HTML中两个字符：< 和 &符号，要写成实体形式 &lt; 和 &amp; 形式；
版权符号@，写成 &copy;