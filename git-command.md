## GIT常用命令

## 本地仓库

- 以初始化后的git目录里，文件只有两种状态，untracked和tracked
  - `untracked`是还没有提交到暂存区`index`
  - 如何提交到`index`  - `git add [filename | -A]`
  - `git add`用于跟踪新文件，把已跟踪的文件放入暂存区 



- 文件处于untracked、tracked（暂存区）、提交（commit）

- 从tracked到提交  `git commit -m "info"`
- 查看当前修改了的文件和暂存区的差别 `git diff`
- 查看当前暂存区文件和上次提交版本的区别 `git diff --staged`
- 删除文件后，还要在git的暂存区删除（停止追踪）	`git rm file`
- 要从暂存区删除文件，以后不再追踪，但是在工作目录中不要删除。如一些log文件等。`git rm --cached`



- 查看工作区状态 `git status`



- 查看提交历史`git log `
  - 查看最近n次提交记录 `git log -n`
  - 查看提交记录的详细差异 `git log -p`
  - 所有提交在一行显示 `git log --pretty=oneline` ，提交量很大时适用
  - 只显示简单的增减行数**统计**，不显示内部细节 `git log --stat`



- 撤销工作目录中file的修改 `git checkout -- file`
  - file自修改后没有提交到index，撤销修改就是回到当前版本库（commit）中的版本
  - file已经提交到index，又做了修改，撤销修改就是回到index的版本



### 远程仓库

- 和本地仓库相对应
- 当我们想要和别人合作，通常都需要建立远程仓库，大家从远程仓库clone项目，获取更新，提交更新等
- 远程仓库也有自己的分支，本地仓库也有自己分支。不要混淆仓库和分支
- 添加远程仓库
  - 当远程仓库里没有内容的时候 可以直接 `git remote add <name> <url>`
  - 远程仓库默认的名字是origin 默认分支branch
  - 当远程仓库里已有内容，想再往里面添加内容的时候，需要先clone远程仓库



## 分支

- 每一个仓库都有分支，不论本地还是远程
- 查看分支 `git branch`
- 创建新分支 `git branch <name>`
- 切换分支 `git checkout <name>`
- **创建分支并切换到该分支** `git checkout -b <name>`
- 合并某分支到当前分支 `git merge <name>`
- 删除某分支 `git branch -d <name>`



### 分支冲突

- 当连个分支内容有冲突时，无法合并。要先手动解决冲突，再提交。
- 分支合并默认使用的是`Fast Forward`，合并后如果删除某个分支，在log上是无法看到这个分支的信息的。
- 为保证log能看到合并分支的历史记录，应该在合并时禁用fast forward `git merge --no-ff -m "info" <branchname>`
- 禁用ff时会强制产生一次commit，因此可以使用`-m`参数，加上提交信息



### 指针HEAD

- HEAD指向的是分支，当切换分支时，只是HEAD指针发生变化，文件并无变化
- 分支在实际意义上，也是不同的指针
- 分支指针指向提交节点，HEAD指针指向当前分支指针



## 多人合作

实际工作中是多人拉取远程仓库内容

- master分支。稳定发布版本，一直同步更新
- dev分支。开发版本，每个人拉取远程dev后，与本地dev关联（设置）
- 开发都在dev分支上，因此如果push出问题，很可能是别人已经先push过，这时自己要先pull更改过后的dev后，再手动fix conflict，最后再push
- 创建与远程分支一样的分支 `git checkout -b dev origin/dev`
- 关联远程分支与现在的分支 `git --set-upstream branch-name origin/branch-name`