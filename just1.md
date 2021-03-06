##git的小结:(Git是分布式版本控制系统)
#### 1.初始化一个Git仓库，使用`git init`命令。
#### 2.添加文件到Git仓库，分两步：
    a. 第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
    b. 第二步，使用命令`git commit`，完成。
#### 3.要随时掌握工作区的状态，使用`git status`命令。
#### 4.如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。
#### 5.HEAD指向的版本就是当前版本，因此，`Git`允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
#### 6.穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
#### 7.要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。
#### 8.暂存区
    * 暂存区是`Git`非常重要的概念，弄明白了暂存区，就弄明白了`Git`的很多操作到底干了什么。
    * 没弄明白暂存区是怎么回事的童鞋，请向上滚动页面，再看一次。
#### 9.场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
#### 10.场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git `reset HEAD file`，就回到了场景1，第二步按场景1操作。
#### 11.场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
#### 12.命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
#### 13.
