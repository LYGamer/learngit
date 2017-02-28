# git学习 #

### 在Windows上安装Git ###
[git,win版下载地址](https://git-for-windows.github.io)

安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

```
>因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。
>
注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

## Git 操作 ##
### 创建版本库 ###

>什么是版本库呢？版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```
第二步，通过`git init`命令把这个目录变成Git可以管理的仓库：
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/

```

### 把文件添加到仓库 ###
第一步，用命令git add告诉Git，把文件添加到仓库：
```
$ git add readme.txt
```
第二步，用命令git commit告诉Git，把文件提交到仓库：
```
$ git commit -m "wrote a readme file"
[master (root-commit) cb926e7] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```
简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录.

### 查看历史 ###

`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令告诉我们，readme.txt被修改过了，但还没有准备提交的修改。
`git diff`查看上次修改的内容。
`git log`命令显示从最近到最远的提交日志,如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数。
`git reset`回退到上一个版本:
```
$ git reset --hard HEAD^
HEAD is now at ea34578 add distributed
```
`git reset`回到指定版本:
```
$ git reset --hard 3628164
HEAD is now at 3628164 append GPL
```
`git reflog`用来记录你的每一次命令：
```
$ git reflog
ea34578 HEAD@{0}: reset: moving to HE AD^
3628164 HEAD@{1}: commit: append GPL
ea34578 HEAD@{2}: commit: add distributed
cb926e7 HEAD@{3}: commit (initial): wrote a readme file
```


`git checkout -- file`可以丢弃工作区的修改：
>命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

>一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

>一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

>总之，就是让这个文件回到最近一次git commit或git add时的状态。

命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
