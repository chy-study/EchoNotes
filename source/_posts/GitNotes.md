---
title: Git 笔记
date: 2020-07-20 22:03:31
top: ture
categories:
- 笔记
tags:
- git
---

Git是版本管理工具，功能很强大
<!--more-->
#### GitHub Pages部署Vue静态页面
- 将dist目录下的所有文件夹推送至远程仓库的gh-pages分支
   - 强制添加dist文件夹
   `git add -f dist`
   - 提交到本地暂存区
   `git commit -m '注释...'`
   - dist目录下的代码推送到远程仓库
   `git subtree push --prefix dist origin gh-pages`