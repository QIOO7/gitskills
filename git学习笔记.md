# git常用命令

(仓库地址：`git@github.com:QIOO7/gitskills.git`)

## 创建版本库

1. 先创建一个空目录：`mkdir 目录名`
2. 切换到将要创建的版本库目录：`cd 目录名`
3. 把这个目录变成Git可以管理的仓库：`git init`

## 添加文件到Git仓库

* 把文件添加到仓库：`git add 文件名`
* 查看仓库当前状态：`git status`
* 查看文件修改情况：`git diff 文件名`(diff是difference的意思)
* 把文件提交到仓库：`git commit -m "说明"`，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样就能从历史记录里方便地找到改动记录

## 版本回退

* 显示从最近到最远的提交日志：`git log`或`git log --pretty=oneline`，在Git中，用`HEAD`表示当前版本，也就是最新的提交，`HEAD^`表示上一个版本，`HEAD^^`表示上上一个版本，`HEAD~100`表示上100个版本
* 显示最后一次提交信息：`git log -l`
* 把当前版本回退到上一个版本：`git reset --hard HEAD^`
* 查看文件内容：`cat 文件名`
* 可以指定回到未来的某个版本：`git reset --hard 版本号`
* 查看命令历史：`git reflog`
* 查看工作区和版本库里面最新版本的区别：`git diff HEAD -- 文件名`

## 删除撤销

* 删除一个文件：`git rm 文件名`，只有这个命令只是删除工作区的文件，要从版本库中删除该文件，得再用`git commit`提交到版本库
* 把文件在工作区的修改全部撤销：`git checkout -- 文件名`，这里有两种情况：一种是文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。总之，就是让这个文件回到最近一次修改时的状态，命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令

## 远程仓库

1. 关联一个远程库：`git remote add 远程库的名字 git@github.com:账户名/仓库目录名.git`，远程库的名字习惯用`origin`
2. 推送分支的所有内容：`git push -u 远程库的名字 分支名`，由于远程库是空的，第一次推送分支时，加上了`-u`参数，Git不但会把本地的分支内容推送的远程新的分支，还会把本地的分支和远程的分支关联起来，在以后的推送或者拉取时就可以简化命令，不用`-u`参数
3. 克隆一个本地库：`git clone git@github.com:账户名/仓库目录名.git`

## 分支管理

* 创建分支，然后切换到分支：`git checkout -b 分支名`，`git checkout`命令加上`-b`参数表示创建并切换，相当于`git branch 分支名`+`git checkout 分支名`
* 查看当前分支：`git branch`
* 合并指定分支到当前分支：`git merge 分支名`；`git merge --no-ff -m "说明" 分支名`，`--no-ff`参数，表示禁用Fast forward，`-m`参数表示创建一个新的commit
* 删除分支：`git branch -d 分支名`
* 强行删除一个没有被合并过的分支：`git branch -D 分支名`
* 创建并切换到新的分支：`git switch -c 分支名`；直接切换到已有的分支不用`-c`参数
* 显示分支合并图：`git log --graph`

## 解决冲突

* 把当前工作现场“储藏”起来，等以后恢复现场后继续工作：`git stash`
* 查看“储藏”的工作现场：`git stash list`
* 恢复“储藏”的工作现场：一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，需要用`git stash drop`来删除；另一种方式是用`git stash pop`，恢复的同时把`stash`内容也删除
* 复制一个特定的提交到当前分支：`git cherry-pick <commit>`

## 多人协作

* 查看远程库的信息：`git remote`；`git remote -v`显示更详细的信息
* 把分支推送到远程库对应的远程分支上：`git push 远程库的名字 分支名`
* 从远程抓取分支：`git pull`
* 建立本地分支和远程分支的关联：`git branch --set-upstream 分支名 远程分支名`
* 把本地未push的分叉提交历史整理成直线：`git rebase`

## 标签管理

* 创建标签：`git tag 标签名`，默认为`HEAD`
* 创建带有说明的标签：`git tag -a 标签名 -m "说明" <commit>`，用`-a`参数指定标签名，`-m`参数指定说明文字
* 查看所有标签：`git tag`，标签按字母排序列出
* 查看标签信息：`git show 标签名`
* 推送一个本地标签：`git push 远程仓库的名字 标签名`
* 推送全部未推送到远程的本地标签：`git push 远程仓库的名字 --tags`
* 删除一个本地标签：`git tag -d 标签名`；
* 删除一个远程标签：`git push 远程仓库的名字 :refs/tags/标签名`

## 自定义Git

* 让Git显示颜色：`git config --global color.ui true`
* 配置别名：`git config --global alias.别名 原命令名`，`--global`参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用，习惯用`st`表示`status`、`co`表示`checkout`，`ci`表示`commit`，`br`表示`branch`，`unstage`表示`'reset HEAD'`，`last`表示`'log -1'`