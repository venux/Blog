---
title: Git笔记
date: 2017-08-30 23:30:58
tags: Git
categories: 工具
---
## 1.初始化

git init

## 2.添加到仓库

git add $filename

## 3.提交到仓库

git commit -m "$comment"

## 4.查看状态

git status

<!--more-->

## 5.对比修改记录

git diff

## 6.查看提交日志

git log 

- `--pretty=oneline`:单行显示
- `--graph`：图像显示
- `--abbrev-commit`：缩写CommitID

## 7.版本回退

git reset --hard

- `HEAD`表示当前版本
- `HEAD^`表示上个版本，`HEAD^^`上上个版本
    - git reset --hard HEAD^
    -  **注意：^在CMD中需要用双引号括起来**
- `HEAD~100`上100个版本
- `versionId`版本号（可只写前几位）：
    -  git reset --hard cfab68213adec8795db301414287dfccadb30499

## 8.查看命令历史

git reflog

## 9.撤销修改

-  未添加到暂存区：git checkout -- $filename
-  已添加到暂存区：git reset HEAD $filename

## 10.删除文件

git rm $filename

## 11.添加远程库

git remote add origin $giturl

- 远程库默认名为`origin`

## 12.推送当前分支master到远程库origin

git push -u origin master

- `-u`：由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
- 第二次后就可去掉`-u`参数直接推送。

## 13.克隆

git clone $giturl

## 14.创建分支

git branch $branchname

## 15.切换分支

git checkout $branchname

## 16.创建并切换分支

git checkout -b $branchname

- `-b`：表示创建并切换，相当于创建`git branch $branchname`和切换`git checkout $branchname`两个命令。

## 17.查看分支

git branch

## 18.合并分支

git merge $branchname

- 合并指定分支到当前分支
- 合并结果中的`Fast-forward`表示快进模式，即直接将当前分支的指针指向指定分支的最新提交位置，故非常快。
- `--no-ff`：禁用`Fast-forward`模式，这样会在merge时生成新的commit信息。合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

## 19.删除分支

git branch -d $branchname

- `-d`：删除已合并的分支；
- `-D`：强制删除未合并的分支（**注意：分支代码无法找回**）。

## 20.解决冲突

1 多分支同时修改同一个文件后add并commit；
2 merge分支时提示冲突；
3 修改冲突文件后再次add并commit即可。

## 21.分支策略

1 master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
2 dev分支干活，不稳定的.每个人都有自己的分支，时不时地往dev分支上合并就可以了。到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
3 所以，团队合作的分支看起来就像这样：
![图1](https://www.liaoxuefeng.com/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0)

## 22.储藏

- git stash：可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作
- git stash list：查看储藏列表
- git stash apply [stash@{n}]：恢复储藏，可选指定储藏
- git stash drop [stash@{n}]：删除储藏，可选指定储藏
- git stash pop [stash@{n}]：恢复并删除储藏，可选指定储藏

## 23.查看远程分支

git remote

- `-v`：显示详细信息

## 24.推送分支

git push origin $branchname

- master分支是主分支，因此要时刻与远程同步；
- dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了；
- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

## 25.标签

- 发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。
- Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。
- 增强版本识别，不用通过版本ID判断版本。

## 26.创建标签

git tag $tagname [$commitid]

- $commitid：指定给对应的提交记录打上标签，如无则给最新提交的记录加标签。

## 27.查看标签

git tag [$tagname]

- $tagname：查看指定标签，如无则查看所有标签。
- `-a`：指定标签名，如`git tag -a v1.0`。
- `-m`：指定说明，如`git tag -a v1.0 -m "这是第一个发布版本"`。

## 28.推送标签

git push origin $tagname

## 29.推送所有标签

git push origin --tags

## 30.删除标签

git tag -d $tagname

## 31.删除远程标签

git push origin :refs/tags/$tagname

- 要求先删除本地标签

## 32.忽略文件

- .gitignore文件[github](https://github.com/github/gitignore)
- 原则是：
    - 忽略操作系统自动生成的文件，比如缩略图等；
    - 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
    - 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

## 33.查看忽略文件

git check-ignore

- `-v`：查看忽略规则的详细行数

## 34.命令别名

git config --global alias.$shortname $name
`git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"`

## 35.配置

- 全局配置文件位置：`C:\Users\$username\.gitconfig`
- git config --global user.name `value`
- git config --global user.email `value` 

## 36.拉取

git pull origin master

- 若提示refusing to merge unrelated histories则需添加参数`--allow-unrelated-histories`

## 37.更新fork的repo

1 **git remote -v**
查看当前Fork项目已配置的远程仓库（List the current configured remote repository for your fork）
2 **git remote add upstream `url`**
指定将要同步Fork项目的一个远程上游仓库（Specify a new remote upstream repository that will be synced with the fork.）
3 **git remote -v**
再次查看
4 **git fetch upstream**
拉取上游仓库的所有分支和更改记录，mater分支提交记录会在本地分支中保存。（Fetch the branches and their respective commits from the upstream repository. Commits to master will be stored in a local branch, upstream/master.）
5 **git checkout master**
迁出本地master分支（Check out your fork's local master branch.）
6 **git merge upstream/master**
将上游仓库的master分支更改记录合并到本地master分支中，即同步且不会丢失本地更改记录。（Merge the changes from upstream/master into your local master branch. This brings your fork's master branch into sync with the upstream repository, without losing your local changes.）

## 参考文章

1 [廖雪峰git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
2 [syncing-a-fork](https://help.github.com/articles/syncing-a-fork/)