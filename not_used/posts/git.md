---
title: Git
tags:
  - git
  - Github
url: 14728.html
id: 14728
categories:
  - Computer
date: 2018-07-08 13:42:59
---

以前很少会写一些比较大型的程序，基本都是爬虫，工具…… 这次写了微信小程序，才大概明白了一些代码版本控制工具的用处。 因为经常逛Github，自然就使用了Git作为版本控制工具。 \[caption id="attachment_14730" align="alignnone" width="455"\]![git-tutorial](http://blog.echo.cool/wp-content/uploads/2018/07/git.jpg) git-tutorial\[/caption\] 所以也来谈一谈自己的理解： 首先，Git将一个工程分成了三个区域。 第一：代码开发区 第二：暂存区 第三：Head \[caption id="attachment_14731" align="alignnone" width="900"\]![trees](http://blog.echo.cool/wp-content/uploads/2018/07/git.png) trees\[/caption\] 当

git init

之后，计算机就自动初始化了一个代码仓库

你可以提出更改（把它们添加到暂存区），使用如下命令：
`git add <filename>`
`git add *`

这是 git 基本工作流程的第一步；使用如下命令以实际提交改动：

    git commit -m "代码提交信息"

之后，如果需要提交的Github 执行如下命令以将这些改动提交到远端仓库：

    git push origin master

可以把 _master_ 换成你想要推送的任何分支。

### 分支

分支是用来将特性开发绝缘开来的。在你创建仓库的时候，_master_ 是"默认的"分支。在其他分支上进行开发，完成后再将它们合并到主分支上。 \[caption id="attachment_14732" align="alignnone" width="900"\]![branches](http://blog.echo.cool/wp-content/uploads/2018/07/git-1.png) branches\[/caption\] 比如我的小程序： ![](http://blog.echo.cool/wp-content/uploads/2018/07/Capture.jpg) 可以看到多次的合并记录。 关于冲突处理，我还没有学习很透彻。将来再补 2018.7.8