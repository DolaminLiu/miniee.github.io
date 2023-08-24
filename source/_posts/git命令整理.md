title: git命令整理
tags:
  - Git
author: Mia Liu
categories:
  - 前端
date: 2018-08-11 11:26:00
photos: 
- /upload/git.jpg
---
<h3>Git常用命令整理</h3>


查看分支：&nbsp;&nbsp;git branch  
创建分支：&nbsp;&nbsp;git branch <name>  
切换分支：&nbsp;&nbsp;git checkout <name>  
创建+切换分支：&nbsp;&nbsp;git checkout -b <name>  
合并某分支到当前分支：&nbsp;&nbsp;git merge <name>  
看分支的合并情况: &nbsp;&nbsp;git log --graph --pretty=oneline --abbrev-commit  
删除分支：&nbsp;&nbsp;git branch -d <name>  
删除untracked files: &nbsp;&nbsp;git clean -nf  
丢弃一个没有被合并过的分支,强行删除: &nbsp;&nbsp;git branch -D <name>  
查看远程库信息: &nbsp;&nbsp;git remote -v  
新建一个标签: &nbsp;&nbsp;git tag <tagname>  
指定标签信息: &nbsp;&nbsp;git tag -a <tagname> -m "blablabla..."  
查看所有标签: &nbsp;&nbsp;git tag  
查看标签信息： &nbsp;&nbsp;git show tag <tagname>  
推送一个本地标签: &nbsp;&nbsp;git push origin <tagname>  
推送全部未推送过的本地标签： &nbsp;&nbsp;git push origin --tags  
删除一个本地标签： &nbsp;&nbsp;git tag -d <tagname>  
删除一个远程标签： &nbsp;&nbsp;git push origin :refs/tags/<tagname>
  


***
<h3>bug分支</h3>  

>当前正在dev上进行的工作还没有提交  $ git stash 可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作 

* 首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支  
git checkout master
* 修复然后提交   
git commit -m "modify info"
* 修复完成后，切换到master分支，并完成合并,最后删除issue-101分支  
git checkout master  
git merge issue-101  
git branch -d issue-101
* 接着回到dev分支   
git checkout dev  
* 工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
  * 一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
  * 另一种方式是用git stash pop，恢复的同时把stash内容也删了
***

<h3>多人协作</h3>
* 首先，可以试图用git push origin <branch-name>推送自己的修改；
* 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
* 如果合并有冲突，则解决冲突，并在本地提交；
* 没有冲突或者解决掉冲突后
* 如果希望log整齐，可以在这里用git rebase
* 再用git push origin <branch-name>
* 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

***
> **本地新建的分支如果不推送到远程，对其他人就是不可见的**
从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
***
> **git pull也失败了** 原因是没有指定本地dev分支与远程origin/dev分支的链接
根据提示，设置dev和origin/dev的链接
$ git branch --set-upstream-to=origin/dev dev