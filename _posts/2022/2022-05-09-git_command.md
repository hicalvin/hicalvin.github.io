---
layout: post
title:  "Often Used Git Command"
date:   2022-05-09 19:23:50 +0800
category: tech
---

Just work as a cheatsheet.

1. 查看当前分支：  `git branch`
2. 查看所有分支：  `git branch -a`
3. 切换分支：`git checkout  分支名`
4. 新建分支：`git checkout -b 分支名`
5. 推送本地分支到远程分支：`git push origin 本地分支名:远程分支名`
6. 让本地分支与远程分支建立关联：`git branch --set-upstream-to=origin/分支名`
7. 删除本地分支：`git branch -d 分支名`
8. 删除远程分支：`git push origin:分支名 或 git push origin` --delete 分支名
9. 将本地未push的分叉提交历史整理成直线，使查看历史提交更容易. git rebase
10. Fast-forward指的是这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。缺点是会丢失合并信息。如果禁用可以用 `--no-ff` `git merge --no-ff -m "merge with no-ff" dev`


### Reference

1. [Know basic knowledge of Git](https://www.bilibili.com/video/BV1FE411P7B3?p=1)
2. [Practice on how to use Git](https://www.bilibili.com/video/BV1i44y1e7hv)
3. [All about Git](https://gitee.com/all-about-git)
4. [Learn Git Game](https://oschina.gitee.io/learn-git-branching/)
5. [廖雪峰的Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
