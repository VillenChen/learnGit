## 1、git的命令
+ ls -ah 命令就可以查看文件夹里的所有文件目录
- mkdir learngit 创建learngit文件夹
* cd learngit 切换到learngit文件夹
+ pwd 显示正在使用的文件的路径
+ git init 初始化正在使用的库，初始化一次就可以了
+ git add just.md 添加just.md这个文件(可以提交多个)
+ git commit -m "wrote a just file" 告诉Git，把文件提交到仓库(开始编写文件)//-m后面输入的是本次提交的说明，可以输入任意内容，最好是有意义的，这样你就能从历史记录里方便地找到改动记录。因为commit可以一次提交很多文件，所以你可以多次add不同的文件每次回顾之前必须要commit一次
+ git status 查看仓库的当前状态,可以让我们时刻掌握仓库当前的状态(运行git status命令查看内容的修改情况，看看结果)
+ git diff just.md 顾名思义就是查看difference,可以命令输出看到，我们在第一行添加了一个“distributed”单词。知道了对just.md作了什么修改后，再把它提交到仓库就放心多了,提交修改和提交新文件是一样的两步,第一步是git add,第二步git commit之前，我们再运行git status看看当前仓库的状态(看看just.md具体修改了什么内容)
+ Q:退出 E:编辑    O:打开    R:恢复    A:中止(git的快捷键)
+ git log 可以告诉我们历史记录,显示从最近到最远的提交日志，我们可以看到3次提交.如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数
+ git reset --hard HEAD^ 上一个版本就是HEAD^,上上一个版本就是HEAD^^,当然往上100个版本写100个^比较容易数不过来,所以写成HEAD~100
+ cat just.md 看看just.md的内容是不是版本自己所需要的版本
+ git log 继续回退到上一个版本前,看看现在版本库的状态(告诉我们历史记录)
+ git reset --hard 3628164 指定回到未来的某个版本,版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。Git的版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，Git仅仅是把HEAD从指向某个版本.然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。
+ git reflog 用来记录你的每一次命令(查看命令历史)