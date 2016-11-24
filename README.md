# GIT 常用命令

$ git init   将当前文件夹用git仓库管理起来
$ git add .  将所有改动提交到工作缓存区
$ git status  查看提交状态
$ git commit -m "注释"    将工作缓存区提交到仓库
$ git remote add origin <repository> 提交到远程仓库后面是仓库创建仓库产生的链接
$ git push -u origin master   更新远程代码

## 版本回退
$ git reset --hard commit_id 版本回退
$ git log 可以查看提交历史，回退前用以便确定要回退到哪个版本。
$ git reflog 要重返未来，用查看命令历史以便确定要回到未来的哪个版本。

## 创建与合并分支

$ git branch 查看分支
$ git branch <name> 创建分支
$ git checkout <name> 切换分支
$ git checkout -b <name> 创建+切换分支
$ git merge <name> 合并某分支到当前分支
$ git branch -d <name> 删除分支