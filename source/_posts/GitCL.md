---
title: Git 常用命令
date: 2017-04-14 21:55:25
categories: Git
thumbnail: "/images/Git/git.png"
---
![](/images/Git/git.png)

## 目的
本文章主要记录一些 Git 常用的命令行，方便开发过程中进行查阅和使用。

<!--more-->

### 配置参数
  `$ git config --global user.name “[name]”`
  设置全局用户名
  `$ git config --global user.email “[email address]”`
  设置全局邮箱

### 代码库操作
  `$ git init [project-name]`
  新建代码库
  `$ git clone [url]`
  下载远程代码库

### 修改操作
  `$ git status`
  列出所有新建的或者修改过的文件
  `$ git diff`
  查看未在缓存区的文件差异
  `$ git add [file]`
  添加新建或修改后的文件到缓存区
  `$ git diff --staged`
  查看已经在缓存区的文件差异
  `$ git reset [file]`
  将已缓存的文件移出缓存区
  `$ git commit -m “[备注信息]”`
  提交代码到代码库

### 分支操作
  `$ git branch`
  列出所有分支
  `$ git branch [branch-name]`
  创建新的分支
  `$ git checkout [branch-name]`
  切换分支
  `$ git merge [branch]`
  将某个分支合并到当前分支
  `$ git branch -d [branch-name]`
  删除分支

### 移动和移除文件
  `$ git rm [file]`
  删除文件
  `$ git rm --cached [file]`
  从代码库中移除文件记录，但保存本地文件
  `$ git mv [file-original] [file-renamed]`
  修改文件名

### 查看忽略的文件
  `$ git ls-files --other --ignored --exclude-standard`
  列出代码库中所有的忽略文件

### 保存当前工作环境
  `$ git stash`
  保存当前的工作环境
  `$ git stash pop`
  恢复最近保存的工作环境
  `$ git stash list`
  列出所有临时保存的记录
  `$ git stash drop`
  丢弃最近保存的工作环境

### 查看历史记录
  `$ git log`
  查看历史提交记录
  `$ git log --follow[file]`
  列出某个文件的所有版本历史
  `$ git diff [first-branch]...[second--branch]`
  查看两个分支的不同内容
  `$ git show [commit]`
  输出某次commit 的内容区别

### 切换工作环境到某个commit节点
  `$ git reset [commit]`
  将当前工作环境回滚到选中得节点，同时保留已修改的记录
  `$ git reset --hard [commit]`
  将当前工作环境回滚到选中得节点，已修改的记录全部清除

### 代码更新
  `$ git fetch [repo]`
  从repo库里面下载所有的历史记录，但并不和本地代码合并
  `$ git merge [repo] / [branch]`
  将repo的branch合并入当前本地branch
  `$ git push [alias][branch]`
  提交当前branch代码到远程库
  `$ git pull`
  下载所有的历史记录，并和本地代码进行merge操作
