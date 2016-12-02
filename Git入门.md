###1. 在Windows上安装Git###
msysgit是Windows版的Git，从http://msysgit.github.io/下载，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。

注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

查看配置信息:
```
$ git config --list
```

###2. 创建版本库###
什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：
```
$ mkdir learngit
$ cd learngit
$ pwd
```
pwd命令用于显示当前目录。在我的Mac上，这个仓库位于```C:\learngit```
如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。
第二步，通过git init命令把这个目录变成Git可以管理的仓库：
```
$ git init
Initialized empty Git repository in C:/learngit/.git/
```
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

###3. 把文件添加到版本库###
首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

现在我们编写一个```index.html```文件，一定要放到learngit目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。

```
> git status //查看当前状态

On branch master //主分支
Untracked files: //未被跟踪的文件
  (use "git add <file>..." to include in what will be committed)

        index.html

nothing added to commit but untracked files present (use "git add" to track)

```
把一个文件放到Git仓库只需要两步。

第一步，用命令git add告诉Git，把文件添加到仓库：
```
$ git add index.html
```
执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。如果要提交整个目录的文件:
```
$ git add .
```

第二步，用命令git commit告诉Git，把文件提交到仓库：
```
$ git commit -m "wrote a readme file"
[master (root-commit) 2e46ccc] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

简单解释一下git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

###4. 对比两个文件的差异###
修改```index.html```,通过 ```$ git status```命令查看状态.
对比两个文件区别:
```
$ git diff ./index.html
diff --git a/index.html b/index.html
index 3d614f3..dc8b6c1 100644
--- a/index.html
+++ b/index.html
@@ -4,6 +4,6 @@
        <title>git 01</title>
 </head>
 <body>
-
+<h1>修改</h1>
 </body>
 </html>
\ No newline at end of file
```
将修改文件添加到暂存区:
```
$ git add index.html
```

再次修改```index.html```,用```$ git status```查看状态:
```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

```

将文件添加至暂存区:
```
$ git add index.html
```

在提交文件:
```
$ git commit -m "修改 index.html 文件"
```

总结: 如果要提交文件,首先应该将被修改的文件或者新增的文件添加到文件的暂存区```$ git add .```,在通过```$ git commint -m (描述)```提交.

###5. 如何重命名文件(在文件系统上重命名)###
添加文件: style-css.css
```
h1 {
	font-size: 30px;
}
```

将文件添加到暂存区:
```
$ git add style.css
```

修改 style-css.css 文件名为: theme.css
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    style-css.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        theme.css

no changes added to commit (use "git add" and/or "git commit -a")

```

使用
```
$ git add theme.css //将重命名的文件添加到暂存区

$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    style.css -> theme.css

$ git commit -m "重命名文件 style.css -> theme.css"
```

###6. 使用git mv 重命名###
```
$ git mv theme.css style.css
$ git commit -m "重命名"

```

###7. 移动文件###
```
$ mkdir css
$ dir
css  index.html  readme.txt  style.css
```
通过```$ git status```查看状态,发现没有更新项,因为git只会跟踪文件而不是目录,除非目录中有更新状态的文件.
```
$ git mv style.css css/   //将style.css文件移动到css目录下
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    style.css -> css/style.css
$ git commit -m "将style.css 文件移动到 css目录下"
[master 55acb09] 将style.css 文件移动到 css目录下
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename style.css => css/style.css (100%)

```
移动或重命名目录也是使用 ```$ git mv```命令
```
$ mkdir asset
$ git mv css asset/
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    css/style.css -> asset/css/style.css
$ git commit -m "将 css 文件夹移动到 asset 下"
[master fa8c7af] 将 css 文件夹移动到 asset 下
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename {css => asset/css}/style.css (100%)
```

###8. 删除文件###
```
$ git rm asset/css/style.css
rm 'asset/css/style.css'

$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    asset/css/style.css
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    asset/css/style.css
```
在删除之前,必须保证在git上已经存在要删除的文件,同时,暂存区中没有对该文件的更新任务.

###9. 恢复刚刚删除或修改的文件###
```
//删除 index.html 文件
$ git rm index.html
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    index.html
$ git commit -m "删除 index.html 文件"
[master 1434a9c] 删除 index.html 文件
 1 file changed, 10 deletions(-)
 delete mode 100644 index.html

```

```
$ git checkout HEAD^ -- index.html
$ dir
index.html  readme.txt

$ git commit -m "恢复 index.html"
[master 1b2c6ab] 恢复 index.html
 1 file changed, 10 insertions(+)
 create mode 100644 index.html

```
以上命令也可用于更新操作

###10. 恢复文件的历史版本###
1. 在工作空间添加css目录,并将bootstrap.min.css文件拷贝进去.
在index.html文件中引入bootstrap.min.css.
提交版本.
2. 在工作空间添加js目录并将jquery-1.7.2.min.js文件拷贝进去.
在index.html文件中引入jquery-1.7.2.min.js.
```
$ git log --oneline
```

回滚提交:
```
//找到上一个提交id
$ git revert 086109e
:wq 保存描述
$ git log --oneline
3f8778c Revert "添加 bootstrap 框架"
4efc664 js
086109e 添加 bootstrap 框架
```

###11. 控制头部指针 reset###
通过reset可以控制指针位置,让它指向之前的某一次提交.这样的话,在下一次提交就会覆盖掉之后的所有提交.
1. --soft: 软提交,不会影响工作区和暂存区的内容.
```
$ git reset --soft 4efc664
```
2. --hard: 硬提交,会将工作区和暂存区直接重置到指定的状态.
```
$ git reset --hard 4efc664
```
3. --mixed: 将暂存区的内容重置到指定的状态.并将指针指向这个提交
```
$ git reset --mixed 4efc664
```

###12. 保存, 恢复, 删除工作进度###
修改readme.txt
```
$ git stash save "修改了 readme.txt"

```
保存readme.txt的工作状态.这时, readme.txt会恢复到修改之前的状态.

查看工作进度:
```
$ git stash list
stash@{0}: On master: 修改了 readme.txt

```
查看工作进度和当前文件的区别:
```
$ git stash show -p stash@{0}
diff --git a/readme.txt b/readme.txt
index d8036c1..930520a 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,4 @@
 Git is a version control system.
-Git is free software.
\ No newline at end of file
+Git is free software.
+
+test
\ No newline at end of file

```

恢复工作进度:
```
$ git stash apply stash@{0}
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
这时候readme.txt又恢复成修改时的内容.

删除工作进度:
```
$ git stash drop stash@{0}
Dropped stash@{0} (d71c794951a295864987da0901920854467c5028)
```

恢复并删除工作进度
```
$ git stash pop stash@{0}
```

###13. 提交日志###
```
$ git log --oneline //简单的日志显示
$ git log --oneline -5 //指定显示条数
$ git log --oneline --author="tangzhenhua" //指定提交者
$ git log --oneline --grep="index.html" //过滤,只查找index.html提交内容
$ git log --oneline --before="2016-03-06" //日期之前的提交

```

###14. 分支###
**14.1 查看/创建/切换 分支**

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个平行宇宙里努力学习SVN。

如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了Git又学会了SVN！
![](images/0.png)

分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

查看当前分支:
```
$ git status
On branch master //显示当前分支为主分支
nothing to commit, working directory clean

```

查看所有分支:
```
$ git branch
* master

```

创建分支:
```
$ git branch mobile-feature

$ git branch
* master
  mobile-feature
```

切换分支:
```
$ git checkout mobile-feature
Switched to branch 'mobile-feature'
```

**14.2 分支中修改**
将当前分支指向 "mobile-feature"
修改index.html
新增img

```
$ git status
On branch mobile-feature
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        img/

no changes added to commit (use "git add" and/or "git commit -a")

Administrator@mac-25e81fb6430 MINGW32 /c/learngit (mobile-feature)
$ git add .
$ git commit -m "修改 index.html 新增 /img"

//查看日志
$ git log --oneline --decorate
35e8518 (HEAD -> mobile-feature) 修改 index.html 新增 /img
72331b0 (master) 修改了 readme.txt
3f8778c Revert "添加 bootstrap 框架"
4efc664 js
...
```
**14.3 对比分支的区别**
```
//查看所有文件区别
$ git diff master..mobile-feature
diff --git a/img/marker-1.gif b/img/marker-1.gif
new file mode 100644
index 0000000..9c52493
Binary files /dev/null and b/img/marker-1.gif differ
diff --git a/img/marker-2.png b/img/marker-2.png
new file mode 100644
index 0000000..9bd8e50
Binary files /dev/null and b/img/marker-2.png differ
diff --git a/img/marker-3.gif b/img/marker-3.gif
new file mode 100644
index 0000000..a3d7d9e
Binary files /dev/null and b/img/marker-3.gif differ
diff --git a/index.html b/index.html
index 705315c..e6c08aa 100644
--- a/index.html
+++ b/index.html
@@ -7,5 +7,8 @@
 <h1>修改</h1>
 <h2>修改02</h2>
 <script type="text/javascript" src="js/jquery-1.7.2.min.js"></script>
+<img src="./img/marker-1.gif">
+<img src="./img/marker-2.png">
+<img src="./img/marker-3.gif">
 </body>
 </html>
\ No newline at end of file


//指定查看的文件
$ git diff master..mobile-feature index.html
diff --git a/index.html b/index.html
index 705315c..e6c08aa 100644
--- a/index.html
+++ b/index.html
@@ -7,5 +7,8 @@
 <h1>修改</h1>
 <h2>修改02</h2>
 <script type="text/javascript" src="js/jquery-1.7.2.min.js"></script>
+<img src="./img/marker-1.gif">
+<img src="./img/marker-2.png">
+<img src="./img/marker-3.gif">
 </body>
 </html>
\ No newline at end of file
```

**14.4 合并分支 fast-forward**

```
//将当前分支切换到主分支(master)
$ git checkout master
Switched to branch 'master'

//合并分支
$ git merge mobile-feature
Updating 72331b0..35e8518
Fast-forward //创建分支之后,没有对master进行任何提交,这种方式就是 fast-forward
 img/marker-1.gif | Bin 0 -> 49 bytes
 img/marker-2.png | Bin 0 -> 294 bytes
 img/marker-3.gif | Bin 0 -> 72 bytes
 index.html       |   3 +++
 4 files changed, 3 insertions(+)
 create mode 100644 img/marker-1.gif
 create mode 100644 img/marker-2.png
 create mode 100644 img/marker-3.gif

```

**14.5 合并分支**

```
//1. 切换到 mobile-feature 分支
$ git checkout mobile-feature
Switched to branch 'mobile-feature'

//2. 切换到 master 主分支
$ git add .
$ git checkout master
Switched to branch 'master'

//添加humans.txt文件
$ git commit -m "添加了 humans.txt"
[master c37c5ae] 添加了 humans.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 humans.txt

$ git log --oneline --decorate --all -10 --graph
* c37c5ae (HEAD -> master) 添加了 humans.txt
| * 36bccda (mobile-feature) index.html 添加 span
|/
* 35e8518 修改 index.html 新增 /img
* 72331b0 修改了 readme.txt
* 3f8778c Revert "添加 bootstrap 框架"
* 4efc664 js
* 086109e 添加 bootstrap 框架
* 1b2c6ab 恢复 index.html
* 1434a9c 删除 index.html 文件
* 2e55020 删除 asset/css/style.css 文件

//主分支和其他分支都发生了变化,这时就不能使用快速合并
$ git merge mobile-feature
:wq

```


**14.6 解决冲突**
修改 master 和 mobile-feature 的index.html文件
在进行合并操作,这个时候会提示冲突:
```
$ git merge master
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```
打开index.html文件进行手动修改,修改完成之后继续提交即可

**14.7 重命名分支**
```
//创建分支
$ git branch bugfix

//重命名
$ git branch -m bugfix bugfix-01

//删除分支
$ git branch -d bugfix-01
Deleted branch bugfix-01 (was 740303d).
```

###15. 远程 remote###

Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。怎么分布呢？最早，肯定只有一台机器有一个原始版本库，此后，别的机器可以“克隆”这个原始版本库，而且每台机器的版本库其实都是一样的，并没有主次之分。

你肯定会想，至少需要两台机器才能玩远程库不是？但是我只有一台电脑，怎么玩？

其实一台电脑上也是可以克隆多个版本库的，只要不在同一个目录下。不过，现实生活中是不会有人这么傻的在一台电脑上搞几个远程库玩，因为一台电脑上搞几个远程库完全没有意义，而且硬盘挂了会导致所有库都挂掉，所以我也不告诉你在一台电脑上怎么克隆多个仓库。

实际情况往往是这样，找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。

完全可以自己搭建一台运行Git的服务器，不过现阶段，为了学Git先搭个服务器绝对是小题大作。好在这个世界上有个叫GitHub的神奇的网站，从名字就可以看出，这个网站就是提供Git仓库托管服务的，所以，只要注册一个GitHub账号，就可以免费获得Git远程仓库。

```
//创建一个空的版本库
…or create a new repository on the command line

echo "# learngit" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/tangzhenhua/learngit.git
git push -u origin master

//将本地版本库推送到github
…or push an existing repository from the command line

git remote add origin https://github.com/tangzhenhua/learngit.git
$ git push -u origin master
Counting objects: 71, done.
Compressing objects: 100% (61/61), done.
Writing objects: 100% (71/71), 56.58 KiB | 0 bytes/s, done.
Total 71 (delta 22), reused 0 (delta 0)
To https://github.com/tangzhenhua/learngit.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

//查看远程分支
$ git branch -r
  origin/master
```



