---
layout:     post   				    # 使用的布局（不需要改）
title:    Git Bash 常用操作				# 标题 
subtitle:  实现 push 、status、commit , 仅仅是目前用到的  #副标题
date:       2019-06-13 				# 时间
author:     helexy22 						# 作者
# header-img: img/post-bg-2015.jpg  #这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Git
---

<div><img align=center src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png"/></div>

## 01 Git  status-查看状态
`git status`
git status 这个命令查看状态，这个命令可以算是使用最频繁的一个命令了，建议大家没事就输入下这个命令，来查看你当前 git 仓库的一些状态

## 02 gitignore 忽略某些文件

**对于未入库的文件，创建。gitignore 文件**

`touch .gitignore`       

在文件中写入需要忽略的文件（如：*.diff  ），或者不遵循忽略原则的特例（文件前加“！”）

**对于已入库的文件**

`git update-index --assume-unchanged FILENAME`    路径+文件名

若以后不想忽略该文件的修改，则输入命令：`git update-index --no-assume-unchanged FILENAME`

## 03 Git add -添加到暂存区

可以提交单个文件到仓库中，比如 a.md 文件

代码实例：

`git add a.md`

当修改多个文件后，根据文件名提交比较麻烦，这时可以提交修改的所有文件

代码实例：

`git add  .`

提交后，为确认是否提交成功，可以再次使用 `git status` 查看状态

## 04 Git commit -提交

以上命令代表我们已经正式进行提交 ，一般默认提交到 master 分支，如果有其他分支存在，需要主要提交到的分支名。

代码实例：

`git commit  -m '输入提交的注释'`

注意如果是修改多个文件，并且有多个注释，建议使用单个 `git add` 命令，在进行 commit 操作，否则所有的修改文件具有相同的注释。

### add 和 commit  的区别

首先 `git add` 是先把改动添加到一个「暂存区」 ，你可以理解成是一个缓存区域，临时保存你的改动，而 `git commit` 才是最后真正的提交。这样做的好处就是防止误提交，当然也有办法把这两步合并成一步，不过后面再介绍，建议新手先按部就班的一步步来。

## 05 Git push-推送

如果你本地代码有更新了，那么就需要把本地代码推到远程仓库，这样本地仓库跟远程仓库就可以保持同步了。

代码实例：

- `git push origin master`

- `git push -u origin master `

其中，`-u`可以在推送的同时，将 origin 仓库的 master 分支设置为本地仓库当前分支的 upstream  。将来从远程仓库获取内容时，本地仓库的这个分支就可以直接从 origin 的 master 分支获取内容，省去了另外添加参数的麻烦  

**如果是推送到到其他分支，则更换 branch 的名词即可。**

代码实例：

`git push origin develop`

由于受到"Black Lives Matter"运动的影响，GitHub 新的源代码仓库将默认被命名为 “main”，而不是原先的"master"。历史的默认是 master，需要把本地的 master 仓库名称修改为远端的 main。

```shell
git branch -m master main
```

## 06 Git branch -查看分支

`branch` 即分支的意思，分支的概念很重要，尤其是团队协作的时候 ，需要写作双方创建不用的分支，然后再进行分支合并。可以使用`git branch`命令查看分支状况，主分支 master 会有 `*` 号提示。

对分支进行的操作有创建、切换、合并、删除、标注（标签）等。

- `git brach` ，查看当前分支

- `git branch -a`，查看当前分支的相关信息 ，可以同时显示本地仓库和远程仓库的分支信息  。

## 07 Git clone & Git Pull-远程仓库

获取远程仓库和获取远程仓库的 feature-D 分支

`git clone git@github.com:helexy22/AndroidDemo_Test.git`

默认在 `master`分支下，同时系统会自动将 `origin `设置成该远程仓库的标识符  。

### git remote add

添加远程仓库，自动将远程仓库的名称设置为 origin

`git remote add git@github.com:helexy22/AndroidDemo_Test.git`

### git pull-获取远程分支

取回远程主机某个分支的更新，再与本地的指定分支合并。

`git pull origin master:brantest`

将远程主机`origin`的`master`分支拉取过来，与本地的`brantest`分支合并。

## 08 GitHub 上添加 SSH key  

本地的 id_rsa 密钥跟 GitHub 上的 id_rsa.pub 公钥进行配对，授权成功才可以提交代码。

```shell
$ ssh #检查 SSH 状态
$ ssh-keygen -t rsa #生成本地密匙，会生成两个文件 id_rsa 和 id_rsa.pub 
```

Linux/Mac 系统 在 ~/.ssh 下，win 系统在 /c/Documents and Settings/username/.ssh 下，接下来要做的是把 `id_rsa.pub `的内容添加到 GitHub 的`SSH and GPG keys`  上 。 

## Wiki

```shell
$ git init  # 在当前目录新建一个 Git 代码库
$ git clone [url]  # 下载一个项目和它的整个代码历史
$ git config --list # 显示当前的 Git 配置
$ git config -e [--global]  # 编辑 Git 配置文件
$ git add  # 添加指定文件到暂存区
$ git rm   # 删除工作区文件，并且将这次删除放入暂存区
$ git commit -m [message]  # 提交暂存区到仓库区
$ git commit -a # 提交工作区自上次 commit 之后的变化，直接到仓库区
$ git commit --amend -m [message]   # 使用一次新的 commit，替代上一次提交 如果代码没有任何新变化，则用来改写上一次 commit 的提交信息
$ git commit --amend [file1] [file2] ...  # 重做上一次 commit，并包括指定文件的新变化

# 分支相关
$ git branch  # 列出所有本地分支
$ git branch -r  # 列出所有远程分支
$ git branch [branch-name]  # 新建一个分支，但依然停留在当前分支
$ git checkout [branch-name]  # 切换到指定分支，并更新工作区
$ git checkout -b [branch]  # 新建一个分支，并切换到该分支
$ git branch [branch] [commit]  # 新建一个分支，指向指定 commit
$ git checkout -b [branch] [tag]  # 新建一个分支，指向某个 tag
$ git branch --track [branch] [remote-branch]  # 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --set-upstream [branch] [remote-branch]  # 建立追踪关系，在现有分支与指定的远程分支之间
$ git merge [branch]  # 合并指定分支到当前分支
$ git cherry-pick [commit]  # 选择一个 commit，合并进当前分支
$ git branch -d [branch-name]  # 删除分支
$ git push origin --delete [branch-name] # 删除远程分支
$ git branch -dr [remote/branch]  # 删除远程分支

# 标签
$ git tag  # 列出所有 tag
$ git tag [tag] # 新建一个 tag 在当前 commit
$ git tag [tag] [commit] # 新建一个 tag 在指定 commit
$ git show [tag]  # 查看 tag 信息
$ git push [remote] [tag]  # 提交指定 tag
$ git push [remote] --tags   # 提交所有 tag

# 查看
$ git status # 显示有变更的文件
$ git log # 显示当前分支的版本历史
$ git log --stat # 显示 commit 历史，以及每次 commit 发生变更的文件
$ git log --follow [file] # 显示某个文件的版本历史，包括文件改名
$ git log -p [file] # 显示指定文件相关的每一次 diff
$ git blame [file] # 显示指定文件是什么人在什么时间修改过
$ git diff # 显示暂存区和工作区的差异
$ git diff --cached [file] # 显示暂存区和上一个 commit 的差异
$ git diff HEAD # 显示工作区与当前分支最新 commit 之间的差异
$ git diff [first-branch]...[second-branch] # 显示两次提交之间的差异
$ git show [commit] # 显示某次提交的元数据和内容变化
$ git show --name-only [commit] # 显示某次提交发生变化的文件
$ git show [commit]:[filename] # 显示某次提交时，某个文件的内容
$ git reflog # 显示当前分支的最近几次提交

# 远程
$ git fetch [remote] # 下载远程仓库的所有变动
$ git remote -v  # 显示所有远程仓库
$ git remote show [remote]  # 显示某个远程仓库的信息
$ git remote add [shortname] [url]  # 增加一个新的远程仓库，并命名
$ git pull [remote] [branch]  # 取回远程仓库的变化，并与本地分支合并
$ git push [remote] [branch] # 上传本地指定分支到远程仓库
$ git push [remote] --force # 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --all # 推送所有分支到远程仓库

# 撤销
$ git checkout [file] # 恢复暂存区的指定文件到工作区
$ git checkout [commit] [file] # 恢复某个 commit 的指定文件到工作区
$ git checkout . # 恢复上一个 commit 的所有文件到工作区
$ git reset [file] # 重置暂存区的指定文件，与上一次 commit 保持一致，但工作区不变
$ git reset --hard # 重置暂存区与工作区，与上一次 commit 保持一致
$ git reset [commit] # 重置当前分支的指针为指定 commit，同时重置暂存区，但工作区不变
$ git reset --hard [commit] # 重置当前分支的 HEAD 为指定 commit，同时重置暂存区和工作区，与指定 commit 一致
$ git reset --keep [commit] # 重置当前 HEAD 为指定 commit，但保持暂存区和工作区不变
$ git revert [commit] # 新建一个 commit，用来撤销指定 commit，后者的所有变化都将被前者抵消，并且应用到当前分支
```

Reference:
- [wiki.geekplux](https://wiki.geekplux.com/)
