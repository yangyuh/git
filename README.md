## GIT 常用命令

    $ git init   将当前文件夹用git仓库管理起来
    $ git add .  将所有改动提交到工作缓存区
    $ git status  查看提交状态
    $ git commit -m "注释"    将工作缓存区提交到仓库
    $ git remote add origin repository提交到远程仓库后面是仓库创建仓库产生的链接
    $ git push -u origin master   更新远程代码
    $ git remote -v 查看远程仓库地址
    $ git remote remove [origin] 删除远程仓库地址
    $ git remote add [origin] 添加远程仓库地址

### 版本回退
    $ git reset --hard commit_id 版本回退
    $ git log 可以查看提交历史，回退前用以便确定要回退到哪个版本。
    $ git reflog 要重返未来，用查看命令历史以便确定要回到未来的哪个版本。

### 创建与合并分支

    $ git branch 查看分支
    $ git branch name 创建分支
    $ git checkout name 切换分支
    $ git checkout -b name 创建+切换分支
    $ git merge name 合并某分支到当前分支
    $ git branch -d name 删除分支

### git使用ssh密钥
1.查看本地是否有密钥对，如果存在就删除

    cd ~/.ssh
    id_dsa id_dsa.pub
2.重新生成密钥对然后一直回车

    ssh-keygen -t rsa -C "your_email@youremail.com"
3.查看本地生成的密钥

    cat ~/.ssh/id_rsa.pub
4.登陆你的github帐户。然后 Account Settings -> 左栏点击 SSH Keys -> 点击 Add SSH key
5.然后你复制上面的公钥内容，粘贴进“Key”文本域内。 title域，你随便填一个都行。 

### git add 报错

    fatal: Unable to create '/path/my_proj/.git/index.lock': File exists.
    If no other git process is currently running, this probably means a
    git process crashed in this repository earlier. Make sure no other git
    process is running and remove the file manually to continue.
 
删除index.lock文件

    rm -f ./.git/index.lock