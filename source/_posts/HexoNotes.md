---
title: HexoNotes
date: 2020-08-07 15:30:13
categories:
- 笔记
tags:
- hexo
---

Hexo：一个快速、简洁且高效的博客框架，Hexo 使用 Markdown（或其他渲染引擎）解析文章，生成静态网页。
<!--more-->
### 常用命令
- 清除缓存文件 (db.json) 和已生成的静态文件 (public)：
`hexo clean`
- 生成静态文件
`hexo g`
- 本地启动服务
`hexo s`
- 部署代码到远程仓库
`hexo d`

### 写作
- 创建新文章或者新的页面
`hexo new [layout] <title>`
Hexo有三种布局：post、page 和 draft
 
### Front-matter
- 文件最上方以 --- 分隔的区域，用于指定个别文件的变量
- 参数：
   - layout, title, date, updated, comments, tags, categories, permalink
   - 例如:
   ```
	categories:
	 - Diary
	tags:
	 - PS3
	 - Games
   ```