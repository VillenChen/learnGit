## 1、git的命令版本库
#### 1.git的创建
+ `cd g:` 打开g盘
+ `ls -ah` 命令就可以查看文件夹里的所有文件目录
+ `mkdir learngit` 创建learngit文件夹
+ `cd learngit` 切换到learngit文件夹
+ `pwd` 显示正在使用的文件的路径
+ `git init` 初始化正在使用的库,初始化一次就可以了

#### 2.git的时光穿梭
- `git add just.md` 添加just.md这个文件(可以提交多个)
- `git commit -m "wrote a just file"` 告诉Git,把文件提交到仓库(开始编写文件)//-m后面输入的是本次提交的说明,可以输入任意内容,最好是有意义的,这样你就能从历史记录里方便地找到改动记录。因为commit可以一次提交很多文件,所以你可以多次add不同的文件每次回顾之前必须要commit一次
- `git status` 查看仓库的当前状态,可以让我们时刻掌握仓库当前的状态(运行git status命令查看内容的修改情况,看看结果)
- `git diff just.md` 顾名思义就是查看difference,可以命令输出看到,我们在第一行添加了一个“distributed”单词。知道了对just.md作了什么修改后,再把它提交到仓库就放心多了,提交修改和提交新文件是一样的两步,第一步是git add,第二步git commit之前,我们再运行git status看看当前仓库的状态(看看just.md具体修改了什么内容)
- `Q`:退出 `E`:编辑    `O`:打开    `R`:恢复    `A`:中止(git的快捷键)
- `git log` 可以告诉我们历史记录,显示从最近到最远的提交日志,我们可以看到3次提交.如果嫌输出信息太多,看得眼花缭乱的,可以试试加上`--pretty=oneline`参数

#### 3.git的历史回顾
* `git reset --hard HEAD^` 上一个版本就是`HEAD^`,上上一个版本就是`HEAD^^`,当然往上100个版本写100个^比较容易数不过来,所以写成`HEAD~100`
* `cat just.md` 看看just.md的内容是不是版本自己所需要的版本(查看文本的内容)
* `git log` 继续回退到上一个版本前,看看现在版本库的状态(告诉我们历史记录)
* `git reset --hard 3628164` 指定回到未来的某个版本,版本号没必要写全,前几位就可以了,Git会自动去找。当然也不能只写前一两位,因为Git可能会找到多个版本号,就无法确定是哪一个了。Git的版本回退速度非常快,因为Git在内部有个指向当前版本的HEAD指针,当你回退版本的时候,Git仅仅是把HEAD从指向某个版本.然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号,你就把当前版本定位在哪。
* `git reflog` 用来记录你的每一次命令(查看命令历史)

#### 4.git的工作区和暂存区
###### a.工作区(Working Directory)
+ 就是你在电脑里能看到的目录,比如learngit文件夹就是一个工作区

###### b.版本库（Repository）
+ 版本库(Repository):`.git`文件夹
![git的版本库](git.jpg)
+ 把文件往Git版本库里添加的时候,是分两步执行的：
第一步是用`git add`把文件添加进去,实际上就是把文件修改添加到暂存区；
第二步是用`git commit`提交更改,实际上就是把暂存区的所有内容提交到当前分支。

#### 5.管理修改
+ `git diff HEAD -- just.md` 提交后,用该命令可以查看工作区和版本库里面最新版本的区别
+ Git的跟踪修改:每次修改,如果不add到暂存区,那就不会加入到commit中。
- `git checkout -- file` 可以丢弃工作区的修改,把file文件在工作区的修改全部撤销:(总之,就是让这个文件回到最近一次`git commit`或`git add`时的状态。)
    a.是`file`自修改后还没有被放到暂存区,现在,撤销修改就回到和版本库一模一样的状态;
    b.是`file`已经添加到暂存区后,又作了修改,现在,撤销修改就回到添加到暂存区后的状态。
    c.没有`--`,就变成了“切换到另一个分支”的命令,我们在后面的分支管理中会再次遇到`git checkout`命令。
+ `cat file` 查看文本的内容
+ `git reset HEAD file` 可以把暂存区的修改撤销掉(unstage),重新放回工作区,再用`git checkout -- file` 来把工作区的内容删除
+ `git reset` 既可以回退版本,也可以把暂存区的修改回退到工作区。当我们用`HEAD`时,表示最新的版本。
+ `rm file` 命令删除文件
    * a.`git rm file`+`git commit` 文件就从版本库中被删除了(确实要从版本库中删除该文件)。
    * b.`git checkout -- file` 删错了,因为版本库里还有,所以可以很轻松地把误删的文件恢复到最新版本,`git checkout`其实是用版本库里的版本替换工作区的版本,无论工作区是修改还是删除,都可以“一键还原”。

#### 6.远程仓库
* 注册一个`GitHub`账号,就可以免费获得Git远程仓库
    1. 创建`SSH Key`,在用户主目录下,看看有没有.ssh目录,如果有,再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件,如果已经有了,可直接跳到下一步。如果没有,打开Shell（Windows下打开Git Bash）,创建SSH Key：`ssh-keygen -t rsa -C "youremail@example.com"`你需要把邮件地址换成你自己的邮件地址,然后一路回车,使用默认值即可,由于这个Key也不是用于军事目的,所以也无需设置密码。一切顺利的话,可以在用户主目录里找到`.ssh`目录,里面有`id_rsa`和`id_rsa.pub`两个文件,这两个就是`SSH Key`的秘钥对,`id_rsa`是私钥,不能泄露出去,`id_rsa.pub`是公钥,可以放心地告诉任何人。
    2. 登陆`GitHub`,打开“`Account settings`”,“`SSH Keys`”页面：然后,点“`Add SSH Key`”,填上任意Title,在Key文本框里粘贴`id_rsa.pub`文件的内容：![addSshKey](../addSshKey.png),点“`Add Key`”,你就应该看到已经添加的Key：![AddKey](../AddKey.png)
    * a.当然,GitHub允许你添加多个Key。假定你有若干电脑,你一会儿在公司提交,一会儿在家里提交,只要把每台电脑的Key都添加到GitHub,就可以在每台电脑上往GitHub推送了。
    * b.最后友情提示,在GitHub上免费托管的Git仓库,任何人都可以看到喔（但只有你自己才能改）。所以,不要把敏感信息放进去。
    * c.如果你不想让别人看到Git库,有两个办法,一个是交点保护费,让GitHub把公开的仓库变成私有的,这样别人就看不见了（不可读更不可写）。另一个办法是自己动手,搭一个Git服务器,因为是你自己的Git服务器,所以别人也是看不见的。这个方法我们后面会讲到的,相当简单,公司内部开发必备。

#####添加远程库
1. 在本地创建了一个Git仓库后,又在`GitHub`创建一个Git仓库,并且让这两个仓库进行远程同步:
    * 登陆GitHub,然后,在右上角找到“`Create a new repo`”按钮,创建一个新的仓库：![Create a new repo](../newPro.png)
    * 在Repository name填入learngit,其他保持默认设置,点击“`Create repository`”按钮,就成功地创建了一个新的Git仓库：![proName](../proName.png)
    * 目前,在GitHub上的这个learngit仓库还是空的,GitHub告诉我们,可以从这个仓库克隆出新的仓库,也可以把一个已有的本地仓库与之关联,然后,把本地仓库的内容推送到GitHub仓库。
    * 在本地的learngit仓库下运行命令：`$ git remote add origin git@github.com:michaelliao/learngit.git`,请千万注意,把上面的michaelliao替换成你自己的GitHub账户名,否则,你在本地关联的就是我的远程库,关联没有问题,但是你以后推送是推不上去的,因为你的SSH Key公钥不在我的账户列表中。添加后,远程库的名字就是origin,这是Git默认的叫法,也可以改成别的,但是origin这个名字一看就知道是远程库。
2. 把本地库的所有内容推送到远程库上：
    * `$ git push -u origin master`,把本地库的内容推送到远程,用`git push`命令,实际上是把当前分支master推送到远程。
    * 由于远程库是空的,我们第一次推送master分支时,加上了-u参数,Git不但会把本地的master分支内容推送的远程新的master分支,还会把本地的master分支和远程的master分支关联起来,在以后的推送或者拉取时就可以简化命令。
3. 推送成功后,可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：![推送成功](../suss.png)
4. 从现在起,只要本地作了提交,就可以通过命令：`$ git push origin master`,把本地master分支的最新修改推送至GitHub,现在,你就拥有了真正的分布式版本库！
5. SSH警告:
    * 当你第一次使用Git的clone或者push命令连接GitHub时,会得到一个警告：这是因为Git使用SSH连接,而SSH连接在第一次验证GitHub服务器的Key时,需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器,输入yes回车即可。
    * Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：`Warning: Permanently added 'github.com,192.30.253.112' (RSA) to the list of known hosts.`

