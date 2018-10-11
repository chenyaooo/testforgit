## GIT常用命令



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