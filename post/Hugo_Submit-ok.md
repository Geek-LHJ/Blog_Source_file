---
title: "hugoBlog_提交到Github_Page"
date: 2018-07-25T10:21:41+08:00
draft: true
---

# Markdown文件

1. 写好对应的Markdown文件(注意日期的问题，参考之前的);
2. 将文件保存在 HugoBlog/content/post 文件夹下面（myBlog）;

# 上传写好的Markdown 文件

1. 本地服务器进行更新操作

```
1. 进入HugoBlog的目录中进行 gitbash 当前目录；
2. $ hugo --theme=hyde --buildDrafts           #更新本地文件
3. $ hugo server --theme=hyde --buildDrafts    #开启hugo本地服务器
[http://localhost:1313/]    #本地运行端口
```

2. 上传更新操作

```
1. 切换到 HugoBlog/public 目录中，进入git 环境
2. git add . && git commit -m "update xxx" && git push #这个是推送master分支上的文件，里面包含的是生成的Blog 的网页所有文件；
3. git checkout src     #切换至src分支，该分支中包含 Markdown源文件；
git add . && git commit -m "update xxx" && git push     #推送远程仓库

```
